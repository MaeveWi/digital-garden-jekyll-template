## What?
- 包含抽象方法的类叫做抽象类，其中 抽象方法只有声明，没有实现。
- 这些方法需要在子类中被重写。
- 抽象类相当于其他类的blueprint。 当我们想为组件的不同实现提供通用接口时，我们使用抽象类。
- 抽象类不能被实例化，实例化会raises error

## How?
- Python不提供抽象类，抽象类通过一个python模块来实现：叫做ABC（Abstract Base Classes）
- ABC提供一个装饰为抽象的基类，通过继承这个基类注册为抽象类
- 抽象方法使用@abstractmethod，或者不需要显示定义abstract method
```python
from abc import ABC, abstractmethod  
  
class Animal(ABC):  
    def move(self):  
        pass  
  
class Human(Animal):  
    def move(self):  
        print("I can walk and run")  
  
class Snake(Animal):  
    def move(self):  
        print("I can crawl")  
  
class Dog(Animal):  
    def move(self):  
        print("I can bark")  
  
# Driver code  
R = Human()  
R.move()  
K = Snake()  
K.move()  
R = Dog()  
R.move()
```
