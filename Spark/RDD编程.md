# 创建`RDD` 
* 两种方式：
  * `textFile`加载本地或者集群文件系统中的数据
  * 用`parallelize`方法将`Driver`中的数据结构并行化成`RDD`
```
# 用parallelize方法将Driver中的数据结构生成RDD，第二个参数指定分区数
rdd = sc.parallelize(range(1, 11), 2)
print rdd.collect()  # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```




# 常用`Action`操作
`Action`操作将触发基于`RDD`依赖关系的计算
* `collect()`：
  * 返回包含该`RDD`所有元素的列表
  * 注：该方法应该只在结果数组较小的情况下被使用，因为所有数据被加载到`Driver`的内存中
```
rdd = sc.parallelize(range(10), 5)
data = rdd.collect()
print data  # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

* `reduce(f)`：
  * 使用指定的满足交换律和结合律的二元算子，从而减少该`RDD`的元素
```
rdd = sc.parallelize(range(10), 5)
sum = rdd.reduce(lambda x, y: x + y)
print type(sum), sum  # <type 'int'> 45
```

* `countByKey()`：
  * 计算每个键的元素数量，并将结果（字典数据类型）返回给`master`
```
pairRdd = sc.parallelize([(1, 1), (1, 4), (3, 9), (2, 16)])
dct = pairRdd.countByKey()
print type(dct), dct  # <type 'collections.defaultdict'> defaultdict(<type 'int'>, {1: 2, 2: 1, 3: 1})
```

* `saveAsTextFile(path)`：




# 常用`Transformation`操作
`Transformation`操作具有懒惰执行的特性，只指定新的`RDD`与其父`RDD`的依赖关系，只有当`Action`操作触发到该依赖时，该`Transformation`操作才会被计算
* `map(f)`：
  * 通过对该`RDD`的每个元素应用函数`f`，从而返回一个新的`RDD`
```
rdd = sc.parallelize(range(10), 3)
print rdd.collect()  # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
print rdd.map(lambda x: x**2).collect()  # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

* `filter(f)`：
  * 返回一个仅包含满足条件的元素的新的RDD
```
rdd = sc.parallelize(range(10), 3)
print rdd.collect()  # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
print rdd.filter(lambda x: x > 5).collect()  # [6, 7, 8, 9]
```
