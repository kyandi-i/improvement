# python学习

##  1.python基础

---

```python
s1 = 72
s2 = 85
r = (s2 - s1) / s1 * 100
print('%.1f%%'%r)
print(f'{r:.1f}%')
```

## 2.使用list和tuple

---

```python
classmates = ['Michael', 'Bob', 'Tracy']
print(classmates)
print(len(classmates))

print(classmates[0])
print(classmates[-1])

classmates.append('Adam')
print(classmates)

classmates.insert(1, 'Jack')
print(classmates)

classmates.pop()
classmates[1] = 'Sarah'
print(classmates)

tuples = ('Michael', 'Bob', 'Tracy')
print(tuples)
t = (1,)
print(t)
t = ('a', 'b', ['A', 'B'])
t[2][0] = 'X'
t[2][1] = 'Y'
('a', 'b', ['X', 'Y'])
```

## 3.条件判断

---

```python
# if <条件判断1>:
#     <执行1>
# elif <条件判断2>:
#     <执行2>
# elif <条件判断3>:
#     <执行3>
# else:
#     <执行4>
```

```python
# 模式匹配
# age = 15

# match age:
#     case x if x < 10:
#         print(f'< 10 years old: {x}')
#     case 10:
#         print('10 years old.')
#     case 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18:
#         print('11~18 years old.')
#     case 19:
#         print('19 years old.')
#     case _:
#         print('not sure.')
# match...case 结构用于模式匹配，可以替代复杂的if...elif...else结构。
```

## 4.循环

---

```python
# 循环
# names = ['Michael', 'Bob', 'Tracy']
# for name in names:
#     print(name)
# sum = 0
# for x in range(101):
#     sum = sum + x   
# print(sum)
# while True:
#     n = int(input('请输入一个整数: '))
#     if n < 0:
#         break
#     print(f'您输入的整数是: {n}')
# print('END')
# break跳出循环，continue跳过当前这次循环，直接进入下一次循环。
```

## 5.字典和集合

---

```python
# d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
# print(d['Michael'])
# d['Adam'] = 67
# print(d)
# print(d.get('Thomas', -1))
# print('Bob' in d)
# d.pop('Bob')
# print(d)
# 查找和插入的速度极快，不会随着key的增加而变慢；
# 需要占用大量的内存，内存浪费多。
```

```python
# s = set([1, 2, 3])
# print(s)
# s.add(4)
# print(s)
# s.remove(4)
# print(s)
```

## 6.函数

---

```python
#函数
# n1 = 255
# n2 = 1000
# print(hex(n1))
# print(hex(n2))
# def my_abs(x):
#     if x >= 0:
#         return x
#     else:
#         return -x
# print(my_abs(-99))
# def nop():
#     pass
# pass语句什么都不做，可以用来作为占位符。
```

```python
# 可变参数
# def calc(*numbers):
#     sum = 0
#     for n in numbers:
#         sum = sum + n * n
#     return sum
# print(calc(1, 2, 3))
# nums = [1, 2, 3]
# print(calc(*nums))
# def person(name, age, **kw):
#     print('name:', name, 'age:', age, 'other:', kw)
# *args是可变参数，args接收的是一个tuple；
# **kw是关键字参数，kw接收的是一个dict。
```

```python
# 递归函数
# def fact(n):
#     if n == 1:
#         return 1
#     return n * fact(n-1)
# def move(n, a, b, c):
#     if n == 1:
#         print(a, '-->', c)
#     else:
#         move(n-1, a, c, b)
#         print(a, '-->', c)
#         move(n-1, b, a, c)   

# 期待输出:
# A --> C
# A --> B
# C --> B
# A --> C
# B --> A
# B --> C
# A --> C
# move(3, 'A', 'B', 'C')
# 3 A B C
# N = 3

# MOVE(2,A,C,B)
# 	MOVE(1,A,B,C)
# 		A--C
# 	A -- B
# 	MOVE(1,C,A,B)
# 		C--B

# A--C

# MOVE(2,B,A,C)
# 	MOVE(1,B,C,A)
# 		B--A
# 	B--C
# 	MOVE(1,A,B,C)
# 		A--C
# 汉诺塔问题
```

## 7.高级特性

---

```python
# 切片
# L = list(range(100 ))
# print(L[:10])
# print(L[-10:])
# print(L[10:20])
# print(L[:10:2])
# print(L[::5])

# def trim(s):
#     if s == '':
#         return s
#     if s[0] == ' ':
#         return trim(s[1:])
#     if s[-1] == ' ':
#         return trim(s[:-1])
#     return s
```

