# `Spark SQL`函数
## 说明：
* `SQL`中都有函数的概念，对应于其他编程语言中的方法/函数
* `Spark SQL`的函数与`HiveQL`的函数是通用的

## 函数分类：
* 内置函数、自定义函数（`UDF`）
* 数学函数：
  * `round`：
    * `round(x[, d])` - 将`x`四舍五入到小数点后`d`位
    * 默认保留`0`位小数，即返回结果为整数
    * `d`为`0`，表示保留个位数；`d`为`-1`，表示保留十位数；...
  * `floor`：
    * `floor(x)` - 求不大于`x`的最大整数
  * `ceil`：
    * `ceil(x)` - 求不小于`x`的最小整数
  * `rand`：
    * `rand([seed])` - 返回`[0, 1]`之间的伪随机数
    * `seed`：
      * 第一次定义：将`seed`与具体的伪随机数绑定
      * 非第一次：返回`seed`绑定的伪随机数
  * `abs`:
    * `abs(x)` - 返回`x`的绝对值
  * `pow`：
    * `pow(x1, x2)` - 返回`x1`的`x2`次方
    * 支持负数、小数
* 条件函数：
  * `if`：
    * `IF(expr1,expr2,expr3)` - 如果`expr1`为真`(expr1 <> 0 and expr1 <> NULL)`，那么返回`expr2`，否则返回`expr3`
    * `IF()`函数返回数值或者字符串值，具体取决于使用它的上下文
  * `case when`：
    * `CASE a WHEN b THEN c [WHEN d THEN e]* [ELSE f] END` - 当`a=b`返回`c`；当`a=d`返回`e`；否则返回`f`
  * `coalesce`：
    * `coalesce(a1, a2, ...)` - 从左到右返回第一个不为`NULL`的参数
* 日期函数：
  * `current_date`：
    * `current_date()`：获取当前的日期，日期格式为标准格式：`yyyy-mm-dd`
  * `current_timestamp`：
    * `current_timestamp()`：获取当前日期的时间戳，格式为：`yyyy-mm-dd hh:mm:ss.xxx`
  * `add_months`：
    * `add_months(start_date, num_months)` - 返回`start_date`之后`num_months`个月的日期
    * `start_date: yyyy-mm-dd`，返回结果`dd`不变，月份对`12`取余
  * `date_add`：
    * `date_add(start_date, num_days)` - 返回`start_date`之后`num_days`天的日期
  * `date_sub`：
    * `date_sub(start_date, num_days)` - 返回`start_date`之前`num_days`天的日期
  * `next_day`：
    * `next_day(start_date, day_of_week)` - 返回`start_date`之后最先到星期`day_of_week`的日期
    * `day_of_week`取值：`mon、tue、wed、thu、fri、sat、sun`
  * `dayofmonth`：
    * `dayofmonth(param)` - 返回`date/timestamp`所在月份的第几天
  * `weekofyear`:
    * `weekofyear(date)` - 返回`date`是所在年份的第几个星期
    * 一周开始于星期一，第一周的天数大于3
  * `minute`：
    * `minute(param)` - 返回`string/timestamp/interval`中的分钟
  * `hour`：
    * `hour(param)` - 返回`string/timestamp/interval`中的小时
  * `day`：
    * `day(param)` - 返回`date/timestamp/interval`中的天
  * `month`：
    * `month(param)` - 返回`date/timestamp/interval`中的月份
  * `year`：
    * `year(param)` - 返回`date/timestamp/interval`中的年份
  * `date_format`:
    * `date_format(date/timestamp/string, fmt)` - 返回指定格式的日期
    * 如：fmt为'yyyy'，则返回年份
  * `datediff`：
    * `datediff(date1, date2)` - 返回`date1`和`date2`之间的天数（`date1 - date2`）
  * `to_unix_timestamp`：
    * `to_unix_timestamp(date[, pattern])` - 返回`UNIX timestamp`
    * 如：`select to_unix_timestamp(current_date())`，返回`1600099200`
  * `from_unixtime`：
    * `from_unixtime(unix_time, format)` - 返回指定格式的时间
    * 如：`select from_unixtime(1600099200)`，返回`2020-09-15 00:00:00`；`select from_unixtime(1600099200, 'yyyy')`，返回`2020`
  * `to_date`：
    * `to_date(datetime)` - 返回`datetime`中的日期部分
    * 若`datetime`不符合date的格式，则返回`NULL`
* 字符串函数：
  * `lower`：
    * `lower(str)` - 将`str`中所有的字符转为小写并返回
  * `upper`：
    * `upper(str)` - 将`str`中所有的字符转为大写并返回
  * `instr`：
    * `instr(str, substr)`：返回`substr`在`str`中第一次出现的索引
    * 索引从`1`开始，若不存在则返回`0`
  * `length`：
    * `length(str)` - 返回字符串`str`的长度
  * `substr/substring`：
    * `substr/substring(str, pos[, len])`：返回字符串`str`的子字符串，从`pos`开始，长度为`len`
    * `len`缺省表示从`pos`位置到字符串末尾
  * `concat`：
    * `concat(str1, str2, ... strN)` - 返回`str1, str2, ... strN`的拼接结果
  * `trim`：
    * `trim(str)` - 删除`str`中开头和结尾的空白字符（`space characters`）
  * `lpad`：
    * `lpad(str, len, pad)` - 将`str`左边用`pad`填充至`len`个字符，并返回`str`
    * 相当于将`pad`无限复制并连接在一起，取其前几位填充在`str`的左边，让`str`最终的字符个数为`len`
  * `rpad`：
    * `rpad(str, len, pad)` - 将`str`右边用`pad`填充至`len`个字符，并返回`str`
    * 相当于将`pad`无限复制并连接在一起，取其前几位填充在`str`的右边，让`str`最终的字符个数为`len`  
 
