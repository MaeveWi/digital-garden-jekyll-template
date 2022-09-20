## 全局变量和局部变量：
局部/本地变量：就是在function内部的变量，在function内部没有声明global 默认都是本地变量  
全局变量用**global**关键字

```python
a = 1 

# Uses global because there is no local 'a'  
def f():  
    print('Inside f() : ', a)  
      
# Variable 'a' is redefined as a local  
def g():  
    a = 2  
    print('Inside g() : ', a)  
  
# Uses global keyword to modify global 'a'  
def h():  
    global a  
    a = 3  
    print('Inside h() : ', a)
```