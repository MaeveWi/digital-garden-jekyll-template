## What？
有嵌套函数，且内部函数使用了外部函数的变量，也就是自由变量。并且外部函数return值是内部函数。这个内部函数被称为 **Closure闭包**
比如：
```python
def startAt(x):  #x被称为自由变量free 
    def increment(y):  
        return x+y  
    return increment  #返回内部函数，不要加()
  
incr1 = startAt(1)  #incr1存储的实际上是increment(1)这个函数，而不是startAt()这个函数
incr5 = startAt(5)  
  
print(incr1(3))  #4
print(incr1(4))  #5
  
print(incr5(3))  #8
print(incr5(4))  #9
```

##### [[Decorators装饰器]]其实就是一种特殊的闭包的使用，就是内部函数调用的自由变量是function的闭包
```python
import logging  
logging.basicConfig(filename='example.log',level=logging.INFO)  
  
def add(x,y):  
    return x+y  
def sub(x,y):  
    return x-y  
  
def logger(func):  
    def log_func(*args):  
        logging.info('Running "{}" with arguments {}'.format(func.__name__, args))  
        print(func(*args))  
    return log_func  
  
add_logger = logger(add)  
sub_logger = logger(sub)  
  
add_logger(3,4)  
sub_logger(5,4)
```
**使用Decorator方式实现**
```python
import logging  
logging.basicConfig(filename='example.log',level=logging.INFO)  

def logger(func):  
    def log_func(*args):  
        logging.info('Running "{}" with arguments {}'.format(func.__name__, args))  
        print(func(*args))  
    return log_func  
  
@logger  
def add(x,y):  
    return x+y  
  
@logger  
def sub(x,y):  
    return x-y  
  
add(3,4)  
sub(5,4)
```

## Why？
在调用外部函数的时候，一般情况下，闭包函数和一个已经赋值的变量一起保存，这样后续调用的时候 能够访问这个变量值。在需要多次调用的时候，可以不用每次都要输入两个参数，使得代码更简洁。也提供了某种数据隐藏，减少全局变量的调用。
当需要的function比较多的时候，可以考虑用闭包。如果有更多的function需要使用，那就要使用class了
