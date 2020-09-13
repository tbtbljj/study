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
* `Hadoop`生态体系中：`MapReduce`作底层计算，`Hive SQL`，`Redis`
* `Spark SQL`的特性：
  * `Integrated`：集成
    * `Spark`程序支持**`SQL`查询**
    * `Spark SQL`支持在Spark`程序中使用`SQL`或者`DataFrame API`查询结构化数据
    * 支持的语言：`Jave、Scala、Python、R`
  * `Uniform Data Access`：统一的数据访问
    * 以相同的方式连接到任何数据源
    * `DataFrames`和`SQL`提供了访问各种数据源的通用方法，包括`Hive、Avro、Parquet、ORC、JSON、JDBC`，甚至可以跨越不同数据源连接数据
      * `Avro`：`Hadoop`的一个数据序列化系统，设计用于支持大批量数据交换的应用
  
  
  
