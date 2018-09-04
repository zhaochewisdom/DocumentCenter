## 通知服务

通知服务包含了短信服务、移动推送、电子邮件。


## 鉴权机制

所有的API均需要携带令牌才能够正常访问。
请求时需要在请求头中携带`ZC-Authorization`字段，令牌可从为从[开发者门户](http://developer.zhaochewisdom.com/portal)中申请获取.

例如：
``` JavaScript
# http request

$.ajax({
    headers: {
        //设置网关令牌
        'ZC-Authorization': "token",
        //设置推送服务accessKey
        'ZC-X-AccessKey':'此key请联系相关人员获取'
    },
    type: "POST",
    success: function (data) {
        //...
    }
});
```