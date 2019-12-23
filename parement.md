HTTP https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview  
# TCP(Transmission Control Protocol)
Refer to:  https://draveness.me/whys-the-design-tcp-three-way-handshake\
RFC793: https://tools.ietf.org/html/rfc793  
The combination of this information, including **sockets**, **sequence numbers**, and **window size**, is called a connection  
一对socket: 互联网地址标志符和端口  
window size: 用于做流量控制  
sequence number： 追踪通信发起方发送的数据包序号， 接收方通过序列号向发送方确认某个数据包是否成功接收  
  
*从以下三个方面讨论为什么我们需要三次握手才能初始化 sockets， window size， 初始序列号 并建立TCP连接*
* 通过三次握手才能阻止重复历史连接的初始化
* 通过三次握手才能对通信双方的初始序列号进行初始化
* 讨论其他次数握手建立连接的可能性  
  
#### 历史连接
 TCP 连接使用三次握手的首要原因 —— 为了阻止历史的重复连接初始化造成的混乱问题，防止使用 TCP 协议通信的双方建立了错误的连接。



IP  
UDP  
python 虚拟环境  
python 内存管理  
请求从发出到返回值中间经历了什么 ：
   S1: 建立TCP连接    
   S2: Http 发出请求（method， http version， path ，authentication， catch, session, body ）   
   S3: TCP 打包http信息，传输到server端  
   S4: 接收response

DNS 与 UDP   

SQL常用
