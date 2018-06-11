## 风格
服务端API使用[REST Full API](http://www.ruanyifeng.com/blog/2014/05/restful_api.html)风格开发。

## 路由规范

### 路径命名

我们称一个路由的一个路径为一个端点（Endpoint）。

Endpoint命名应遵守以下格式：

格式：`/api/{version}/{resources}/:resource?key=value`
``` javascript
// 示例：获取用户
router.get('/api/v1/users/:userId');
```
在某些业务涉及到无法用`CURD`来描述时，可使用标准的`actions`进行替代。
格式：`/api/{version}/{resources}/:resource/actions/:action`
例如：
```javascript
// 示例：停止某个任务
router.get('/api/v1/task/:taskId/actions/stop');

```
约定：

+ 严格准守REST Full API 关于`HTTP Method`的使用说明。
+ 以`/api`开头，例如：`https://test.com/api/xxx`
+ 版本：在`/api`之后是版本信息，在朝彻API网关之后的所有服务不要有版本这一段，具体查看[版本特殊说明](#/版本特殊说明)。
+ 资源：版本只有是资源名称，例如：`Users`，命名应为**名词复数**。
+ 参数：[参数规范](#/参数规范)。

### 版本管理

正式版本使用`v{版本号}`表示，例如：`/api/v1/xxx`

#### 版本特殊说明

朝彻API网关已经处理了对于API版本的管理，开发人员无需在代码层面考虑API版本问题。

例如：

```javascript
# Node.js

// 正常Endpoint
router.get('/api/v1/users',callbak);
// 网关后应用Endpoint
router.get('/api/users',callbak);

```



## 参数规范

参数应按REST Full API风格定义，如果自定义参数应加在`QueryString`中。

例如定义一个获取所有年龄为18岁的男性用户的Endpoint：

```javascript
# Node.js
// 正确示例
// server.js
router.get('/api/v1/users',callback);
// client.js
ajax.get('/api/v1/users?gender=man&age=18');

// 错误示例
// server.js
router.get('/api/v1/users/:gender/:age');
// client.js
ajax.get('/api/v1/users/man/18')
```



## 请求规范

请求使用的Method应该严格准守HTTP规范的定义。

[MDN HTTP 请求方法](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods)

示例：

```javascript
# Node.js

// 获取资源列表
ajax.GET('/api/v1/users');

// 获取单个资源
ajax.GET('/api/v1/users/:userId');
         
// 创建资源
ajax.POST('/api/v1/users');

// 修改单个资源整个对象
ajax.PUT('/api/v1/users/:userId');

// 修改单个资源部分内容
ajax.PATCH('/api/v1/users/:userId');

// 删除单个资源
ajax.DELETE('/api/v1/users/:userId');
```

### Accept

默认应该使用`application/json`。

### 关于批量操作Method选择问题说明

REST Full 设置中经常碰到的批量操作问题，此处列举出具体操作规范。

#### 复杂查询问题

复杂查询指的是一个列表有很多参数，在传统的API编写中经常会作为`POST`请求进行操作，这与HTTP协议对于`POST`不符。

REST Full  API中的复杂查询不应该使用`POST`，而应该使用`GET` + `QueryString`的方式进行。这种方式涉及到URL长度问题。此处将超长的`QueryString`作为小概率事件，应从设计上避免出现此类Endpoit。

#### 批量删除问题

TODO:待完善

## 响应规范 

响应数据在没有特殊情况下，一律使用`application/json`。

### Content-Type

默认应该使用`application/json

### 状态码

严格准守HTTP协议规定的[HTTP 响应代码](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status)用法。

成功：2xx

重定向：3xx

客户端错误：4xx

服务端错误：5xx

### 响应格式

- GET /collection 返回资源对象的列表
- GET /collection/resource 返回一个单独的资源对象
- POST /collection 返回新创建的资源对象
- PUT /collection/resource 返回完整的资源对象
- PATCH /collection/resource 返回完整的资源对象
- DELETE /collection/resource 返回一个空文档

### 错误处理

当HTTP 响应代码为4xx和5xx时，返回格式为：

```json
{
    code:10001,//自定义错误码
    message:'自定义错误信息'
}
```



## 参考及文献

[阮一峰 RESTful API 设计指南](http://www.ruanyifeng.com/blog/2014/05/restful_api.html)
