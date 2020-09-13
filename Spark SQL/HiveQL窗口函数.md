## `HiveQL`窗口函数的语法
* `over()`窗口函数的语法：
  * 分析函数 `over([partition by 列名] [order by 列名] [rows between 开始位置 and 结束位置])`
    * `partition by 列名`：
      * 相当于`group by 列名`，分析函数按照每一组的数据进行计算
    * `[rows between 开始位置 and 结束位置]`：
      * 指定窗口范围，如：第一行到当前行，且这个范围随着行数变化
      * 搭配分析函数时，分析函数按照这个范围进行计算
      * 经常使用的窗口范围：`ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`（表示从起点到当前行）
 ```
PRECEDING：往前
FOLLOWING：往后
CURRENT ROW：当前行
UNBOUNDED：（一般结合PRECEDING，FOLLOWING使用）
UNBOUNDED PRECEDING 表示该窗口最前面的行（起点）
UNBOUNDED FOLLOWING：表示该窗口最后面的行（终点）
例子：
ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW（表示从起点到当前行）
ROWS BETWEEN 2 PRECEDING AND 1 FOLLOWING（表示往前2行到往后1行）
ROWS BETWEEN 2 PRECEDING AND 1 CURRENT ROW（表示往前2行到当前行）
ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING（表示当前行到终点）
 ```
* 与over()窗口函数一起使用的常见分析函数：
  * 聚合类：
    * `avg()、sum()、max()、min()`
  * 排名类：
    * `row_number()`：按照相应数值进行排序时产生一个自增编号，不重复，如：`1、2、3、4、5、...`
    * `rank()`：按照相应数值进行排序时产生一个自增编号，数值相等时重复，并产生空位，如：`1、2、3、3、5、...`
    * `dense_rank()`：按照相应数值进行排序时产生一个自增编号，数值相等时重复，不产生空位，如：`1、2、3、3、4、...`
  * 其他：
    * `lag`：
      * `LAG  (scalar_expression [,offset] [,default]) OVER ([query_partition_clause] order_by_clause);` ：lag()函数用于访问前面行的数据
    * `lead`：
      * `LEAD (scalar_expression [,offset] [,default]) OVER ([query_partition_clause] order_by_clause);` ：lead()函数用于返回后面行的数据
    * `ntile`：
      * `ntile(n)`：把有序分区的行分配到指定数量的大致相等的组中，每个组的编号从`1`开始。对于每一行，`ntile()`函数返回其所属组的编号
