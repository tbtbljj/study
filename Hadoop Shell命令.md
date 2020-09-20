[Hadoop Shell命令](https://hadoop.apache.org/docs/r1.0.4/cn/hdfs_shell.html)
* `FS Shell`：
  * 使用文件系统（`FS`）`Shell`命令的形式：
    * `bin/hadoop fs <args>`
  * 所有的`FS Shell`命令使用`URI`路径作为参数：
    * `URI`格式：`scheme://authority/path`
      * 对于`HDFS`文件系统，`scheme`为`hdfs`
      * 对于本地文件系统，`scheme`为`file`
      * `scheme`和`authority`参数都是可选的，若未加指定则会使用配置中指定的默认`scheme`
      * 例子，一个`HDFS`文件/目录（如：`/parent/child`）可以表示成`hdfs://namenode:namenodeport/parent/child`，或者`/parent/child`（配置文件中的默认值为`namenode:namenodeport`）
  * 大多数`FS Shell`命令的行为和对应的`Unix Shell`命令类似
  * 出错信息输出到`stderr`，其他信息输出到`stdout`

* 









* 从hdfs导出文件到本地  
`hadoop fs -get hdfs文件的路径 本地路径`
