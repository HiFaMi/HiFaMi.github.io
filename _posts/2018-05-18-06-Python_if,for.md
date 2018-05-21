---
title: Python 제어문
description: <center>python for, if</center><br><center>-이 글은 fastcampus에서의 수강 후 쓴 글 입니다.-<center>
categories:
 - python
tags:
---
# 제어
## if, elif, else(조건문)
if와 else는 조건이 참인지 거짓인지 판단하는 파이썬 선언문(Statement)이며, elif는 else내 if를 중첩해야 할 때 사용한다.
```python
if 조건:
  조건이 참일 경우
else:
  조건이 거짓일 경우
```
```python
if 조건1:
  조건1이 참일 경우
elif:
  조건1이 거짓이나, 조건2가 참일 경우
else:
  조건1,2 가 모두 거짓일 경우
```

## 조건표현식
` 참일경우 if 조건식 else 거짓일 경우 `<br>
is_holiday에 True또는 False값을 할당한 후, if문과 조건표현식을 사용해서 각각 'Good'과 'Bad'를 출력하는 코드를 짜본다.
```python
In [187]: is_holiday = True
In [188]: if is_holiday == True:
     ...:     print('Good')
     ...: else:
     ...:     print('Bad')
     ...:
Good
In [189]: 'Good' if is_holiday == True else 'Bad'
Out[189]: 'Good'
```
## 중첩 조건표현식
```
조건1이 참일경우 if 조건1 else 조건1은 거짓이나 조건2가 참일경우 if 조건2 else 조건1,2가 모두 거짓일 경우
```
vacation에 1에서 10중 아무 값이나 할당 후, if, elif, else문과 중첩 조건표현식을 사용해서 각각 vacation이 7이상이면 'Good', 5이상이면 'Normal', 그 이하면 'Bad'를 출력하는 코드를 짜본다.
```python
In [190]: vacation = 5
In [192]: if vacation >= 7:
     ...:     print('Good')
     ...: elif vacation >= 5:
     ...:     print('Normal')
     ...: else:
     ...:     print('Bad')
     ...:
Normal

In [193]: 'Good' if vacation >=7 else 'Normal' if vacation >= 5 else 'Bad'
Out[193]: 'Normal'
```
# for문(조건에 따른 순회)
## 기본형태
시퀀스형 데이터를 순회하고자 할 때 사용한다.
```python
for 항목 in 순회가능(iterable)객체:
  <항목을 사용한 코드>
```
iterable한 객체에는 문자열, 튜플, 딕셔너리, 셋 등이 있다.

```python
In [195]: song_list = ['지나오다', 'My Way', '선물']
In [196]: for song in song_list:
     ...:     print(song)
     ...:
지나오다
My Way
선물
```
딕셔너리의 경우 key값은 dict.keys(), value값은 dict.values(), 두 값은 dict.items()값을 사용한다.

## 중첩
```python
for 항목1 in iterable객체1:
  iterable객체1을 순회하며 실행할 코드
  for 항목2 in iterable객체2:
    iterable객체1 내부에서 새로운 iterable객체2를 순회하며 실행할 코드
```

## 중단하기(break)
데이터를 순회하던 중, 특정 조건에서 순회를 멈추고 반복문을 빠져나갈 때 사용한다.
```python
for 항목 in iterable객체:
  break
```

## 건너뛰기(continue)
반복문을 중단하지 않고 다음으로 넘어가기 위해 사용한다.
```python
for 항목 in iterable객체:
  continue
```

## 여러 시퀀스 동시순회(zip)
```python
In [197]: fruits = ['apple', 'banana', 'melon']
In [198]: colors = ['red', 'yellow', 'green', 'purple']
In [199]: for fruit, color in zip(fruits, colors):
     ...: ...   print('fruit:', fruit, ' color:', color)
     ...:
fruit: apple  color: red
fruit: banana  color: yellow
fruit: melon  color: green
```

zip으로 묶은 시퀀스들 중, 가장 짧은 시퀀스가 완료되면 순회가 종료된다.<br>
zip으로 반환되는 것은 리스트가 아닌 zip클래스 형태의 iterable객체이기 때문에, 리스트 형태로 사용하려면 list()함수를 사용해준다.<br>
dict()함수를 사용할 경우 딕셔너리 객체가 만들어지게 된다.  

## 숫자 시퀀스 생성(range)
range()함수는 특정 범위의 숫자 스트림 데이터를 반환한다.
```python
range(start, stop, step)
```

## while문(반복문)
for문과 유사하나, while뒤의 조건이 참일 경우에 계속해서 반복한다.
```python
while 조건:
  조건이 참일경우 실행
  조건이 거짓이 될 경우까지 계속해서 반복
```
```python
In [200]: count = 0
In [201]: while count < 10:
 ...:     print(count)
 ...:     count+=1
 ...:
0
1
2
3
4
5
6
7
8
9
```

