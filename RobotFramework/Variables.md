首先参照官方文档：
<https://robotframework.org/robotframework/latest/RobotFrameworkUserGuide.html#built-in-variables>

python 的 None 和 Java的 Null 一样  ， 在robot中 ${None} 和 ${null} 最终变为 None

空字符串(长度为0 ，分配存储空间)

Null ，None 不分配存储空间

在 robot中的对比体现：

上图：图2为打印结果
![](/Users/zoe/Desktop/RobotFramework_Notes/image/Variables_01.png)
![](/Users/zoe/Desktop/RobotFramework_Notes/image/Variables_02.png)


### 在robot中的使用请注意：params 的是没有类型的区分的，body 才有

当 **${None}** 作为某个param的值传给后端时是 **xxx=None**,get 查询参数实际上就是 URL 后面的 ?id=xxx

此时的**${None}**被作为字符串None处理，后端会自动转换为相应的类型。 

如果接口原本要求该参数为Integer 则转换为int型失败会报错。

如果接口原本要求该参数为string，则此时None就是string，此时请求成功

在body中，xxx=${None}, 则作None处理，不分配存储空间

 
