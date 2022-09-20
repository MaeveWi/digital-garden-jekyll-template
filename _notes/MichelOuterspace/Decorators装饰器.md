## What？
装饰器允许我们包装另一个函数以扩展被包装函数的行为，而无需永久修改它。

我的理解就是类似于触发器或者git hooks，可以在一个函数调用之前或者之后，做一些扩展操作。

function函数，在python中是第一类对象，which means：
1. function是一个Object类型的实例，
2. 可以将function赋给一个变量
3. 可以将function作为一个参数传递给另一个function
4. 可以在一个function中返回一个function
5. 可以在任意数据结构中存储function，比如lists, hash tables...

### 装饰器的统一模板：
```python
from functools import wraps
# 对函数的装饰器，对类func最好为cls
def decorate(func):

    @wraps(func)
    def wrapper(*args,**kwargs):
        # 执行被装饰的函数
        result = func(*args,**kwargs) 
        # 返回结果
        return result
    # 返回内层函数
    return wrapper
```
[[什么是cls]]

## How
**Syntax for Decorator:** 
```python
def fun_decortar(function):
	def inner():
		...
		function()
		...
	return inner
		
@fun_decorator
def hello_decorator():
    print("hello")

# Above code is equivalent to

def hello_decorator():
    print("Gfg")
hello_decorator = fun_decorator(hello_decorator)

```

### For example
```python
# importing libraries
import time
import math

# decorator to calculate duration
# taken by any function.
def calculate_time(func):
    
# if function takes any arguments,
# can be added like this.
    def inner1(*args, **kwargs):
        # storing time before function execution
        begin = time.time()
        
        func(*args, **kwargs)
        
        # storing time after function execution`
        end=time.time()
        print("Total time taken in : ", func.__name__, end - begin)
    return inner1


# factorial 阶乘
@calculate_time
def factorial(num):
    # sleep 2 seconds because it takes very less time
    # so that you can see the actual difference
    time.sleep(2)
    print (math.factorial(num))

# calling the function
factorial(10)
```
#### Output
```
3628800
Total time taken in :  factorial 2.0061802864074707
```

### Chaining Decorators多重装饰器
```python
@decor1
@decor
def num():
    return 10

#上面就相当于
decor1(decor(num))
```


## functools.wraps装饰器伪装
经过装饰器之后的函数还是原来的函数吗？原来的函数还存在，但是调用的其实是经过装饰之后的新函数。  （**装饰器返回的是持有被装饰函数引用的闭包函数**）
导致`print(add.__name__)`或者`print(add.__doc__)`的结果不再是原来的函数的属性了。  
为了消除装饰器对原函数的影响，我们需要伪装成原函数，拥有原函数的属性，看起来就像是同一个人一样。

