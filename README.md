# 出门走走APP
## 价值主张设计
### 1.加值宣言
- 运用百度云API的图像识别识别图中场景，然后运用高德API的关键词搜索功能，让用户从识图到搜索与图片有关的地理地点，达到推荐用户外出地点的目的。
- 使用过本产品的用户可以将自己进行过满意的出行路线进行上传，供其他用户参考，但是为了防止有不安全、不良的出行路线出现，会启用百度API的文本审核功能。
### 2.核心价值
- 用识图的方式给用户推荐值得出行的地点。
### 3.用户痛点
- 用户想出门但是不知道去哪里好。
- 用户对某一类店铺、景点、产品感兴趣但不清楚本地有没有。
- 用户因为不知道有什么好去处而感到不想出门。
### 4.人工智能概率性
- 可能会出现用户提供的图片得不出值得搜索的关键词，或搜索结果少、搜索结果的内容不符合常规的情况，因此会在搜索结果的窗口设置一个小悬浮标，点击后可选“得不到想要结果”或者“帮助”，选择“得不到想要结果”后会提供输入窗口让用户自行输入希望的关键词。
### 5.需求列表
序号|标题|用户案例|重要程度|笔记
---|---|---|---|---
1|识图搜索|用户添加用于识别的图片，调用图像识别API识别出关键词，再调用关键词搜索API得出搜索结果|非常重要|核心功能，百度API-图像识别、高德API-关键词搜索
2|结果详情|在地图标出位置，显示目的地的详细信息|重要|核心功能，高德API-关键词搜索
3|自定义路线|使用过产品的用户可以对自己进行过满意的出行路线进行上传，供其他用户参考|次重要|增加用户体验的功能，百度API-文本审核

# 原型
- 正在制作中
