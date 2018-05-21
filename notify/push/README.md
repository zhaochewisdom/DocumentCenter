## 什么是移动推送
移动推送服务可以为APP提供推送服务，支持 Android, iOS, Winphone 三大手机平台。

## 支持的消息形式

提供四种消息形式：
+ 通知
+ 自定义消息
+ 本地通知

### 通知
指在手机的通知栏（状态栏）上会显示的一条通知信息。通知主要用于提示用户的目的，应用于新闻内容、促销活动、产品信息、版本更新提醒、订单状态提醒等多种场景

### 自定义消息
自定义消息不是通知，所以不会被SDK展示到通知栏上。其内容完全由开发者自己定义。 自定义消息主要用于应用的内部业务逻辑。一条自定义消息推送过来，有可能没有任何界面显示。
### 本地通知
本地通知API不依赖于网络，无网条件下依旧可以触发；本地通知的定时时间是自发送时算起的，不受中间关机等操作的影响。 本地通知与网络推送的通知是相互独立的，不受保留最近通知条数上限的限制。 本地通知适用于在特定时间发出的通知，如一些Todo和闹钟类的应用，在每周、每月固定时间提醒用户回到应用查看任务。

## 开发流程
移动推送服务开发主要分为APP端SDK集成和服务端API集成两部分。

## SDK集成
移动推送APP端需要集成SDK。  
SDK详细使用文档：
+ [IOS 接入文档](https://docs.jiguang.cn/jpush/client/iOS/ios_sdk/)
+ [Android 接入文档](https://docs.jiguang.cn/jpush/client/Android/android_sdk/)
+ [WindowsPhone 接入文档](https://docs.jiguang.cn/jpush/client/WindowsPhone/winphone_sdk/)

## 服务端集成

提供遵从 REST 规范的 HTTP API，以供开发者远程调用推送服务。

### REST API 基本约束
+ API 被设计为符合 HTTP, REST 规范。
+ 如无特殊说明，调用参数值应转码为：UTF-8, URL编码。
+ API 请求有频率限制。

### 鉴权机制

所有的API均需要携带令牌才能够正常访问。
请求时需要在请求头中携带`ZC-Authorization`字段，令牌可从为从[开发者门户](http://developer.zhaochewisdom.com/portal)中申请获取.

例如：
``` JavaScript
# http request

$.ajax({
    headers: {
        //设置令牌
        'ZC-Authorization': "token"
    },
    type: "POST",
    success: function (data) {
        //...
    }
});
```

### API列表

+ 消息推送接口

| 名称     | 说明                                                                       |
| -------- | :------------------------------------------------------------------------- |
|          | 推送消息                                                                   |
| Base URL | http://api.zhaochewisdom.com/notify                                        |
| Path     | /push                                                                      |
| Method   | POST                                                                       |
| Params   | [完整参数](https://docs.jiguang.cn/jpush/server/push/rest_api_v3_push/#_7) |

+ 获取推送唯一标识符

| 名称     | 说明                                                                        |
| -------- | :-------------------------------------------------------------------------- |
|          | 获取推送唯一标识符                                                          |
| Base URL | http://api.zhaochewisdom.com/notify                                         |
| Path     | /push/cid                                                                   |
| Method   | GET                                                                         |
| Params   | [完整参数](https://docs.jiguang.cn/jpush/server/push/rest_api_v3_push/#cid) |