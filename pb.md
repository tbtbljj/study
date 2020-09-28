
## 定义`message`类型
* 例子：定义`search request message`的`.proto`文件如下：
  * 文件第一行指定使用`proto3`语法：
    * 若没有指定则`protocol buffer`编译器默认使用`proto2`语法
    * 必须是文件的第一个非空、非注释行
  * `SearchRequest message`定义指定了3个`field`
    * 每个`field`具有一个名称和类型
```
syntax = "proto3";

message SearchRequest {
  string query = 1;
  int32 page_number = 2;
  int32 result_per_page = 3;
}
```
### 指定`field`类型
* 标量类型（`scalar types`）
  * 上述例子中的所有`field`均为标量类型
* 复合类型（`composite types`）
### 分配`field`编号
* `message`定义中的每个`field`都有一个不同的编号
* 

## 定义服务（service）
* 将消息类型用在RPC（远程过程调用）框架中，可以在.proto文件中定义一个RPC service接口
* protocol buffer编译器根据选择的不同语言生成service接口代码和stub
* 例子：定义一个RPC service，其方法能够接收SearchRequest并返回SearchResponse
```
service SearchService {
   rpc Search(SaerchRequest) returns (SearchResponse);
}
```
