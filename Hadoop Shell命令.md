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

* `cat`：
  * 使用方法：`$ hadoop fs -cat URI [URI ...]`
    * 将路径指定文件的内容输出到`stdout`
  * 返回值:
    * 成功返回`0`
    * 失败返回`-1`
  * 示例：
```
$ hadoop fs -cat hdfs://host1:port1/file1 hdfs://host2:port2/file2
$ hadoop fs -cat file:///file3 /user/hadoop/file4
```

* `cp`：
  * 使用方法：`$ hadoop fs -cp URI [URI ...] <dest>`
    * 将文件从源路径复制到目标路径
    * 允许有多个源路径，此时目标路径必须是一个目录
    * 路径可以是本地路径
  * 返回值:
    * 成功返回`0`
    * 失败返回`-1`
  * 示例：
```
$ hadoop fs -cp /user/hadoop/file1 /user/hadoop/file2
$ hadoop fs -cp /user/hadoop/file1 /user/hadoop/file2 /user/hadoop/dir
```

* `get`：
  * 使用方法：`$ hadoop fs -get <src> <localdst>`
    * 复制文件到本地文件系统
  * 返回值:
    * 成功返回`0`
    * 失败返回`-1`
  * 示例：
```
$ hadoop fs -get /user/hadoop/file localfile
$ hadoop fs -get hdfs://host:port/user/hadoop/file localfile
```

* `ls`：
  * 使用方法：`$ hadoop fs -ls <args>`
    * 若是文件则按照如下格式返回文件信息：
      * `文件名 <副本数> 文件大小 修改日期 修改时间 权限 用户ID 组ID`
    * 若是目录则返回直接子文件的列表，目录返回列表的信息如下：
      * `目录名 <dir> 修改日期 修改时间 权限 用户ID 组ID`
  * 返回值:
    * 成功返回`0`
    * 失败返回`-1`
  * 示例：
```
$ hadoop fs -ls /user/hadoop/file1 /user/hadoop/file2 hdfs://host:port/user/hadoop/dir1 /nonexistentfile
```

* `mkdir`：
  * 使用方法：`hadoop fs -mkdir <paths>`
    * 接受路径指定的`URI`作为参数，创建这些目录
    * 类似于`Unix`系统的`mkdir -p`，会创建路径中的各级父目录
  * 返回值:
    * 成功返回`0`
    * 失败返回`-1`
  * 示例：
```
$ hadoop fs -mkdir /user/hadoop/dir1 /user/hadoop/dir2
$ hadoop fs -mkdir hdfs://host1:port1/user/hadoop/dir hdfs://host2:port2/user/hadoop/dir
```

* `mv`：
  * 使用方法：`hadoop fs -mv URI [URI …] <dest>`
    * 将文件从源路径移动到目标路径
    * 允许有多个源路径，此时目标路径是一个目录
    * 不允许在不同的文件系统间移动文件
  * 返回值:
    * 成功返回`0`
    * 失败返回`-1`
  * 示例：
```
$ hadoop fs -mv /user/hadoop/file1 /user/hadoop/file2
$ hadoop fs -mv hdfs://host:port/file1 hdfs://host:port/file2 hdfs://host:port/file3 hdfs://host:port/dir1
```

* `put`:
  * 使用方法：`hadoop fs -put <localsrc> ... <dst>`
    * 从本地文件系统中复制单个或多个源路径到目标文件系统
    * 也支持从标准输入中读取输入写入目标文件系统
  * 返回值:
    * 成功返回`0`
    * 失败返回`-1`
  * 示例：
```
$ hadoop fs -put localfile /user/hadoop/hadoopfile
$ hadoop fs -put localfile1 localfile2 /user/hadoop/hadoopdir
$ hadoop fs -put localfile hdfs://host:port/hadoop/hadoopfile
$ hadoop fs -put - hdfs://host:port/hadoop/hadoopfile # 从标准输入中读取输入
```

* `rm`：
  * 使用方法：`hadoop fs -rm URI [URI …]`
    * 删除指定的文件，只删除空目录和文件
  * 返回值:
    * 成功返回`0`
    * 失败返回`-1`
  * 示例：
```
hadoop fs -rm hdfs://host:port/file /user/hadoop/emptydir
```

* `rmr`：
  * 使用方法：`hadoop fs -rmr URI [URI ...]`
    * `delete`的递归版本
  * 返回值:
    * 成功返回`0`
    * 失败返回`-1`
  * 示例：
```
$ hadoop fs -rmr /user/hadoop/dir
$ hadoop fs -rmr hdfs://host:port/user/hadoop/dir 
```
