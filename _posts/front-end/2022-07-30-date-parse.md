---
layout: display
title:  "Date.parse的兼容性问题"
categories: front-end
digest: "浏览器兼容问题"
---
<h2>{{ page.title }}</h2>
<p>{{ page.date | date_to_string }}</p>

最近在做项目的时候遇到一个很奇怪的现象 `Date.parse('2018-03-30')`转换日期的时候  在电脑上模拟的一切正常 Android手机也正常  但是在ios上会转化成NAN 
一开始的时候我还以为异步请求没有获取数据 后来发现不是这个原因 仔细一查得出如下结论:  
`Date.parse('2023-03-30')`在safari 以及ios上不被支持 解决的方法是将日期格式换成 `Date.parse('2023/03/30')`  
完美解决~