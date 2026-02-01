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

