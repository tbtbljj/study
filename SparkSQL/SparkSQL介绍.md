# SparkSQL的发展
## 简述
* Spark生态体系中，构建在Spark core基础上的一个基于SQL的计算模块
  * Spark core：Spark核心，Spark最基础的一部分
  * 利用SparkSQL完成数据分析的工作
* `Shark`:
  * `SparkSQL`最开始的名称
  * 基于代码优化、SQL解析、Hive执行引擎
  * 随着`Shark`技术发展，其执行速度远远快于`Hive`，故`Hive`制约了`Shark`的发展
  * 在2015年，`Shark`项目结束。新的项目`SparkSQL`，不依赖于`Hive`，做到了独立的发展
  
  
  
