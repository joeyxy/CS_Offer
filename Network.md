
## TCP/IP 参考模型

OSI(Open System Interconnect)，即开放式系统互联。 一般都叫 OSI 参考模型，是 ISO （国际标准化组织）组织在 1985 年研究的网络互联模型。该体系结构标准定义了网络互连的七层框架（物理层、数据链路层、网络层、传输层、会话层、表示层和应用层），即 ISO 开放系统互连参考模型。在这一框架下进一步详细规定了每一层的功能，以实现开放系统环境中的互连性、互操作性和应用的可移植性。

根据分而治之的原则， ISO 将整个通信功能划分为七个层次，划分原则是：

* 网路中各节点都有相同的层次；
* 不同节点的同等层具有相同的功能；
* 同一节点内相邻层之间通过接口通信；
* 每一层使用下层提供的服务，并向其上层提供服务；
* 不同节点的同等层按照协议实现对等层之间的通信。
    
分层的好处是利用层次结构可以把开放系统的信息交换问题分解到一系列容易控制的软硬件模块－层中，而各层可以根据需要独立进行修改或扩充功能，同时，有利于个不同制造厂家的设备互连，也有利于大家学习、理解数据通讯网络。

各层功能详述如下：

1. 物理层 (Physical Layer)：物理层是 OSI 参考模型的最低层，它利用传输介质为数据链路层提供物理连接。它主要关心的是通过物理链路从一个节点向另一个节点传送`比特流`，物理链路可能是铜线、卫星、微波或其他的通讯媒介。它关心的问题有：多少伏电压代表 1 ？多少伏电压代表 0 ？时钟速率是多少？采用全双工还是半双工传输？总的来说物理层关心的是链路的机械、电气、功能和规程特性。
2. 数据链路层 (Data Link Layer)：数据链路层是为网络层提供服务的，解决两个相邻结点之间的通信问题，传送的协议数据单元称为`数据帧`。数据帧中包含物理地址（又称 MAC 地址）、控制码、数据及校验码等信息。该层的主要作用是通过校验、确认和反馈重发等手段，将不可靠的物理链路转换成对网络层来说无差错的数据链路。此外，数据链路层还要协调收发双方的数据传输速率，即进行流量控制，以防止接收方因来不及处理发送方来的高速数据而导致缓冲器溢出及线路阻塞。
3. 网络层 (Network Layer)：网络层是为传输层提供服务的，传送的协议数据单元称为`数据包（分组）`。该层的主要作用是解决如何使数据包通过各结点传送的问题，即通过路径选择算法（路由）将数据包送到目的地。另外，为避免通信子网中出现过多的数据包而造成网络阻塞，需要对流入的数据包数量进行控制（拥塞控制）。当数据包要跨越多个通信子网才能到达目的地时，还要解决网际互连的问题。
4. 传输层 (Transport Layer)：传输层的作用是为上层协议提供端到端的可靠和透明的数据传输服务，包括处理差错控制和流量控制等问题，传输层传送的协议数据单元称为`数据段（报文）`。该层向高层屏蔽了下层数据通信的细节，使高层用户看到的只是在两个传输实体间的一条主机到主机的、可由用户控制和设定的、可靠的数据通路。
5. 会话层 (Session Layer)：会话层主要功能是管理和协调不同主机上各种进程之间的通信（对话），即负责建立、管理和终止应用程序之间的会话。会话层得名的原因是它很类似于两个实体间的会话概念。例如，一个交互的用户会话以登录到计算机开始，以注销结束。
6. 表示层 (Presentation Layer)：表示层处理流经结点的数据编码的表示方式问题，以保证一个系统应用层发出的信息可被另一系统的应用层读出。如果必要，该层可提供一种标准表示形式，用于将计算机内部的多种数据表示格式转换成网络通信中采用的标准表示形式。数据压缩和加密也是表示层可提供的转换功能之一。
7. 应用层 (Application Layer)：应用层是 OSI 参考模型的最高层，是用户与网络的接口。该层通过应用程序来完成网络用户的应用需求，如文件传输、收发电子邮件等。 

各层包含的协议大致如下图所示：
   
![][3]

