# 实验一 常用网络命令及工具实验报告

## 一. 实验名称

常用网络命令及工具练习。

## 二. 实验目的

掌握常用网络命令（ping、tracert、ipconfig、route等）的使用，掌握常用网络工具（如Wireshark，putty等）的使用。

## 三. 实验内容

1．常用网络命令练习；

2．网络分析软件练习。

## 四. 实验设备环境

按照实际网络情况绘制拓扑图，实验结束后标注出内网、公网地址。【获取公网地址方式：Wireshark 抓包分析、查看路由器配置、访问 https://ip138.com/ 等网站和HTTP File Server软件等】。

**答：**首先查询公网IP，如下图：

![image-20220120154710504](https://gitee.com/bright_xu/blog-image/raw/master/202204221550321.png)

因此我的本机网络拓扑图如下：

<img src="https://gitee.com/bright_xu/blog-image/raw/master/202204221550063.png" alt="image-20220120155015724" style="zoom:80%;" />

## 五. 实验过程及结果分析

#### 步骤1：

以命令行方式查看并记录本机的网络配置信息，查看本机共有几个网卡，哪些是物理网卡，哪些是虚拟网卡；【参考命令：ipconfig /all】

**答：**使用`ipconfig /all`命令，可以看到6个网卡，由于图片过长，这里贴上图形化界面截图：

![image-20220119200209648](https://gitee.com/bright_xu/blog-image/raw/master/202204221551633.png)

使用`ipconfig /all`命令，可以看到其中以太网适配器`VMware Network Adapter VMnet1`和`VMware Network Adapter VMnet8`是虚拟网卡，其他4个都是物理网卡。WLAN部分截图如下：

![image-20220119200442018](https://gitee.com/bright_xu/blog-image/raw/master/202204221551844.png "截图")

本机上网时用的是哪一个网卡，IP地址、子网掩码、默认网关及DNS服务器地址分别是多少？

**答：**根据上一张截图可以看出信息分别如下表所示：

| 字段         | 配置值                        |
| :----------- | ----------------------------- |
| 上网网卡描述 | Intel(R) Wireless-AC 9462     |
| IP地址       | 192.168.1.104                 |
| 子网掩码     | 255.255.255.0                 |
| 默认网关     | 192.168.1.1                   |
| DNS服务器    | 211.137.130.3，211.137.130.19 |

#### 步骤2：

用命令行修改本机IP地址和DNS服务器地址为自动获取方式，查看并记录网卡配置信息，与手动设置地址时的配置有什么不同？

【参考命令：手动设置地址命令：netsh interface ip set address name="本地连接" static 192.168.1.101 255.255.255.0 192.168.1.1，netsh interface ip set dns name="本地连接" source=static add=202.117.1.20。自动获取地址命令：netsh interface ip set address name="本地连接" source=dhcp，netsh interface ip set dns name="本地连接" source=dhcp】

**答：**手动设置地址，截图如下：

![image-20220119213118500](https://gitee.com/bright_xu/blog-image/raw/master/202204232247102.png)

可以看到访问该网站时，用到了TCP协议和HTTP协议，主要作用如下：

##### TCP协议：

**协议功能：**传输控制协议TCP是为了在不可靠的互联网络上提供可靠的端到端字节流而专门设计的一个传输协议。

**源地址-目的地址：**192.168.1.104 ——202.117.1.13

**请求/应答信息：**6467 → 80 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 WS=256 SACK_PERM=1

##### HTTP协议：

**协议功能：**超文本传输协议HTTP是一种用于分布式、协作式和超媒体信息系统的应用层协议，是因特网上应用最为广泛的一种网络传输协议。

**源地址-目的地址：**202.117.1.13 ——192.168.1.104

**请求/应答信息：**HTTP/1.1 200 OK 

#### 步骤3：

运行Wireshark截获报文，登陆QQ或微信，和好友进行语音或者视频聊天。查看截获的报文，找出QQ或微信的服务器地址，分析语音或视频通信过程中双方的IP地址、协议及端口等信息。

**答：**与好友进行语音通话，本机截图如下：

![image-20220119220507252](https://gitee.com/bright_xu/blog-image/raw/master/202204232248516.png)

好友截图如下：

![image-20220119220554672](https://gitee.com/bright_xu/blog-image/raw/master/202204232248915.png)

根据上面截获的报文可以得出QQ的服务器地址，看到语音通信过程中双方的IP地址、协议及端口等信息，如下表：

##### 本机捕获信息：

| 描述项               |       值       |
| :------------------- | :------------: |
| QQ/微信服务器地址    | 36.155.248.242 |
| 本机IP地址           | 192.168.1.104  |
| 本机自测公网地址     | 111.20.226.11  |
| 通信好友的IP地址     | 111.30.159.58  |
| 通信协议（Protocol） |      UDP       |
| 通信源端口-目的端口  | 8000 -> 63986  |

好友捕获信息：

| 描述项               |       值       |
| -------------------- | :------------: |
| QQ/微信服务器地址    | 113.250.24.70  |
| 通信好友IP地址       | 192.168.1.102  |
| 通信好友自测公网地址 | 111.30.159.58  |
| 好友看到的我的IP地址 | 111.20.226.11  |
| 通信协议（Protocol） |      UDP       |
| 通信源端口-目的端口  | 55955 -> 18004 |

### 3. 互动讨论主题

本地计算机接入网络之后，需要通过哪些设置、启用哪些协议之后才能上网。

**答：**计算机接入网络，必须要设置IP地址、子网掩码、网关和DNS服务器地址之后才能上网。因此需要启用ARP协议、路由协议、DHCP协议、DNS协议、IP协议等之后才能上网。

**IP地址：**Internet上的每台主机都有一个唯一的IP地址。IP协议就是使用这个地址在主机之间传递信息，这是Internet 能够运行的基础。IP地址的长度为32位(共有2^32个IP地址)，分为4段，每段8位，用十进制数字表示，每段数字范围为0～255，段与段之间用句点隔开。**IP地址 = 网络标识号码 + 主机标识号码。**

**子网掩码（Net Mask）**用来指明一个IP地址的哪些位标识的是主机所在的子网以及哪些位标识的是主机的位掩码。子网掩码不能单独存在，它必须结合IP地址一起使用。子网掩码只有一个作用，就是将某个IP地址划分成网络地址和主机地址两部分。

**网关（Gateway）**就是一个网络连接到另一个网络的“关口”。（同一网络段的不同主机可以直接连接，不同网络直接连接需要通过网关）。一个用于 TCP/IP 协议的配置项，是一个可直接到达的 IP路由器的 IP地址。

**DNS服务器**是由解析器以及域名服务器组成的。域名服务器是指保存有该网络中所有主机的域名和对应IP地址，并具有将域名转换为IP地址功能的服务器。在上网时输入的网址，是通过域名解析系统解析找到了相对应的IP地址，这样才能上网。

### 4. 进阶自设计

通过Wireshark抓包分析QQ的登陆认证、消息传输和退出登录过程，分析其中涉及到的主要协议、关键数据和标识。【QQ的主要通讯协议类型是QICQ，注意观察数据包中的标识，看看能找到多少种类型的数据包，分析各种数据包的主要作用。】

**答：**打开wireshark开始抓包，然后登录QQ，可以看到出现大量的QICQ数据包，进行过滤，截图如下：

![image-20220120150012736](https://gitee.com/bright_xu/blog-image/raw/master/202204242237719.png)

点开一个数据包，可以看到QICQ数据包主要使用了QICQ协议（应用层）、UDP协议（传输层）、IPv4协议（网络层）等协议，接下来进行详细分析。

登录QQ时，可以看到客户端先向QQ服务器发起连接，可以看到数据包携带的数据是登录的QQ号，这里也就是我的QQ号（2191579187），command信息是：`Request KEY(29)`，也就是验证密码是否正确，进行登录。在本次抓包中，客户端IP为192.168.1.104，QQ服务器IP地址为61.151.180.240 。

登录成功后，服务器command变为`Get status of friend(129)`，开始获取QQ好友的状态。还会有各种命令，用于获取好友信息和进行消息发送。下列一系列图都是具体的command。

![image-20220120151815293](https://gitee.com/bright_xu/blog-image/raw/master/202204242238125.png)

![image-20220120151744708](https://gitee.com/bright_xu/blog-image/raw/master/202204252322026.png)

接收消息时，抓到的数据包command为`Receive message`，如下图：

![image-20220120152603824](https://gitee.com/bright_xu/blog-image/raw/master/202204242239490.png)

退出QQ登录，抓到的包中command为`Log out(1)`，也就是退出登录，如下图：

![image-20220120152752483](https://gitee.com/bright_xu/blog-image/raw/master/202204242239823.png)


