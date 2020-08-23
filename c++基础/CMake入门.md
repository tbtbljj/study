# CMake入门实战
[CMake入门实战](https://www.hahack.com/codes/cmake/#)
## 什么是CMake
* Make工具：
  * 如：GNU Make、QT qmake、微软 MS nmake、BSD Make (pmake)、Makepp等
  * 这些Make工具遵循着不同的规范和标准，所执行的**Makefile格式**也千差万别
  * 存在的问题：
    * 若软件想跨平台，则必须保证能够在不同平台上**编译**
    * 若使用上面的Make工具，则必须为每一种标准写一次**Makefile**
* CMake:
  * 针对上面问题所设计的工具
  * 先允许开发者**编写**一种平台无关的**CMakeList.txt文件**，来定制整个**编译**流程
  * 再根据目标用户的平台进一步生成所需的本地化**Makefile**和工程文件，如：Unix的Makefile或者Windows的Visual Studio工程
  * Write once, run everywhere
  * CMake是比上述几种Make更高级的**编译配置工具**
  * 使用CMake作为项目架构系统的知名开源项目：
    * VTK、ITK、KDE、OpenCV、OSG等
* 在`linux`平台下使用`CMake`生成`MakeFile`并**编译**的流程：
  * 1 编写`CMake`配置文件`CMakeLists.txt`
  * 2 执行命令`cmake PATH`或者`ccmake PATH`生成`MakeFile`
    * `ccmake`和`cmake`的区别在于前者提供了一个交互式的界面
    * `PATH`是`CMakeList.txt`所在目录
  * 3 利用`make`命令进行编译
  
## 入门案例：单个源文件
* 对于简单的项目，只需要写几行代码即可
  * 如：项目中只有一个源文件`main.cc`，该程序的用处是计算一个数的指数幂
```
#include <stdio.h>
#include <stdlib.h>

/**
 * power - Calculate the power of number.
 * @param base: Base value.
 * @param exponent: Exponent value.
 *
 * @return base raised to the power exponent.
 */
double power(double base, int exponent)
{
    int result = base;
    int i;
    
    if (exponent == 0) {
        return 1;
    }
    
    for(i = 1; i < exponent; ++i){
        result = result * base;
    }

    return result;
}

int main(int argc, char *argv[])
{
    if (argc < 3){
        printf("Usage: %s base exponent \n", argv[0]);
        return 1;
    }
    double base = atof(argv[1]);
    int exponent = atoi(argv[2]);
    double result = power(base, exponent);
    printf("%g ^ %d is %g\n", base, exponent, result);
    return 0;
}
```
* 编写`CMakeLists.txt`：
  * 先编写`CMakeLists.txt`文件，并保存在于`main.cc`源文件同个目录下
  * `CMakeLists.txt`文件中的命令：
    * `cmake_minimum_required`：指定运行此配置文件所需的`CMake`的最低版本
    * `project`：参数值是`Demo1`，该命令表示项目的名称是`Demo1`
    * `add_executable`：将名为`main.cc`的源文件**编译**成一个名称为`Demo`的可执行文件
```
# CMake 最低版本号要求
cmake_minimum_required (VERSION 2.8)

# 项目信息
project (Demo1)

# 指定生成目标
add_executable(Demo main.cc)
```
* `CMakeLists.txt`语法：
  * 语法比较简单，由命令、注释和空格组成
  * 命令不区分大小写
  * 符号`#`后面的内容被认为是注释
  * 命令由命令名称、小括号和参数组成，参数之间使用空格进行间隔
* 编译项目：
  * 在当前目录执行`cmake .`，得到`Makefile`后再使用`make`命令编译得到`Demo`可执行文件
```
[ehome@xman Demo1]$ cmake .
-- The C compiler identification is GNU 4.8.2
-- The CXX compiler identification is GNU 4.8.2
-- Check for working C compiler: /usr/sbin/cc
-- Check for working C compiler: /usr/sbin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working CXX compiler: /usr/sbin/c++
-- Check for working CXX compiler: /usr/sbin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/ehome/Documents/programming/C/power/Demo1
[ehome@xman Demo1]$ make
Scanning dependencies of target Demo
[100%] Building C object CMakeFiles/Demo.dir/main.cc.o
Linking C executable Demo
[100%] Built target Demo
[ehome@xman Demo1]$ ./Demo 5 4
5 ^ 4 is 625
[ehome@xman Demo1]$ ./Demo 7 3
7 ^ 3 is 343
[ehome@xman Demo1]$ ./Demo 2 10
2 ^ 10 is 1024
```

## 多个源文件
### 同一目录，多个源文件
* 把`power`函数单独写进一个名为`MathFunctions.c`的源文件里
* 工程的形式为：
```
./Demo2
    |
    +--- main.cc
    |
    +--- MathFunctions.cc
    |
    +--- MathFunctions.h
```
* `CMakeLists.txt`的形式改为：
  * 唯一的改动：在`add_executable`命令中增加了`MathFunctions.cc`源文件
  * 问题：若源文件很多，把所有源文件的名字都加进去将是一件烦人的工作
  * 方法：使用`aux_source_directory`命令，该命令会查找指定目录下的所有源文件，再将结果存进指定变量名
    * `aux_source_directory(<dir> <variable>)`
    * `CMake`会将当前目录所有源文件的文件名复制给变量`DIR_SRCS`，再指示变量`DIR_SRCS`中的源文件需要编译成一个名称为`Demo`的可执行文件
```
# CMake 最低版本号要求
cmake_minimum_required (VERSION 2.8)

# 项目信息
project (Demo2)

# 指定生成目标
add_executable(Demo main.cc MathFunctions.cc)
```
```
# CMake 最低版本号要求
cmake_minimum_required (VERSION 2.8)

# 项目信息
project (Demo2)

# 查找当前目录下的所有源文件
# 并将名称保存到 DIR_SRCS 变量
aux_source_directory(. DIR_SRCS)

# 指定生成目标
add_executable(Demo ${DIR_SRCS})
```

### 多个目录，多个源文件
* 将`MathFunctions.h`和`MathFunctions.cc`文件移动到`math`目录下
* 工程形式为：
```
./Demo3
    |
    +--- main.cc
    |
    +--- math/
          |
          +--- MathFunctions.cc
          |
          +--- MathFunctions.h
```
* 需要分别在项目根目录`Demo3`和`math`目录里各编写一个`CMakeLists.txt`文件
* 为了方便，可以先将`math`目录里的文件编译成静态库再由`main`函数调用
* 根目录中的`CMakeLists.txt`：
  * 使用命令`add_subdirectory`指明本项目包含一个子目录`math`，这样`math`目录下的`CMakeLists.txt`文件和源代码也会被处理
  * 使用命令`target_link_libraries`指明可执行文件`Demo`需要一个名为`MathFunctions`的链接库
```
# CMake 最低版本号要求
cmake_minimum_required (VERSION 2.8)

# 项目信息
project (Demo3)

# 查找当前目录下的所有源文件
# 并将名称保存到 DIR_SRCS 变量
aux_source_directory(. DIR_SRCS)

# 添加 math 子目录
add_subdirectory(math)

# 指定生成目标 
add_executable(Demo main.cc)

# 添加链接库
target_link_libraries(Demo MathFunctions)
```
* 子目录`math`中的`CMakeLists.txt`文件：
  * 在该文件中使用命令`add_library`将源文件编译为静态链接库
```
# 查找当前目录下的所有源文件
# 并将名称保存到 DIR_LIB_SRCS 变量
aux_source_directory(. DIR_LIB_SRCS)

# 生成链接库
add_library (MathFunctions ${DIR_LIB_SRCS})
```
