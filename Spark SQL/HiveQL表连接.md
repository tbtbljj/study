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
## `Union`
* 语法：
```
select_statement UNION [ALL | DISTINCT] select_statement UNION [ALL | DISTINCT] select_statement ...
```
* 功能：
  * 将来自多个`SELECT`语句的结果组合为单个结果集
    * `Hive 1.2.0`之前的版本只支持`UNION ALL`，不能消除重复行
    * `Hive 1.2.0`及之后的版本，`UNION`默认消除重复行
* 可选项：
  * `DISTINCT`：消除重复行
  * `ALL`：不消除重复行
* 可以在同一个查询中同时使用`UNION ALL`和`UNION DISTINCT`
  * 字段名称和类型以第一个`SELECT`语句为准
  * `DISTINCT union`覆盖其左侧的所有`ALL union`
  * `DISTINCT union`两种生成方式：
    * 显式使用`UNION DISTINCT`
    * 隐式使用不带`DISTINCT`或者`ALL`关键字的`UNION`
* `FROM`子句中的`UNI0N`：
  * 需要在`UNION`结果上进行某些操作
```
SELECT *
FROM (
  select_statement
  UNION ALL
  select_statement
) unionResult
```
```
SELECT u.id, actions.date
FROM (
    SELECT av.uid AS uid
    FROM action_video av
    WHERE av.date = '2008-06-03'
    UNION ALL
    SELECT ac.uid AS uid
    FROM action_comment ac
    WHERE ac.date = '2008-06-03'
 ) actions JOIN users u ON (u.id = actions.uid) 
```

## 公用表表达式(`Common Table Expression, CTE`)
[公用表表达式](https://cwiki.apache.org/confluence/display/Hive/Common+Table+Expression)

















