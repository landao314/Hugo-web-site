---
title: 1. Install Msys2 In China
date: 2017-06-08 08:42:34
tags:
---

#. 先从国内[MSYS2镜像](http://mirrors.ustc.edu.cn/msys2/distrib/)下载对应的版本msys2
压缩包。
#. 再用BOOTICE生成一个VHD镜像，因为用镜像可以打包一堆小文件，U盘携带方便。
#. 挂载VHD镜像并格式化成NTFS
#. 解压msys2到这个VHD镜像里，是一个单独的磁盘，非常方便，不用时又可以不挂载，
   window10支持双击挂载
#. 修改/etc/nsswitch.conf如下，其中landao64是我的用户名，你可以改自己的。
这样改了就不会换电脑时依据系统用户生成新的用户目录

```bash
 
# Begin /etc/nsswitch.conf

passwd: files db
group: files db

db_enum: cache builtin

db_home: /home/landao64
db_shell: cygwin desc
db_gecos: cygwin desc

# End /etc/nsswitch.conf

```

#. 运行mingw64.exe，等待初始化，然后pacman -Syu 两次更新系统的包数据库，和软件。
#. 然后安装如下的依赖软件，依据你的系统选择相应的版本，32位用mingw-w64-x86_64-xxxx,
64位用mingw-64-x86_64-xxxx

``` bash
$pacman -S mingw-w64-x86_64-gcc
$pacman -S mingw-w64-x86_64-cmake
$pacman -S mingw-w64-x86_64-llvm
$pacman -S mingw-w64-x86_64-python2
$pacman -S mingw-w64-x86_64-python3
$pacman -S mingw-w64-x86_64-make
$pacman -S git
$pacman -S make
```
#. 下一步就可以编译gvim了
