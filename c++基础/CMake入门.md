# CMake入门实战
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
* 编写`CMakeLists.txt`
  * 先编写`CMakeLists.txt`文件，并保存在于`main.cc`源文件同个目录下
```
# CMake 最低版本号要求
cmake_minimum_required (VERSION 2.8)

# 项目信息
project (Demo1)

# 指定生成目标
add_executable(Demo main.cc)
```
