===python的print  用 ', '连接，不像java用 '+' 连接===

-  print
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
    firstName = input('Enter your first name: ')
    lastName = input('Enter your last name: ')
    print('Hello',firstName, lastName)
    ===
    Enter your first name: Brooks
    Enter your last name: Henry
    Hello Brooks Henry
    ```
    
    ```python
    n1 = input("enter a number:")
    print(type(firstName))  #查看变量类型
    n2 = int(input("enter another number")) 
    print(type(n2))
    ===
    enter a number:123
    <class 'str'>
    enter another number:2
    <class 'int'>
    ```
    