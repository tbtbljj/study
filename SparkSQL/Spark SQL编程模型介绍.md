# `Spark SQL`编程模型介绍
## 编程模型简介
* 操作`Spark SQL`的两种主要方式：
  * `SQL`：
    * `HiveQL`操作的对象是**表**，使用`Spark SQL`进行操作前，需要将其对应的**编程模型**转化为**表/视图**
    * 同时支持`SQL`和`HiveQL`
  * `DataFrame`和`DataSet`：
    * `DataFrame`：
      * `Spark SQL`的第二代编程模型
      * `Spark 1.3`引入的编程模型
      * 早期的时候称为`SchemaRDD`
        * 与`RDD`相比，多了一个`Schema`（表明，表字段，字段类型），即**元数据**信息
    * `DataSet`：
      * `Spark SQL`的第三代编程模型
      * `Spark 1.6`引入的编程模型
        * `Flink`底层用到`DataSet`
        * `Spark core`使用`RDD`作为第一代编程模型，`RDD`在第三代编程模型中已被淘汰
      * 吸收`RDD`的有点和`DataFrame`的优化（`SQL`优化引擎、内存的列式存储）
    * `DataFrame`和`DataSet`可以理解为一张`MySQL`的二维表，有表头、表明、表字段、字段类型以及数据
      * `RDD`也可以理解为一张表，但是其只有数据

