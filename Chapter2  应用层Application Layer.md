# Chapter2  应用层Application Layer

## 1.应用层协议原理Principles of Network Applications

### ①概述：研发网络应用程序的核心是能够写出运行在不同端系统和通过网络彼此通信的程序。网络核心设备并不在应用层上起作用，而仅在较低层起作用，特别是在网络层及下面层次起作用。----仅将应用软件限制在端系统。

### ②网络应用程序体系结构（application architecture)：有应用程序研发者设计，规定了如何在各种端系统上组织该应用程序。选择应用程序体系结构时：

- A.客户-服务器系统（client-server architecture):在此结构中，有一个总是打开的主机称为服务器。服务于来自许多其他称为客户的主机请求。Eg:WEB应用程序

	- 特点1：客户相互之间不通信Clients do not communicate with each other
	- 特点2：该服务器有固定的、周知的地址（IP）Server has a fixed,well-known address
	- 特点3：强大的虚拟服务器需要有大量主机的数据中心 a data center,housing a number of hosts,is often used to create a powerful server

- B.对等结构P2P（P2P Architecture）

	- 特点1：应用程序在间断连接的主机对之间使用直接通信
	- 特点2：流行的 流量密集型的应用（Bittorrent）Xunlei Skype
	- 特点3：自扩展性（self-scalability)：在一个P2P文件共享应用中，尽管每个对等方都由于请求文件产生工作负载，但每个对等方通过向其他对等方分发文件也为系统增加服务能力。
	- 特点4：面临的安全性 性能和可靠性等挑战

### ③进程通信processing communicating

- A.对运行在多个端系统上的程序是如何相互通信的情况有个基本了解。进行通信的就是进程（process)，在两个不通端系统上的进程，通过跨越计算机网络交换报文（message)而相互通信。
- B.客户和服务器进程：客户（client）和server(服务器) 、区别WEB和P2P的服务器和进程:In the context of a communication session between a pair of processes,the process that initiates the communication (that is,initially contacts the other process at the beginning of the session)is labeled as the client.The process that waits to be contacted to begin the session is the server
- C.进程与计算机网络之间的接口The interface Between the process and the computer network

	- 套接字（socket)的软件接口向网络发送报文和从网络接受报文。
	- 应用程序编程接口（Application Programming Interface,API)
	- 应用程序开发者可以控制套接字在应用层端的一切，但是对该套接字的运输层端几乎没有控制权。对运输层的控制权仅限于：选择运输层协议、也许能设定几个运输层参数

		- The choice of transport protocol and perhaps the ability to fix a few transport-layer parameters such as maximum buffer and maximum segment sizes

- D.进程寻址Addressing process

	- 定义主机的地址、在目的的主机中指定接收进程的标识符

		- The Address of the host and an identifier that specifies the receiving process in the destination host

### ④可供应用程序使用的运输服务Transport Services Available to Applications 

- A.选择运输层协议
- B.一个运输层协议能够为调用它的应用程序提供什么样的服务呢？

	- （1）可靠数据传输reliable data transfer
	- （2）吞吐量throught
	- （3）定时Timing
	- （4）安全性Security

### ⑤因特网提供的运输服务Transport service provided by the Internet

- A.当你作为一个开发者，为因特网(更一般的是TCP/IP网络 创建一个新的应用时，首先要做出的决定是，选择UCP还是TCP
- B.TCP(面向连接服务和可靠数据传输服务）

	- 关注TCP的安全/SSL（安全套接字层） Secure socket layer

- C .UDP服务
- D.因特网运输协议不提供的服务（P62表格）
- E.TCP和UDP的区别：UDP协议和TCP协议都是传输层协议。

TCP（Transmission Control Protocol，传输控制协议）提供的是面向连接，可靠的字节流服务。即客户和服务器交换数据前，必须现在双方之间建立一个TCP连接，之后才能传输数据。并且提供超时重发，丢弃重复数据，检验数据，流量控制等功能，保证数据能从一端传到另一端。

UDP（User Data Protocol，用户数据报协议）是一个简单的面向数据报的运输层协议。它不提供可靠性，只是把应用程序传给IP层的数据报发送出去，但是不能保证它们能到达目的地。由于UDP在传输数据报前不用再客户和服务器之间建立一个连接，且没有超时重发等机制，所以传输速度很快。


### ⑥应用层协议（application-layer protocol)定义了运行在不同端系统上的应用程序进程如何相互传递报文。

- A.交换的报文类型
- B.各种报文类型的语法
- C.字段的语义
- D.确定一个进程何事以及如何发送报文，对报文进行相应的规则
- F.RFC/HTTP

### ⑦本书涉及的网络应用

## 2.WEB和HTTP

### ①HTTP概况：Web的应用层协议是超文本传输协议HyperText transfer protocol

- A.一个客户程序和一个服务器程序:客户程序和服务器程序运行在不同的端系统中，通过交换HTTP报文进行会话，HTTP定义了这些报文的结构和客户服务器进行报文交换的方式。
- B.WEB页面是由对象组成的。一个对象只是一个文件，JEPG/HTML/JAVA等，且他们可以通过一个URL地址寻址
- C.每个URL地址由两部分组成，存放对象的服务器主机名和对象的路径名
- D.WEB的浏览器实现了HTTP的客户端，WEB服务器实现了HTTP的服务器端，用于存WEB对象。
- E.HTTP使用TCP作为它的支撑运输协议
- F.无状态协议：因为HTTP服务器并不保存关于客户的任何信息，所以我们说HTTP是一个无状态协议（stateless protocol)

### ②非持续连接和持续连接

- A.非持续连接non-persistent connection：每个请求响应对是经一个单独的TCP连接发送；

	- （1)往返时间

