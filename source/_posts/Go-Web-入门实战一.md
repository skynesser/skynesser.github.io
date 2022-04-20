---
title: Go Web 入门实战(一)
mathjax: true
date: 2022-04-20 13:43:34
tags:
- Go Web 
categories:
- Go 
---
# Go Web 入门实战(一)

[点击此处](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/Go/Go%20web/Go%20web%E5%85%A5%E9%97%A8%E5%AE%9E%E6%88%98%28%E4%B8%80%29/temp/Go-Web-%E5%85%A5%E9%97%A8%E5%AE%9E%E6%88%98%E4%B8%80.pdf),下载PDF

## 前言
>该系列既是博客也是我的学习笔记，我将从这里开始记录下我在学习过程中的点点滴滴并把它分享出来。
我们会用Go Web的知识从零开始搭建一个博客。关于Go的各种环境搭配，不会进行过多的介绍，这里全部的任务都是用Goland完成的，我也十分建议大家使用Goland，下载好Goland以后，你可以利用它十分简单的帮助你配置好go所需要的各种环境，免去了搭建环境的痛苦。
[下载链接](https://www.jetbrains.com/go/download/#section=windows)

***

## 学会查阅文档
>我们在学习的过程中，会查阅文档时必要的技能。当我们下载了go以后，其实go的文档就已经下载好了，我们可以通过**godoc**命令实现本地查阅，先下载**godoc**(我们建议命令的执行都在Goland的终端中执行)：
```bash
$ go install golang.org/x/tools/cmd/godoc@latest
```
>然后使用下面的命令我们就可以在本地查看了：
```bash
$ godoc -http=:6060
```
>执行完命令以后，在本地打开下面网址即可打开：
http://localhost:6060/

![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/Go/Go%20web/Go%20web%E5%85%A5%E9%97%A8%E5%AE%9E%E6%88%98%28%E4%B8%80%29/temp/AP1FQ%286K%29%29%5BE%28M%7B4LNB%7DKC8.png)
此外，我们可以使用Ctrl+F来快速检索我们需要的信息。

![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/Go/Go%20web/Go%20web%E5%85%A5%E9%97%A8%E5%AE%9E%E6%88%98%28%E4%B8%80%29/temp/4%7E_%7BY%29_QL%7D%40%7E%29M%24NOG%25%7BBI2.png)
***

## 关于项目

>该项目是一个博客项目，功能点大致如下：
>- 注册登录
>- 授权策略
>- 文章功能
>- 分类系统
***

## 项目的开始
>在根目录下新建一个main.go文件，并写下如下代码:

![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/Go/Go%20web/Go%20web%E5%85%A5%E9%97%A8%E5%AE%9E%E6%88%98%28%E4%B8%80%29/temp/JAFP1H91%7D15HF__Z0UNZ%7E%25X.png)
```go
package main

import (
	"fmt"
	"net/http"
)

func HandlerFunc(w http.ResponseWriter, r *http.Request) {
	fmt.Fprint(w, "<h1>开始我们的项目吧</h1>")
}

func main() {
	http.HandleFunc("/", HandlerFunc)
	http.ListenAndServe(":8080", nil)
}

```
>我们暂时不必深究代码，后面会慢慢解释。运行项目以后，我们可以打开下面的网址，看到如下页面：
http://localhost:8080/

![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/Go/Go%20web/Go%20web%E5%85%A5%E9%97%A8%E5%AE%9E%E6%88%98%28%E4%B8%80%29/temp/AJ%604_G%60_0W%28N01SJ3VD%7BFGM.png)
***
## 代码的解析

### package main
>每个go程序必须在一个包的内部，而**package main**的作用就好像C语言中的main函数一样，一个标准可执行的go程序必须要有**package main**的声明。

### import
>import可以引入当前go程序所需要的包，在这里我们引入了两个Go标准库的包：
>1. **fmt**
>这个包实现了Go的基本I/O函数
>2. **net/http**
>提供了HTTP编程相关的接口

### http.ListenAndServe
>用于监听本地端口以提供服务
### http.HandleFunc
>指定出来HTTP请求的函数
>```go
>http.HandleFunc("/", handlerFunc)
>```
>其中第一个参数是站点的路径，第二个是处理函数。
>如果第一个参数是"/"，意味着可以是任意路径。
```go
package main

import (
	"fmt"
	"net/http"
)

func HandlerFunc(w http.ResponseWriter, r *http.Request) {
	fmt.Fprint(w, "<h1>开始我们的项目吧</h1>")
	fmt.Fprint(w, "请求路径为"+r.URL.Path)
}

func main() {
	http.HandleFunc("/", HandlerFunc)
	http.ListenAndServe(":8080", nil)
}

```
>通过如下代码实践，访问任意路径：
http://localhost:8080/ww
http://localhost:8080/abc
比如第一个网址，会出现如下结果：

![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/Go/Go%20web/Go%20web%E5%85%A5%E9%97%A8%E5%AE%9E%E6%88%98%28%E4%B8%80%29/temp/%24J%5D%5BMUNCLRBQ58%5D0W%29WJSKM.png)

>通过这种机制，我们可以根据访问页面网址的不同，设置出不同的访问结果：
```go
package main

import (
	"fmt"
	"net/http"
)

func HandlerFunc(w http.ResponseWriter, r *http.Request) {
	if r.URL.Path == "/"{
		fmt.Fprintf(w,"开始项目吧")
	}else if r.URL.Path == "/ww"{
		fmt.Fprint(w,"加油")
	}else{
		fmt.Fprint(w,"页面不存在")
	}
}

func main() {
	http.HandleFunc("/", HandlerFunc)
	http.ListenAndServe(":8080", nil)
}
```
>自己大胆尝试吧。
### http.Request
>用于获取用户的信息。
### http.ResponseWriter
>返回用户的响应。

### 设置标头
>因为我之前设置过的原因，我的页面显示是正常的，然而事实上大部分人可能会出现如下的情况：

![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/Go/Go%20web/Go%20web%E5%85%A5%E9%97%A8%E5%AE%9E%E6%88%98%28%E4%B8%80%29/temp/7XW%60%40%29AT%60R%7BXF%281Y%7D6W%291%40W.png)
>我们可以右键鼠标，检查页面：

![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/Go/Go%20web/Go%20web%E5%85%A5%E9%97%A8%E5%AE%9E%E6%88%98%28%E4%B8%80%29/temp/%7EL%60%29K%5DHTW0K5MP_TP%29805HK.png)
>我们发现这里显示的**plain**，而这是文本形式的内容，我们希望这里显示的是html形式的，修改代码如下即可：
```go
package main

import (
	"fmt"
	"net/http"
)

func HandlerFunc(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-type", "text/html; charset=utf-8")
	fmt.Fprint(w, "<h1>开始我们的项目吧</h1>")
}

func main() {
	http.HandleFunc("/", HandlerFunc)
	http.ListenAndServe(":8080", nil)
}
```
```go
w.Header().Set("Content-type", "text/html; charset=utf-8")
```
>其中这一行代码的作用就是设置标头，设置完后就可以解决问题了，同时我们可以查看此时内容形式变成html。

![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/Go/Go%20web/Go%20web%E5%85%A5%E9%97%A8%E5%AE%9E%E6%88%98%28%E4%B8%80%29/temp/_Z_X7H%7D0J3C%7E%28R_S90BA4UA.png)

### 状态码
>状态码的具体含义详见http的基本知识，我们介绍怎么为页面添加404状态码。
```go
package main

import (
	"fmt"
	"net/http"
)

func HandlerFunc(w http.ResponseWriter, r *http.Request) {
	if r.URL.Path == "/" {
		fmt.Fprint(w, "<h1>开始我们的项目吧</h1>")
	} else {
		w.WriteHeader(http.StatusNotFound)
	}
}

func main() {
	http.HandleFunc("/", HandlerFunc)
	http.ListenAndServe(":8080", nil)
}
```
```go
w.WriteHeader(http.StatusNotFound)
```
>使用该函数即可简单的为页面添加404状态码。

![](https://skynesserblog.oss-cn-hangzhou.aliyuncs.com/Go/Go%20web/Go%20web%E5%85%A5%E9%97%A8%E5%AE%9E%E6%88%98%28%E4%B8%80%29/temp/KI%7EQ%60_%7D%24756%5D0VUWGU%7DF6PY.png)


