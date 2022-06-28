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
|控制位（Control Bits）|6|URG（紧急指针是否启用），ACK（ACK是否启用），PSH（Push函数是否启用），
RST（重置连接是否启用），SYN（同步序列号是否启用），FIN（结束是否启用）|
|窗口（Window）|16|当前发送者愿意接受的窗口长度|
|校验和（Checksum）|16|用于校验数据是否出错|
|紧急指针（Urgent Pointer）|16||
|选项（Options）|可变长度||
|填充（Padding）|||

### 讲一下TCP三次握手过程？

讲述连接同步握手。

1. TCP A发送一个带有SEQ_1和开启SYN，ACK控制位的报文给TCP B，此时TCP A转入SYN-SENT状态。
2. TCP B收到报文后，发送一个带有SEQ=SEQ_2，ACK=SEQ_1+1和开启SYN，ACK控制位给B，此时TCP B转入SYN-RECEIVED状态。
3. TCP A收到报文后，转入ESTABLISHED状态，然后发送一个SEQ=SEQ_1+1，ACK=SEQ2+1和开启ACK控制位的报文给TCP B，TCP B 接受到报文后转入ESTABLISHED状态。

至此，TCP A和TCP B已经建立有效连接，可以开始发送带有数据的报文了。

## 参考文档

1. [RFC793-TRANSMISSION CONTROL PROTOCOL](https://datatracker.ietf.org/doc/html/rfc793)













