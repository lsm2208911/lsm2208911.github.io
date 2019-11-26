---
layout:     post
title:      "TCP基础知识之报文格式、三次握手与四次挥手"
subtitle:   "让你的电脑起飞"
date:       2019-11-23
author:     "无力去闹"
# header-img: "img/post-bg-js-version.jpg"
tags:
    - 网络协议
---
今天上午把公司项目做完了后。下午看了一会java IO方面的知识。在此记录一下。有参考[TCP的三次握手与四次挥手（详解+动图）][1]、[TCP报文格式][2]、[TCP三次握手、四次挥手及状态转换详解](https://www.jianshu.com/p/29868fb82890)《码出高效-java开发手册》。

## TCP报文格式
![](/img/in-post/tcp-learning/tcpbaowen.png)

* tcp报文第一行是指向目标与源IP端口，
* 第二、三行是序列号与确认序号，因为TCP连接是基于字节的，所以需要给每个字节设置一个序号，而seq就是第一个字节的序号。确认号：当ACK为1时有效，即上次已成功接收到的数据字节序号加1。
* SYN：同步序号标识，用来发起一个连接。
* ACK：确认序号有效标识。只有当ACK=1时确认号字段才有效。当ACK=0时，确认号无效。
* FIN：发端完成发送任务标识。用来释放一个连接。FIN=1表明此报文段的发送端的数据已经发送完毕，并要求释放连接。

## TCP三次握手
1. 服务器启动后进入Listen状态，等待客户端的连接。
2. 客户端启动向服务器发起连接，会选择一个初始序列号SEQ=x与SYN=1一起向服务器发送，并且从close状态进入SYN-SEND状态。（第一次握手）
3. 服务器收到客户端发来的报文，如果同意连接，会发出确认报文：ACK=1 SYN=1 确认号ack=x+1同时还有一个自己生成的序列号SEQ=y，此时服务器进入SYN-REVD状态。（第二次握手）
4. 客户端收到服务器发来的确认报文，还要向服务器发送确认，确认报文：ACK=1 sck=y+1。此时客户端进入ESTABLISHED已建立状态。（第三次握手）
5. 服务器收到确认报文后也进入ESTABLISHED已连接状态。
![三次握手](https://img-blog.csdn.net/20170605110405666?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXpjc3U=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
## TCP四次挥手
1. 此时客户端与服务器都处于ESTABLISHED状态。
2. 客户端发生主动关闭，主动关闭的一方向对方发送FIN=1与seq=u（u为最后一次接收的数据包中的确认序号），并从ESTABLISHED变为FIN_WAIT_1状态。（第一次挥手）
3. 服务器收到客户端发来的请求关闭的数据包，确认后向客户端发送确认ACK=1，ack=u+1，服务器状态变为CLOSE_WAIT。客户端收到服务端的确认后状态由FIN_WAIT_1变为FIN_WAIT_2，此时客户端处于半关闭状态（可以接受，无法发送），这是要等服务器处理完向客户端发送数据后，向客户端发送关闭信号才可以关闭（第二次挥手）
4. 服务器处理完客户端的数据，向客户端发送FIN=1，ACK=1，ack=u+1，seq=w 表示已经处理完可以关闭了，并将状态改为LASK_ACK（第三次挥手）
5. 客户端收到后向服务器发送ACK=1，ack=w+1，并将状态更新为TIME_WAIT。服务器收到后状态改为CLOSE，不在回复。客户端在等待2个周期没有收到服务器的回复后，确认服务器已断开，便将状态改为CLOSE。（第四次挥手）
![](https://img-blog.csdn.net/20170606084851272?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXpjc3U=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)



[1]:https://blog.csdn.net/qzcsu/article/details/72861891
[2]:http://023wg.com/message/message/cd_feature_tcp_message_format.html