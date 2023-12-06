

## Introduction

### Internet edge

#### Internet structure

##### network edge

hosts:clients and servers

##### Access networks,physical media

wired,wireless communication links

###### How to connect end systems to edge router

residential access nets

intitutional access network

mobile access networks(WiFi,4G/5G)

##### network core

interconnected routers

network of networks

### Network Core

#### circut switch(电路交换)

##### 主要特点

- 电路交换通常采用面向连接方式
- 先呼叫建立连接，实现端到端的资源预留
- 预留的资源包括:链路带宽资源、交换机的交换能力
- 电路交换连接建立后，物理通路被通信双方独占，资源专用，即使空闲也不与其他连接共享
- 由于建立连接并预留资源，因此传输性能好;但如果传输中发生设备故障，则传输被中断

###### 电路交换特点

通话的两个用户始终占用端到端的通信资源

##### 三个阶段

- **建立连接**：建立一条专用的物理通路（占用通信资源）。
- **通话**：主叫和被叫双方互相通电话（一直占用通信资源）。
- **释放连接**：释放刚才使用的专用的物理通路（归还通信资源）。

##### FDM and TDM

#### packet switching(分组交换)

##### Packet-switching key functions

Forwarding and routing(转发？和路由)

##### Packet-switching: store-and-forward

packet transmission delay: L/R

store and forward:entire packet must arrive at router before it can be transmitted on next link

##### 分组在互联网中的转发

- 根据**首部**中包含的目的地址、源地 址等重要控制信息进行转发。
- 每一个分组在互联网中**独立选择**传输路径。
- 位于网络核心部分的**路由器负责转发分组**，即进行分组交换。
- 路由器要创建和动态维护**转发表**。

###### 路由器处理分组的过程

暂存收到的分组；检查分组首部；查找转发表；按照首部中的目的地址，找到合适的接口转发出去。

##### 优点

高效、灵活、迅速、可靠

##### Packet-switching: queueing

##### forwarding

###### datagram network

destination address in packet determines next hop

routes may change during session

analogy: driving, asking direction

###### virtual circuit network

each packet carries tag (virtual circuit ID), tag determines next ho

fixed path determined at call setup time, remains fixed thru call

routers maintain per-call state

##### 计算机网络拓扑结构

###### 通信子网的拓扑构型

点——点线路通信子网拓扑结构

广播信道通信子网拓扑结构

#### Delay, loss and throughput in packet-switch network

##### 指标

速率：数据传输速率 bit/s

##### 节点总时延

节点处理时延$d_{proc}$，排队时延$d_{queue}$，传输时延(发送时延)$d_{trans}=\frac{数据帧长}{发送速率}$，传播时延$d_{prop}$

#### Protocol layers, service models

##### 分层原因

- 各层之间是独立的
- 灵活性好
- 结构上可分割开
- 易于实现和维护
- 能促进标准化工作

##### Why Data Encapsulation

To add control information (in form of header or trailer or both) to the data being encapsulated in order to ensure accurate and secure communication. The data after encapsulated is called protocol data unit (PDU)

###### control imformation

Address,Erro-detecting code,protocol control

##### Functions of Physical Layer

- physical characteristics of interfaces and media
- representation of bits: data rate, Synchronization of bits,Line configuration,physical topology,Transmission mode

##### Functions of Data Link Layer

###### node-to-node delivery

Framing, Physical addressing

- *Flow control
- Error control
- Access control

##### Functions of Network Layer

###### source-to-destination

Logical addressing

##### Functions of the Transport Layer

end-to-end

- Connection control
- Flow control
- Error control

##### Functions of the Session Layer

**establish**,**maintain** and **synchronize** the interaction between communication systems

##### Functions of the Presentation Layer

- Translation
- Encryption
- compression

##### Functions of the Application Layer

- Network virtural terminal
- File transfer,access,and management
- mail services
- directory services

<img src="https://www.pjl.xiezaiwangzhe.top/computer-network/1.png" style="zoom:150%;" />

##### TCP/IP参考模型

- 应用层
- 传输层
- 互联网层
- 链路层
- 物理层

<img src="https://www.pjl.xiezaiwangzhe.top/computer-network/2.png" style="zoom:80%;" />

## Application Layer

### Principles of network applications

#### Application architectures

- ##### Client-sever

- ##### Peer-to-peer

- ##### Hybrid of above

#### Application-layer protocol defines

