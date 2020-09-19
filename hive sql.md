pycharm : ctrl+shift+f全局查找某个关键字

create table if not exists
grouping sets
数据类型：struct map
in ()


## 切换数据库：
`use 数据库;`
## 创建表：
* `describe formatted db1.table1;`：
  * 查看建表相关的各种配置属性及默认属性
  * 建表的一些属性（如：location、storage information等）没有直接配置，选择系统默认
  * 使用'\t'制表符作为字段的分隔符
* 默认为内部表
* 内部表和外部表的区别：
```
create table `db1.table1` (
  `feature1` string,
  `feature2` bigint)
partitioned by (feature0 string)
row format delimited fields terminated by '\t';
```
* show databases; # 查看数据库
* use 数据库; # 进入某个数据库
* show tables; # 展示所有表
* desc 表名; # 显示表结构
* show partitions 表名; # 显示表名的分区
* show create 表名; # 显示创建表的结构

# 建表语句
* use 数据库; create table 表名; # 内部表
* create table 表名1 like 表名2; # 创建表1，结构跟表2一样
* use 数据库; create external table ....#TODO

# 表结构修改
* use 数据库; alter table 原表名 rename to 新表名; # 重命名表
* alter table 表名 add columns (列名 数据类型 [comment 列说明]); # 增加列，[]表示可选
* alter table 表名 change 原列名 新列名 新的数据类型; # 修改列名和数据类型
* alter table 表名 replace columns #TODO
* use 数据库; drop table 表名; # 删除表
* alter table 表名 drop if exists partitions (day='20200731'); # 删除分区，外表的情况？

# 列的数据类型
* tinyint, smallint, int, bigint, float, decimal, boolean, string
* struct, array, map # 符合数据类型

# 复合数据类型
## array
* create table person (name string, work_locations array<string>)
  row format delimited
  fields terminated by '\t'
  collection items terminated by ',';

# 常用函数
* if (条件表达式, A, B); # if条件语句，若满足条件则返回A，否则返回B
* case a when b then c when d then e else f end; # case条件语句，当a为b时返回c，当a为d时返回e，否则返回f
* coalesce(v1, v2, v3, ...); # 返回列表中第一个非空元素，若所有值均为空，则返回null
* concat(string A, string B, string C, ...); # 字符串连接
* concat_ws(string sep, string A, string B, string C, ...); # 自定义分隔符sep的字符串连接
* length(); # 返回字符串的长度
* reverse(); # 反转字符串
* cast(表达式 as 数据类型); # 类型转换

# HQL与SQL的差异点

# 基本概念
* hive：
  * 基于hadoop的一个数据仓库工具，可以将结构化的数据文件映射为一张数据库库表，并提供类SQL查询功能
  * 用户接口：CLI，shell命令行
  * 元数据存储：
    * 通常是存储在关系数据库，如MySQL、derby中
    * hive的元数据：表名，表的列、分区及其属性，表的属性（是否为外部表），表的数据所在目录等
  * HQL查询结果存储在hdfs中，并随后mapreduce调用执行
  * table：
    * hive中的table和数据库中的table在概念上是类似的，每一个table在hive中都有一个相应的目录存储数据
  * partition：
    * partition对应于数据库中的partition列的密集索引
    * 但是，hive中partition的组织方式和和数据库很不相同
    * hive表中的一个partition对应于表下的一个目录，所有partition的数据都存储在对应的目录中
  * buckets:
    * buckets对指定列计算hash，根据hash值切分数据。目的是为了并行，每一个bucket对应一个文件

# 实际使用
* 更新分区中的数据：
  * insert overwrite table 表名 partition (day = '${之前的日期}')
* 建表语句：

* 


