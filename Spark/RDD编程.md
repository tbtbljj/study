# 创建`RDD` 
* 两种方式：
  * `textFile`加载本地或者集群文件系统中的数据
  * 用`parallelize`方法将`Driver`中的数据结构并行化成`RDD`




# 常用`Action`操作
* `collect()`：
  * 返回包含该`RDD`所有元素的列表
  * 注：该方法应该只在结果数组较小的情况下被使用，因为所有数据被加载到`Driver`的内存中
