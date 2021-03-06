* 查询的语法：
  * `DISTRIBUTE BY`：指定分发器（Partitioner），多`Reducer`可用
```
SELECT [ALL | DISTINCT] select_expr, select_expr, ...
FROM table_reference
[WHERE where_condition]
[GROUP BY col_list]
[CLUSTER BY col_list | [DISTRIBUTE BY col_list] [SORT BY col_list] | [ORDER BY col_list]]
[LIMIT number]
```
* 查询`table`的基本信息（字段名称、字段类型、分区名称、分区类型等）：`hive> desc table_name;`
* `Hive`中的绝大部分查询都会转化为`MapReduce`作业
* 查询整张表的数据：`hive> select * from table_name;`
* 查询`table`的部分字段数据：`hive> select col1, col2, ..., expr1, expr2, ... from table_name;`
  * 可以将字段进行某种操作的结果作为新的一列输出
  * 若表达式中某些字段为`NULL`，则其结果为`NULL`
    * `NULL`不区分大小写
    * 判断表达式的结果是否为`NULL`:
      * `is NULL`
      * `is not NULL`
* `nvl()`函数：
  * `nvl(value, default_value)` - 若`value`为`null`则返回`default_value`，否则返回`value`
* `DISTINCT`关键字：
  * `DISTINCT col1, col2, ...`：输出`col1, col2, ...`所有不同的组合
* `WHERE`子句：
  * `WHERE`子句对`FROM`后面表中的记录先进行过滤，`SELECT`查询的范围是满足`WHERE`子句过滤条件的那一部分记录
  * `WHERE`子句后面可以跟上多个过滤条件，过滤条件之间用逻辑运算符连接，如：`AND、OR`
  * `LIKE`关键字：
  * 通配符：
  * 转义字符：
* `ORDER BY`子句：
  * 默认按照**升序**进行排列
  * 若要按照**降序**进行排列，则需在`ORDER BY col`后面加上`desc`
  * `ORDER BY`后面可以跟：字段名称、表达式、别名（使用`AS`）
  * `NULL`在升序下排在最前面，在降序下排在最后面
    
  

