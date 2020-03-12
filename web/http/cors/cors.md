# CORS跨域

伪跨域，如iframe、window.name、window.postMessage

跨站HTTP请求(Cross-site HTTP request)是指发起请求的资源所在域不同于该请求所指向资源所在的域的HTTP请求
跨站 HTTP正常请求，但是结果被浏览器拦截了，就是跨域问题。

跨域问题只有在浏览器才会出现，javascript等脚本的主动http请求才会出现跨域问题。后端获取http数据不会存在跨域问题。跨域问题可以说是浏览器独有的（或者说http客户端独有的，这个其实看制定者是否遵循协议）

如果两个页面的协议，端口（如果有指定）和域名都相同，则两个页面具有相同的源

不同源就是跨域

http://127.0.0.1:3000

url	结果	原因
http://127.0.0.1:3000/index	同源
https://127.0.0.1:3000	跨源	协议不同
https://localhost:3000	跨源	域名不同
http://127.0.0.1:3001	跨源	端口不同

## 为什么要有跨域限制

同源策略限制了从同一个源加载的文档或脚本如何与来自另一个源的资源进行交互。这是一个用于隔离潜在恶意文件的重要安全机制。
还是安全问题，如果不限制，那么CSRF（Cross-site request forgery，中文名称：跨站请求伪造）攻击就很容易实现了。

举个例子，假设没有跨域限制：

假设你是a.com网站的管理员，你在a.com网站有一个权限是删除用户，比如说这个过程只需用你的身份登陆并且POST数据到http://a.com/deleteUser，就可以实现删除操作。
然后假设有个b.com网站被攻击了，别人种下了恶意代码，你点开的时候就会模拟跨域请求（你同时在浏览器中不同标签打开了a.com和b.com网站，并且你已经登录了a.com），那么b.com的恶意代码就可以模拟对a.com的跨域请求，模拟一个用户删除操作是很简单的（当然是攻击者有意针对，而且知道了删除接口）。

通过例子可知道，这是多危险的事情，所以浏览器都会做跨域限制。