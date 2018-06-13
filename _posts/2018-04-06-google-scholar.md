---
layout: post
title: "Googsle 学术访问受限问题"
date: 2018-04-06
categories: tech
image: birds.jpg
published: true
---



## 问题
搭建好ss服务后，可以科学上网，但是谷歌学术打不开，或者是Google频繁出现验证码。

出现这种问题往往是因为你使用的VPS服务商（Vultr，搬瓦工，DigitalOcean， Linode等等）有很多人用它搭建ss服务，或者是使用你的这个IP段来爬虫，Google把你的IPv4段给封了。

于是，在你打开https://scholar.google.com时，就会出现如下页面：

![访问受限](https://www.flyzy2005.com/wp-content/uploads/2018/04/sorry-google-scholar.png)

> Google Sorry…
We’re sorry…
…but your computer or network may be sending automated queries. To protect our users, we can’t process your request right now. See Google Help for more information.


## 解决

**step1**: 打开vps，修改 hosts 文件，在最后添加以下代码：

~~~
2404:6800:4008:c06::be scholar.google.com
2404:6800:4008:c06::be scholar.google.com.hk
2404:6800:4008:c06::be scholar.google.com.tw
2401:3800:4001:10::101f scholar.google.cn #www.google.cn
~~~

最新 [hosts](https://raw.githubusercontent.com/lennylxx/ipv6-hosts/master/hosts) 文件地址

**step2**: 保存，重启ss服务.
~~~
/etc/init.d/shadowsocks restart
~~~

**step3**:修改vultr，使其允许 IPv6 访问。   