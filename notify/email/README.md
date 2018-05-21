## 服务端集成
提供遵从 REST 规范的 HTTP API，以供开发者远程调用推送服务。

#### REST API 基本约束
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

## API列表