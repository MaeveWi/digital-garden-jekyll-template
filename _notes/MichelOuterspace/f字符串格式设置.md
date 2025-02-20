## Python f 字符串

Python f-string 是执行字符串格式化的最新 Python 语法。 自 Python 3.6 起可用。 Python f 字符串提供了一种更快，更易读，更简明且不易出错的在 Python 中格式化字符串的方式。

f 字符串的前缀为`f`，并使用`{}`括号评估值。

在冒号后指定用于类型，填充或对齐的格式说明符； 例如：`f'{price:.3}'`，其中`price`是变量名。

## Python 字符串格式

以下示例总结了 Python 中的字符串格式设置选项。

`formatting_strings.py`

```python
#!/usr/bin/env python3

name = 'Peter'
age = 23

print('%s is %d years old' % (name, age))
print('{} is {} years old'.format(name, age))
print(f'{name} is {age} years old')
```

该示例使用两个变量设置字符串格式。

```python
print('%s is %d years old' % (name, age))
```

这是最旧的选项。 它使用`%`运算符和经典字符串格式指定，例如`%s`和`%d`。

```python
print('{} is {} years old'.format(name, age))
```

从 Python 3.0 开始，`format()`函数被引入以提供高级格式化选项。

```python
print(f'{name} is {age} years old')
```

从 Python 3.6 开始，Python f 字符串可用。 该字符串具有`f`前缀，并使用`{}`评估变量。

```python
$ python formatting_string.py
Peter is 23 years old
Peter is 23 years old
Peter is 23 years old
```

## Python f 字符串表达式

我们可以将表达式放在`{}`括号之间。

`expressions.py`

```python
#!/usr/bin/env python3

bags = 3
apples_in_bag = 12

print(f'There are total of {bags * apples_in_bag} apples')
```

该示例对 f 字符串中的表达式求值。

```python
$ python expressions.py
There are total of 36 apples
```

## Python f 字符串字典

我们可以使用 f 字符串中的字典。

`dicts.py`

```python
#!/usr/bin/env python3

user = {'name': 'John Doe', 'occupation': 'gardener'}

print(f"{user['name']} is a {user['occupation']}")
```

该示例以 f 字符串形式评估字典。

```python
$ python dicts.py
John Doe is a gardener
```

## Python 多行 f 字符串

我们可以使用多行字符串。

`multiline.py`

```python
#!/usr/bin/env python3

name = 'John Doe'
age = 32
occupation = 'gardener'

msg = (
    f'Name: {name}\n'
    f'Age: {age}\n'
    f'Occupation: {occupation}'
)

print(msg)
```

该示例显示了多行 f 字符串。 F 弦放在方括号之间； 每个字符串前面都带有`f`字符。

```python
$ python multiline.py
Name: John Doe
Age: 32
Occupation: gardener
```

## Python f 字符串调用函数

我们还可以在 f 字符串中调用函数。

`call_function.py`

```python
#!/usr/bin/env python3

def mymax(x, y):

    return x if x > y else y

a = 3
b = 4

print(f'Max of {a} and {b} is {mymax(a, b)}')
```

该示例在 f 字符串中调用自定义函数。

```py
$ python call_fun.py
Max of 3 and 4 is 4
```


## Python f 字符串对象

Python f 字符串也接受对象。 对象必须定义了`__str__()`或`__repr__()`魔术函数。

`objects.py`

```python
#!/usr/bin/env python3

class User:
    def __init__(self, name, occupation):
        self.name = name
        self.occupation = occupation

    def __repr__(self):
        return f"{self.name} is a {self.occupation}"

u = User('John Doe', 'gardener')

print(f'{u}')
```

该示例评估 f 字符串中的对象。

```python
$ python objects.py
John Doe is a gardener
```

## Python F 字符串转义字符

下面的示例显示如何对 f 字符串中的某些字符进行转义。

`escaping.py`

```python
#!/usr/bin/env python3

print(f'Python uses {{}} to evaludate variables in f-strings')
print(f'This was a \'great\' film')
```

为了避免花括号，我们将字符加倍。 单引号以反斜杠字符转义。

```python
$ python escaping.py
Python uses {} to evaludate variables in f-strings
This was a 'great' film
```

## Python f 字符串格式化日期时间

以下示例格式化日期时间。

`format_datetime.py`

```python
#!/usr/bin/env python3

import datetime

now = datetime.datetime.now()

print(f'{now:%Y-%m-%d %H:%M}')
```

该示例显示格式化的当前日期时间。 日期时间格式说明符位于<colon>：</colon>字符之后。

```python
$ python format_datetime.py
2019-05-11 22:39
```

## Python f 字符串格式化浮点数

浮点值的后缀为`f`。 我们还可以指定精度：小数位数。 精度是一个点字符后的值。

`format_floats.py`

```python
#!/usr/bin/env python3

val = 12.3

print(f'{val:.2f}')
print(f'{val:.5f}')
```

该示例打印格式化的浮点值。

```python
$ python format_floats.py
12.30
12.30000
```

输出显示具有两位和五个小数位的数字。

## Python f 字符串格式化宽度

宽度说明符设置值的宽度。 如果该值短于指定的宽度，则该值可以用空格或其他字符填充。

`format_width.py`

```python
#!/usr/bin/env python3

for x in range(1, 11):
    print(f'{x:02} {x*x:3} {x*x*x:4}')
```

该示例打印三列，每个列都有一个预定义的宽度。 第一列使用 0 填充较短的值。

```python
$ python format_width.py
01   1    1
02   4    8
03   9   27
04  16   64
05  25  125
06  36  216
07  49  343
08  64  512
09  81  729
10 100 1000
```

## Python f 字符串对齐字符串

默认情况下，字符串在左边对齐。 我们可以使用`&gt;`字符来对齐右侧的字符串。 `&gt;`字符在冒号后面。

`justify.py`

```python
#!/usr/bin/env python3

s1 = 'a'
s2 = 'ab'
s3 = 'abc'
s4 = 'abcd'

print(f'{s1:>10}')
print(f'{s2:>10}')
print(f'{s3:>10}')
print(f'{s4:>10}')
```

我们有四个不同长度的弦。 我们将输出的宽度设置为十个字符。 值在右对齐。

```python
$ python justify.py
         a
        ab
       abc
      abcd
```

## Python f 字符串数字符号

数字可以具有各种数字符号，例如十进制或十六进制。

`format_notations.py`

```python
#!/usr/bin/env python3

a = 300

# hexadecimal
print(f"{a:x}")

# octal
print(f"{a:o}")

# scientific
print(f"{a:e}")
```

该示例以三种不同的表示法打印值。

```python
$ python format_notations.py
12c
454
3.000000e+02
```
