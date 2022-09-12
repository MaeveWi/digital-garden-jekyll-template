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
    
    