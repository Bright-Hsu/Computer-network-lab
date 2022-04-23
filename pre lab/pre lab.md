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
