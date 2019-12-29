## This file generate some errors during daily use
---  
**1. random error**  
	Evaluating expression 'random.randint(900,1010)' failed: NameError: name 'random' is not defined

```
 ${returned_amount}    evaluate    random.randint(${amt_min},${amt_max})
```
Error because miss the module  
Should write like below
```
${returned_amount}    evaluate    random.randint(${amt_min},${amt_max})    modules=random
```
random.randrange(start,stop)  
random.choice("str","str","str")  
...  
all need add the **modules=random**


