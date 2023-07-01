Forsaken-Mail
==============
即收即毁的临时邮件服务

[在线演示](http://forsaken.somecolor.cc:3000/)


### 步骤 

### 域名解析 

为了接收电子邮件，您的smtp服务器地址应该在某处可用。两个记录应该添加到您的DNS记录中。

假设我们想在``@subdomain.domain.com``:接收电子邮件
首先是MX记录：``subdomain.domain.com MX 10 mxsubdomain.domain.com``。
即
|主机记录|记录类型|优先级|记录值|
|:---:|:---:|:---:|:---:|
|subdomain.domain.com|MX|10|mxsubdomain.domain.com|

这意味着像`@subdomain.domain.com` 这样的地址的邮件服务器将是`mxsubdomain.domain.com`.

然后是：A记录：`mxsubdomain.domain.com`是你邮箱服务的的ip address。这会告诉您可以在哪个ip地址找到邮件服务器。

您可以启动 mail（请参阅下一节）并使用[smtp服务器测试]（http://mxtoolbox.com/diagnostic.aspx）   验证所有内容是否正确。

#### 如果上面不好理解，可以按照下面的设置

要绑定域名（如example.com）的DNS解析记录；

新建解析 (A)，主机记录 @，记录值填写为云服务器的IP。

新建解析 (MX)，主机记录 @，记录值 example.com，MX优先级默认

例如，如下配置：

123.123.123.123 代表你的服务器IP，

mail.example.com 是访问此邮箱页面的主机名，

example.com 是邮箱的后缀，例如 username@example.com。

| 主机记录 | 记录类型  | 记录值             | TTL  |
| ---- | ----- | --------------- | ---- |
| mail | CNAME | example.com     | 10分钟 |
| @    | MX    | example.com     | 10分钟 |
| @    | A     | 123.123.123.123 | 10分钟 |



### 开始 

部署文章：https://51.ruyo.net/3210.html

```
npm install && npm start
```

或利用pm2 启动本项目
```
pm2 start start.json
```

或Docker启动
```
docker pull malaohu/forsaken-mail
docker run --name forsaken-mail -d -p 25:25 -p 3000:3000 malaohu/forsaken-mail
```


愉快的使用吧！ 
http://ip:3000

### 配置

config.js 支持黑名单, 支持拒收某域名的邮件

推荐：https://cloudflare.com