* 统计函数：
  * 聚合函数：将多行数据合成一行
  * `index(a, n)` - 返回`a`的第`n`个元素
    * `a`的类型：`map、list、array`等，不支持`string`
    * 索引从`0`开始
  * `sum`：
    * `sum(x)` - 返回一组数据的和
  * `count`：
    * `count(*)` - 返回检索行的总数，包括包含`NULL`的行
    * `count(expr)` - 返回所提供表达式**非空**的行数
    * `count(DISTINCT expr[, expr...])` - 返回所提供表达式**非空且唯一**的行数
  * `max`：
    * `max(expr)` - 返回`expr`中的最大值
  * `avg`：
    * `avg(x)` - 返回一组数字的平均值
  * `min`：
    * `min(expr)` - 返回`expr`中的最小值
* 特殊函数：
  * `array`：
    * `array(n0, n1...)` - 使用给定元素创建数组
  * `map`：
    * `map(key0, value0, key1, value1...)` - 创建给定键/值对的`map`
  * `collect_set`：
    * `collect_set(x)` - 返回消除重复元素的一组对象
    * 返回结果中的元素不重复
  * `collect_list`：
    * `collect_list(x)` - 返回具有重复项的对象列表
    * 返回结果中的元素允许重复
  * `explode`：
    * `explode(a)` - 将数组`array`的元素分隔为多行，或者将映射`map`的元素分隔为多行和多列
  * `cast`：
    * `cast(ele as type)`：将元素`ele`的类型转为`type`
  * `split`：
    * `split(str, regex)` - 使用`regex`正则表达式分割`str`，返回字符串数组
  * `concat_ws`：
    * `concat_ws(separator, [string | array(string)]+)` - `concat with separator`：返回有分隔符`separator`分隔的字符串组的级联
  * `size`：
    * `size(a)` - 返回`a`的元素个数


* 查询`HiveQL`中的所有函数：`hive> show functions;`
* 查询`HiveQL`中某个函数的用法：
  * 如，查询`round`函数的用法：`hive> desc function round;`
  * 查询结果：`round(x[, d]) - round x to d decimal places`
```
!
!=
$sum0
%
&
*
+
-
/
<
<=
<=>
<>
=
==
>
>=
^
abs
acos
add_months
aes_decrypt
aes_encrypt
and
array
array_contains
ascii
asin
assert_true
atan
avg
base64
between
bin
bloom_filter
bround
cardinality_violation
case
cbrt
ceil
ceiling
char_length
character_length
chr
coalesce
collect_list
collect_set
compute_stats
concat
concat_ws
context_ngrams
conv
corr
cos
count
covar_pop
covar_samp
crc32
create_union
cume_dist
current_database
current_date
current_timestamp
current_user
date_add
date_format
date_sub
datediff
day
dayofmonth
dayofweek
decode
default.indigouidhash
default.openid2imouid
degrees
dense_rank
div
e
elt
encode
ewah_bitmap
ewah_bitmap_and
ewah_bitmap_empty
ewah_bitmap_or
exp
explode
extract_union
factorial
field
find_in_set
first_value
floor
floor_day
floor_hour
floor_minute
floor_month
floor_quarter
floor_second
floor_week
floor_year
format_number
from_unixtime
from_utc_timestamp
get_json_object
get_splits
greatest
grouping
hash
hex
histogram_numeric
hour
if
in
in_bloom_filter
in_file
index
indigo_us.openid2imouid
initcap
inline
instr
internal_interval
isnotnull
isnull
java_method
json_tuple
lag
last_day
last_value
lcase
lead
least
length
levenshtein
like
ln
locate
log
log10
log2
logged_in_user
lower
lpad
ltrim
map
map_keys
map_values
mask
mask_first_n
mask_hash
mask_last_n
mask_show_first_n
mask_show_last_n
matchpath
max
md5
min
minute
mod
month
months_between
mysql_tb.indigouidhashmod
named_struct
negative
next_day
ngrams
noop
noopstreaming
noopwithmap
noopwithmapstreaming
not
ntile
nullif
nvl
octet_length
or
parse_url
parse_url_tuple
percent_rank
percentile
percentile_approx
pi
pmod
posexplode
positive
pow
power
printf
quarter
radians
rand
rank
reflect
reflect2
regexp
regexp_extract
regexp_replace
regr_avgx
regr_avgy
regr_count
regr_intercept
regr_r2
regr_slope
regr_sxx
regr_sxy
regr_syy
repeat
replace
replicate_rows
reverse
rlike
round
row_number
rpad
rtrim
second
sentences
sha
sha1
sha2
shiftleft
shiftright
shiftrightunsigned
sign
sin
size
sort_array
sort_array_by
soundex
space
split
sq_count_check
sqrt
stack
std
stddev
stddev_pop
stddev_samp
str_to_map
struct
substr
substring
substring_index
sum
tan
tmp.domianfind
tmp.replaceall
tmp.timescount
tmp.urlfind
to_date
to_unix_timestamp
to_utc_timestamp
translate
trim
trunc
ucase
unbase64
unhex
unix_timestamp
upper
uuid
var_pop
var_samp
variance
version
weekofyear
when
windowingtablefunction
xpath
xpath_boolean
xpath_double
xpath_float
xpath_int
xpath_long
xpath_number
xpath_short
xpath_string
year
|
~
```
