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
