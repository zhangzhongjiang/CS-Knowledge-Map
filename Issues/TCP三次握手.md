1. TCP 特点：顺序问题、丢包问题、连接维护、流量控制（针对另一个端）、拥塞控制（针对网络）。
2. 状态位：SYN 是发起一个连接，ACK 是回复，RST 是重新连接，FIN 是结束连接。
3. 三次握手除了双方建立连接外，主要还是为了沟通一件事情，就是 TCP 包的序号的问题。

   - 每个连接都要有不同的序号，这个序号的起始序号是随着时间变化的，可以看成一个 32 位的计数器，每 4 微秒 加一，如果计算一下，如果到重复，需要 4 个多小时，那个绕路的包早就死翘翘了，因为 IP 包头里有个 TTL，即生存时间。

4. 三次握手时序图：一开始，客户端和服务端都处于`CLOSE`状态。先是服务端主动监听某个端口，处于`LISTEN`状态。然后客户端主动发起连接`SYN`，之后处于`SYN-SENT`状态。服务端收到发起的连接后，返回`SYN`，并且`ACK`客户端的`SYN`，之后处于`SYN-RCVD`状态。客户端收到服务端发送的`SYN`和`ACK`之后，发送`ACK`的`ACK`，之后处于`ESTABLISHED`状态，因为它的一收一发成功了。服务端收到`ACK`的`ACK`之后，处于`ESTABLISHED`状态，因为它也一收一发了。
   ![](/Images/TCP三次握手状态时序图.png)