```python
# 迭代
# from collections.abc import Iterable
# print(isinstance('abc', Iterable))
# def findMinAndMax(L):
#     if len(L) == 0:
#         return (None, None)
#     min = max = L[0]
#     for k in L:
#         if k < min:
#             min = k
#         if k > max:
#             max = k
#     return (min, max)

# 测试
# if findMinAndMax([]) != (None, None):
#     print('测试失败!')
# elif findMinAndMax([7]) != (7, 7):
#     print('测试失败!')
# elif findMinAndMax([7, 1]) != (1, 7):
#     print('测试失败!')
# elif findMinAndMax([7, 1, 3, 9, 5]) != (1, 9):
#     print('测试失败!')
# else:
#     print('测试成功!')

```

```python
# 列表生成式
# L = []
# for x in range(1, 11):
#     L.append(x * x)
# print(L)
# L = [x * x for x in range(1, 11)]
# print(L)
# L = [x * x for x in range(1, 11) if x % 2 == 0]
# print(L)
# import os
# L = [d for d in os.listdir('.')]
# print(L)
# d = {'x': 'A', 'y': 'B', 'z': 'C' }
# for k, v in d.items():
#     print(k, '=', v)

# L1 = ['Hello', 'World', 18, 'Apple', None]
# L2 = [s.lower() for s in L1 if isinstance(s,str)]
# print(L2)
# if L2 == ['hello', 'world', 'apple']:
#     print('测试通过!')
# else:
#     print('测试失败!')

```

````python
#生成器
# L = [x * x for x in range(10)]
# g = (x * x for x in range(10))
# for n in g:
#     print(n)
#定义generator的另一种方法。如果一个函数定义中包含yield关键字，那么这个函数就不再是一个普通函数，而是一个generator函数，调用一个generator函数将返回一个generator：
#generator每次调用next()的时候执行，遇到yield语句返回，再次执行时从上次返回的yield语句处继续执行。
# def triangles():
#     L = [1]
#     while True:
#         yield L
#         L = [1] + [L[i] + L[i + 1] for i in range(len(L) - 1)] + [1]
# n = 0
# for t in triangles():
#     print(t)
#     n = n + 1
#     if n == 10:
#         break
# 杨辉三角
````

## 8.函数式编程

---

### 8.1高阶函数

#### 8.1.1. map/reduce

```python
# 变量可以指向函数
# f = abs
# print(f(-10))
# 一个函数就可以接收另一个函数作为参数，这种函数就称之为高阶函数。
# def add(x, y, f):
#     return f(x) + f(y)
# 内置map函数
# def f(x):
#     return x * x
# r = map(f, [1, 2, 3, 4, 5])
# p = [2,4,6,8,10]
# h = map(f, p)
# print(list(r))
# print(list(h))
# 内置reduce函数
# from functools import reduce
# def add(x, y):
#     return x + y
# sum = reduce(add, [1, 3, 5, 7, 9])
# print(sum)
# 把str转换成int
# def char2num(s):
#     digits = {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4, '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}
#     return digits[s]

# def str2int(s):
#     return reduce(lambda x, y: x * 10 + y, map(char2num, s))
# print(str2int('12345'))

# def normalize(name):
#     return name[0].upper() + name[1:].lower()
# L1 = ['adam', 'LISA', 'barT']
# L2 = list(map(normalize, L1))
# print(L2)

# from functools import reduce

# def prod(L):
#     def fn(x, y):
#         return x * y
#     return reduce(fn, L)
# print('3 * 5 * 7 * 9 =', prod([3, 5, 7, 9]))
# if prod([3, 5, 7, 9]) == 945:
#     print('测试成功!')
# else:
#     print('测试失败!')

# DIGITS = {'0': 0, '1': 1, '2': 2, '3': 3, '4': 4,
#           '5': 5, '6': 6, '7': 7, '8': 8, '9': 9}
# def str2float(s):
#     if '.' in s:
#         int_part,dec_part = s.split('.')
#     else:
#         int_part = s
#         dec_part = ''
#     def fn(x,y):
#         return x * 10 + y
#     def char2num(s):
#         return DIGITS[s]
#     int_value = reduce(fn,map(char2num,int_part)) if int_part else 0
#     dec_value = reduce(fn, map(char2num, dec_part)) / (10 ** len(dec_part)) if dec_part else 0
#     return int_value + dec_value
```



