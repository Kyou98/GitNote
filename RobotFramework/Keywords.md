## RobotFramework_Keywords
### Run Keyword If
     
#### 1. 组合条件的用法
 AND 和 OR 必须全部小写，否者无法识别（You should use small caps "or" and "and" instead of OR and AND.）

And beware also the spaces/tabs between keywords and arguments (you need at least two spaces)

但是不能留超过四个 空格，否者robot 会认为  and/or 为 keyword

```
    ${color}    set variable  red
    ${validate_object}    set variable  def
    ${o}    run keyword if    "${color}" == "red" and "${validate_object}" != "def"    set variable    OK
    ${w}    run keyword if    "${color}" == "white" or "${validate_object}" != "def"    set variable    OK

```
#### 2. 存在性条件语句
   *Run Keyword If ${variable} in ['value1','value2','value3']*
   
##### 使用举例：
   
    Run Keyword If ${request_source} in ['INDIVIDUAL_US','INDIVIDUAL_US_PER','INDIVIDUAL_US_NonPER'], Set To Dictionary, ${payload.profile}, signature=${signature2}, ELSE, Set To Dictionary, signature=${signature1}
Documentation:  
Runs the given keyword with the given arguments, if condition is true.
##### 错误返回：
Start / End / Elapsed:  20190923 16:30:37.969 / 20190923 16:30:37.969 / 00:00:00.000
16:30:37.969    FAIL    Evaluating expression 'INDIVIDUAL_US in ['INDIVIDUAL_US','INDIVIDUAL_US_PER','INDIVIDUAL_US_NonPER']' failed: NameError: name 'INDIVIDUAL_US' is not defined

##### 解决办法： 参数加 ""
*Run Keyword If "${variable}" in ['value1','value2','value3']*


   
#### 3. Run Keyword If 和 Run keywords 搭配使用，实现满足条件的多种操作



### Create Dictionary
##### 错误用法
     @{body}    create dictionary    email=${email}    password=${password}
  返回值为:
	@{body} = [ email | password ]

##### 正确用法
     ${body}    create dictionary    email=${email}    password=${password}
     
     
     
### Create Session
     ...待更
     

### Create List
##### 1. 创建空数组 ： 
        ${roles}    create list
keyword后面不接任何参数即可
##### 2. 创建string类型数组：
        ${list}    create list    1    2
result: list=['1','2']
##### 3. 创建int类型数组：
        ${roles}.   create list    ${1}    ${2}
result: roles=[1,2]   
      
        
        
### LOG 不同使用方法的不同效果
##### LogMany /  Log(level=INFO,INFO is default) / Log(level=DEBUG)
    Log Many    -------------Balance--------------------    
    ...    cash: ${balance_resp0.balance.cash}
    Log    cash: ${balance_resp0.balance.cash}    level=DEBUG
    Log    netLiquidationValue: ${balance_resp0.balance.netLiquidationValue}
    
下图为打印结果：
![](/Users/zoe/Desktop/RobotFramework_Notes/image/loginfo.png)

Log 关键字的DEBUG级别不会在log里显示参数详细信息

Log Many 默认每个参数换行显示，如果在pycharm中写脚本的时候需要换行则用 ...

Log Many 在for 循环中的使用方法（换行写方法）：

    :For    ${item}    IN RANGE   0    ${position_items}
    \    Log Many    -----------------RIA Positions----------------
    \    ...    ${resp.data[${position_items}]}
    [Return]    ${status_code}    ${resp}


### ：For    IN  和 ：For    IN RANGE 使用区别
函数结构范例：

:For 变量  IN  序列(or 列表)

:For 变量  IN RANGE    [初始值    循环限量)开区间    循环变量的递增量（默认为1）
####：For IN 使用示例：
![](/Users/zoe/Desktop/RobotFramework_Notes/image/ForIn01.png)
![](/Users/zoe/Desktop/RobotFramework_Notes/image/ForIn02.png)

#### For In Range示例：
  
    :For    ${i}    IN    0    5
    \    Log    i=${i}
    :For    ${j}    IN RANGE    0    5
    \    Log    j=${j}
    :For    ${k}    IN RANGE    0    5   3
    \    Log    k=${k}
 运行结果：   
![](/Users/zoe/Desktop/RobotFramework_Notes/image/ForInRange01.png)
示例2:
![](/Users/zoe/Desktop/RobotFramework_Notes/image/ForInRange02.png)



      


