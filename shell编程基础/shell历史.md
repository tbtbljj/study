# shell的作用：
命令解析器，解释执行用户的命令
* shell执行命令的方式：
  * 交互式（interactive）：用户输入**一条命令**，shell就解释执行一条
  * 批处理（batch）：用户事先编写一个shell脚本（script），包括**多条命令**，shell一次执行全部这些命令，无需一条条敲命令
* **注**：
  * shell脚本是解释执行的，无需编译
  * shell程序从脚本中一行行读取并执行这些命令，相当于用户把脚本中的命令一行行敲到shell提示符下执行
# shell的历史：
* UNIX系统上的shell：
  * sh (Bourne shell)：
    * Steve Bourne开发
    * 各种UNIX系统都配有sh
  * csh (C shell)：
    * Bill Joy开发，随BSD UNIX发布
    * 流程控制语句类似c语言
    * 支持很多Bourne shell所不支持的功能：作业控制、命令历史、命令行编辑
  * ksh (Korn shell)：
    * David Korn开发
    * 向后兼容sh的功能，并添加csh引入的新功能
    * 目前很多UNIX系统标准配置的shell，在这些系统上的/bin/sh往往是指向/bin/ksh的符号链接
  * tcsh (TENEX C shell)：
    * csh增强版本，引入了命令补全等功能
    * 在FreeBSD、MacOS等系统上替代了csh
  * bash (Bourne Again shell)：
    * GNU开发
    * 主要目标是与POSIX标准保持一致，同时兼顾对sh的兼容
    * 从csh和ksh借鉴了很多功能，是各种Linux发行版标准配置的shell
    * 在linux系统上/bin/sh往往是指向/bin/bash的符号链接
    * bash和sh存在很多差异：
      * bash扩展了一些命令和参数
      * bash并不完全兼容sh
* 用户在命令行输入命令后。一般情况下shell会fork并exec该命令
  * shell的内建命令除外：
    * 执行内建命令相当于调用shell进程中的一个函数，并不创建新的进程
  * 内建命令：
    * 如：cd、alias、exit等
    * 凡是用which命令查不到程序文件所在位置的命令都是内建命令（？？？存疑）
  * 内建命令会有exit status，通常也用0表示成功非0表示失败，可以用特殊变量$?读出
```
[tbtbljj@tbtbljj ~]$ echo $SHELL
/bin/bash
```
