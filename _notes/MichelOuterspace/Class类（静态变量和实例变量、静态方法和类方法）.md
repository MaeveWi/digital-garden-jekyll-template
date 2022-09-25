## The self
-   类中的方法在定义时必须有一个额外的第一个参数self。当调用方法时，不需要给这个参数一个值，Python 自动提供它。
- 当我们调用一个对象的方法`myobject.method(arg1, arg2)`时，Python 会自动将 `this` 转换为 `MyClass.method(myobject, arg1, arg2)` 
- 这类似于 C++ 中的 this 指针和 Java 中的 this 引用。

## Constructor：`__init__` 
`__init__` 方法类似于 C++ 和 Java 中的构造函数。构造函数用于初始化对象。构造函数里面包含在对象创建时执行的一组语句，它在类的对象被实例化后立即运行。这个方法里面你可以做任何你在初始化对象的时候想做的事。
## Destructor：`__del__`
python拥有自动垃圾清理机制，当程序结束 或者一个对象的所有引用都被删除时，就会调用它的`__del__`方法
```python
# Python program to illustrate destructor  
class Employee:  
    # Initializing  
    def __init__(self):  
        print('Employee created.')  
  
    # Deleting (Calling destructor)  
    def __del__(self):  
        print('Destructor called, Employee deleted.')  
  
obj = Employee()  
del obj
===
Employee created.
Destructor called, Employee deleted.
```

```python
# Python program to illustrate destructor  
class A:  
    def __init__(self, bb):  
        self.b = bb  
class B:  
    def __init__(self):  
        self.a = A(self) #B把自己传给了A，同时又引用了A，这就造成一个循环调用，导致垃圾处理器不知道先处理哪一个对象，这样只要程序运行 A B对象就会一直留在内存中。  
        
    #destructor  
    def __del__(self):  
        print("die")  
def fun():  
    b = B()  
fun()
```

## 全局变量和局部变量？

## Class/Static and Instance Variables类变量和实例变量
- 类、静态变量是在类中、方法外赋值的变量（不需要static关键字）；实例变量是在构造函数或方法中使用 self 赋值的变量。
- 静态变量是在实例第一次创建的时候进行内存分配的。
- 实例变量对每个实例都可以是不同的，类变量对所有实例是相同的值，可以用过`类名.变量名`调用和修改。（虽然通过`实例名.变量名`可以单独进行修改，但是通常不建议修改）
```python
class Dog():  
    #class variable 静态变量、类变量  
    animal = 'dog'  
    def __init__(self,name,age):  
        #instance variable 实例变量  
        self.name = name  
        self.age = age  
          
    #也可以用普通set方法添加实例变量  
    def setcolor(self,color):  
        self.color = color  
  
    def get_color(self):  
        return self.color  
        
steve = Dog('steve',12) 
bob = Dog('bob',2)
#静态变量可以通过类名和实例名请求
print(Dog.animal)
print(steve.animal)
print(bob.animal)
#静态变量可以单独修改，但是之后再通过类修改静态变量的时候他不会再改变
steve.animal = 'bird'
Dog.animal  = 'dogggg'
print(Dog.animal) #doggg
print(bob.animal) #doggg
print(steve.animal)  #bird

#Dog.age  实例变量不能用类名请求
steve.setcolor("red")  
print(steve.get_color())
```



## Class Method and StaticMethod类方法和静态方法
- **Class method**使用@classmethod装饰器进行装饰，第一个参数默认需要传递当前class: cls；
- Class method是绑定到类，而不是类的实例；它可以修改类的状态，适用于类的所有实例

- **Static method**使用@staticmethod进行装饰，没有默认参数
- Static method也是绑定到类，而不是类的实例，但他不能修改类的状态。通常用于utility 方法

- Static和Class method都可以通过类名来调用，可以不需要对类进行实例化再调用其中的函数
```python
class C(object):  
    @classmethod  
    def fun1(cls,arg1,...):  
        pass  
    @staticmethod  
    def fun(arg1, arg2, ...):  
        pass
```

#### Why class method
- python不支持多个参数的重载构造函数，通过class method就可以在对象实例化之前调用这些函数，相当于多个构造函数。
- 我们一般使用Class method来创建factory方法，它返回object对象。很大程度上替代了其他OOP语言中的工厂模式，就像在Java中，通常通过factory类，实例化一个factory对象后通过它来构造实际需要的对象。
- ==classmethod还可以通过额外的类引用，提供继承时的多态特性，实现子类挂载点等？？？==

```python
class Person:  
    def __init__(self, name, age):  
        self.name = name  
        self.age = age  
  
    # a class method to create a Person object by birth year.  
    
    @classmethod  
    def fromBirthYear(cls, name, year):  
        return cls(name, date.today().year - year)  
  
person1 = Person('mayank', 21)  
person2 = Person.fromBirthYear('mayank', 1996)
```