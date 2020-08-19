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


