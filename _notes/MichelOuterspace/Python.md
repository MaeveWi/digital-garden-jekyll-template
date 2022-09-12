python官方包索引：[[pypi]]

安装或者升级包：
>pip install -U pytest

[[input, output]]

[[DataType]]

[[Collections]]

[[operators运算符]]

[[Decorators装饰器]]

[[Function函数]]

[[lambda函数]]

[[内置方法]]

[[隐藏属性、隐藏方法]]
-   range()
    
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
    print(x)
    ```
    

-   filter()
    
    **syntax:**
    
    ```python
    filter(function, sequence)
    Parameters:
    	function: OPTIONAL function that tests if each element of a sequence true or not. If function is None, return the items that are true.
    	sequence: sequence which needs to be filtered, it can be sets, lists, tuples, or containers of any iterators.
    Returns: returns an iterator that is already filtered.
    ```
    
    for example：
    
    It is normally used with **[Lambda functions](https://www.geeksforgeeks.org/python-lambda-anonymous-functions-filter-map-reduce/)** to separate list, tuple, or sets.
    
    ```python
    seq =[0, 1, 2, 3, 5, 8, 13]
    # result contains odd numbers of the list
    result = filter(lambda x:x %2!=0, seq)
    ```
    
    [](https://www.geeksforgeeks.org/filter-in-python/)[https://www.geeksforgeeks.org/filter-in-python/](https://www.geeksforgeeks.org/filter-in-python/)
    
