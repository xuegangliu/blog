title: 开发中遇到的问题记录
date: 2019-08-30 10:20:53
updated: 2019-08-30 10:20:53
tags:
  - java_base
categories:
  - problem
---

### 开发中遇到的问题记录

#### 1.idea启动项目后页面不能访问
解决方案：新版本部署tomcat需要勾选Deploy

#### 2.idea中启动tomcat项目，控制台乱码
- 原因：tomcat编码与本地环境编码不一致
- 解决方案：在catalina.out|catalina.sh文件中的JAVA_OPTS后加`-Dfile.encoding=UTF8 -Dsun.jnu.encoding=UTF8`

#### 3.公网无法下载，安装jar到本地仓库
- `mvn install:install-file -Dfile=jar包的位置 -DgroupId=jar包的groupId -DartifactId=jar包的artifactId -Dversion=jar包的version -Dpackaging=jar `

#### 4.用一些证书后，报java.security.InvalidKeyException: Illegal key size异常
- 原因：安全证书果密钥大于128报错，java默认的安全证书是受限制的
- 解决方案：替换环境中%JDK_HOME%\jre\lib\security目录下的local_policy.jar和US_export_policy.jar
- [blog文章](https://www.cnblogs.com/lilinzhiyu/p/8024100.html)

#### 5.springboot中jpa默认的查询中，对象与数据表的映射时，当数据库中表中字段为null时，查询错误
- 原因：对象映射字段为基本类型导致null映射错误
- 解决方案：将基本数据类型修改为包装类型

#### 6.oracle merge into用到自增序列,生成多次无用的序列
- 原因:存储过程中,对主键设置时,会造成序列很快用完
- https://blog.csdn.net/zlh313_01/article/details/82745526

#### 7.java.lang.UnsatisfiedLinkError: no jacob-1.17-x64 in java.library.path
- 原因：未找到匹配信息
- 需要把jacob-1.17-x64.dll添加到系统的变量文件下

#### 8.oracle sql语句查询,子查询查出数据不正确
- 原因: 未按别名展示出列，(子查询中的字段在上级中存在同样字段,未添加表别名，按自身的值去查询)
- 字段展示，带上表别名展示

#### 9.前端ajax请求数据,后端没有按key取到值
- 原因: 传过去为string，未按key：value去传过去
- 按key、value格式传过去

#### 10.在https服务中发ajax请求http被浏览器block
- 原因: (从https发送http请求是不可以)
- 协议，域名，端口有任何一个的不同，就被当作是跨域,请求https

#### 11.ios h5页面软键盘弹出后造成的触控不准BUG以及其解决方法
- 原因: ios h5页面软键盘弹出后造成的触控不准
- https://blog.csdn.net/soband_xiang/article/details/85697948

#### 12.hibernate sessionFactory hql查询完， 查询出的的bean 重新set filed时会发生更新数据操作
- 原因: sessionFactory查询完，未释放sessionFactory
- https://blog.csdn.net/shine0181/article/details/6187939