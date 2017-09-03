---
layout: post
title: "Centos7 内核升级"
category: 系统
tags: [Centos, OS, Linux]
published: true
date:   2017-08-13 17:30:00
---

## Centos7 内核升级及删除无用内核

### 1. 导入key

```
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
```

### 2. 安装elrepo的yum源

```
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm
```
### 3. 安装内核


```
yum --enablerepo=elrepo-kernel install  kernel-ml-devel kernel-ml
```
### 4. 查看默认启动项

```
awk -F\' '$1=="menuentry " {print $2}' /etc/grub2.cfg 

```
默认启动的顺序是从0开始，新内核是从头插入（目前位置在0，而4.4.4的是在1），所以需要选择0。

```
grub2-set-default 0
```
### 5. reboot重启，使用新的内核，重启后使用的内核版本:

```
uname -r  
4.4.4-1.el7.elrepo.x86_64
```
### 6. 查询存在的内核
```
rpm -qa | grep kernel
```

### 7. 删除旧内核

```
yum remove kernel
```




 


