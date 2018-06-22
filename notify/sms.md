## 短信服务
提供遵从 REST 规范的 HTTP API，以供开发者远程调用推送服务。

## REST API 基本约束
+ API 被设计为符合 HTTP, REST 规范。
+ 如无特殊说明，调用参数值应转码为：UTF-8, URL编码。
+ API 请求有频率限制。

## 鉴权机制
> **注意：Rest API 只需要提供此令牌即可，无需再提供其他信息。例如`appKey`、`masterSecret`等信息**

## API列表
### 消息推送接口

| 名称     | 说明                                                                                           |
| -------- | :--------------------------------------------------------------------------------------------- |
|          | 短信发送接口(Beta)                                                                                   |
| Base URL | http://api.zhaochewisdom.com/notify                                                              |
| Path     | /api/message                                                                                       |
| Method   | POST                                                                                           |
| Params   | [完整参数](https://help.aliyun.com/document_detail/57458.html?spm=a2c4g.11186623.6.572.kze2m1) |

### 短信批量发送接口

| 名称     | 说明                                                                                           |
| -------- | :--------------------------------------------------------------------------------------------- |
|          | 短信批量发送接口(Beta)                                                                               |
| Base URL | http://api.zhaochewisdom.com/notify                                                             |
| Path     | /api/message/batch                                                                                  |
| Method   | POST                                                                                           |
| Params   | [完整参数](https://help.aliyun.com/document_detail/66264.html?spm=a2c4g.11186623.6.575.dG6TVV) |


### 短信发送详情查询接口

| 名称     | 说明                                                                                           |
| -------- | :--------------------------------------------------------------------------------------------- |
|          | 短信发送详情查询接口(Beta)                                                                           |
| Base URL | http://api.zhaochewisdom.com/notify                                                               |
| Path     | /api/message                                                                              |
| Method   | GET                                                                                            |
| Params   | [完整参数](https://help.aliyun.com/document_detail/57459.html?spm=a2c4g.11186623.6.573.m71Z8K) |