#### 8.1.2. filter

```python
# filter
#Python内建的filter()函数用于过滤序列。和map()类似，filter()也接收一个函数和一个序列。和map()不同的是，filter()把传入的函数依次作用于每个元素，然后根据返回值是True还是False决定保留还是丢弃该元素。
# def is_odd(n):
#     return n % 2 == 1

# list(filter(is_odd, [1, 2, 4, 5, 6, 9, 10, 15]))
# 结果: [1, 5, 9, 15]
# 求素数
# def _odd_iter():
#     n = 1
#     while True:
#         n = n + 2
#         yield n

# def _not_divisible(n):
#     lambda x: x % n > 0

# def primes():
#     yield 2
#     it = _odd_iter()
#     while True:
#         n = next(it)
#         yield n
#         it = filter(_not_divisible(n), it)
# for n in primes():
#     if n < 100:
#         print(n)
#     else:
#         break

# 回数是指从左向右读和从右向左读都是一样的数，例如12321，909。
# def is_palindrome(n):
#     s = str(n)
#     return s == s[::-1]
# output = filter(is_palindrome, range(1, 1000))
# print('1~1000:', list(output))
# if list(filter(is_palindrome, range(1, 200))) == [1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 22, 33, 44, 55, 66, 77, 88, 99, 101, 111, 121, 131, 141, 151, 161, 171, 181, 191]:
#     print('测试成功!')
# else:
#     print('测试失败!')
```

#### 8.1.3. sorted

```python
# 排序
# sorted()函数也是一个高阶函数，它还可以接收一个key函数来实现自定义的排序。
# L = [('Bob', 75), ('Adam', 92), ('Bart', 66), ('Lisa', 88)]
# def by_name(t):
#     return t[0]
# def by_score(t):
#     return t[1]
# L2 = sorted(L, key=by_score)
# print(L2)
```

### 8.2 返回函数

```python
# 闭包
# def createCounter():
#     n = 0
#     def counter():
#         nonlocal n
#         n += 1
#         return n
#     return counter
# # 测试:
# counterA = createCounter()
# print(counterA(), counterA(), counterA(), counterA(), counterA()) # 1 2 3 4 5
# counterB = createCounter()
# if [counterB(), counterB(), counterB(), counterB()] == [1, 2, 3, 4]:
#     print('测试通过!')
# else:
#     print('测试失败!')
```

### 8.3 匿名函数

```python
# 匿名函数
# is_odd = lambda n: n % 2 == 1
# L = list(filter(is_odd, range(1, 20)))
# print(L)
# def is_odd(n):
#     return n % 2 == 1
# L = list(filter(is_odd, range(1, 20)))
# print(L)
```

### 8.4装饰器

```python
# 装饰器
# 在代码运行期间动态增加功能的方式，称之为“装饰器”（Decorator）。
# import functools, time


# def metric(fn):
#     @functools.wraps(fn)
#     def wrapper(*args, **kw):
#         print(f'{fn.__name__} executed in {10.24} ms')
#         return fn(*args, **kw)
#     return wrapper

# @metric
# def fast(x, y):
#     time.sleep(0.0012)
#     return x + y;

# @metric
# def slow(x, y, z):
#     time.sleep(0.1234)
#     return x * y * z;

# f = fast(11, 22)
# s = slow(11, 22, 33)
# if f != 33:
#     print('测试失败!')
# elif s != 7986:
#     print('测试失败!')
```

### 8.4 偏函数

```python
# 偏函数
# import functools
# int2 = functools.partial(int, base=2)
# print(int2('1000000'))
```

## 9.模块

---

`import`

## 10.面向对象编程

---

