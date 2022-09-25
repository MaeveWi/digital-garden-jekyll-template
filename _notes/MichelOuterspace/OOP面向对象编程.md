- Class and Objects
	- [[Class类（静态变量和实例变量、静态方法和类方法）]]
- Encapsulation 封装
- Inheritance 继承
- Polymorphism 多态

## Encapsulation
#### protected member
`_member` 只能被本类的他的子类调用
#### private member
`__member` 只能被本类调用，外部和子类都不能直接调用，可以使用本类的方法实现访问和修改
```python
class Dog():  

    #前面两个__表示hidden的变量    
    __safeword = ''  
    
    def __init__(self,name,age):  
        #instance variable 实例变量  
        self.name = name  
        self.__age = age  #private变量
        
    #通过本类的方法获取和修改private变量
    def setAge(self,age):  
        self.__age= age  
    def getAge(self):  
        return self.__age  

#子类
class LittleDog(Dog):  
    def __init__(self, name, age):  
        Dog.__init__(self, name, age)  
  
    def call(self):  
        print(self.name)  
        print(self.__age)  #无法访问父类private变量
  
dog = Dog('gg',12)  
print(dog.__age) #无法外部直接访问private变量
dog.setAge(123)  
print(dog.getAge())  
  
little = LittleDog('ll',11)  
print(little.__age)  #不能调用  
print(little.getAge()) #用父类的方法可以调用
```

## Inheritance
所有的类都是继承自Object类，默认继承Object
如果我们忘记在子类的`__init__`里面调用父类的`__init__`，那就无法在子类调用父类的方法和属性了。
```python
class Base1(object):  
    def __init__(self,a):  
        self.str1 = "Geek1"  
        self.a = a  
  
class Base2(object):  
    def __init__(self,b):  
        self.str2 = "Geek2"  
        self.b= b  

class Derived(Base1, Base2):  
    def __init__(self, a, b, c):  
        # Calling constructors of Base1 and Base2 classes  
        Base1.__init__(self, a)  
        Base2.__init__(self, b)  
        self.c = c
```
- single inheritance
- multiple inheritance 多继承，一个子类继承多个父类
- multilevel inheritance 多层继承
- hierarchical inheritance 多个父类被多个子类继承
- hybrid inheritance

## Polymorphism
#### 函数中的多态
一个函数可以接受不同类的实例 作为参数

或者简单的函数的多态：
```python
def add(x, y, z=0):  
    return x + y + z  

print(add(2, 3))  
print(add(2, 3, 4))
```

#### 类继承中的多态
继承了同一个父类的两个子类，可以各自重写父类的方法，达成同一个函数不同的实现。叫做overriding
