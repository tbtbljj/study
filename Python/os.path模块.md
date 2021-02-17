
## join()方法
* 功能：将目录和文件名合成一个路径
* 语法：`os.path.join(path1[, path2[, ...]])`
  * 参数：`path1, path2, ...`均为字符串
  * 返回值：字符串`path1\path2\...`
* 实例：
```
data_path = os.path.join('root', 'linjiajun', "test.py")
print data_path  # root/linjiajun/test.py
```
