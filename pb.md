



## 定义服务（service）
* 将消息类型用在RPC（远程过程调用）框架中，可以在.proto文件中定义一个RPC service接口
* protocol buffer编译器根据选择的不同语言生成service接口代码和stub
* 例子：定义一个RPC service，其方法能够接收SearchRequest并返回SearchResponse
```
service SearchService {
   rpc Search(SaerchRequest) returns (SearchResponse);
}
```
