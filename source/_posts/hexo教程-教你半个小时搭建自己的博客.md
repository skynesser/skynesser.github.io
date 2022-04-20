---
title: hexo教程--教你半个小时搭建自己的博客
mathjax: true
date: 2022-04-14 14:24:44
tags:
categories: 
- 教程
---
![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/%E5%8D%9A%E5%AE%A2%E8%B5%84%E6%96%99/1650114432383.webp.webp)
# 前言
>1. hexo是一个相当好用的博客框架，仅仅用短短的几十分钟就可以上手。
>2. 本文会着重于hexo的使用，在开始之前，请确保安装好**git**和**node.js**，涉及到这个部分的教程在网上都很多，在这里不会额外介绍。
>3. 如果想快速看到效果，请务必按照下面的步骤执行。

博客地址:http://skynesser.github.io/

# 本地搭建
这个部分会教你让你在本地上运行你的博客，以下命令均在控制台上执行。
## 安装hexo
通过下面的代码检查node.js是否安装成功
>node -v
>
>npm -v

 安装hexo
 >npm install -g hexo-cli

 ![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/%E5%8D%9A%E5%AE%A2%E8%B5%84%E6%96%99/1.png)

## 初始化hexo
>hexo init blogname

这里的blogname是你要建立博客文件夹的名字。

![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/%E5%8D%9A%E5%AE%A2%E8%B5%84%E6%96%99/1R2CNTJD%60E%7BWRZU_Z%7EOVWLD.png)
这里就会出现一个blogname的文件夹
![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/%E5%8D%9A%E5%AE%A2%E8%B5%84%E6%96%99/H%28%7BW22VP%5DN%7D%5B4INL%7E1N6KX9.png)
然后文件夹的内部就会出现一些文件。
然后进入到这个blogname的目录下，执行下面这个命令。
>npm install

执行完以后，就可以在本地运行了，执行下面两行命令，就可以看见你搭建的博客。
## 在本地运行

>hexo g
>
>hexo server

![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/%E5%8D%9A%E5%AE%A2%E8%B5%84%E6%96%99/5QRXB2U4%294VFTXXL_7H7P%60K.png)
这就是默认的博客。

## 特别需要注意的命令
>需要注意的是，上面的命令在后续博客使用过程中会频繁使用的只有
>
>1. hexo g
>>这个命令或生产静态文件，在你写完一份你的博客之后，如果想要在本地上看到改变，必须要使用这个命令。换言之，就是该命令生成了博客的html等文件。
>2. hexo server
>>可以让你在本地上查看你的博客，在后续部署到github的过程中，强烈建议写完博客后先在本地查看无误后，再更新到github上。
>
>总结起来就是在你写完博客以后，先使用hexo g命令，再使用hexo server命令即可在本地上查看你的博客。

***

# 部署github

## github上创建仓库
![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/%E5%8D%9A%E5%AE%A2%E8%B5%84%E6%96%99/_J%254E1%7E%285V%25HSL6SM45OEPC.png)

![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/%E5%8D%9A%E5%AE%A2%E8%B5%84%E6%96%99/2G%28ILXYES2JL%40%40E%7DX1%5BCB8W.png)
>这里的username就是你的github里的用户名。

## 配置文件

![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/%E5%8D%9A%E5%AE%A2%E8%B5%84%E6%96%99/WA7HF0QC3AV%7D%25B%7B%25GB1VC%25V.png)

![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/%E5%8D%9A%E5%AE%A2%E8%B5%84%E6%96%99/%5BGBS%60QB%7B%7EW9H%7ELZD5S%243L%29N.png)

找到这个位置，修改如下：
```cpp
deploy:
  type: git
  repo: https://github.com/username/username.github.io.git
  branch: master
```
将username处改为你的github用户名即可。

## 完成部署
先下载命令如下：
>npm install hexo-deployer-git --save

下载安装好后，执行下面三行命令即可完成部署：
>hexo clean
>
>hexo g
>
>hexo d

## 需要特别注意的命令
>与上面本地运行类似的是，我们在修改完博客后，使用下面两个命令即可实现部署。
>1. hexo g
>2. hexo d
>
>部署完后就可以在https://username.github.io访问你的博客。

# 最后关于发布文章
文章都存在与source的_post目录下，想要删除文章直接将其移除即可，新建文章可以执行以下命令：
>hexo new articlename

 ![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/%E5%8D%9A%E5%AE%A2%E8%B5%84%E6%96%99/E%25TECKN4R%29TS8ZF1I9HC%4091.png)
 ![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/%E5%8D%9A%E5%AE%A2%E8%B5%84%E6%96%99/%286Y%28%60TWXCQ%40O_1Z7Y_CZVDU.png)

更多的命令可以查询官方文档：https://hexo.io/zh-cn/index.html