---
title: 'Http header'
date: 2020-07-18T17:18:05+08:00
tags: [WebSecurity,CTF]
---

<a name="pazYR"></a>
# GET
get是明文链接的形式发送请求，所以发送带参数的get请求只要在url后附加?key=value键值对即可<br />例如：请以get请求发送名为a，值为1的变量<br />解：访问链接http://220.249.52.133:38678/?a=1
<a name="zpLcN"></a>
# POST
post 请求非明文，需要借助工具<br />例如：请用post请求发送名为b，值为2的变量
```python
import requests
url='http://220.249.52.133:38678/?a=1'
payload={
    'b':2
}
r=requests.post(url,data=payload)
r.encoding='utf-8'
print(r.text)
```
<a name="uVvsV"></a>
# SESSION
使用r = request.post() 每次发出的请求都是无状态的，暂时的，不会保持页面状态。<br />而有的题目中要求在当前页面填写表单并显示，然后才能获取flag<br />情景(moectf 2020 ezmath)：
```html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
<p>不会吧不会吧，不会有人连加法都不会吧</p><br>
528+211=<form action="index.php" method="post"><input type="text" name="a"><input type="submit" value="提交"></form>
<script language="JavaScript">
function myrefresh()
{
window.location.reload();
}
setTimeout('myrefresh()',1000); //指定1秒刷新一次
</script>

</body>
</html>
听说你算数挺快？？
```
 <a name="68500ac9"></a>
## 会话对象
> 会话对象让你能够跨请求保持某些参数。它也会在同一个 Session 实例发出的所有请求之间保持 cookie， 期间使用 `urllib3` 的 [connection pooling](http://urllib3.readthedocs.io/en/latest/reference/index.html#module-urllib3.connectionpool) 功能。所以如果你向同一主机发送多个请求，底层的 TCP 连接将会被重用，从而带来显著的性能提升



<a name="9t2I3"></a>
# 伪造IP

<br />X-Forwarded-For<br />
