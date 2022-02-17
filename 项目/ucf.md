## 在线


## 离线
* 模型网络(双塔)
  * 批处理(假设batch大小为B)
  * user侧
    * 将sparse特征映射为embedding向量(假设维度为E)
    * 将每个sparse特征(假设U个user特征)对应的embedding向量进行concat操作，维度为[B, U*E]
    * bn操作，维度为[B, U*E]
      * tf.layers.batch_normalization()
    * reshape操作，维度为[B, U, E]
      * tf.reshape()
    * average pooling操作，维度为[B, E]
      * 对相同样本的不同特征对应的embedding进行取平均操作
      * tf.reduce_mean()
  * item侧
    * 将sparse特征映射为embedding向量(假设维度为E)
    * 将每个sparse特征(假设I个item特征)对应的embedding向量进行concat操作，维度为[B, I*E]
    * bn操作，维度为[B, I*E]
      * tf.layers.batch_normalization()
    * reshape操作，维度为[B, I, E]
      * tf.reshape()
    * average pooling操作，维度为[B, E]
      * 对相同样本的不同特征对应的embedding进行取平均操作
      * tf.reduce_mean()
  * 内积
    * 计算user侧向量与item侧向量的余弦相似度，维度为[B, 1]
      * tf.keras.layers.Dot()
  * 位置偏差(position bias)
    * one hot编码
      * 下发/展现位置为1，其他位置为0
      * 维度为[B, P]
    * 将余弦相似度与位置偏差进行concat操作，维度为[B, 1+P]
      * tf.concat()
  * 经过一层全连接网络，维度为[B, 1]
    * 不使用激活函数
    * tf.layers.dense()
  * 值域截断
    * [-10, 10]
    * tf.clip_by_value()
  * 模型输出
    * sigmoid激活函数
      * tf.sigmoid()
  * 损失函数
    * 交叉熵
    * 每个样本根据用户行为设置不同的权重，每个样本的loss的加权和作为最终的loss
* 模型特征
  * user侧(下面所有特征最终转换为**64位哈希值**)
    * user_inherent(特征取值一般不发生变化)
      * 用户id
      * 年龄
      * 性别
      * 城市(注册)
    * user_online(客户端请求携带的信息，上下文特征，特征取值可能发生变化)
      * 经纬度
      * 国家
      * 设备id(根据一定逻辑生成，不是随机生成)
      * 操作系统及其版本
      * 网络
      * 设备供应商
      * 语言
      * 分辨率
      * 买量渠道
      * 请求次数
    * user_session
      * 获取session队列action_tpl
        * session三种定义
          * 完整的session下发(按照session原始定义，对session间隔不做限制)
          * 最近一次session下发(限制session隔间，如30分钟)
          * 最近n个下发
        * 不同的行为
          * (展示数, 点击数, 播放数, 播完数, 点赞, 关注, 分享, 累计播放时长)
        * 返回用户在一个session内各种行为的数量
      * 用户活跃度分桶
        * 点击率、播完率、点赞率、互动率
  * item侧(以短视频为例)
    * item_inherent(下面所有特征最终转换为**64位哈希值**)
      * 视频id
      * 生产者id
      * 标签(tag)
        * 人打标签
        * 机打标签
      * 话题(hashtag)
      * 音乐id
      * 视频生产所在的经纬度
      * 视频生产所在的国家
      * 生产者性别
      * 是否搬运
      * 视频长度
        * 最小值/最大值截断
        * 取对数
        * 分桶
          * 桶间距
      * 物品聚类id
      * 视频下发时间与发布时间差
        * 以天为单位
        * 最小值/最大值截断
        * 取对数
        * 分桶
        * 注：视频下发时间是上下文特征
