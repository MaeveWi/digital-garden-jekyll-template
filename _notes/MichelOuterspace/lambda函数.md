
```python
str1 = 'GeeksforGeeks'  

# lambda returns a function object
# function倒序并且大写String  
rev_upper = lambda string: string.upper()[::-1]  
print(rev_upper(str1))
```

####  Lambda Function with if-else
```python
Max = lambda a, b: a if (a > b) else b   
print(Max(1, 2))
```


### filter() 通常和lambda函数一起用来拆分list,sets等
##### syntax:
	filter(function, sequence)
Parameters:
- function: OPTIONAL function that tests if each element of a sequence true or not. If function is None, return the items that are true.
- sequence: sequence which needs to be filtered, it can be sets, lists, tuples, or containers of any iterators.
  Returns: returns an iterator that is already filtered.
```python
seq =[0, 1, 2, 3, 5, 8, 13]
# result contains odd numbers of the list
result = filter(lambda x:x %2!=0, seq)
 ```
或者定义一个function之后再筛选
```python
# function that filters vowels  
def fun(variable):  
  letters = ['a', 'e', 'i', 'o', 'u']  
  if (variable in letters):  
    return True  
  else:  
    return False  
    
# sequence  
sequence = ['g', 'e', 'e', 'j', 'k', 's', 'p', 'r']  

# using filter function  
filtered = filter(fun, sequence)
```