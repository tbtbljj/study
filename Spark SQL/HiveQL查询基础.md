
* 查询`table`的基本信息：`hive> desc table_name;`
* 查询整张表的数据：`hive> select * from table_name;`
* 查询`table`的部分字段数据：`hive> select col1, col2, ..., expr1, expr2, ... from table_name;`
  * 可以将字段进行某种操作的结果作为新的一列输出

* Hive中的绝大部分查询都会转化为MapReduce作业

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
