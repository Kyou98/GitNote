# 残酷面试的复习纲要 #

## HTTP(原理 请求头 请求体) ##

参考文献：
[MDN Http 文档](https://developer.mozilla.org/en-US/docs/Web/HTTP)

重点：
1. [Overview](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)
2. [headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
3. [methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
4. [http messages](https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages)  
5. 请求从发出到返回值中间经历了什么 ：  
   S1: 建立TCP连接    
   S2: Http 发出请求（method， http version， path ，authentication， catch, session, body ）   
   S3: TCP 打包http信息，传输到server端  
   S4: 接收response

需要浏览的点：

[status code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
经常遇到：
* Successful responses:  
  * 200  OK
  * 201  Create
  * 204  No Content
* Client error responses:  
  * 400 Bad Request
  * 401 Unauthorized
  * 403 Forbidden
  * 404 Not Fund
* Server error responses:
  * 500 Internal Error
  * 501 Not Implement
  * 502 Bad Gateway
  * 503 Service Unavailable
  * 504 Gateway Timeout 


难点：[CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

## HTTPS ##

[《图解HTTP》](https://kingyinliang.github.io/PDF/%E5%9B%BE%E8%A7%A3HTTP+%E5%BD%A9%E8%89%B2%E7%89%88.pdf) 第七章

## TCP ##

1. 三次握手，[为什么 TCP 建立连接需要三次握手](https://draveness.me/whys-the-design-tcp-three-way-handshake)
2. 为什么需要四次挥手？

参考文献：[《图解 TCP/IP》](https://github.com/dolotech/ebook/blob/master/%E3%80%8A%E5%9B%BE%E8%A7%A3TCP%20IP(%E7%AC%AC5%E7%89%88)%E3%80%8B.((%E6%97%A5)%E7%AB%B9%E4%B8%8B%E9%9A%86%E5%8F%B2).%5BPDF%5D.%26ckook.pdf) 6.4 

## DNS （Domain Name System） ##
管理主机名和IP地址之间对应关系的系统
过一下 《图解 TCP/IP》 5.2 即可


## UDP（User Datagram Protocol） ##

看《图解 TCP/IP》 6.3  
按照“制作程序的用户的指示行事” 。  面向无连接，可随时发送数据，简单高效，开销小
* 包总量较少的通信（DNS，SNMP等）
* 视频，音频等多媒体通信（即时通信）
* 限定于LAN等特定网络中的应用通信
* 广播通信（广播，多播）


## MYSQL 面试题与 SQL 常用 ##

增删改查，备份，索引，主从数据库，inner/left/outer/right on 和 where 区别谁先谁后，分库分表
1. MySQL 的复制原理以及流程：
  * 主： binlog线程： 记录下所有改变了数据库数据的语句，放进Master的binlog中；
  * 从： io线程： 在使用start slave之后，负责从master上拉取内容，放进自己的relay log中
  * 从： sql执行线程： 执行relay log中的语句
  
2. 备份：  
   mysqldump
   数据库导入导出命令（结构+数据):  
导出数据库结构和数据：mysqldump -u用户名 -p密码 数据库名> 路径+导出的文件名.sql  
导出数据库所有表结构：mysqldump -u用户名 -p密码 -d 数据库名>路径+文件名.sql  
导出数据表结构和数据：mysqldump -u用户名 -p密码 数据库名 表名>路径+文件名.sql  
导出数据表结构：mysqldump -u用户名 -p密码 -d 数据库名 表名>路径+文件名.sql  
3. 存储过程  
   预编译的代码块，对单表或多表进行增删改查
4. 索引
5. 事务  
事务（Transaction）是并发控制的基本单位。所谓的事务，它是一个操作序列，这些操作要么都执行，要么都不执行，它是一个不可分割的工作单位。事务是数据库维护数据一致性的单位，在每个事务结束时，都能保持数据一致性。
6.   
* DDL – Data Definition Language  
  *  Truncate  , drop    
* DQl – Data Query Language  

* DML – Data Manipulation Language  
* DCL – Data Control Language  
7. 数据库的乐观锁和悲观锁  
数据库管理系统（DBMS）中的并发控制的任务是确保在多个事务同时存取数据库中同一数据时不破坏事务的隔离性和统一性以及数据库的统一性。乐观并发控制(乐观锁)和悲观并发控制（悲观锁）是并发控制主要采用的技术手段。  
悲观锁：假定会发生并发冲突，屏蔽一切可能违反数据完整性的操作  
乐观锁：假设不会发生并发冲突，只在提交操作时检查是否违反数据完整性。
8. LIMIT OFFSET  
从第九条开始取，取18条记录：    
SELECT column FROM table LIMIT 18 OFFSET 8   
   同： SELECT column FROM table LIMIT 8， 18   
   
      
   SELECT column FROM table LIMIT 18  
   同： SELECT column FROM table LIMIT 0， 18
## ORM  (Object Relational Mapping) ##

看一下这个 [stackoverflow 回答](https://stackoverflow.com/questions/1279613/what-is-an-orm-how-does-it-work-and-how-should-i-use-one)就好

ORM 操作 和 直接SQL操作数据库表的区别    
区别在修改表结构，列名的时候会比较明显  
ORM 修改transfer表的wireID wire表会不会同步  （不会同步，改具体的数据的值时和执行SQL修改没区别）  
ORM 操作 我们系统具体怎么找到这么表对象：  
mss 项目  -> from msscore.account.models import Account
回忆上次统一修改邮件地址的问题
结束之后记得migration （migrate是Django框架的内置命令）


## Git 熟练消化理解 ##

1. fetch 与 pull 的区别；  
   git fetch 命令从服务器上抓取本地没有的数据时，它并不会修改工作目录中的内容。 它只会获取数据然后让你自己合并.  
   git pull = git fetch + git merge
2. 如何产生/解决 conflict；  
    我只知道手动，快捷方法不清楚
3. rebase；
   改变提交历史
4. git cherry-pick 'commit_id'   
   Apply the changes introduced by some existing commits  
   选择分支中的某几次commit操作， 比如只想合并部分到上一级分支中，可以用 git cherry-pick 代替merge整个分支
     
5. log 以及 log search 以及  blame
   git log  
   一个常用的选项是 -p，用来显示每次提交的内容差异。 你也可以加上 -2 来仅显示最近两次提交  
   git log -p -2
   git log --stat 列出所有被修改过的文件
   git log --graph 图标显示分支合并历史
   git log --grep 含指定关键字的提交
   git log -S   仅显示添加或移除了某个关键字的提交
   git log --author 仅指定相关作者的提交
   git log --all-match 以上条件  且 关系

   git blame  
   Show what revision and author last modified each line of a file

6. 删除远程分支：  
   git push origin --delete featurename 
   git branch -d featurename
   git rm 
  
## python 基本语法 ##

接着看完，能独立完成一个爬虫程序（至少能完全看懂）

## Redis ##

过一遍： [commands](https://redis.io/commands)，起码知道 redis 有什么功能。

难点：

1. https://redis.io/topics/distlock
2. https://redis.io/topics/pubsub


## RPC Remote Procedure Call ##
一种进程间的通信模式
<https://zh.wikipedia.org/wiki/%E9%81%A0%E7%A8%8B%E9%81%8E%E7%A8%8B%E8%AA%BF%E7%94%A8>

还是得看看这个啊gRPC Google开发的RPC框架：https://grpc.io/docs/guides/

## MQ 相关文章阅读 ##

[什么是 MQ](https://aws.amazon.com/cn/message-queue/)
消息队列是一种异步的服务间通信方式，适用于无服务器和微服务架构。消息在被处理和删除之前一直存储在队列上。每条消息仅可被一位用户处理一次。消息队列可被用于分离重量级处理、缓冲或批处理工作以及缓解高峰期工作负载。  
  
我们公司自己开发的组件 Hermes 处理MQ  
  
[kafka](https://kafka.apache.org/documentation/)  
由于 Kafka 的特性是支持分布式，同时也是基于分布式的，所以主题也是可以在多个节点上被分区和覆盖的。

## Zookeeper ##
维基百科  
分布式应用程序协调服务，是Google的Chubby一个开源的实现，是Hadoop和Hbase的重要组件。它是一个为分布式应用提供一致性服务的软件，提供的功能包括：配置维护、域名服务、分布式同步、组服务等。
ZooKeeper的基本运转流程：  
1、选举Leader。  
2、同步数据。  
3、选举Leader过程中算法有很多，但要达到的选举标准是一致的。  
4、Leader要具有最高的执行ID，类似root权限。  
5、集群中大多数的机器得到响应并接受选出的Leader。

## Docker ##
Linux cgroup


## Linux ##

第六章（文件处理）/第十二章 （进程相关）

Shell Script

## 基础算法题 50 题 python 语言 ##
0. 查找（二分查找，顺序查找，分块查找，哈希查找）
1. 堆 （
2. 栈  
3. 队列 
4. 排序（冒泡，快排，归并）https://www.geeksforgeeks.org/quick-sort/
5. 树（前序，中序，后序）


## python ##
https://juejin.im/post/5ca2471df265da307b2d45a3

### python的内存处理 ###
python 内存池 ：   预先申请内存留作备用，对于小的对象，Pymolloc 在内存池中申请空间，避免大量的内存碎片，提高回收效率  
大的对象则调用 new/malloc 申请新的内存空间


### python 垃圾回收 ###
https://juejin.im/post/5ca2471df265da307b2d45a3
1. 引用计数， 等于0回收。 无法回收循环引用的对象
2. 标记清除
3. 分代回收

## 项目回顾 ##
1. 常见异常类型（业务需求，代码实现，组件错误） 
+ python  <https://docs.python.org/3/library/exceptions.html#concrete-exceptions> 

  + **Concrete Exceptions：**  
    * EOFError  
    * AttributeError  
    * IndexError   
    * OverflowError     
    * TypeError    
    * SyntaxError  
    * SystemError  
    * ZeroDivisionError    
    * IOError    
  + **OS Exceptions：**    
    * FileNotFoundError   
    * FileExistsError  
    * ConnectionError    
    * PermissionError  
    * TimeoutError
+  java <https://www.geeksforgeeks.org/exceptions-in-java/>  
    * Exceptions
      * CheckedExceptions  
        * IO Exception
        * Compile Exception 
          * ClassNotFoundException 
          * IllegalAccessException
          * IllegalArgumentException
          * NoSuchMethodException
          * NoSuchFieldException
      * UncheckedExceptions  
        * Runtime Exceptions
          * SystemException
          * UnknownElementException
          * NullPointer Exceptions
          * ArithmeticException  eg:2/0


    * Error
      * Virtual Mechine Error
      * Assertion Error



2. 印象深刻的bug
  
3. 关于redis 的使用，bitmap + redis 实现order_id唯一性
4. RIA MCB Margin业务内部逻辑梳理， 小黄鸭练习
   
5. flash 与 cashier 的内部通信
   gRPC
   NGINX 协助锁相关的东西
6. X-mind，Paw，Curl使用
7. 两次点击 怎么防止重复下单（并发，关键资源加锁，同步机制）
   
8. 关于基金的业务知识