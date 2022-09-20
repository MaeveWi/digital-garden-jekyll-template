## yield关键字
yield和return一样，都是用在一个function中，可以返回值。但是它们的区别是什么？
1. yield 执行后，不会中断function，而是继续执行。
2. 这允许函数一个一个地返回值，而不是像return一样 一次返回全部结果的list
3. yield用在generators中，只要函数中有yield，这个函数就是一个generator


## Generators的使用
generators function返回的是一个generator object。遍历generator Object中的value，可以用`__next__()`或者`for loop`

```python
# A generator for Fibonacci Numbers  
def fib(limit):  
    a, b = 0, 1  
    # One by one yield Fibonacci Number  
    while a < limit:  
        yield a  
        a, b = b, a + b  

# Create a generator object  
x = fib(5)  

# Iterating over the generator object using __next__()  
print(x.__next__())  
print(x.__next__())  
print(x.__next__())  
print(x.__next__())  
print(x.__next__())  
  
# Iterating over the generator object using for loop.  
for i in fib(5):  
    print(i)
```