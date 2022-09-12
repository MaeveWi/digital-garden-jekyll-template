## What？
装饰器允许我们包装另一个函数以扩展被包装函数的行为，而无需永久修改它。

我的理解就是类似于触发器或者git hooks，可以在一个函数调用之前或者之后，做一些扩展操作。

function函数，在python中是第一类对象，which means：
1. function是一个Object类型的实例，
2. 可以将function赋给一个变量
3. 可以将function作为一个参数传递给另一个function
4. 可以在一个function中返回一个function
5. 可以在任意数据结构中存储function，比如lists, hash tables...


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

# this can be added to any function present,
# in this case to calculate a factorial 阶乘
@calculate_time
def factorial(num):
    # sleep 2 seconds because it takes very less time
    # so that you can see the actual difference
    time.sleep(2)
    print (math.factorial(num))

# calling the function 阶乘.
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