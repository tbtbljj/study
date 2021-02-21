[codecs模块官方文档](https://docs.python.org/3/library/codecs.html)


## codecs.open()方法
* 语法：open(filename, mode='r', encoding=None, errors='strict', buffering=-1)
  * 使用给定mode打开一个encoded文件，并返回一个StreamReaderWriter实例
  * `mode`：
    * 默认文件mode为`r`，即以读模式打开文件
    * 底层编码文件总是以二进制模式（binary mode）打开，读写时不会自动转换`\n`
    * `mode`参数可以是内建函数`open()`接受的任何二进制模式，`b`自动添加
  * `encoding`：
    * 指定用于文件的编码
    * 支持对`bytes`进行编码和解码的任何编码
