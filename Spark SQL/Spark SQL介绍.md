# SparkSQL的发展
## 简述
* [`Spark SQL`官网](http://spark.apache.org/sql/)
* Spark生态体系中，构建在Spark core基础上的一个基于SQL的计算模块
  * Spark core：Spark核心，Spark最基础的一部分
  * 利用SparkSQL完成**数据分析、统计**的工作
* `Shark`:
  * `Spark SQL`最开始的名称
  * 基于代码优化、SQL解析、Hive执行引擎
  * 随着`Shark`技术发展，其执行速度远远快于`Hive`，故`Hive`制约了`Shark`的发展
  * 在2015年，`Shark`项目结束。新的项目`Spark SQL`，不依赖于`Hive`，做到了独立的发展
* 两条相互独立的业务：
  * `Spark SQL`
  * `Hive-on-Spark`
* `Hadoop`生态体系中：`MapReduce`作底层计算，`HiveQL`，`Redis`

## 特性
* `Spark SQL`的特性：
  * `Integrated`：集成
    * `Spark`程序（`Spark core`程序）支持`SQL`**查询**
    * `Spark SQL`支持在`Spark`程序中使用`SQL`或者`DataFrame API`查询结构化数据
      * `Spark`第一代数据模型：`RDD`，第二代数据模型：`DataFrame`，第三代数据模型：`DataSet`
    * 支持的语言：`Jave、Scala、Python、R`
  * `Uniform Data Access`：统一的数据访问
    * 以相同的方式连接到任何数据源
    * `DataFrames`和`SQL`提供了访问各种数据源的通用方法，包括`Hive、Avro、Parquet、ORC、JSON、JDBC`，甚至可以跨越不同数据源连接数据
      * `Avro`：`Hadoop`的一个数据序列化系统，设计用于支持大批量数据交换的应用
      * 大数据把不同数据源收集在一起进行处理
  * `Hive Integration`：`Hive`集成
    * 在现有数据仓库上运行`SQL`或者`HiveQL`查询
    * `Spark SQL`支持`HiveQL`语法以及`Hive SerDes`和`UDF`，允许访问现有的`Hive`仓库
  * `Standard Connectivity`：
    * 通过`JDBC、ODBC`连接
    * 服务器模式为商业智能工具提供了行业标准`JDBC`和`ODBC`的连接
  * 总结：
    * `Spark SQL`兼容性强，可以利用之前的代码来执行`Spark`引擎，学习成本低
    * `Spark SQL`是`Spark`生态体系中用于处理**结构化数据**的一个计算模块
      * 结构化数据：存储在`RDBMS`中的数据
      * 半结构化数据：如，`xml、json`等
      * 非结构化数据：如，音频、视频、图片等
  