［[网络层含有的协议](http://www.nowcoder.com/questionTerminal/4d87fe456e39498c995011813be0230b)］  
［[网络层功能](http://www.nowcoder.com/questionTerminal/b79339e956ac4330937b01af14b3102b)］

参考：
[TCP/IP协议族](https://zh.wikipedia.org/wiki/TCP/IP协议族)

## IP 地址

每个 32 位的 IP 地址由高位的可变长网络和低位的主机两部分组成。同一网络的所有主机，其地址的网络值是相同的。这意味着一个网络对应一块连续的 IP 地址空间，这块地址空间就称为`地址的前缀`。如果前缀包含 2^8 个地址，那么就留下了 24 位用于网络部分，可以写成 `*.*.*.*/24`。`子网掩码`用来与一个 IP 地址进行 AND 操作，提取出该 IP 地址的网络部分。

`子网划分`：在内部将一个网络块分成几个部分供多个内部网络使用，但对外部世界仍像单个网络一样。
`路由聚合`：把多个小前缀的地址块合并成一个大前缀的地址块。（解决路由表过大的问题）。

1953年，IP 地址被分为 5 个类别：

![][1]

注意全零（0.0.0.0）地址对应于当前主机。全1的IP地址（255.255.255.255）是当前子网的广播地址。

还有三个范围的 IP地址被声明为私有化，任何网络可以在内部随意地使用这些地址，但是不允许包含这些地址的数据包出现在 Internet 上。

* 1  个A类地址：10.0.0.0~10.255.255.255/8      (2^24 个地址) 
* 16 个B类地址：172.16.0.0~172.31.255.255/16   (16 * 2^16 个地址)
* 256个C类地址：192.168.0.0~192.168.255.255/24 (256*2^8 个地址)

保留IP地址不会在internet网上出现，用于企业网络，A企业可以用,B企业也可以使用！

# NAT 网络地址转换

## 网络套接字 socket

网络上不同的计算机之间进行 TCP、UDP通信需要使用网络套接字（socket）。socket是在不同计算机之间进行通信的一个抽象。他工作于TCP/IP协议中应用层和传输层之间的一个抽象。

![][2]

socket起源于UNIX，在Unix`一切皆文件`哲学的思想下，socket是一种"打开—读/写—关闭"模式的实现，服务器和客户端各自维护一个"文件"，在建立连接打开后，可以向自己文件写入内容供对方读取或者读取对方内容，通讯结束时关闭文件。

详细内容参见 [Network_Socket](more/Network_Socket.md)

参考：  
[Socket通信原理简介](http://www.jianshu.com/p/90348ef3f41e)  
[简单理解Socket](http://www.cnblogs.com/dolphinX/p/3460545.html)

# TCP 协议

TCP(Transmission Control Protocol)为应用程序之间提供面向连接的可靠的字节流服务。TCP为全双工协议，提供流控制机制，即允许接收方控制发送方的发送速度，此外还提供拥塞控制功能。

［[TCP 协议细节](http://www.nowcoder.com/questionTerminal/7aa912d4886e45759698dd074521c726)］  
［[滑动窗口协议](http://www.nowcoder.com/questionTerminal/3d9d35cc024840d2ae21929bcf868d53)］  
［[nagle算法](http://www.nowcoder.com/questionTerminal/787f0b432012420cb2918b7e1ca37ab2)］  
［[拥塞控制算法](http://www.nowcoder.com/questionTerminal/a2b95450f85c4855877a0c4f06c91a72)］  
［[状态转换流程](http://www.nowcoder.com/questionTerminal/246945f0e26541b89f4735c79e3f16a2)］  

详细内容参见 [Network_TCP](more/Network_TCP.md)
 
### TCP，UDP区别

TCP协议和UDP协议特性区别，主要从连接性、可靠性、有序性、拥塞控制、传输速度、头部大小(Header size)等6个方面来讲。

1. TCP是面向连接的协议，UDP是无连接协议。TCP用三次握手建立连接，UDP发送数据前不需要建立连接；
2. TCP可靠，UDP不可靠。TCP丢包会重传，并且有确认机制，UDP不会；
3. TCP有序，UDP无序。消息在传输过程中可能会乱序，后发送的消息可能会先到达，TCP会对其进行重排序，UDP不会；
4. TCP 必须对数据进行校验，而UDP的校验是可选的；
5. TCP有流量控制（滑动窗口）和拥塞控制，UDP没有；
6. TCP传输慢，UDP传输快。因为TCP需要建立连接、保证可靠性和有序性，所以比较耗时。
7. TCP要建立连接、保证可靠性和有序性，就会传输更多的信息，包头比较大（TCP头部至少需要20字节，UDP头部只要8个字节）。

基于TCP的协议有：HTTP/HTTPS，Telnet，FTP，SMTP。
基于UDP的协议有：DHCP，DNS，SNMP，TFTP，BOOTP。

参考： [TCP和UDP的区别](http://liangjiabin.com/blog/2015/03/difference-between-tcp-vs-udp-protocol.html)

# HTTP 协议

操作方式 | 数据位置 | 明文密文 | 数据安全 | 长度限制 | 应用场景
--------|---------|--------|---------|---------|-------
GET     | HTTP包头 |  明文  |  不安全  |  长度较小 | 查询数据
POST    | HTTP正文 | 可明可密|  安全   | 支持较大数据传输 |修改数据

详细内容参见 [Network_HTTP](More/Network_HTTP.md)

## 访问网页过程

从网络模型的角度来分析，主要涉及

* 应用层：DNS、HTTP；
* 传输层：TCP
* 网络层：IP，路由选择协议RIP，OSPF(内部网关协议),BGP(外部网关协议）
* 数据链路层：ARP

`应用层`：客户端浏览器发起一个HTTP会话到服务器。客户端浏览器通过 DNS 解析到 www.baidu.com 的IP地址，通过这个IP地址找到客户端到服务器的路径。

`传输层`：在客户端的传输层，把HTTP会话请求分成报文段，添加源和目的端口（服务器使用80端口监听客户端的请求，客户端由系统随机选择一个端口如5000），和服务器建立 TCP 连接后进行通信。

`网络层`：客户端的网络层不关心应用层或者传输层的东西，主要做的是通过查找路由表确定如何到达服务器，期间可能经过多个路由器。其中可能用到的路由选择协议有 RIP协议、OSPF协议、EGP协议。

`链路层`：包从路由器到达服务器的局域网后，通过 ARP 协议查找服务器IP地址对应的MAC地址，然后将数据帧传到服务器。

参考：[在浏览器中输入URL后执行的全部过程的个人总结](http://www.nowcoder.com/discuss/3853)

## Ping 过程


## 路由器与交换机区别

## 网络端口

TCP 服务器由发送端和接收端创建一种称为`套接字`的端点来获得，每个套接字有一个套接字编号（地址），该编号由主机的 IP 地址以及一个本地的16位数值组成的。这个16位数值称为端口，所以一共有2^16 ＝ 65535个端口可用。

1024以下的（不0包括1024）的端口被保留，只能用作由特权用户（比如UNIX系统的 root）启动的标准服务，这些端口称为`知名端口`。一些知名的端口如下：

|端口|协议|用途|
|---|---|---|
|20，21| FTP | 文件传输协议，21是控制端口，20是数据端口|
|22| SSH | 远程登录，Telnet的替代|
|23| Telnet | TELNET 终端仿真服务 |
|25| SMTP |简单邮件传输协议|
|53| DNS | 域名解析服务|
|80| HTTP| 万维网, 超文本传输服务|
|443| HTTPS| 安全的 Web|

1024～49151 之间的的其它端口可以通过 IANA 注册，由非特权用户使用，但是应用程序可以选择自己的端口号。

## 网络延迟

在传输介质中传输所用的时间，即从报文开始进入网络到它开始离开网络之间的时间。(网络延迟PING值越低速度越快)

* 1~30ms:极快，几乎察觉不出有延迟，玩任何游戏速度都特别顺畅
* 31~50ms:良好，可以正常游戏，没有明显的延迟情况
* 51~100ms:普通，对抗类游戏能感觉出明显延迟，稍有停顿
* > 100ms:差，无法正常游戏，有卡顿，丢包并掉线现象

# IP 报文

TTL 字段：

1. TTL长度8 bit，最大值是255，TTL的一个推荐值是64。
2. 虽然从字面上翻译，TTL是IP数据包在计算机网络中的存在的最长时间。但实际上TTL是IP数据包在网络中可以转发的最大跳数。
3. TTL字段由IP数据包的发送者设置，在IP数据包从源到目的的整个转发路径上，每经过一个路由器，把该TTL的值减1，然后再将IP包转发出去。
4. 如果在IP包到达目的IP之前，TTL减少为0，路由器将会丢弃收到的TTL=0的IP包并向发送者发送 ICMP time exceeded消息。
5. TTL的主要作用是避免IP包在网络中的无限循环和收发，节省了网络带宽，并能使IP包的发送者能收到告警消息。

## 路由权

路由权是衡量路由好坏的标准。路由算法修改路由表的基本目的是将最好路由信息添加到路由表中，路由的好坏是由路由算法根据自己获得的路由信息计算出来的。

对于每一条路由，路由算法产生一种权值来表示路由的好坏。通常情况下，这种权值越小，该路径越好。路由权的计算可能基于路径某单一特性计算，也可能基于路径多种属性进行计算。有几种路径特性经常被用于权值计算，如下：

* 带宽 -- 链路的数据容量。例如，通常情况下10M 以太网链路比 64K 出租线路要更好。
* 时延 -- 报文到达目标网络所需要的时间。
* 负载 -- 处于活跃状态的网络资源数量。
* 可靠性 -- 每条数据链路的出错率。
* 跳数 -- 报文到目的地需要经过的网络数。
* 开销 -- 一种人为设定的值，通常由网络管理员根据带宽、线路价格或其他一些因素综合得出。


# ARP(地址解析协议) 

首先，每个主机都会在自己的ARP缓冲区中建立一个ARP列表，以表示IP地址和MAC地址之间的对应关系。

当源主机要发送数据时，首先检查ARP列表中是否有对应IP地址的目的主机的MAC地址，如果有，则直接发送数据，如果没有，就向本网段的所有主机发送ARP数据包，该数据包包括的内容有：源主机 IP地址，源主机MAC地址，目的主机的IP 地址。

当本网络的所有主机收到该ARP数据包时，首先检查数据包中的IP地址是否是自己的IP地址，如果不是，则忽略该数据包，如果是，则首先从数据包中取出源主机的IP和MAC地址写入到ARP列表中，如果已经存在，则覆盖，然后将自己的MAC地址写入ARP响应包中，告诉源主机自己是它想要找的MAC地址。

源主机收到ARP响应包后。将目的主机的IP和MAC地址写入ARP列表，并利用此信息发送数据。如果源主机一直没有收到ARP响应数据包，表示ARP查询失败。

注意：广播发送ARP请求，单播发送ARP响应。

`RARP协议`：反向地址转换协议，允许局域网的物理机器从网关服务器的ARP表或者缓存上请求其IP地址。其因为较限于IP地址的运用以及其他的一些缺点，因此渐为更新的BOOTP或DHCP所取代。

工作流程：在网络中配置一台RARP服务器，里面保存着IP地址和MAC地址的映射关系。当无盘工作站启动后，就封装一个RARP数据包，里面有其MAC地址，然后广播到网络上去，当服务器收到请求包后，就查找对应的MAC地址的IP地址装入响应报文中发回给请求者。因为需要广播请求报文，因此RARP只能用于具有广播能力的网络。

## 以太网工作模式

常用的以太网卡支持以下工作模式：广播模式、多播模式、直接模式和混杂模式。

1. 广播模式（Broad Cast Model）:物理地址（MAC）地址是 0Xffffff 的帧为广播帧，工作在广播模式的网卡接收广播帧。它将会接收所有目的地址为广播地址的数据包，一般所有的网卡都会设置为这个模式。
2. 多播模式（MultiCast Model）：多播传送地址作为目的物理地址的帧可以被组内的其它主机同时接收，而组外主机却接收不到。但是，如果将网卡设置为多播传送模式，它可以接收所有的多播传送帧，而不论它是不是组内成员。
3. 直接模式（Direct Model）：工作在直接模式下的网卡只接收目地址是自己Mac地址的帧。只有当数据包的目的地址为网卡自己的地址时，网卡才接收它。
4. 混杂模式（Promiscuous Model）：工作在混杂模式下的网卡接收所有的流过网卡的帧，信包捕获程序就是在这种模式下运行的。网卡的缺省工作模式包含广播模式和直接模式，即它只接收广播帧和发给自己的帧。如果采用混杂模式，一个站点的网卡将接受同一网络内所有站点所发送的数据包这样就可以到达对于网络信息监视捕获的目的。它将接收所有经过的数据包，这个特性是编写网络监听程序的关键。

## ADSL

ADSL 是非对称数字用户线路（Asymmetric Digital Subscriber Line）的缩写，亦可称作非对称数字用户环路。ADSL技术提供的上行和下行带宽不对称，因此称为非对称数字用户线路，是一种异步传输模式（ATM）。

[1]: http://7xrlu9.com1.z0.glb.clouddn.com/Network_1.png
[2]: http://7xrlu9.com1.z0.glb.clouddn.com/Network_2.jpg
[3]: http://7xrlu9.com1.z0.glb.clouddn.com/Network_3.png




