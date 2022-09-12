- 算数运算符：
	- +，-，* ，/ ，% **求余数**，** **求幂**，// **求商**
- 比较运算符：
	- , < , == , != , >=, <= , 
	- is：指向同一块内存，比如c=a，拥有相同值的两个int/float/str变量也是同一块内存
	- is not
- 逻辑运算符 
		- **You can use non-zero number instead of True and zero for False.**
	- and
	- or
	- not：boolean的相反
- 成员运算符：
	- in：`x in collection`is any collection of items like a list, tuple, set, string, etc.
	- not in
- 位运算符[Bitwise operators](https://www.geeksforgeeks.org/python-bitwise-operators/)
	- & , | , ~ , ^ , >> , <<
- 赋值运算符[Assignment operators](https://www.geeksforgeeks.org/assignment-operators-in-python/)
	- =, += , -= , *= , /= , %= , //= , **= , &= , |= , ^= , >>= , <<=
- **三元运算符Ternary operators**
	- 允许在单行中使用if-else，使代码更紧凑
	- [on_true] if [expression] else [on_false]
	```python
	a, b = 10, 20
	min = a if a < b else b
	```
- [运算符的关联性和优先级🔗](https://www.geeksforgeeks.org/python-operators/)

## 运算符的重载overloading
比如：+ 运算符可以用来相加两个int，也可以连接两个str，或者合并两个list。——这是因为str和list两个类重载了+ 运算符，通过类中的魔法方法 _ _ add_ _()方法定义了 + 运算符的操作。当我们使用 + 运算符时，会自动调用魔术方法 _ _add_ _

我们也可以在类中自定义 重载+方法，For example
```python
class complex:  
  def __init__(self, a, b):  
    self.a = a  
    self.b = b  
  
  # adding two objects   
def __add__(self, other):  
    return self.a + other.a, self.b + other.b  
  
  
Ob1 = complex(1, 2)  
Ob2 = complex(2, 3)  
Ob3 = Ob1 + Ob2  
print(Ob3)
===
(3,5)
```

还有其他的operators魔法方法见[魔法 隐藏方法](魔法%20隐藏方法.md)



