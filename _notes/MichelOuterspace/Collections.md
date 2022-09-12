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
        