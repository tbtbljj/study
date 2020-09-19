# Hive数据类型
[Hive数据类型](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Types#LanguageManualTypes-StringsstringStrings)

## 概述
* 数值类型（Numeric Types）：

|类型|说明|
|-|-|
|TINYINT|1字节有符号整数：[-128, 127]|
|SMALLINT|2字节有符号整数：[-32768, 32,767]|
|INT/INTEGER|4字节有符号整数：[-2147483648, 2147483647]|
|BIGINT|8字节有符号整数：[-9223372036854775808, 9223372036854775807]|
|FLOAT|4字节单精度浮点数|
|DOUBLE|8字节双精度浮点数|
|DECIMAL|Hive 0.11.0引入，精度为38 digits；Hive 0.13.0引入了 user-definable precision and scale|
|NUMERIC|跟DECIMAL一样，Hive 3.0.0引入|

* 日期/时间类型（Date/Time Types）：

|类型|说明|
|-|-|
|TIMESTAMP|Hive 0.8.0引入|
|DATE|Hive 0.12.0引入|
|INTERVAL|Hive 1.2.0引入|

* 字符串类型（String Types）：

|类型|说明|
|-|-|
|STRING||
|VARCHAR|Hive 0.12.0引入|
|CHAR|Hive 0.13.0引入|

* Misc Types：

|类型|说明|
|-|-|
|BOOLEAN||
|BINARY|Hive 0.8.0引入|

* 复杂类型（Complex Types）：

|类型|说明|
|-|-|
|ARRAY<data_type>||
|MAP<primitive_type, data_type>|Hive 0.14 允许使用负值和非常量表达式|
|STRUCT<col_name: data_type [COMMENT col_comment], ...>|Hive 0.14 允许使用负值和非常量表达式|
|UNIONTYPE<data_type, data_type, ...>|Hive 0.7.0引入|

## 列类型
* 整型（TINYINT, SMALLINT, INT/INTEGER, BIGINT）
  * 默认情况下，整型值假定为INT
  * 例外：
    * 整型值超过了INT类型的表示范围，此时类型为BIGINT
    * 整型值加上后缀
  * Hive 2.2.0引入INT的同义词INTEGER

|类型|后缀|例子|
|-|-|-|
|TINYINT|Y|100Y|
|SMALLINT|S|100S|
|BIGINT|L|100L|

* String：
  * string值可以用单引号（'）或者双引号（"）表示
  * string值中的字母区分大小写
  * Hive uses C-style escaping within the strings
  
* Varchar：
  * 创建时指定长度说明符（length specifier，[1, 65535]），其定义了字符串中允许的最大字符数
  * 若将一个字符串值转化/赋值给一个varchar值超过指定的最大字符数，则该字符串会被截断
  * 与string类型一样，在varchar类型中尾随空格（trailing whitespace）重要且会影响对比结果
  * 局限性：
    * 非泛型（non-generic）UDFs不能直接使用varchar类型作为输入参数或者返回值
    * 可以创建string UDFs，将varchar值转化为string值，从而传递给UDF
    * 若要使用varchar参数或者返回varchar值，则可以创建GenericUDF
  * Hive 0.12.0引入Varchar类型

* Char：
  * 与varchar类似
  * 固定长度，最大长度为255
    * 字符数目少于指定长度时填充空格
  * 在字符串对比中尾随空格不重要
  * 在Hive 0.13.0引入char类型
```
CREATE TABLE foo (bar CHAR(10))
```

* Timestamp：
  * 支持传统的UNIX时间戳，可选纳秒精度
  * 支持的转换：
    * 整数数值类型：以秒单位的UNIX时间戳
    * 浮点数值类型：以秒单位的UNIX时间戳，具有小数精度
    * 字符串：JDBC兼容的java.sql.Timestamp格式"YYYY-MM-DD HH:MM:SS.fffffffff"（9位小数精度）
  * 没有时区（timezoneless），offset from the UNIX epoch
  * 提供了跟timezone进行转换的UDFs
    * to_utc_timestamp
    * from_utc_timestamp
  * text文件中的时间戳格式：yyyy-mm-dd hh:mm:ss[.f...]
    * 若使用其他格式，则声明其为合适的类型（INT, FLOAT, STRING, etc.）并使用UDF将其转化为时间戳
  * Hive 0.8.0引入了timstamp类型
  
* Date：
  * Date值描述特定的年月日，格式：YYYY-MM-DD，如：2013-01-01
  * Date类型不包含一天中的时间
  * Date类型取值范围：从0000-01-01到9999-12-31
  * Hive 0.12.0引入了Date类型
  * Date类型只能在Date、Timestamp、string之间进行转换
  
|Date类型的有效转换|结果|
|-|-|
|cast(date as date)|相同的date值|
|cast(timestamp as date)|根据当地时区确定timestamp中的年月日，返回date值|
|cast(string as date)|若string的形式为'YYYY-MM-DD'，则返回与该年月日对应的date值；若string值不是上述格式，则返回NULL|
|cast(date as timestamp)|timestamp值对应于date值的年月日，时间为当地时区的午夜|
|cast(date as string)|date值中的年月日格式化为string值，形式为：'YYYY-MM-DD'|
