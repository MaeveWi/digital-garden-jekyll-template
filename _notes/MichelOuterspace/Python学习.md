python官方包索引：[[pypi]]

安装或者升级包：
`pip install -U pytest`

- [[input, output]]
- [[Data Type]]
- [[global and local variables]]
- [[Collections集合 (list,dic,set,tuple)]]
- [[operators运算符]]
- [[Function函数]]
- [[Generators生成器函数 and yield]]
- [[lambda函数]]
- [[Closure闭包]]
- [[Decorators装饰器]]
- [[魔法 隐藏方法]]
- [[Class类]]
- [[OOP面向对象编程]]
- [[f字符串格式设置]]
````python
for _ in range(3):
	print(_)
````
`_`就是个占位符

pass 占位
break 直接跳出loop
continue loop中用来跳过当前循环剩下的代码

re库 按照正则匹配字符串
re.match 返回match对象，用group(), groups()获取具体
re.search
re.findall
re.finditer

json库
json.load() 字符串转换成json
json.dump() json转换成字符串

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

