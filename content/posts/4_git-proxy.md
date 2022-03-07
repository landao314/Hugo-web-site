---
title: 4. git proxy
date: 2017-06-01 16:34:53
tag: [git,proxy,ca,cert,crt,代理,github,提速]
---
我常用的是GoAgent的梯子，即是XX-net
但是一个比较麻烦的问题是Ca根证书要手动导入
这是Windows7下的Msys2环境下的git，linux下类似
首先要设置git的代理服务器

``` bash
$git config --global http.proxy http://localhost:8087
```

这时使用git时会报证书错误，所以要导入证书

可以用

``` bash
GIT_CURL_VERBOSE=true git clone https://google.com
```
查看CAfile和CApath确定git是用哪一个证书的，linux下应该会是系统证书的地方
但是Msys2下是

``` bash
D:\msys32\usr\ssl\certs\ca-bundle.crt
```
于是我将GoAgent的证书直接粘贴到这个文件的未尾，注意不要有多余的空行和字符

现在git下载github上的文件速度可以说大辐提速，从50KB/s跳到1.5MB/s，爽！！