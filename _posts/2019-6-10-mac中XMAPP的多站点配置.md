---
layout:     post                    # 使用的布局（不需要改）
title:      如何在XMAPP中进行多站点配置       # 标题 
subtitle:   XMAPP多站点配置                 #副标题
date:       2019-06-18                # 时间
author:     Day                       # 作者
header-img: img/post-bg-2019.png     #这篇文章标题背景图片
catalog: true                        # 是否归档
tags:                                 #标签
    - 配置工具
---
# 在Mac上基于XAMPP本地多站点的配置
* 从年初到现在一直都没有什么技术积累，最近因为公司业务发展需要，开始从移动端开发转向web开发，今天就总结一下在Mac上面配置多域名访问的配置，虽然没什么技术含量，但还是想写写，有总结才有进步嘛！
* 什么是多站点配置呢?就是指在xmapp下配置多个虚拟域名,以便学习调试使用的一种配置.
* 在本地配置多站点的访问主要涉及到三个文件的配置，主要是hosts、httpd-conf、vhosts-conf。关于XAMPP的安装之类的就不多说了，自行百度、谷歌。下面就来具体说说配置过程。

## hosts的配置（配置本地DNS服务器）
* 首先要找到host文件，Mac中hosts的路径是/private/etc/hosts，下面利用终端来操作,按 i 之后就可以进行编辑
![hosts配置图](/img/1560873336053.jpg)
* 编辑需要配置的域名，然后ESC > :wq > 回车退出vi编辑器 ( > 指的下一步)

## 配置Apache中的配置文件httpd.conf 
* 找到http.conf文件 
![http.conf文件](/img/1560873886344.jpg)
* 修改用户，否则后面会报403错误 
* 由于本人的电脑是Mac端,如何查看自己的用户名 左上角 > 系统偏好设置 > 用户与群组 
* ![找到http-vhosts.conf](/img/1560906676580.jpg) 
## 引入httpd-vhosts.conf配置文件 
![引入httpd-vhosts.conf](/img/1560906466759.jpg) 
## 配置http-vhosts.conf文件 
* 找到对应的文件,我的话复制路径是option+command+c
![配置http-vhosts.conf文件](/img/1560907062212.jpg)

添加之前hosts文件配置的域名，然后重启Apache服务 
![添加虚拟域名](/img/1560907952260.jpg)


* 多站点的配置就是这么简单。
## 大功告成
![成功](/img/1560908426309.jpg)

* 最后在介绍下Apache配置文件 

* Listen 监听地址和端口 
* Listen 80 ：监听所有地址的80端口
* ServerRoot服务器安装目录 



> ServerAdmin 设置网站管理员的邮箱 


> DocumentRoot httpd服务的目录 


> DirectoryIndex 设置网站首页文件名 


* 目录访问权限 
> Options:控制哪些服务器特性 
> 
> All：用户可以在此目录做任何操作 
> 
> None:不允许访问此目录 
> 
> Indexes:是否显示文件列表 
> 
> Allow：允许哪个版本可以访问 
> 
> Deny：禁止哪些主机访问 
> 
> Order:控制Deny和Allow生效顺序 
> 
> AllowOverride：根据All和None的值来决定是否读取.htaccess文件中的信息来改变原配置 
> 
> .htaccess控制相关目录下的配置 
