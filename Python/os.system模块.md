* 应用场景：在`Python`中执行`Linux`命令
* 语法：`os.system(shell_cmd)`
  * 参数：
    * `shell_cmd`：`Linux`命令，字符串格式
  * 返回值：
    * 若`Linux`命令执行成功，则返回`0`
* 实例：
```
import os

path_test = '/linjiajun/test'
if os.system('ls {}'.format(path_test)) == 0:
  print "{} exists.".format(path_test)
else:
  print '{} not exists. Creating the path.'.format(path_test)
  os.system('mkdir {}'.format(path_test))
```
