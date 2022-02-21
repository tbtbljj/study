## 在线

## 离线
* 模型网络
  * 用户历史行为
    * 获取用户历史行为特征对应的embedding，维度为[B, H\*S\*E]
      * `B`：batch大小
      * `H`：用户历史(history)行为特征数量
      * `S`：session长度
      * `E`：embedding长度(如16)
    * reshape操作，维度为[B, H, S*E]
      * tf.reshape()
    * average pooling操作，维度为[B, S*E]
      * 对相同样本的不同特征对应的embedding进行取平均操作
      * tf.reduce_mean()
    * bn操作，维度为[B, S*E]
      * tf.layers.batch_normalization()
    * reshape操作，维度为[B, S, E]
      * tf.reshape()
    * 兴趣网络
      * B2ICapsules函数
        * 输入
          * 用户历史行为embedding，维度为[B, S, E]
          * 兴趣胶囊数量(如3)
          * 
