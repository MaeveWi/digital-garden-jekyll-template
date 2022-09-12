-   cast type to another
    
    ```python
    #cast int to float, string
    n = 100  #integer
    f = float(n)
    s = str(n)
    print(f,type(f), s,type(s))
    ===
    100.0 <class 'float'> 100 <class 'str'>
    ```
    
    ```python
    #cast float to int
    f = 100.99
    n = int(f)
    print(n,type(n))
    ===
    100 <class 'int'>
    ```
    
    ```python
    #string
    s = "132.65"
    #cast string to integer
    n = **int(float(**s))  #带小数点的str直接转int会报错：ValueError: invalid literal for int() with base 10: '132.65'
    #cast string to float
    f = float(s)
    print(f)
    print(type(f))
    ===
    132
    <class 'int'>
    132.65
    <class 'float'>
    ```

## Enum in python枚举类型
在Python中，枚举可以视为是一种数据类型，当一个变量的取值只有几种有限的情况时，我们可以将其声明为枚举类型。  
例如表示周几的这一变量weekday，只有七种可能的取值，我们就可以将其声明为枚举类型。

**为了让枚举类型key不能重复，且不可在外部更改value值，使用python内置的enum模块，常用的Enum，IntEnum，Unique**
```python
from enum import Enum  
class Weekday(Enum):  
  monday=1  
  tuesday=2  
  thrisday=3  
  
print(Weekday.monday)  # Weekday.monday  
print(Weekday.monday.name) # monday  
print(Weekday.monday.value) # 1  
print(type(Weekday.monday)) # <enum 'Weekday'>
```
对于枚举成员，.name和.value是其内置属性，我们还可以给枚举成员增加其他属性
```python
Weekday.monday.label="空"  
Weekday.monday.time=10  
  
print(Weekday.monday.label)  # 空  
print(Weekday.monday.time) # 10
```

注意：
- 在获取枚举类型的成员时，我们可以通过 类名+key的方式实现，即上面的`Weekday.monday`，还可以使用Weekday['key']这样的方式。也可以通过value来获取枚举成员，Weekday(value)这样的方式。
- 枚举类不能用来实例化对象
- 枚举类在外部不能修改value值
- 枚举成员可以进行比较，==或者is
- **如果想让value也不相同的话，可以导入unique。然后`@unique`**
- **如果要枚举类中的Value只能是整型数字，那么，可以导入IntEnum，然后继承IntEnum即可。注意，此时，如果value为字符串的数字，也不会报错**