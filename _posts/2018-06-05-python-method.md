---
layout: post
title: "python 常用内置方法"
date: 2018-06-05
categories: technology
image: city.jpg
published: true
---

```python
# python 常用模块
# 返回数字的绝对值
abs(-112451)
```




    112451




```python
# 返回值和余数
divmod(7,2)
divmod(8,2)
```




    (4, 0)




```python
# @staticmethod 声明静态方法
class c(object):
    @staticmethod
    def df():
        print('runood')

c.df() # 静态方法无需实例化调用
```

    runood
    


```python
# all(iterable) 判断参数中所有元素是否都为true
all([0,1,2,3,4])
```




    False




```python
all(['a','b','','c'])
```




    False




```python
# enumerate(iterable) 将一个参数组合为索引数列
seasons = ['Spring','Summer','fall','winter']
[i for i in enumerate(seasons)]
list(enumerate(seasons,start=10))
```




    [(10, 'Spring'), (11, 'Summer'), (12, 'fall'), (13, 'winter')]




```python
i = 0
seq = ['one','two','three']
for i,elememnt in enumerate(seq):
    print(i,seq[i])
```

    0 one
    1 two
    2 three
    


```python
ord('a')
chr(1)
```




    '\x01'




```python
# class int(x, base=10) int() 函数用于将一个字符串或数字转换为整型。 x -- 字符串或数字。
# base -- 进制数，默认十进制。
int("12")
```




    12




```python
# any() 与all 相对，判断iterable是否全部为False,如果有一个为True，则返回 True
any(['a',0,False,''])
```




    True




```python
# eval() 函数用来执行一个字符串表达式，并返回表达式的值。
eval('3*7')
```




    21




```python
#　isinstance type isinstance考虑继承
# isinstance(object,classinfo)

isinstance(123,(int,str,list))
```




    True




```python
pow(100,-2)
```




    0.0001




```python
sum([1,2,3,4,5,],10)
```




    25




```python
#execfile(filename[,globals[,locals]]) # 执行一个文件
```


```python
class A(object):
    pass
class B(A):
    pass
issubclass(B,object) # issubclass(class,classinfo)判断参数是否是classinfo的子类
```




    True




```python
# super()可以调用父类的方法，super().xxx  xxx--方法名称
class FooParent(object):
    def __init__(self):
        self.parent = 'I \'m the parent a'
        print('Parent')
    def bar(self,message):
        print("%s from Parent123" % message)
class FooChild(FooParent):
    def __init__(self):
        super(FooChild,self).__init__()
        print('child')
    def bar(self, message):
        super(FooChild,self).bar(message)
        print('Child bar fuction')
        print(self.parent)
fooChild = FooChild()
fooChild.bar("helloWorld!")
```

    Parent
    child
    helloWorld! from Parent123
    Child bar fuction
    I 'm the parent a
    


```python
#　@property
class C(object):
    def __init__(self):
        self._x = None
    def getx(self):
        print("i am getx")
        return self._x
    def setx(self,value):
        self._x = 'value123'
    def delx(self):
        del self._x
    x = property(getx,setx,delx,"i 'm groot ")
c = C()
c.x # 触发 getx
c.x = 'value123' #触发 setx
del c.x # 触发 delx

```

    i am getx
    


```python
class Parrot(object):
    def __init__(self):
        self._voltage = 10000
    @property
    def voltage(self):
        """get the current voltage"""
        return self._voltage
    @voltage.setter
    def voltage(self,value):
        self._voltage = value
        print(self._voltage)
    @voltage.deleter
    def voltage(self):
        del self._voltage
        print("delete success!")
p = Parrot()
print(p.voltage)
p.voltage = "sad"
del p.voltage
# 总结：@property可以把方法设置成只读属性，相当于get，该属性拥有set，del等方法，也可以通过x.setter等进行设置

```

    10000
    sad
    delete success!
    


```python
float(1)
```




    1.0




```python
# callable() 检查一个对象是否可调用
callable(0) # false
callable("runoob") # false
def add(a):
    return a*2
callable(add) # true
class A():
    def __call__(self):
        return 0
callable(A()) # True
```




    True




```python
a = "{},{}".format("hello","world")
print(a)
b = {"name":"me","age":17}
print("{name},{age}".format(**b))
mylist = ["me","you"]
print("{0[0]},{0[1]}".format(mylist))
c = "{:2f}".format(3.1415)
print(c)
```

    hello,world
    me,17
    me,you
    3.141500
    


