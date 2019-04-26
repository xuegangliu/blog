title: 前端问题
comments: true
date: 2017-07-19 13:33:02
updated: 2017-07-13 15:33:02
tags:
  - simple
  - javascript
categories:
  - problem
---
# 问题记录
------
1. ajax怎么解决跨域？
    - 1，代理（通过后台操作）
    - 2，JSONP（添加响应头，允许跨域 ）
              addHeader(‘Access-Control-Allow-Origin:*’);//允许所有来源访问 
               addHeader(‘Access-Control-Allow-Method:POST,GET’);//允许访问的方式
    - 3，在ajax的dataType方式改为“jsonp”