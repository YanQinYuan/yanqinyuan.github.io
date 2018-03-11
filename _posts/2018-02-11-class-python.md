---
layout: post
title: "python class 详解"
date: 2018-02-11
categories: tech
---

## 限制访问属性

实例的变量名如果以__开头，就变成了一个私有变量（private），只有内部可以访问，外部不能访问
```python
class MyObject(object):
  def __init__(self, name, score):
      self.__name = name
      self.__name = score
```
## 操作对象信息
几个方法：dir(), hasattr(),setattr(),getattr(),isinstance()
```python
dir("abc") # 列出str类所有的方法属性
hasattr(MyObjcet,name) # 返回True or Not
getattr(MyObject,name,400)# 如果没有则返回 default（400）
setattr(MyObject,name,"jack")
isinstance(my, MyObject) # 判断class的类型
```
## 给类绑定一个方法
```python
Student.set_score = set_score
```

## __slots__ 限制绑定属性
```python
class Teacher(objcet):
    __slots__ = ('name','age')

s.name = "jack"
s.age = 29
s.sex = "man" # attribute error cause sex is not in __slots__
```
## 使用 @property 把方法变成属性

```python
class Student(object):
    @property
    def width(self):
        return self._width
    @width.setter
    def width(self,value):
        if not isinstance(value,int):
          raise ValueError("width must integer")
        self.width = value
```

## 多重继承
```python
class MytcpServer(TCPServer,CoroutineMixIn):
    pass
# MytcpServer 同时拥有两个类的方法和属性
```