- **types of messages exchanged**:e.g. request,response
- **meesage syntax**:语法
- **message semantics:**语义
- **rules for when and how process send & respond to messages**

open protocols:HTTP,SMTP

proprietary protocols

#### Transport service an app need

- 可靠数据传输
- 吞吐量
- 定时
- 安全性

#### Internet transport protocols services

##### TCP services

- **connection-oriented**
- **reliable transport**
- flow control (for receiver)

- congestion control (for network)

- does not provide:定时和带宽保证,(安全性)

##### UDP services

### 应用层协议

#### Web and HTTP

- HTTP使用**TCP**
- **无状态协议**：不保存关于客户的任何信息，同时请求两次仍然重新发送

##### 非持续连接和持续连接

每个请求/相应对是经过一个单独的TCP连接发送，还是所有请求及其响应经相同的TCP连接

###### 非持续连接的缺点

- 每请求一个文档就要有两倍RTT开销
- 客户和服务器每次建立新的TCP连接都要分配缓存和变量
- 使服务器的负担很重

###### RTT

![](https://www.pjl.xiezaiwangzhe.top/computer-network/3.png)

###### 持续连接

- 流水方式：客户在收到前一个响应之后才能发出下一个请求

- 非流水方式：在收到响应报文之前就能接着发送新的请求报文

#### COOKIE

##### cookie技术的4个组件：

- 在HTTP响应报文中的一个cookie首部行
- 在HTTP请求请求报文中的一个首部行
- 在用户端系统中保留一个cookie文件，由用户浏览器进行管理
- 位于Web站点的一个后端数据库

#### Web Cache

##### Web Cache 的用途

- Reduce response time for client
- Reduce traffic on an institution’s access link
- Internet dense with caches enables “poor” content providers to effectively deliver content

##### 保证一致性：

- 启发式策略：服务器响应web页的Last Modified 和Explires头启发
- 询问式策略 conditional get ?

#### Web安全与隐私

#### 全文检索搜索和分类目录搜索

#### 垂直搜索引擎和元搜索引擎

元搜索：将用户提交的检索请求发送到多个独立的搜索引擎上去搜索

#### FTP

##### 客户和服务器之间的两个从属进程和两个TCP连接

- 控制进程之间的TCP连接整个会话期间一直保持打开，由主进程创建
- 数据传送进程之间的连接动态创建，传送完毕后释放，由控制进程创建

##### FTP使用两个不同的端口号

控制进程21，数据传送进程20

#### 电子邮件

##### 电子邮件系统的三个组成部分

- 用户代理
- 邮件服务器：发送和接收邮件。**客户服务器**方式工作
- 邮件发送和读取协议：SMTP（**发送**），POP3（IMAP）（**读取**）。他们都使用TCP连接

##### 电子邮件格式

分为**信封**和**内容**两大部分

![](https://www.pjl.xiezaiwangzhe.top/computer-network/4.png)

##### SMTP

- 使用客户服务器模式
- 基于TCP
- 通信的三个阶段：建立连接，邮件传送，连接释放

##### POP3协议

- 使用客户服务器
- 基于TCP
- 支持用户鉴别
- *删除被读取的邮件

#### IMAP

- 客户服务器方式，端口143
- 基于TCP

- 连接后只下载邮件首部（部分下载）。
- 用户直接在 IMAP 服务器上创建和管理文件夹。
- 用户可以搜索邮件内容。
- 用户可以在不同的地方使用不同的计算机随时上网阅读和处理自己的邮件。
- 允许收信人只读取邮件中的某一个部分。
- **缺点**：要想查阅邮件，必须先联网

#### 万维网电子邮件

- 接收和发送电子邮件时使用HTTP协议
- 两个邮件服务器之间传送使用SMTP协议
- HTTP post提交邮件，get读取邮件

### DNS（域名解析系统）

UDP，端口53

采用客户服务器方式

NS,A类型

### P2P

#### 时间计算

- CS时间：$max{(\frac{NF}{u_s},\frac{F}{d_{min}}})$
- P2P时间：$max{(\frac{F}{u_s},\frac{F}{d_{min}}},\frac{NF}{u_s+\sum{u_i}})$

#### 具有集中目录服务器的 P2P 工作方

文件传输是分散的，文件定位是集中的

#### 具有全分布式结构的 P2P 文件共享程序

- BitTorrent 所有对等方集合称为一个**洪流** (torrent)。
- 下载文件的数据单元为长度固定的**文件块** (chunk)。
- 基础设施结点，叫做**追踪器**(tracker)。
- A 和对等方建立了 TCP 连接。所有与 A 建立了 TCP 连接的对等方为**相邻对等方**

##### 应当从邻居请求哪些块

针对她没有的块在邻居中决定最稀缺的块，**最稀缺优先**

##### 决定响应哪个请求

能够以**最高速率**向她提供数据的邻居，给出优先权

除了上面的，还要另外随机找一个试探的对等方

## Transport Layer

### 多路复用与多路分解

- 多路分解：将运输层报文段中的数据交付到正确的套接字的工作
- 多路复用：从不同套接字中收集数据块，并为每个数据块封装首部信息生成报文段，并将报文段传递到网络层

##### UDP

- 源端口号

- 目的端口号

##### TCP

- 源IP
- 源端口号
- 目的IP
- 目的端口号

### UDP

#### 采用UDP的原因

- 不需要建立连接
- 简单
- 分组首部开销小
- 没有拥塞控制，速度快

#### 校验核

### RDT

#### 1.0

#### 2.0

加了**肯定确认**和**否定确认**

##### 缺陷

ACK和NAK可能受损

#### 2.1

##### 发送方

- 分组加序号
- 收到损坏的回答或者NAK，重发
- 收到正确的ACK则发下一个分组

##### 接收方

- 收到损坏的包返回NAK
- 收到不是当前应该接收的包，返回ACK
- 收到没损坏且序号正确的，则接收并等待下一个

#### 2.2

##### 发送方

- 分组加序号
- 收到损坏的回答或者对上一个分组的ACK，重发
- 收到正确的ACK则发下一个分组

##### 接收方

- 收到损坏的或者上一个分组的包，发送ACK上一个分组
- 未损坏、序号正确则接收

#### 3.0

解决了丢包

##### 发送方

- 发送完分组开始计时
- 收到损坏或者对上一个分组的确认，不做处理等待超时
- 超时重发，重新计时
- 收到正确的ACK则停止计时，准备发下一个分组

### 流水线可靠数据传输

- 增加序号
- 发送方接收方增加缓冲

#### GO-Back-N

#### Selective Repeat

窗口长度必须小于等于序号空间大小的一半

###  TCP

#### 建立连接

<img src="https://www.pjl.xiezaiwangzhe.top/computer-network/5.jpeg" style="zoom: 80%;" />

#### 超时值的设置

EstimatedRTT=(1-$\alpha$)*EstimatedRTT+$\alpha$*SampleRTT

DevRTT=(1-$\beta$)*DevRTT+$\beta$*|SampleRTT-EstimatedRTT|

TImeoutInterval=EstimatedRTT + 4*DevRTT、

### 网络拥塞的几种代价

- 当分组的到达速率接近链路容量时，分组经历巨大的排队时延。
- 发送方必须执行重传以补偿因为缓存溢出而丢弃 (丢失) 的分组
- 发送方在遇到大时延时所进行的不必要重传会引起路由器利用其链路带宽来转发不必要的分组副本
- 当一个分组沿一条路径被丢弃时，每个上游路由器用于转发该分组到丢弃该分组而使用的传输容量最终被浪费掉了。

#### TCP 可靠传输

##### TCP流量控制

##### TCP拥塞控制

###### 慢开始

先令拥塞窗口cwnd=1，即一个最大报文段长度MSS。每收到一个对新报文的确认后，将cwnd加1.

###### 拥塞避免

每个RTT，cwnd加1

###### 网络拥塞处理

- cwnd<ssthresh,慢开始
- cwnd>=ssthresh，拥塞避免
- **出现拥塞，ssthresh设为出现拥塞时发送发cwnd的一半，然后将cwnd设为1。**
- cwnd在慢启动时，如果最后加倍超过了ssthresh，则cwnd=ssthresh

#### TCP关闭

![](https://www.pjl.xiezaiwangzhe.top/computer-network/6.png)

<img src="https://www.pjl.xiezaiwangzhe.top/computer-network/7.png" style="zoom: 80%;" />

## Network Layer

### 转发和路由选择：数据平面和控制平面

#### 转发

当一个分组到达某路由器的一条输人链路时，该路由器必须将该分组移动到适当的输出链路。

#### 路由

路由选择。当分组从发送方流向接收方时，网络层必须决定这些分组所采用的路由或路径。计算这些路径的算法被称为路由选择算法

#### 转发和路由选择的区别

##### 转发

- 根据转发表将用户的 IP 数据报从合适的端口转发出去
- 仅涉及到一个路由器
- 转发表是从路由表得出的。
- 转发表必须包含完成转发功能所必需的信息，每一行必须包含从要到达的目的网络到输出端口和某些MAC 地址信息 (如下一跳的以太网地址)的映射。

##### 路由选择

- 按照路由选择算法，根据网络拓扑的变化情况，动态地改变所选择的路由，并由此构造出整个的路由表
- 涉及到很多路由器。
- 路由表一般仅包含从目的网络到下跳 (用 IP 地址表示) 的映射

#### 数据层面

- 路由器根据本路由器生成的**转发表**，把收到的分组从查找到的对应接口**转发**出去。
- **独立**工作。
- 采用**硬件**进行转发，快。

#### 控制层面

- 根据路由选择协议所用的路由算法**计算路由**，创建出本路由器的路由表
- 许多路由器**协同**动作。
- 采用**软件**计算，慢。

#### 网络层提供的两种服务

##### 无连接服务

- 不需要提前建立连接
- 网络层向上只提供简单灵活**无连接的、尽最大努力交付**的**数据报服务**
- 发送分组时不需要先建立连接，每个分组独立发送
- 数据报独立转发，相同源-目的的数据报可能经过不同的路径
- **网络层不提供服务质量的承诺**
- 传输网络**不提供端到端**的可靠传输服务:丢包、乱序、错误

###### 优点

**网络的造价大大降低**，**运行方式灵活**，**能够适应多种应用**

##### 面向连接服务

- 面向连接服务:如打电话
- 通信之间先建立**逻辑连接**:在此过程中，如有需要，可以预留网络资源
- 结合使用可靠传输的网络协议，保证所发送的分组无差错按序到达终点
- 虚电路是逻辑连接
- 虚电路表示这只是一条**逻辑上的连接**，分组都沿着这条逻辑连接**按照存储转发方式传送**，而并不是真正建立了一条物理连接

**注意**，电路交换的电话通信是先建立了一条**真正的连接**。因此分组交换的虚连接和电路交换的连接只是类似，但并不完全相同

#### 面向连接的虚电路

虚电路转发决策基于分组标签，即虚电路号

- 建立连接
- 发送数据
- 释放连接

#### 无连接数据报

转发策略：基于分组的目的地址

### 路由器

路由器的主要工作：**转发分组**

#### 输入端口对收到分组的处理

<img src="https://www.pjl.xiezaiwangzhe.top/computer-network/8.png" style="zoom: 67%;" />

- 物理层处理：从输入端口接收比特
- 数据链路层处理：剥去帧的首部和尾部
- 网络层处理：分组**排队**。查表和转发。若收到的分组是交换路由信息的 分组，送交路由 选择处理机。 若收到的是数据分组，按目的地址查找 转发表，根据得出的结果，经交换结构 到达合适的输出端口。若某分组正在查 找转发表，该分组排队等待。

#### 输出端口将交换结构传送来的分组发送到线路

<img src="https://www.pjl.xiezaiwangzhe.top/computer-network/9.png" style="zoom: 67%;" />

- 网络层处理分组排队。缓存管理。从交换结构接收分组。当交换结构传送的分组 的速率超过输出链路的发送速率时，来不及发 送的分组就必须缓存在队列中。若分组处理的 速率赶不上分组进入队列的速率，队列满时， 丢弃后面进入的分组。
- 数据链路层处理：给分组加上链路层的 首部和尾部
- 物理层处理：发送到输出线路上

#### 交换结构

##### 通过存储器

<img src="https://www.pjl.xiezaiwangzhe.top/computer-network/10.png" style="zoom:67%;" />

1. 当路由器的某个输入端口收到一个分组时就用**中断**方式通知路由选择处理机。然后分组就从输入端口复制到存储器中
2. 路由器处理机从分组首部提取目的地址，查找路由表，再将分组复制到合适的输出端口的**缓存**中
3. 若存储器的带宽(读或写) 为每秒 M个分组，那么路由器的交换速率 (即分组从输入端传送到输出端口的速率) **一定小于 M/2**

##### 通过总线

<img src="https://www.pjl.xiezaiwangzhe.top/computer-network/11.png" style="zoom:67%;" />

1. 数据报从输入端口通过**共享的总线**直接传送到合适的输出端口，而**不需要**路由选择处理机的干预。
2. 当分组到达输入端口时若发现**总线忙**，则被阳塞而不能通过交换结构，并在输入端口**排队**等待。
3. 因为每一个要转发的分组都要通过这一条总线，因此路由器的转发带宽就受总线速率的限制

##### 通过互连网络（纵横交换结构）

<img src="https://www.pjl.xiezaiwangzhe.top/computer-network/12.png" style="zoom: 67%;" />

1. 它有 2N 条总线，控制交叉节点可以使 N 个输入端口和 N 个输出端口相连接
2. (2) 当输入端口收到一个分组时，就将它发送到**水平总线**上
3. (3) 若通向输出端口的垂直总线空闲，则将**垂直总线**与水平总线接通，把该分组转发到这个输出端口。若输出端口已被占用，分组在输入端口**排队**等待

特点:是一种**无阻塞**的交换结构，分组可以转发到任何个输出端口，只要这个输出端口没有被别的分组占用

#### 输入端口排队

线路前部阻塞（HOL）：因为线路前部的另一个分组而阻塞

#### 输出端口排队

##### 分组调度

- 先进先出
- 优先权排队：表现最好（高优先权队列，低优先权队列）
- *循环和加权公平排队

### IP地址

#### IP地址及其表示方法

- 32位二进制代码
- 点分十进制记法
- 两个字段：**网络号**和**主机号**

ip地址在整个互联网范围内是**唯一**的

#### ip地址的分类

<img src="https://www.pjl.xiezaiwangzhe.top/computer-network/13.png" alt="13" style="zoom: 80%;" />

##### 地址范围

- A：1.0.0.0~126.0.0.0
- B：128.0.0.0~191.255.255.255
- C：192.0.0.0~223.255.255.255

##### 可指派范围

- A：1~126
- B：128.1~191.255
- C：192.0.1~223.255.255

##### 注意：

- A 类网络地址中，**网络号 0 和 127 是保留地址**，不指派。0 表示“本网络”，127 保留作为本地环回测试地址。
- B 类网络地址中网络号 128.0 是被IANA 保留的，不指派。采用无分类编址 (CIDR) 时可以指派
- C 类网络地址中，网络号 192.0.0 是被 IANA 保留的，不指派。采用无分类编址 (CIDR) 时可以指派
- 指派主机号时，要**扣除**全 0 和全 1。全 0 和全 1 有特殊含义和用途。

#### IP特殊地址

- 全0网络地址：只在系统启动时有效，用于启动时临时通信，又叫主机地址
- 网络127.0.0.0：指本地节点(一般为127.0.0.1)，用于测试网卡及TCP/IP软件， 这样浪费了1700万个地址
- 全0主机地址：用于指定网络本身，称之为网络地址或者网络号
- 全1主机地址：用于广播，也称定向广播，需要指定目标网络
- 0.0.0.0 指任意地址
- 255.255.255.255 用于本地广播，也称有限/受限广播，无须知道本地网络地址

##### 私有地址

<img src="https://www.pjl.xiezaiwangzhe.top/computer-network/14.png" alt="13" style="zoom: 50%;" />

#### ip地址和子网掩网

<img src="https://www.pjl.xiezaiwangzhe.top/computer-network/15.png" style="zoom: 67%;" />

**(IP 地址) AND (子网掩码) =网络地址**

#### 子网掩码是一个重要属性

- 子网掩码是一个网络或一个子网的重要属性
- 路由器在和相邻路由器交换路由信息时，必须把自己所在网终 (或子网)的子网掩码告诉相邻路由器
- 路由器的路由表中的每一个项目，除了要给出目的网络地址外，还必须同时给出该网络的子网掩码
- 若一个路由器连接在两个子网上就拥有两个网终地址和两个子网掩码

##### 不同的子网掩码得出相同的网络地址。 但不同的掩码的效果是不同的。

- 在不划分子网的两级 IP 地址下，从 IP 地址得出网络地址是个很简单的事。
- 但在划分子网的情况下，从 IP 地址却**不能唯一地得出网络地址**来，这是因为网终地址取决于那个网终所采用的子网掩码但数据报的首部并没有提供子网掩码的信息
- 因此分组转发的算法也必须做相应的改动。

#### IP 层转发分组的流程

- 有四个 A 类网络通过三个路由器连接在一起。每一个网络上都可能有成干上万个主机。
- 可以想像，若按目的主机号来制作路由表，则所得出的路由表就会过于庞大
- 但若按主机所在的网络地址来制作路由表，那么每一个路由器中的路由表就只包含 4 个项目。这样就可使路由表大大简化

