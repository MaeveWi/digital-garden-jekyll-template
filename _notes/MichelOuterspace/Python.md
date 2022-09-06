-   print
    
    ```python
    x = 'pi is'
    y = 3.14
    print(x,y)
    ===
    pi is 3.14
    ```
    
    ```python
    x = 'pi is'
    y = 3.14
    print(x, y, **sep=' : '**)
    ===
    pi is : 3.14
    ```
    
    ```python
    print('Hello', **end='-'**)
    print('World', **end='.\\n'**)
    ===
    Hello-World.
    ```
    
-   input(read context from user)
    
    ```python
    #read string from user
    firstName = **input(**'Enter your first name: ')
    lastName = input('Enter your last name: ')
    print('Hello',firstName, lastName)
    ===
    Enter your first name: Brooks
    Enter your last name: Henry
    Hello Brooks Henry
    ```
    
    ```python
    n1 = input("enter a number:")
    print(**type(**firstName))  #查看变量类型
    n2 = **int(**input("enter another number")) 
    print(type(n2))
    ===
    enter a number:123
    <class 'str'>
    enter another number:2
    <class 'int'>
    ```
    
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
    
-   operators
    
    **You can use non-zero number instead of True and zero for False.**
    
    and
    
    or
    
    not：boolean的相反
    
    is：指向同一块内存，比如c=a，拥有相同值的两个int float str变量也是同一块内存
    
    is not
    
    in：`x in collection`is any collection of items like a list, tuple, set, string, etc.
    
    not in
    
    运算符：+，-，*，/ ，% 求余数，** 求幂，// 求商
    
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
    
-   collection
    
    -   List（list里的元素可以是不同数据类型）
        
        ```python
        a = [52, 85, 41, 'sum', 'str', 3 + 5j, 6.8]
        #access item or a range of items
        x=a[2]   #index从零开始，访问第三个元素
        print(x)
        y = a[1:4]  #1-4不包含4
        print(y)
        ===
        41
        [85, 41, 'sum']
        ```
        
        ```python
        #访问所有元素
        a = [52, 85, 41, 'sum', 'str', 3 + 5j, 6.8]
        for x in a:
        	print(x)
        #或者
        for i in range(len(a)):
        	print(a[i])
        #同时访问index和元素
        for i,x in enumerate(a):
        	print('element#',i,'is :',x)
        ```
        
        ```python
        #a list
        a = [21, 10, 21, 334, 21]
        length = len(a)
        #some updates on list
        a.append('Tata')
        a.remove(21)
        print(a)
        for i in a:
           if(i == 21):
              a.remove(i)
        print(a)
        ```
        
    -   Tuple
        
    -   Dictionary
        
        ```python
        #Create Dictionary
        	#1.
        myDictionary = **{**
        	"name": "Lini",
        	"year": 1989,
        	"expertise": "data analytics"**}**
        	#2.用dict()，不填就是空字典
        myDict = **dict(**[(1, 'foo'), (2, 'bar'), (3, 'moo')]**)**
        	#3.仅当键符合命名变量的规则时
        myDict = dict(a='foo', b='bar', c='moo')
        	#4.
        def someThing(x):
        	x = x**3
        	return x
        myDict = {x: someThing(x) for x in (5, 8, 9, 12)}
        ```
        
        ```python
        #全部打印成一串字符串
        print(myDictionary)
        
        #打印key-value pairs
        for **key, value** in myDictionary**.items(): 
        #dict.items() returns an iterator that provides access to both key and value.**
        	print(key, ': ', value)
        
        #或者
        for key in myDictionary:
        	print(key, '-', myDictionary[key])
        
        #打印keys。。。如果直接print(resp.json.keys()),打印出来是<class 'dict_keys'>类型
        for key in dictionary**.keys():**
        	print(key)
        
        #打印values
        for value in dictionary**.values():**
        	print(value)
        ```
        
        ```python
        #dictionary.get(key, value)
        #value - 可选参数，如果没有找到对应的key，就返回这个值，没有设置的话未找到就返回none
        myDict = {
        	'foo':12,
        	'bar':14
        }
        print(myDict.get('moo', 10))
        
        #嵌套字典的查询：
        myDict = 
        {
        	'foo': {
        		'a':12,
        		...
        	},...
        }
        print(myDict['foo']['a'])
        ===12
        
        #检查key是否存在，Check if Key is present in Python Dictionary
        isPresent = 'foo' **in** myDict
        print(isPresent)
        ===
        10
        True
        ```
        
        ```python
        **#Update, add, delete**
        myDict = {
        	'foo':12,
        	'bar':14
        }
        #update value for key 'foo'
        myDict['foo'] = 56
        
        #add key:value to dictionary
        myDict['moo'] = 85
        
        #del key:value pair from dictionary
        #1.pop()会返回删除的value
        poppedItem = myDictionary.pop('c')
        print(poppedItem)
        #2. 
        del myDict['foo']
        
        print(myDict)
        
        #delete all the items in the dictionary
        myDict.clear()
        ===
        {'bar': 14, 'moo': 85}
        ```
        
        ```python
        mylist = [12, 3, 4, 5, 12, 0, 23, 12]
        r_item =12
        mylist = list(**[filter](<https://www.notion.so/Python-1fa87a9d47c3468d9f16dc559ab0cc83>)**(r_item.__ne__, mylist))
        print(mylist)		
        ```
        
        ```python
        #Dictionary Keys/Values to List
        keysList = list(myDict.keys())
        keysList = [key for key in myDict]
        valuesList = list(myDict.values())
        valuesList = [key for key in myDict]
        ```
        
    -   Set (**Python Set can have only Unique Values**)
        
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
    
-   隐藏属性、隐藏方法
    
    相当于java的私有属性 私有方法？不让外部随意调用？
    
    `__getitem__()`、`__setitem__()`、`__delitem__()`
    
    这三个特殊成员，用于执行与中括号有关的动作。它们分别表示取值、赋值、删除数据。



test