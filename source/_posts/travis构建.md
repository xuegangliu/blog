title: travis配置
comments: true
date: 2019-01-08 16:52:37
updated: 2019-01-08 16:52:37
tags:
  - build
  - Travis
categories: Travis
---

# travis
构建github代码库中的项目

## 配置

`travis.yml`

```travis.yml
# 选择项目的语言及版本
language: python
python:
  - "2.7"

# 打包之前的操作
before_install: "sudo apt-get update"
# 依赖安装等
install: "pip install -q -r requirements.txt --use-mirrors"

# 构建
script: make html

# 限制项目分支
branches:
  only:
    - mybranch

## 构建完成之后的命令
after_success:
    "find ./make/output -type f -exec curl --ftp-create-dirs -u $FTP_USER:$FTP_PASSWORD -T {} ftp://123.45.67.89/myproject/{} \\;"

#环境变量
env:
  global:
    - "FTP_USER=myusername"
    - "FTP_PASSWORD=mypassword"

# 邮件通知
notifications:
  email:
    recipients:
        - 1453860636@qq.com
    on_success: change
    on_failure: always
```