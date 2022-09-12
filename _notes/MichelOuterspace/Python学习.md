python官方包索引：[[pypi]]

安装或者升级包：
`pip install -U pytest`

[[input, output]]

[[Data Type]]

[[Collections]]

[[operators运算符]]

[[Function函数]]

[[lambda函数]]

[[Decorators装饰器]]

[[魔法 隐藏方法]]

#### range()
```python
	range(stop)
    range(start, stop[, step])
    #All start, stop and step are integers.**step**可以是负数
    #没有start的时候默认从0开始，直到stop但**不包含stop**
    r = range(2, 100, 8)
    print(r[5]) # r[5] = 2 + [8 * 5]
    print(r[7]) # r[7] = 2 + [8 * 7]
    ===
    42
    58
    #可以用来初始化list，相比于list,tuple好处是，只需要三块内存空间
    x = list(range(4, 9))
    print(x)```