- B.持续连接persistent connection：所有的请求及响应经过相同的TCP连接发送

### ③HTTP报文格式，RFC1945 2616 7540包含了对HTTP报文格式的定义

- A.HTTP请求报文

	- （1）请求行（2）首部行（3）实体体（GET和POST) （4）

- B.HTTP响应报文

	- （1）状态行（2）6个首部行（3）实体体

- C.常见报文和状态码的含义

###  ④用户与服务器的交互：cookie（RFC 6265)

- A.在HTTP响应报文中的一个cookie首部行
- B.在HTTP请求报文中的一个cookie首部行
- C.在用户端系统中保留一个cookie文件
- D.位于web站点的一个后端数据库

### ⑤WEB缓存（WEB CACHE)也叫做代理服务器（proxy server)

- content distribution network内容分发网络CDN
- 共享的CDN和专用的CDN

### ⑥条件GET（conditional get）方法

- A.概念：条件GET就是HTTP协议的机制，允许缓存器证实它的对象是最新的

	- （1）请求报文使用GET方法（2）请求报文中包含一个“If-Modified-Since”首部行

- B.学习了一点WEB应用程序基础设施，包括缓存cookie 后端数据库。

## 3.因特网中的电子邮件Electronic Mail in the Internet

### ①概述：由用户代理（User agent 邮件服务器mail server和简单邮件传输协议 Simple Mail Transfer Protocol(SMTP)组成；SMTP是因特网电子邮件的核心。

### ②SMTP：RFC(request for comment) 5321;ASCII(American Standard Code for Information Interchange)***编程作业

### ③与HTTP的对比：HTTP是从WEB服务器向Web客户传送文件；SMTP是从一个邮件服务器向另一个邮件服务器传送文件。持续到HTTP和持续的SMTP都使用持续连接。 区别在于，（1）HTTP主要是一个拉协议，SMTP是一个推协议。（2）SMTP要求每个报文采用7比特ASCII码格式。（3）HTTP把每个对象封装到它自己的HTTP响应报文中，SMTP把所有报文对象放在一个报文之中。

### ④邮件报文格式：首部行

### ⑤邮件访问协议：

- (1)POP3(Post Office Protocol-Version3)第三版邮局协议

	- 特许、事务处理、更新

- （2）IMAP(internet mail  Access Protocol(因特网邮件访问协议）
- （3）HTTP(Web based E-mail)

## 4.DNS:因特网的目录服务DNS:the Internet's Directory Service

### ①概述

### ②DNS提供的服务：域名系统DNS(Domain Name System)：一个由分层的DNS服务器实现的分布式数据库，一个使得主机能够查询分布式数据库的应用层协议、运行在BIND软件的UNIX机器，DNS协议运行在UDP之上，使用53号端口

- A.主机别名Host Aliasing
- B.规范主机名Mail server Aliasing
- C.邮件服务器别名Load distribution
- D.负载分配Load distribution

### ③DNS工作机理概述Overview of How DNS Works

- 概述
- 单点故障 通信容量 远距离的集中式数据库 维护
- A.分布式层次数据库A Distributed ,Hierartichical Database
- B.DNS缓存DNS Catching

### ④DNS记录和报文DNS Records and Messages

## 5.P2P文件分发Peer to Peer File Distributions

### ①P2P体系结构的扩展性

### ②BitTorrent

## 6.视频流和内容分发网Video Streaming and Content Distribution Networks

### ①因特网视频Internet Video

### ②HTTP流和DASH Http streaming and DASH(Dynamic Adaptive Streaming over HTTP

### ③内容分发网Content distribution networks

- 缩写：CDN

### ④案例：Netflix Youtube和看看

## 7.套接字编程：生成网络应用Socket Programming:Creating Network Applications

### ①概述

### ②UDP套接字编程Socket programming with UDP

### ③TCP套接字编程Socket Programming with TCP

*XMind: ZEN - Trial Version*