
# TCP
Transmission Control Protocol\
SYN  
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

**ACK**: 确认信息，是在電腦網路中通訊協定的一部份，是設備或是行程發出的訊息，回覆已收到資料。  
  
**RTT**: 往返时延，在通訊、電腦網路領域中，意指：在雙方通訊中，發訊方的訊號傳播到收訊方的時間，加上收訊方回傳訊息到發訊方的時間





# HTTP
refer to:  https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview  
  
# IP  
# UDP  
python 虚拟环境  
python 内存管理  
请求从发出到返回值中间经历了什么 ：
   S1: 建立TCP连接    
   S2: Http 发出请求（method， http version， path ，authentication， catch, session, body ）   
   S3: TCP 打包http信息，传输到server端  
   S4: 接收response

HTTP(原理 请求头 请求体)
HTTPS  
TCP 三次握手四次挥手能画出来
DNS 与 UDP 
SQL常用
MYSQL 面试题（增删改查，备份，索引，主从数据库，inner/left/outer/right  on 和 where 区别谁先谁后，分库分表）
Git 熟练消化理解  
python 基本语法接着看完，能独立完成一个爬虫程序（至少能完全看懂） 
Redis  原理透彻  
RPC <https://zh.wikipedia.org/wiki/%E9%81%A0%E7%A8%8B%E9%81%8E%E7%A8%8B%E8%AA%BF%E7%94%A8>
Kafak / MQ   相关文章阅读
Zookeeper / Docker 相关文章阅读，只需要了解原理
ORM 相关文章阅读，只需要了解
Linux 第六章（文件处理）/第十二章 （进程相关）
Shell Script
基础算法题 50 题 python 语言（各类排序）
python的内存处理 
python 垃圾回收
数据结构的堆栈内存



业务整理
两次点击 怎么防止重复下单（并发，关键资源加锁，同步机制）
常见异常类型（业务需求，代码实现，组件错误）
Nullpointer
format
index
filenotfund


异常状态码：
502
504
500
404
400

RIA 整块业务，小黄鸭演习






