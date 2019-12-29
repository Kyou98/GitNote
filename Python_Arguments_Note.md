# Python_Arguments Note
## Lambda Expression:
The example uses a lambda expression to return a function.
```
>>> def make_incrementor(n):
...     return lambda x: x + n
...
>>> f = make_incrementor(42)
>>> f(0)
42
>>> f(1)
43
```
lambda parameters: expression
```
>>>def <lambda>(parameters):
>>>    return expression
```
---
```
lambda x: x + 1
```
example:
```
(lambda x: x + 1)(2)
3
```
Reduction is a lambda calculus strategy to compute the value of the expression. It consists of substituting the argument 2 for x:
```
(lambda x: x + 1)(2) = lambda 2: 2 + 1
                     = 2 + 1
                     = 3
```
---
```
lambda x, y: x + y
```
example
```
>>> (lambda x, y: x + y)(2, 3)
>>> 5
```
---
### Mapping a List of Functions
The map function of the previous chapter was used to apply one function to one or more iterables. We will now write a function which applies a bunch of functions, which may be an iterable such as a list or a tuple, for example, to one Python object.

把list,dict,str等Iterable变成Iterator可以使用iter()函数。 

可迭代对象（Iterable）:可以直接作用于for循环的对象统称为可迭代对象。
```
from math import sin, cos, tan, pi

def map_functions(x, functions):
     """ map an iterable of functions on the the object x """
     res = []
     for func in functions:
         res.append(func(x))
     return res

family_of_functions = (sin, cos, tan)
print(map_functions(pi, family_of_functions))
```


python书籍：    <流畅的python>