```
# 类和实例
# class Student(object):
#     def __init__(self,name,score):
#         self.name = name
#         self.score = score
# bart = Student('Bart Simpson',59)
# print(bart.name)
#数据封装
# class Student(object):
#     def __init__(self, name, score):
#         self.name = name
#         self.score = score

#     def print_score(self):
#         print('%s: %s' % (self.name, self.score))
# print(bart.print_score())

# 访问限制
# class Student(object):
#     def __init__(self, name, score):
#         self.__name = name
#         self.__score = score
#    def get_name(self):
#        return self.__name
#    def get_score(self):
#        return self.__score
#    def set_score(self, score):
#        if 0 <= score <= 100:
#            self.__score = score
#        else:
#            raise ValueError('bad score')

# 继承和多态
# class character(object):
#     def fun(self):
#         print('hello my friend')

# class swordman(character):
#     pass

# swordman = swordman()
# print(swordman.fun())

# 获取对象信息
# type()
# isinstance()
# dir()
# class MyObject(object):
#      def __init__(self):
#          self.x = 9
#      def power(self):
#          return self.x * self.x

# obj = MyObject()

# print(hasattr(obj, 'x'))

# 设置一个属性'y'
# setattr(obj, 'y', 19) 
# 获取属性'y'
# getattr(obj, 'y') 
# obj.y 

# 实例属性和类属性
# class Student(object):
#     name = 'Student' # 类属性

# 面向对象高级编程

# _slots_
# class students(object):
#     限制实例的属性
#     _slots_ = ('name', 'age')

# @property
# class Screen(object):
#     @property
#     def width(self):
#         return self._width
#     @width.setter
#     def width(self, value):
#         self._width = value

#     @property
#     def height(self):
#         return self._height

#     @height.setter
#     def height(self, value):
#         self._height = value

#     @property
#     def resolution(self):
#         return self._width * self._height

# 测试:
# s = Screen()
# s.width = 1024
# s.height = 768
# print('resolution =', s.resolution)
# if s.resolution == 786432:
#     print('测试通过!')
# else:
#     print('测试失败!')
# 多重继承
# class Animal(object):
#     def run(self):
#         print('Animal is running...')
# class Dog(Animal):
#     def run(self):
#         print('Dog is running...')
# class Cat(Animal):
#     def run(self):
#         print('Cat is running...')
# class Tortoise(Animal):
#     def run(self):
#         print('Tortoise is running slowly...')
# class Timer(object):
#     def run(self):
#         print('Start...')
# class TimerDog(Dog, Timer):
#     pass
# dog = TimerDog()
# dog.run()
# print(isinstance(dog, Timer))
# print(isinstance(dog, Dog))

# 定制类
# class student(object):
#     def __init__(self,name):
#         self.name = name
#     def __str__(self):
#         return f'student object (name: {self.name})'

# print(student('Michael'))

# class Fib(object):
#     def __init__(self):   
#         self.a, self.b = 0, 1
#     def __iter__(self):
#         return self
#     def __next__(self):
#         self.a, self.b = self.b, self.a + self.b
#         if self.a > 100000:
#             raise StopIteration();
#         return self.a
# for n in Fib():
#     print(n)
#判断一个对象是否能被调用 callable()
# print(callable(Fib()))

# 使用枚举类
# from enum import Enum
# Month = Enum('Month', ('Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'))
# for name, member in Month.__members__.items():
#     print(name, '=>', member, ',', member.value)
# from enum import Enum, unique

# @unique
# class Weekday(Enum):
#     Sun = 0 # Sun的value被设定为0
#     Mon = 1
#     Tue = 2
#     Wed = 3
#     Thu = 4
#     Fri = 5
#     Sat = 6
# day1 = Weekday.Mon
# print(day1)

# 使用元类
#type()
# metaclass
```

## 11.测试

---

```
# 错误、调试与测试
# 错误处理
# try:
# try:
#     print('try...')
#     r = 10 / 2
#     print('result:', r)
# except ZeroDivisionError as e:
#     print('except:', e)
# finally:
#     print('finally...')
# print('END')
# Python的错误其实也是class，所有的错误类型都继承自BaseException。
# try...except...finally...结构用于捕获错误并处理。
# import logging

# def foo(s):
#     return 10 / int(s)

# def bar(s):
#     return foo(s) * 2

# def main():
#     try:
#         bar('0')
#     except Exception as e:
#         logging.exception(e)

# main()
# print('END')
# logging模块可以输出错误信息到日志，方便事后排查。
# 调试
# assert断言
# def foo(s):
#     n = int(s)
#     assert n != 0, 'n is zero!'
#     return 10 / n
# def main():
#     foo('0')
# logging模块
# import logging
# logging.basicConfig(level=logging.INFO)
# s = '0'
# n = int(s)
# logging.info('n = %d' % n)
# print(10 / n)
#pdb调试器
#   python -m pdb err.py
# (Pdb) n
# (Pdb) p s
# '0'
# (Pdb) p n
# 0
# (Pdb) q
# err.py

# 单元测试
```

## 12.IO编程

---

