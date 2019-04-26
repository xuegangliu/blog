title: tomcat服务
date: 2016-07-28 10:30:12
updated: 2016-07-28 10:30:12
tags:
  - tomcat
categories:
  - server
---

# Tomcat服务

## 组织架构
``` lua
server
├── service
    ├── container 处理线程请求(connector接收的请求) [Engine Host Context Wrapper]
        ├── connector 负责接收浏览器发过来的TCP连接请求
        ├── connector
```
## 设计模式
- 责任链设计模式
- 模板模式
- 工厂模式
- 单例模式
- 门面设计模式
- 观察者设计模式
- 命令设计模式
