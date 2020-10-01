# `sed`
* 定义：
  * `Stream Editor`：流编辑器
* 应用场景：
  * 一般在`Shell`脚本和`Makefile`中作为**过滤器**使用
  * 把前一个程序的输出作为`sed`的输入，经过一系列编辑命令对文本进行**格式转换**
  * perform basic **text transformations** on an input stream (a file or input from a pipeline)
  * **filter text** in a pipeline
* `sed`和`vi`都源于早期`UNIX`的`ed`工具，故很多`sed`命令和`vi`的**末行命令**是相同的
* 语法：`sed [options] {script only if no other script} [input files]`
* 选项：
  * `-n`或者`--quiet`或者`--silent`：
    * 抑制`pattern space`的自动输出
  * `-e script`或者`--expression=script`：
    * 将`script`添加到要执行的命令里面
  * `-f script-file`或者`--file=script-file`：
    * 将`script-fille`中的内容添加到要执行的命令里面
  * `-r`或者`--regexp-extended`:
    * 在`script`中使用`extended`正则表达式
  * `--help`：
    * 显示帮助文档
  * `--version`;
    * 显示版本信息
  * 注：
    * 若没有给定`-e、--expression、-f、--file`选项
      * 第一个非选项的参数将作为`sed`的`script`来解析
      * 剩下的所有参数是输入文件的名称
      * 若没有指定输入文件，则读取标准输入
  
