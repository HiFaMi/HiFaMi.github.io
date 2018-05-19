---
title: Python
description: <center>python 변수</center><br><center>-이 글은 fastcampus에서의 수강 후 쓴 글 입니다.-<center>
categories:
 - python
tags:
---

## 변수

파이썬은 모든것이 객체(Object)로 이루어져 있다.<br>
객체는 데이터의 형태를 결정해주는 타입으로, python에서는 객체의 타입을 바꿀 수 없다.<br>
프로그래머는 <strong>변수</strong>를 선언하고 사용하는 형태로 컴퓨터의 메모리 값에 할당하고, 참조할 수 있다.
<blockquote>일반적으로, 프로그래밍 언어에서의 같다(Equal)의 의미는 =가 아닌 ==을 사용한다.</blockquote>

```python
var1 = 100
print(var1)
100
```
변수는 단지 이름일 뿐이며, 그 자체가 어떠한 값을 가지는 것이 아니라 해당 객체를 참조 하는 것이다.

```python
var2=var1
var3=ver1
```
```python
In [4]: id(var1)
Out[4]: 4368711440
In [5]: id(var2)
Out[5]: 4368711440
In [6]: id(var3)
Out[6]: 4368711440
```
각 변수의 id를 확인해 보면 var1의 id 값과 var2,3의 id값이 같다는 것을 확인 할 수 있다.

```python
In [7]: var1 = 200
In [8]: id(var1)
Out[8]: 4368714640
In [9]: id(var2)
Out[9]: 4368711440
In [10]: id(var3)
Out[10]: 4368711440
```
var1의 값을 변경하게되면 var1은 새로운 참조값을 갖게 되지만 기존의 var1과 같은 참조값을 가지고 있던 var2,3는 변한 참조값으로 바뀌지 않고 기존의 참조값을 계속 가지고 있다.

## 변수의 타입 확인

내장함수의 type을 사용하여 확인할 수 있다.
```python
In [11]: type(var1)
Out[11]: int
In [12]: type(1.0)
Out[12]: float
In [13]: type('string')
Out[13]: str
```
## 변수의 입력과 출력
입력의 경우 내장함수 input을 사용, 출력은 print 사용
```python
In [14]: user_input = input('값을 입력하세요: ')
값을 입력하세요:  Hello world
In [15]: print(user_input)
Hello world
```
## 실습
1. 1일이 몇 초인지 계산 후, 해당 결과를 seconds_per_day 변수에 할당하라.
```python
In [16]: seconds_per_day= 24*60*60
```
2. 1년이 몇 초인지 계산 후, 해당 결과를 seconds_per_year 변수에 할당하라.
```python
In [17]: seconds_per_year = 365*seconds_per_day
```
3. 각 변수의 타입을 확인해본다.
```python
In [18]: type(seconds_per_day)
Out[18]: int
In [19]: type(seconds_per_year)
Out[19]: int
```
4. 문자열을 입력해주세요 :라는 안내문구를 띄워주도록 input함수를 사용해본다. 결과는 var에 할당한다.
```python
In [21]: var = input("문자열을 입력하여 주세요: ")
문자열을 입력하여 주세요: hello world
```
