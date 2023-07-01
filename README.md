Forsaken-Mail
==============
即收即毁的临时邮件服务

[在线演示](http://forsaken.somecolor.cc:3000/)


### 步骤 

### 如何自己部署

进行之前，请先确保云服务厂商允许25端口入站以及安全组/防火墙设置运行了25端口。
目前已知情况，阿里云的服务器默认25端口可以入站，所以你只需要将安全组设置运行25端口TCP即可。

随后，编辑要绑定域名的DNS解析记录，假设域名为 example.com
新建解析 (A)，主机记录 @，记录值填写为云服务器的IP。新建解析 (MX)，主机记录 @，记录值 example.com，MX优先级默认

例如如下配置，123.123.123.123 代表你的服务器IP，mail.example.com 是访问此邮箱页面的主机名，example.com 是邮箱的后缀例如 abcdef@example.com。

| 主机记录 | 记录类型  | 记录值             | TTL  |
| ---- | ----- | --------------- | ---- |
| mail | CNAME | example.com     | 10分钟 |
| @    | MX    | example.com     | 10分钟 |
| @    | A     | 123.123.123.123 | 10分钟 |

这样，你已经完成了域名相关的配置，随后进入云服务器进行以下操作。

您可以启动Mailin（请参阅下一节）并使用[smtp服务器测试]（http://mxtoolbox.com/diagnostic.aspx) 验证所有内容是否正确。


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