```python
# locals() 返回全部局部变量
def runoob(arg):
    z = 1
    b = "stir"
    lis = ["12","21","4"]
    di = {"a":"b","c":1}
    print(locals())
runoob(5)
```

    {'di': {'a': 'b', 'c': 1}, 'lis': ['12', '21', '4'], 'b': 'stir', 'z': 1, 'arg': 5}
    


```python
# reduce(function,iterable) 函数会对参数序列中元素进行累积。 
from functools import reduce
reduce(lambda x,y: x*y,[1,2,3,4,5,6])
```




    720




```python
# @classmethod 修饰对应的函数不需要实例化，不需要self参数。
# 但第一个参数需要是表示自身类的 cls 参数，可以来调用类的属性，类的方法，实例化对象等。
class A(object):
    bar = 1
    def func1(self):
        print('foo')
    @classmethod
    def func2(cls):
        print('func2')
        print(cls.bar)
        cls().func1()  
A.func2()    # 不需要实例化
```

    func2
    1
    foo
    


```python
# getattr(object,name[,default]) 
class A(object):
    bar = 1
    def __init__(self):
        pass
    @classmethod
    def fun2(cls):
        cls().func1()
    @property
    def fun3(self):
        return self._fun3
a = A()
getattr(a,"bar")
```




    1




```python
#map(function,iterable)　每个元素分别作用于函数，返回一个ｉｔｅｒａｂｌｅ对象
a = map(lambda x:x**2 ,[1,2,3,4,5])
[y for y in a]
b = map(lambda x,y,z:x%2+y**2+z-1,[1,2,4],[3,4,5],[5,6,7,8,9]) # 每个iterable按顺序传入给function
[y for y in b]
```




    [14, 21, 31]




```python
#　repr() 函数将对象转化为供解释器读取的形式。
print(repr('bbaasd'))
print(repr({"a":12,"b":"me"}))
```

    'bbaasd'
    {'a': 12, 'b': 'me'}
    


```python
# xrange(start=0，stop[,step])用法和range相同，但range返回列表，而xrange返回生成器
[i for i in range(8)]# 在python3，xrange=range
```




    [0, 1, 2, 3, 4, 5, 6, 7]




```python
max([1,2,3,4,5])#　５
max({2:"a",3:"b"}) # 3
max((1,2,3,4,5),(4,5,56,6,7))#(4, 5, 56, 6, 7)
```




    (4, 5, 56, 6, 7)




```python
from collections import deque
queue = deque(["eric",'join','michael'])
queue.append("terry")
queue.append("craham")
queue.popleft()

```




    'eric'




```python
# zip(iterable,...) 用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的列表。

# 如果各个迭代器的元素个数不一致，则返回列表长度与最短的对象相同，利用 * 号操作符，可以将元组解压为列表。

ziped = [i for i in zip([1,2,3],[3,4,5])]# 
print(ziped)
[i for i in zip(*ziped)]# 解压、降维
```

    [(1, 3), (2, 4), (3, 5)]
    




    [(1, 2, 3), (3, 4, 5)]




```python
#　round(x [,n]) 返回float的小数点第n位
round(82.23145,2)
```




    82.23




```python
# 动态导入 __import__('a') 动态导入 a.py 模块，
```


```python
# hash()
hash('test')
sorted({'1':1})
hash(str([1,2,3]))
```




    -1810799843154591726




```python
#set() 函数创建一个无序不重复元素集，可进行关系测试，删除重复数据，还可以计算交集、差集、并集等。

x = set('reebok')
y = set("google")
print(x)
print(y)
print(x,y)
print(x & y) # 交集
print(x | y)#  并集
print(x - y)# 差集
```

    {'e', 'k', 'b', 'r', 'o'}
    {'l', 'e', 'g', 'o'}
    {'e', 'k', 'b', 'r', 'o'} {'l', 'e', 'g', 'o'}
    {'e', 'o'}
    {'e', 'l', 'g', 'o', 'k', 'b', 'r'}
    {'b', 'r', 'k'}
    


```python
help([].append)
```

    Help on built-in function append:
    
    append(...) method of builtins.list instance
        L.append(object) -> None -- append object to end
    
    


```python
next(iter([1,2,3]))
```




    1




```python
student = [("john","A",15),("man","B",16),("girl","C",17)]
sorted(student,key=lambda s:s[2],reverse=False) # 按list[2]排列
```




    [('john', 'A', 15), ('man', 'B', 16), ('girl', 'C', 17)]


