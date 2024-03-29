## 在线
* (用户)(历史)行为
  * 也称种子
  * 分类(以短视频为例)
    * 点赞
    * 分享
    * 播完
  * 融合队列(以点赞、分享、播完为例)
    * 点赞和分享属于互动指标，播完属于消费指标
    * 访问redis，获取当前请求用户不同行为的种子队列
    * 融合逻辑
      * 融合队列长度：50
      * 点赞和分享队列均看作互动队列，种子分数为1.5
      * 播完队列长度不超过100，种子分数为1.0
      * 若互动和播完队列总的长度超过预设的融合队列长度，则对互动和播完队列按照比例进行截断，使得最后总的长度等于融合队列长度
      * 若一个种子同时属于多个队列，则将多个队列的权重之和作为该种子分数
      * 种子行为多样性
  * 遍历融合队列中每一个种子
    * 获取相似item列表
      * item2item
        * 访问kv词典，获取当前种子的相似item列表，列表元素为<item, score>
      * item2vec
        * 获取融合队列中每一个种子的embedding
        * 通过计算embedding之间的距离，得到每一个种子的topk相似items
          * ann
    * 种子分数乘以共现分数作为item的最终分数
      * 若不同种子对应同一相似item，则将各自分数相加，作为该item最终分数
