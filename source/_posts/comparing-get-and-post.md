title: GET与POST的区别
date: 2017-12-01 14:39:11
tags: web
---

### 对比项
1. 参数：
- GET传递的参数只能带URL后面，文本格式QueryString，各浏览器一般有长度限制，一般认为是2083，如果有中文字符更短。提交到服务器端的数据量小。参考：https://www.cnblogs.com/henryhappier/archive/2010/10/09/1846554.html
- POST可以传递application/x-www-form-urlencoded的类似QueryString、multipart/form-data的二进制报文格式（支持文件信息嵌入报文传输）、纯文本或二进制的body参数。提交到服务器端的数据量大。参考：http://blog.csdn.net/kimmking/article/details/2051169

2. 用途：
- GET用于从服务器端获取数据，包括静态资源(HTML|JS|CSS|Image等等)、动态数据展示(列表数据、详情数据等等)。
- POST用于向服务器提交数据，比如增删改数据，提交一个表单新建一个用户、或修改一个用户等。

3. 缓存：
- GET时默认可以复用前面的请求数据作为缓存结果返回，此时以完整的URL作为缓存数据的KEY。所以有时候为了强制每次请求都是新数据，我们可以在URL后面加上一个随机参数Math.random或时间戳new Date().getTime()、或版本号，比如abc.com?a=1&rnd=0.123987之类的。这也是目前一些静态资源后面加一个很长的版本号的原因，jquery-min.js?v=13877770表示一个版本，当页面引用jquery-min.js?v=13877771时浏览器必然会重新去服务器请求这个资源。jQuery.ajax方法，如果cache=false，则会在GET请求参数中附加"_={timestamp}"来禁用缓存。
- POST一般则不会被这些缓存因素影响。

4. 安全性：
- 默认对于nginx的access log，会自动记录get或post的完整URL，包括其中带的参数。
- 对于POST来说，请求的报文却不会被记录，这些对于敏感数据来说，POST更安全一些。

5. 自动化性能测试：
- 基于上面提到的nginx日志，可以使用grep GET+日期，awk格式化，然后sort -u去重，从而提取到某天的所有GET请求URL，使用程序模拟登陆，然后请求所有URL即可获取简单的性能测试数据，每个请求是否正确，响应时间多少等等。
- 但是对于POST请求，因为不知道报文，无法这样简单处理。可以通过nginx-lua获取报文输出到log，这样格式化会麻烦很多，但不失为一个办法。