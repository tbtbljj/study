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























