# 项目难点

> CORS通过`Access-Control-Allow-Origin`字段控制哪些域名可以共享资源。

设置为通配符`*`可以使所有的域名都获取资源。

## Origin字段

请求头中的Origin字段针对跨域操作。如果浏览器不存在跨域，则不携带`Origin`。如果存在跨域，则带上`Origin`字段，值为当前域名。

根据`Origin`设置如下：

```js
Access-Control-Allow-Origin: <Origin>
```

## 跨域异常

两个域名`a.buzuosheng.com`和`b.buzuosheng.com`访问该网站。当`a.buzuosheng.com`访问该网站的时候，响应头返回`Access-Control-Allow-Origin: a.buzuosheng.com`，该记录就会被CDN缓存。当域名`b.buzuosheng.com`访问该网站时，响应头中还是返回`Access-Control-Allow-Origin: a.buzuosheng.com`，因此跨域出现问题。

## Vary: Origin

使用`Vary: Origin`为不同的`Origin`缓存不同的资源。

服务器总是设置`Vary: Origin`，避免CDN缓存破坏CORS配置。

当请求头带有`Origin`，证明浏览器存在跨域行为，根据`Origin`设置相应的`Access-Control-Allow-Origin: <Origin>`。