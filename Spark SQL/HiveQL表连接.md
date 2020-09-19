## 表连接
* 等值连接：
  * 连接条件为等号
* 不等值连接：
  * 连接条件不为等号
* 外连接：
  * 可以将对于连接条件不成立的记录仍然包含在最后的结果中
  * 分类：
    * 左外连接
    * 右外连接
* 自连接：
  * 通过表的别名将同一张表视为多张表
  
## 子查询
[子查询](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+SubQueries)
* `FROM`子句中的子查询：
  * 子查询必须拥有一个名称，因为`FROM`子句中的每个表必须具有一个名称
  * 子查询的`select`列表中的列可以在外部查询中使用，就像一个表中的列一样
  * 例子：
```
SELECT ... FROM (subquery) name ... (Hive 0.12)
SELECT ... FROM (subquery) AS name ... (Hive 0.13.0)
```
```
SELECT col
FROM (
  SELECT a+b AS col
  FROM t1
) t2
```
* `WHERE`子句中的子查询：
  * 自`Hive 0.13`起，`WHERE`子句中支持部分类型的子查询
  * 这些查询的结果能够视为`IN`和`NOT IN`语句的常量
  * 称为**不相关子查询**，因为子查询不引用父查询中的列
  * 若子查询的返回结果中存在`NULL`则不能使用`NOT IN`，只能使用`IN`
  * 局限性：
    * `IN`和`NOT IN`子查询只能`select`一列
```
SELECT *
FROM A
WHERE A.a IN (SELECT foo FROM B);
```

