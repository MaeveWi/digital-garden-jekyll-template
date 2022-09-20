


可以像java**指定参数和返回类型**：
```python
def add(a: int, b: int) -> int:
  ...
  return c
```

也可以**不指定参数和返回类型**：
```python
def add(a, b):
 return a+b
```

可以定义函数时**指定参数的默认值**
- 指定默认值的参数必须都在右边
- 指定默认值的参数是optional，没有默认值的是required
- 所有参数传值时按顺序一一对应
```python
def add(a, b, c=1, d=2):
 return a+b+c+d
```

可以用**keyword arguments调用函数**
- 不用在意顺序，但是keyword必须完全一样
```python 
def student(name, age, a, className):  
  print("學生",name,age,a,className)  
  
student(a=0, age=11, name="wang", className="物理")
```


## 当用mutable object作为参数时：
如果定义函数时，直接使用空list或者dictionary或者其他mutable object作为默认值：  
注意：这个mutable object只在第一次调用的时候定义一次，后面每次调用会使用同一个对象
```python
def appendItem(itemName, itemList=[]):  
  itemList.append(itemName)  
  return itemList  
  
print(appendItem('notebook'))  
print(appendItem('pencil'))  
print(appendItem('eraser'))
```
返回：
```
['notebook']
['notebook', 'pencil']
['notebook', 'pencil', 'eraser']
```
而不是
```
['notebook']
['pencil']
['eraser']
```
#### 所以，最好实现方式  
将默认值分配为 none，然后在function内检查预期的列表或字典参数是否为 none 
```python
def appendItem(itemName, itemList=None):  
  if(itemList==None):  
    itemList = []  
  itemList.append(itemName)  
  return itemList  
  
print(appendItem('notebook'))  
print(appendItem('pencil'))  
print(appendItem('eraser'))
```

### 函数中的可变长度参数*args, **kwargs
In Python, we can pass a variable number of arguments to a function using special symbols. There are two special symbols:
-   *args (Non-Keyword Arguments)
-   **kwargs (Keyword Arguments)
```python
def myFun(*args, **kwargs):  
  for arg in args:  
    print(arg)  
  for key, value in kwargs.items():  
    print("%s == %s" % (key, value))  #将%后面的值插入到%s占位符的字符串中  
# Driver code  
myFun(1,'a','b',first='Geeks', mid='for', last='Geeks')
```


### Lambda/Anonymous functions匿名函数
**lambda** keyword is used to create anonymous functions.
详见[[lambda函数]]

### Function的Docstring
定义function第一行下面的字符串，通常用来说明function的用处用法，可以使用`.__doc__`([[魔法 隐藏方法]]）查看
```python
def evenOdd(x):  
  """This is function Docstring:  
  Function to check if the number is even or odd"""  ...  
# Driver code to call the function  
print(evenOdd.__doc__)
```