## 컴프리헨션(Comprehension)
```python
[표현식 for 항목 in iterable객체]
```
range와 for문을 사용할 경우
```python
In [202]: numbers=[]

In [203]: for item in range(1, 6):
     ...:     numbers.append(item)
     ...:
In [204]: numbers
Out[204]: [1, 2, 3, 4, 5]
```

리스트 컴프리헨션을 사용할 경우
```python
In [205]: [item for item in range(1, 6)]
Out[205]: [1, 2, 3, 4, 5]
```
리스트 컴프리헨션의 중첩
```python
for color in colors:
  for fruit in fruits:
```
```python
[(color, fruit) for color in colors for fruit in fruits]
```
# 실습
1.for문을 2개 중첩하여 (0,0), (0,1), (0,2), (0,3), (1,0), (1,1)..... (6,3)까지 출력되는 반복문을 구현한다.
```python
In [206]: for i in range(7):
     ...:     for j in range(4):
     ...:         print((i,j))
     ...:
(0, 0)
(0, 1)
(0, 2)
(0, 3)
(1, 0)
(1, 1)
(1, 2)
(1, 3)
.
.
.
(6, 2)
(6, 3)
```
2.리스트 컴프리헨션을 중첩하여 위 결과를 갖는 리스트를 생성한다.
```python
In [207]: [(i,j) for i in range(7) for j in range(4)]
Out[207]:
[(0, 0),
 (0, 1),
 (0, 2),
 (0, 3),
 (1, 0),
 (1, 1),
 .
 .
 .
 (6, 2),
 (6, 3)]
```
3.1, 2번의 반복문에서 1번은 튜플의 첫 번째 항목이 짝수일때만 출력하도록, 2번은 첫 번째 항목이 짝수일때만 리스트의 원소로 추가한다.
```python
In [209]: for i in range(7):
     ...:     for j in range(4):
     ...:         if i%2 == 0:
     ...:             print((i,j))
     ...:
     ...:
(0, 0)
(0, 1)
(0, 2)
(0, 3)
(2, 0)
(2, 1)
(2, 2)
(2, 3)
(4, 0)
(4, 1)
(4, 2)
(4, 3)
(6, 0)
(6, 1)
(6, 2)
(6, 3)
```
```python
In [212]: [(i,j) for i in range(7) for j in range(4) if i%2 == 0]
Out[212]:
[(0, 0),
 (0, 1),
 (0, 2),
 (0, 3),
 (2, 0),
 (2, 1),
 (2, 2),
 (2, 3),
 (4, 0),
 (4, 1),
 (4, 2),
 (4, 3),
 (6, 0),
 (6, 1),
 (6, 2),
 (6, 3)]
 ```
4.1000에서 2000까지의 숫자 중, 홀수의 합을 구해본다.
```python
In [223]: for i in range(1000,2001):
     ...:     if i%2 == 1:
     ...:         all_sum+=i
     ...:
In [224]: all_sum
Out[224]: 750000
```
```python
In [226]: for i in range(1001, 2001, 2):
     ...:     all_sum+=i
     ...:
In [227]: all_sum
Out[227]: 750000
```
5.리스트 컴프리헨션을 사용하여 구구단 결과를 갖는 리스트를 만들고, 해당 리스트를 for문을 사용해 구구단 형태로 나오도록 출력해본다. 각 단마다 한 번 더 줄바꿈을 넣어준다.

```python
In [1]: gugudan_list = ['{}X{}={}'.format(i,j,i*j) for i in range(1,10) for j in
    ...:  range(1,10)]
In [2]: for gugudan in gugudan_list:
    ...:
    ...:     if gugudan[2] == '9':
    ...:         print(gugudan)
    ...:         print()
    ...:     else:
    ...:         print(gugudan)
    ...:
   1X1=1
   1X2=2
   1X3=3
   1X4=4
   1X5=5
   1X6=6
   1X7=7
   1X8=8
   1X9=9

   2X1=2
   2X2=4
   2X3=6
   .
   .
   .
   9X7=63
   9X8=72
   9X9=81

```

6.1에서 99까지의 정수 중, 7의 배수이거나 9의 배수인 정수인 리스트를 생성한다. 단, 7의 배수이며 9의 배수인 수는 한 번만 추가되어야 한다.

```python
In [237]: for i in range(1,99):
     ...:     if i%7==0:
     ...:         seven.append(i)
     ...:     elif i%9 == 0:
     ...:         nine.append(i)
     ...:
     ...:
In [238]: seven
Out[238]: [7, 14, 21, 28, 35, 42, 49, 56, 63, 70, 77, 84, 91, 98]
In [239]: nine
Out[239]: [9, 18, 27, 36, 45, 54, 72, 81, 90]
In [240]: seven_nine = seven + nine
In [242]: seven_nine.sort()

In [243]: seven_nine
Out[243]:
[7, 9, 14, 18, 21, 27, 28, 35, 36, 42, 45, 49, 54, 56, 63, 70, 72, 77, 81, 84, 90, 91, 98]
```
