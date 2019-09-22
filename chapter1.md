# ComputerNetworking
Computer Networking: A Top-Down Approach 7th Notes
# Chapter 1:Introduction（理解网络协议的构成 原理和工作方式）

## 1.What is the Internet?什么是因特网？

### ①具体构成描述

- A.概念Host主机/end system端系统
communication link通信链路

- B.Packet switch分组交换机
transmission rate传速速率是bit/s比特每秒

	- (1)路由器router
	- (2)链路层交换机layer-link switch
	- (3）路径：一个分组所经历的一系列通信链路和分组交换机统称为经过该网络的路径
	- （4）ISP因特网服务提供商。每个ISP自身就是一个由多台分组交换机和多段通信链路组成的网络，各ISP为端系统提供了各种不同类型的网络接入。

-  C.Packet分组：发送端系统将数据分段，并为每段加上首部字节，由此形成的信息叫做分组。
- D.协议：端系统 分组交换机和其他因特网部件都要运行一系列协议，这些协议控制因特网中信息的接收和发送

	- （1）TCP
	- (2)IP：IP协议定义了在路由器和端系统之间发送和接收的分组格式
	- （3）因特网工程任务组Internet Engineering Task Force,IETF,制定了一系列标准，标准文档也就是RFC request for comment.叫做请求评论

### ②服务描述

- A.分布式应用程序distributed application 涉及多个相互交换数据的端系统
- B.套接字接口（socket interface)该接口规定了运行在一个端系统上的程序请求因特网基础设施向运行在另一个端系统上的特定目的地程序交付数据的方式

### ③what is protocol

- A.定义了在两个或者多个通信实体之间交换的报文的格式和顺序，以及报文发送和/或接收一条报文或其他事件所采取的动作

	- 网络协议：

## 2.Network edge网络边缘

### ①概述：端系统位于因特网边缘，所以叫做端系统。也叫做主机。分类

- A客户client
- B服务器server :通常是更强大的机器。

### ②接入网：将端系统物理连接到边缘路由器(edge router)的网络

- A.家庭接入：DSL数字用户线(Digital Subscriber Line)复用器（DSLAM)CO(本地中心局）

	- 家庭电话线同时承载了数据和传统的电话信号，他们用不同的频率进行编码

		- 高速下行信道
		- 中速上行信道
		- 普通的双向电话信道

	-  混合光纤同轴Hybird Fiber Coax 使用了光纤和同轴电缆相结合的技术
	- 电缆调制解调器端接系统Cable Modem Termination System CMTS
	- 光纤到户Fiber to the home FTTH

		- 主动光纤网络AON、被动光纤网络PON
		- 光纤线路端接器optical line terminator

- B.企业（和家庭）接入

	- 以太网和WIFI

- C.广域无线接入：3G和LTE(long-term evolution)

### ③物理媒体

- A.导引型媒体：电波沿着固体媒体前行

	- （1）双绞铜线 UTP unshielded twisted pair
	- (2)同轴电缆 导引型共享媒体
	- （3）光纤
	- （4）陆地无线电信道
	- （5）卫星无线电信道

		- 同步卫星
		- 近地轨道

- B.非导引型媒体：电波在空气或外层空间中传播

## 3.Network core网络核心

### ①分组交换packet switching

- A.报文：message 为了从源端系统向目的端系统发送一个报文，源将长报文划分为较小的数据块，称之为分组。（Packet）
- B.每个分组通过通信链路和分组交换机传送

	- 路由器
	- 链路层交换机
	- 传送时间L/R秒

- C.存储转发传输（store-and-forward transmission)：在交换机能够开始向输出链路传输该分组的第一个比特之前，必须接收到整个分组。
- D.排队时延和分组丢失☆ 理解并描述
- E.转发表和路由选择协议routing protocol

### ②电路交换circuit switching

- A.端到端连接end-to-end connection
- B.电路交换网络中的复用

	- （1）频分复用frequency-division multiplexing FDM：链路频谱由跨越链路创建的所有连接共享。在连接期间链路为每条连接专用一个频段
	- （2）时分复用 time-division multiplexing TDM 时间被划分为固定期间的帧，每帧被划分为固定时间的频隙，当网络跨越一条链路创建一条连接时，网络在每个帧中为该连接制定一个时隙，这些时隙专门由该连接单独使用，一个时隙可用于传输该连接的数据 

- C.分组交换和电路交换的对比

	- （1）分组交换

		- 优点：提供了比电路交换更好的带宽共享、比电路交换更简单有效，实现成本更低、☆原因分析
		- 缺点：分组交换不适合实时服务，因为他端到端时延时可变和不可预测的

	- （2）电路交换

		- 电路交换在静默期专用电路空闲而不够经济

	- （3）分组交换性能优于电路交换性能：电路交换不考虑需求，而预先分配了传输链路的使用，使得已分配而并不需要链路时间未被利用；分组交换按需分配链路使用，链路传输能力将在所有需要在链路上传输分组的用户之间逐分组地被共享。

### ③网络的网络

- A. 因为因特网是由数以亿计的用户构成的，要解决这一问题，ISP自身必须互联，接入ISP被称为是客户customer，全球运输ISP被认为是提供商provider
- B.存在点POP( point of presence)

	- 第一层ISP 和区域竞争ISP

- C.

## 4.Delay loss throughput in networks分组交换网中的时延、丢包和吞吐量

### ①分组交换网中的时延概述：这四个累计相加是节点总时延

- A.节点处理时延nodal processing delay:检查分组首部和决定将该分组导向何处所需要的时间
- B.排队时延queuing delay：在队列中，当分组在链路上等待传输时
- c.传输时延transmission delay：L/R
- D.传播时延propagation delay:一个比特被推向链路，该比特需要向路由器B传播。从该链路的起点到路由器B传播所需要的时间
- E.传输时延和传播时延的比较

### ②排队时延和丢包:计算

- A.
- B.丢包：由于没有地方储存这个分组，路由器将丢弃这个分组

### ③端到端时延

- A.traceroute
- B.端系统 应用程序和其他时延

### ④计算机网络中的吞吐量

## 5.Protocol layers ,service models协议层次及服务模型

### ①分层的体系结构/OSI模型

- A.协议分层概述
- B.应用层

	- DNS域名系统
	- HTTP/SMTP/FTP

- C.运输层

	- TCP/UDP

- D.网络层
- E.链路层
- F.物理层

### ②封装encapsulation

- ☆理解并解释封装

## 6.networks under attack:security 面对攻击的网络

### ①坏家伙能够经因特网将有害程序放入你的计算机

- malware恶意软件
- Botnet僵尸网络
- 自我复制
- 病毒Virus
- worm蠕虫

### ②坏家伙能够攻击服务器和网络基础设施

- DOS denial of service 拒绝服务攻击
- 弱点攻击 带宽洪泛 连接洪泛
- 计算机网络设计者能够采取那些措施防止DOS攻击？

### ③坏家伙能够嗅探分组

- 分组嗅探器Packet sniffer
- wireshark的使用

### ④坏家伙能够伪装成你信任的人

## 7.history

### ①分组交换的发展1961-1972

### ②专用网络和网络互联2972-1980

### ③网络的激增1980-1990

### ④因特网爆炸：20世纪90年代

### ⑤最新发展

*XMind: ZEN - Trial Version*
