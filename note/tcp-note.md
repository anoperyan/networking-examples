# TCP笔记

## 谈谈对TCP的理解

TCP协议是一个用于分组交换网络中主机到主机的高度可靠的网络协议。

## TCP协议的特点

1. TCP协议是面向流的协议。
2. TCP是面向连接的协议。
3. 使用校验和，确认和重传机制来保证可靠性。

## 常见问题

### TCP报文有哪些首部有哪些字段，说说其作用？

|字段名|位数|说明|
|----|----|----|
|源端口号（Source Port）|16|发送端的端口号|
|目标端口号（Destination Port）|16|目标端的端口号|
|序列号（Sequence Number）|32|数据序列号，不包括建立连接时候的序列号|
|应答号（Acknowledge Number）|32| |
|数据偏移（Data Offset）|4|指示真实数据从哪儿开始，前面都是TCP头|
|保留位（Reserved）|6|必须全部为0，暂未启用|
|控制位（Control Bits）|6|URG（紧急指针是否启用），ACK（ACK是否启用），PSH（Push函数是否启用），RST（重置连接是否启用），SYN（同步序列号是否启用），FIN（结束是否启用）|
|窗口（Window）|16|当前发送者愿意接受的窗口长度|
|校验和（Checksum）|16|用于校验数据是否出错|
|紧急指针（Urgent Pointer）|16||
|选项（Options）|可变长度||
|填充（Padding）|||

### 讲一下TCP三次握手过程？

讲述连接同步握手。

1. TCP A发送一个SEQ=SEQ_1和开启SYN，ACK控制位的报文给TCP B，此时TCP A转入SYN-SENT状态。
2. TCP B收到报文后，发送一个SEQ=SEQ_2，ACK=SEQ_1+1和开启SYN，ACK控制位给B，此时TCP B转入SYN-RECEIVED状态。
3. TCP A收到报文后，转入ESTABLISHED状态，然后发送一个SEQ=SEQ_1+1，ACK=SEQ2+1和开启ACK控制位的报文给TCP B，TCP B 接受到报文后转入ESTABLISHED状态。

至此，TCP A和TCP B已经建立有效连接，可以开始发送带有数据的报文了。

### 为什么TCP建立连接是3次握手，而不是2两次或者4次？

所谓三次握手，实际上是三次信息发送。TCP协议旨在建立一个高度可靠的网络协议，所以在开始通信之前双方确定对方是否在线是提升可靠度的一个措施。

确认对方是否在线的方法就是“我发送一个消息，你按照规定规则回复我这个信息，使得我知道你已经在线。”。

在TCP三次握手中，第一次是A询问B，第二次是B回应A，同时询问B，第三次是A回应B。所以通过3次握手，刚好不多不少的实现了对方是否在线等额检测。

### 讲一下四次挥手的过程？

**第一次挥手**：

TCP A发送一个SEQ=SEQ_1，ACK=SEQ_2+1和开启ACK,FIN控制位的报文给TCP B，此时TCP A转入FIN-WAIT-1状态。

**第二次挥手**：

TCP B收到报文后，转入CLOSE-WAIT状态，同时发送一个SEQ=ACK_1，ACK=SEQ_1+1和开始ACK控制位的报文给TCP A。 TCP A收到报文后转入到FIN-WAT-2状态。 此时TCP B还是可以继续向TCP
A发送报文。

**第三次挥手**：

TCP B发送一个SEQ=SEQ_2，ACK=ACK_1和开启ACK，FIN控制位的报文给TCP A，此时TCP B转入LAST-ACK状态。

**第四次挥手**：

TCP A收到报文后，发送一个SEQ=ACK_2，ACK=SEQ_2+1和开启ACK控制位的报文，TCP A发出此报文，等待2MSL后，转入CLOSED状态，当TCP B收到此报文后，转入CLOSED状态。

## 参考文档

1. [RFC793-TRANSMISSION CONTROL PROTOCOL](https://datatracker.ietf.org/doc/html/rfc793)













