# 别屏蔽我APP
- [带描述PPT录屏](https://github.com/NFUNM084-CN/API_ML_AI/blob/master/%E6%8A%A5%E5%91%8A.mp4)  
- [备用地址](https://www.bilibili.com/video/av82764819/)
## 价值主张设计
### 1.加值宣言
- 通过百度图像审核API和阿里云文本风险内容识别API，检测用户所上传的图片或文字内容是否存在不良信息，从而达到在社交媒体平台上发布信息减少被屏蔽、删除次数的目标。
### 2.核心价值
- 用图像审核和文本风险内容识别去检测内容的安全性，减少被屏蔽次数。
### 3.用户痛点
- 用户在某社交平台因为发布不良内容被封号/屏蔽，但不知道是什么内容导致自己被封了。
- 用户为了账号安全不想误发不良内容。
- 用户想要发一些特殊内容但是担心被屏蔽。
### 4.人工智能概率性
- 可能会发生有敏感词汇但没有检测出来的误差，会提供二次检测入口给用户。
### 5.需求列表
序号|标题|用户案例|重要程度|笔记
---|---|---|---|---
1|图片检测|用户想要查看自己的图片是否存在不良信息，有没有被屏蔽的风险|非常重要|核心功能，百度图像审核API
2|文字检测|用户想要查看自己的文字是否存在不良信息，有没有被屏蔽的风险|重要|核心功能，阿里云文本风险内容识别API

## 原型
### 流程图  
![流程1](https://github.com/NFUNM084-CN/API_ML_AI/blob/master/APP流程1.png "流程1")  
![流程2](https://github.com/NFUNM084-CN/API_ML_AI/blob/master/APP流程2.png "流程2")  
### 可交互原型
[点击查看产品原型]( http://nfunm084.gitee.io/api_final_prototype_c "产品原型")  
## API
### 使用水平
- **百度图像审核API**
- 请求代码
```python
POST /rest/2.0/face/v1/detect HTTP/1.1
accept-encoding: gzip, deflate
x-bce-date: 2015-03-24T13:02:00Z
connection: keep-alive
accept: */*
host: aip.baidubce.com
x-bce-request-id: 73c4e74c-3101-4a00-bf44-fe246959c05e
content-type: application/x-www-form-urlencoded
authorization: bce-auth-v1/46bd9968a6194b4bbdf0341f2286ccce/2015-03-24T13:02:00Z/1800/host;x-bce-date/994014d96b0eb26578e039fa053a4f9003425da4bfedf33f4790882fb4c54903
```  
- 合规返回结果  
```python
{
    "log_id": 15560926651500013,
    "conclusion": "合规",
    "conclusionType": 1,
    "data": [{
        "type": 8,
        "subType": 0,
        "conclusion": "合规",
        "conclusionType": 1,
        "msg": "命中用户自定义图像白名单",
        "datasetName": "用户自定义图像白名单1"
    }]
}
```
- 不合规返回结果
```python
{
    "log_id": 15656776740396212,
    "conclusion": "不合规",
    "conclusionType": 2,
    "data": [{
            "type": 0,
            "subType": 0,
            "conclusion": "不合规",
            "conclusionType": 2,
            "msg": "存在百度官方违禁图不合规"
        }
```  
- **阿里云文本风险内容识别API**
- 请求代码  
```python
{
  "scenes": ["antispam"],
  "tasks": [
    {
      "dataId": "xxxx$rdBjUC1C-1rd9Ah",
      "content": "奥巴马特朗普昨日在白宫进行了会面"
    }
  ]
}
```  
- 返回结果  
```python
{
    "msg":"OK",
    "code":200,
    "data":[
        {
            "msg":"OK",
            "code":200,
            "dataId":"xxxx$rdBjUC1C-1rd9Ah",
            "results":[
                {
                    "rate":50.0,
                    "suggestion":"review",
                    "details":[
                        {
                            "hintWords":[
                                {
                                    "context":"奥巴马"
                                }
                            ],
                            "contexts":[
                                {
                                    "libCode":"123456",
                                    "libName":"您自定义的词库名称",
                                    "context":"特朗普"
                                }
                            ],
                            "label":"politics"
                        }
                    ],
                    "label":"politics",
                    "scene":"antispam"
                }
            ],
            "content":"奥巴马特朗普昨日在白宫进行了会面",
            "filteredContent":"***特朗普昨日在白宫进行了会面",
            "taskId":"xxxxxxyyyyyy-xxxx"
        }
    ],
    "requestId":"yyyyyyyy-862F-4BAE-8B4E-xxxxxxx"
}
```  
### 使用比较
- 本APP选择使用百度图像审核API和阿里文本风险内容识别API，实际上百度有文本审核API，阿里有图像审核API。  
- **价格比较**  
- 百度图像审核API：未实名用户单账户一次性2000次调用免费
- 阿里云图像审核API：31天内拥有每日3,000张免费图片扫描额度，第32天起不享有免费量，1.8元/千张
- 百度文本审核API：累计50万次免费，超出后基础服务0.00025元/次
- 阿里云文本风险内容识别：31天内拥有每日3,000张免费图片扫描额度，第32天起不享有免费量，1.8元/千条
- **使用场景比较**
- 百度图像审核API：百度官方违禁图库、色情识别、暴恐识别、政治人物识别、恶心图像识别、广告检测、图文审核等
- 阿里云图像审核API：智能鉴黄、暴恐涉政检测、图文违规检测、二维码检测、不良场景检测、logo检测
- 百度文本审核API：文本色情、暴恐违禁、政治敏感、恶意推广、低俗辱骂、低质灌水
- 阿里云文本风险内容识别：广告内容检测、涉政暴恐检测、辱骂检测检测、色情内容检测、灌水内容检测、无意义内容检测、违禁品内容检测、自定义关键词检测
### 风险报告
- 两个API被分类为人工智能的内容安全/内容审核，由于属于百度和阿里云，竞争力比较强，性能也较为稳定，价格定位对于初起步APP比较友好。
- 产品详情页  
[百度图片审核API](https://ai.baidu.com/tech/imagecensoring)  
[阿里云文本风险内容识别API](https://ai.aliyun.com/lvwang/text?spm=5176.12825654.h2v3icoap.247.6add2c4aAuI4Ed&aly_as=TP8z0HP8)
