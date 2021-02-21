


## codecs.open()方法
* 语法：open(filename, mode='r', encoding=None, errors='strict', buffering=-1)
  * 使用给定mode打开一个encoded文件，并返回一个StreamReaderWriter实例
  * 默认文件mode为`r`，即以读模式打开文件
  * 注：
    * 底层编码文件总是以二进制模式（binary mode）打开，读写时不会自动转换`\n`
    * `mode`参数可以是内建函数`open()`接受的任何二进制模式，`b`自动添加
  
