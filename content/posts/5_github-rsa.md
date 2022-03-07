---
title: 5. git rsa setting
date: 2017-06-01 16:34:53
tag: rsa
---


### Github 上密钥对

Github上可以上传公钥，本地保存私钥，这样可以push时不用老输密码。

### 生成SSH Key

``` bash
ssh-keygen -t rsa -C "your_email@example.com"
```

这样在/home/chen/.ssh/文件夹下生成两个文件: xyz_rsa.pub和xyz_rsa, 分别是你的公钥和私钥.

然后登录Github上传公钥。

### 测试SSH Key登录

``` bash
ssh -T git@github.com
```

### 设置项目

``` bash
git config  user.name "your-id"
git config  user.email "your-id@gmail.com"
```
就可以直接git push

More info: [简书](http://www.jianshu.com/p/ddd3122cb351)