```
# 操作文件和目录
# import os
# print(os.name)

# import os
# 1. 获取存在的环境变量（如PATH）
# print(os.environ.get('PATH'))  
# 输出系统PATH的所有路径
# 2. 获取不存在的环境变量，返回默认值（推荐）
# print(os.environ.get('XXX', 'default_value'))  
# 输出'default_value'，避免报错

# 获取当前目录的绝对路径

# import os
# print(os.path.abspath('.'))
# print(os.path.abspath('./testdir'))

# 拼接路径
# import os
# print(os.path.join('/home/user', 'testdir'))

# 拆分路径
# import os
# print(os.path.split('/home/user/testdir/file.txt'))

# 获取文件扩展名
# import os
# print(os.path.splitext('/home/user/testdir/file.txt'))

# 列出目录下的所有文件和子目录
# import os
# print(os.listdir('.'))

# 创建目录
# import os
# 1. 拼接要创建的目录的完整路径（当前目录下创建testdir）
# new_dir = os.path.join(os.path.abspath('.'), 'testdir')
# 2. 创建目录
# os.mkdir(new_dir)

# 删除目录
# import os
# os.rmdir(os.path.join(os.path.abspath('.'), 'testdir'))

# 重命名文件或目录
# import os
# os.rename('oldname.txt', 'newname.txt')

# 删除文件
# import os
# os.remove('unwanted_file.txt')

# 复制文件
# import shutil
# 将源文件src复制到目标文件dst，src/dst为文件路径（相对/绝对）
# shutil.copyfile('source.txt', 'target.txt')

# import os
# 一行代码过滤：当前目录下的所有.py文件
# py_file_list = [x for x in os.listdir('.') if os.path.isfile(x) and os.path.splitext(x)[1] == '.py']
# print(py_file_list)  # 输出示例：['main.py', 'test.py', 'utils.py']

# import os
# import shutil


# 1. 拼接test_files目录的绝对路径
# test_dir = os.path.join(os.path.abspath('.'), 'test_files')
# 2. 创建目录（递归创建，避免上级目录不存在）
# os.makedirs(test_dir, exist_ok=True)  # exist_ok=True：目录已存在时不报错

# 3. 在test_dir下创建3个文件
# files = ['1.txt', '2.py', '3.md']
# for file in files:
#     file_path = os.path.join(test_dir, file)
    # 写入空内容，创建文件
    # with open(file_path, 'w', encoding='utf-8') as f:
    #     f.write(f'这是{file}的内容')

# 4. 列出test_dir下的所有.py文件
# py_files = [x for x in os.listdir(test_dir) if os.path.isfile(os.path.join(test_dir, x)) and os.path.splitext(x)[1] == '.py']
# print(f'test_files下的.py文件：{py_files}')

# 5. 复制2.py为2_copy.py
# src_file = os.path.join(test_dir, '2.py')
# dst_file = os.path.join(test_dir, '2_copy.py')
# shutil.copyfile(src_file, dst_file)
# print('文件复制完成')

# 6. 递归删除test_files目录及其所有内容
# shutil.rmtree(test_dir)
# print('目录删除完成')

# 序列化
# import json  
# d = dict(name='Bob', age=20, score=88)
# 序列化：Python dict → JSON字符串
# json_str = json.dumps(d) //json.dump(obj, file, ensure_ascii=True, encoding='utf-8')
# print(type(json_str))  
# print(json_str)        

# import json
# 包含中文的Python对象
# d = dict(name='张三', age=20, score=95)
# 写入文件，ensure_ascii=False显示中文，encoding='utf-8'保证编码正确
# with open('data.json', 'w', encoding='utf-8') as f:
#     json.dump(d, f, ensure_ascii=False)
# data.json中内容：{"name": "张三", "age": 20, "score": 95}（直接显示中文，非转义）

# 反序列化：JSON字符串 → Python dict
# import json
# 标准的JSON字符串
# json_str = '{"age": 20, "score": 88, "name": "Bob"}'
# 反序列化：JSON字符串 → Python dict
# d = json.loads(json_str)
# print(type(d))  # 输出：<class 'dict'>
# print(d)        # 输出：{'age': 20, 'score': 88, 'name': 'Bob'}

# 从JSON文件中反序列化
# with open('data.json', 'r', encoding='utf-8') as f:
#     data = json.load(f)
# print(data)  
# 输出：{'name': '张三', 'age': 20, 'score': 95}
```

