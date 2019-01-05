1. ```r'str'```表示str中字符串不转义
2. ```'''str'''```表示str中字符串自动换行
3. True,False表示布尔值，用and,or,not运算
4. 空值用None表示
5. 习惯上用全大写表示常量，但未规定全大写变量无法更改
6. /表示除法，返回值为浮点数。 //表示地板除，返回值为整数
7. python默认用unicode码，ora()函数获取字符的整数表示， chr()把编码转换为对应字符 
8. 用b表示字节，例如 b'ABC' 区别于'ABC' 前者为字节，后者为字符串
9. decode()方法将字节以字符集编码，例如 b'ABC'.decode('utf-8')
10. len(str)方法能计算字符串长度,len(list)计算size
11. 文件头 第一句告诉linux系统这是个可执行文件，windows系统直接忽略，第二句定义文件编码
```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```
12. 字符串占位符： ```'Hello, %s' % 'World'```
    %d 整数， %s 字符串， %f 浮点数， %x 十六进制整数，%s将所有类型转换为string
    ```'zzz{0},zzz{1}'.format('a','b')```
13. 有序列表：
    list[] append('') insert(i,'') pop(i)
    tuple() t(1)表示1，t(1,)表示一个tuple里面有个元素1
    tuple 初始化后无法修改
14. 判断：
```python
    if a==0:
        print('')
    elif a==1:
        print('')
    else:
        print('')

    if x:
        print(True)
```
    只要x是非零数值，非空字符串，非空list等
15. 循环
    ```python
    for x in (range(101)):
        sum += sum + x
    print(sum)
    # 其中break continue用法与java类似
    ```

16. dict定义： 
    ```python
    d = {'Michael':95, 'Bob':75, 'Trancy':85}
    ```
    取：
    ```python
    d['Michael']
    ```
    判断：
    ```python
    'Bob' in d 
    ```
    取：
    ```python
    d.get('Bob')
    ```
    删除：
    ```python
    d.pop('Bob')
    ```
    增：
    ```python
    d['Jack'] = 90
    ```

17. help(函数名) 查看帮助信息 help(abs)
    int() float str() bool() 类型转化

18. 函数定义：
    ```python
    def my_abs(x):
        if x >= 0:
            return x
        else:
            return -x
    ```
   函数从test.py中导入：
   ```python
   from test import my_abs
   ```

19. 空函数：
    ```python
    def nop():
        pass
    ```

20. 参数检查：
    ```python
    def my_abs(x):
        if not isinstance(x,(int,float)):
            raise TypeError('bad operand type')
        if x>= 0:
            return x
        else:
            return -x
    ```
21. 多值返回，python中多值返回其实返回的是一个tuple，但是()省略了
    ```python
    import math
    def move(x, y, step, angle = 0):
        nx = x + step * math.cos(angle)
        ny = y - step * math.sin(angle)
        return nx,ny
    #angle = 0 意味着angle参数若未传则默认为0
    ```

22. 默认函数： 默认函数用法同21，但需要注意：默认参数必须指向不变对象！
    ```python
    def add_end(L = []):
        L.append('End')
        return L
    #在第二次调用add_end时L就有两个End了，python的默认参数若指向了一个对象
    #可以修改为：
    def add_end(L = None):
        if L is None:
            L = []
        L.append('End')
        return L
    ```

23. 可变参数,可传递0到多个参数，也能传递tuple或list：
    ```python
    def mutical(*number):
        sum = 0
        for n in number:
            sum += n
        return sum 

    a = [1,2,3]
    mutical(*a)
    mutical(1,2,3)
    mutical()
    ```

24. 关键字参数，加**，自动将参数转化为dict
    ```python
    def person(name, age, **keyword):
        print('name:', name, ' age:', age, ' other:', keyword)

    person('Bob', 23, city = 'BeiJing', gender = 'M')
    extra = {'job' = 'Engineer'}
    person('Bob', 23, **extra)
    ```

25. 命名关键字参数，参数用 * 作为分隔符，*后面的参数被视为命名关键字参数，以限制关键字参数的名字key
    ```python
    def f2(a,b,c=0,*,d,**kw):
        print(a,b,c,d,kw)

    def f1(a, b, c=0, *args, **kw):
        print(a,b,c,args,kw)
    #若已经有一个 可变 参数，可省略*，其后面的参数都视为命名关键字参数。
    def f3(a,b,c=0, *d, e):
        print(a,b,c,d,e)
    ```

26. python中有必选参数，默认参数，可变参数，关键字参数，命名关键字参数。
    其定义顺序必须为： 必选参数，默认参数，可变参数，命名关键字参数，关键字参数。

27. 递归函数
    ```python
    def fact(n):
        if n==1:
            return 1
        return n * fact(n-1)
    ```
    此函数会导致栈溢出，每次调用一次函数用一个栈保存。可以做尾递归优化（即return中只包含函数本身，编译器自动做尾递归优化，始终在一个栈中运行）。
    ```python
    def fact(n):
        return fact_iter(n,1)
    def fact_iter(num, product):
        if num == 1:
            return product
        return fact_iter(num-1, num*product)
    ```
    尾递归其实和for循环是等价的，但大多数编程语言都没有对尾递归进行优化，python解释器也未优化。。。

28. 切片（str，list,tuple）
    ```python
    L[x:y] #前闭后开，0可以省略
    L[:] #复制一个list
    L[:x：y] #前n个数，隔y取一个
    L[::x] #所有数，隔x取一个
    ```

    取L前三个元素： L[0:3] L[:3] 
    取最后一个元素： L[-1] L[-1:0]

29. 迭代，for in + 可迭代
    判断是否可迭代
    from collections import Iterable
    isinstance('abc',Iterable)

    循环下标
    for i,value in enumerate(['A','B','c']):
        print (i,value)
    循环dict(默认循环的key)
    for a,b in d.items()
    for a in d
    for a in d.values

30. 列表生成式(生成列表)
    [m+n for m in 'ABC' for n in 'XYZ']

31. 生成器，列表生成式生成的列表若很大则有内存不足的问题，可以考虑用生成器generator
    将列表生成式的[]换为()即为生成器，函数中有yield也是生成器
    g = (x * x for x in range(10))
    然后取值 next(g)
    斐波拉契函数：
    ```python
    def feb(m):
    n, a, b = 0, 0, 1
    while n < m:
        yield b
        a, b = b, a + b #此处相当于 t=(b, a+b) a=t[0] b=t[1]
        n += 1
    return 'Done'


    g = feb(6)
    while True:
       try:
           print(next(g))
       except StopIteration as e:
           print('return value', e.value)
           break
    ```

    杨辉三角：
    ```python
    def triangles():
    a = 0
    s = [1]
    while a < 10:
        yield s
        temp = s[:]
        s = [1] + [temp[i] + temp[i + 1] for i in range(len(temp) - 1)] + [1]
        # s.insert(0, 1)
        # s.append(1)
        a += 1

    g = triangles()
    for x in g:
        print(next(g))
    ```

32. 迭代。可迭代对象Iterable(可用于for循环的),迭代器Iterator(可用于next的)
    isinstance((x for x in range(10)), Iterator) True  生成器generator
    isinstance([x for x in range(10]), Iterator) False 列表生成式
    可用iter()函数获得一个Iterator对象：
        iter([1,2,3,4]) #将一个列表转换成生成器


