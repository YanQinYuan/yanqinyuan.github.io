---
layout: post
title: "Cross origin requests are only supported for HTTP?"
date: 2018-02-05
categories: tech
---
问题：浏览器不支持本地跨域请求

解决方法：chrome 右键->属性->快捷方式处添加  

~~~js
--allow-file-access-from-files
~~~
