---
title: Python 함수
description: <center>python function</center><br><center>-이 글은 fastcampus에서의 수강 후 쓴 글 입니다.-<center>
categories:
 - python
tags:
---
# 함수
반복적인 작업을 하는 코드를 재사용이 가능하게 정의해 놓은 것.

```python
def 함수명(매개변수[parameters]):
  동작
```

## 함수의 정의, 실행
```python
In [1]: def func():
   ...:     print('call func')
   ...:

In [3]: func()
  call func
```

함수 자체 func는 객체를 참조하는 변수이다.

## 리턴값이 있는 함수 정의
```python
In [5]: def return_true():
   ...:     return True
   ...:

In [6]: return_true()
Out[6]: True
```

함수의 결과로 Bool값을 갖는 데이터를 리턴하여 if문이나 while문의 조건으로 사용 가능하다.

## 매개변수를 사용하는 함수 정의

```python
In [7]: def print_argument(something):
   ...:     print(something)
   ...:

In [8]: print_argument('ABC')
ABC
```
## 매개변수(parameter)와 인자(argument)의 차이
함수 내부에서 함수에게 전달되어 온 변수는 매개변수라 부르며, 함수를 호출할 떄 전달하는 변수 인자로 부른다.

```python
def func(매개변수1, 매개변수2):
  ...

func(인자1, 인자2)
```

## 리턴값이 없을 경우

함수에서 리턴해 주는 값이 없을 경우, 아무것도 없다는 뜻을 가진 `None` 객체를 얻는다.

## 위치 인자(Positional arguments)

매개변수의 순서대로 인자를 전달하여 사용하는 경우
```python
def student(name, age, gender):
    return {'name': name, 'age': age, 'gender': gender}  

student('kim', 25, 'male')
{'name': 'kim', 'age': 25, 'gender': 'male'}
```

키워드 인자(Keyword arguments)
매개변수의 이름을 지정하여 인자로 전달하여 사용하는 경우
```python
student(age=30, name='hanyeong.lee', gender='male')
{'name': 'hanyeong.lee', 'age': 30, 'gender': 'male'}
```
<strong>위치인자와 키워드인자를 동시에 쓴다면, 위치인자가 먼저 와야 한다.</strong>

## 기본 매개변수값 지정

인자가 제공되지 않을 경우, 기본 매개변수로 사용할 값을 지정할 수 있다.

```python
def student(name, age, gender, cls='WPS'):
    ...:    return {'name': name, 'age': age, 'gender': gender, 'class': cls}

student('hanyeong.lee', 30, 'male')
{'name': 'hanyeong.lee', 'age': 30, 'gender': 'male', 'class': 'WPS'}
```

## 기본 매개변수값의 정의 시점
기본 매개변수값은 함수가 실행될 때 마다 계산되지 않고, 함수가 정의되는 시점에 계산되어 계속해서 사용된다.

```python
def return_list(value, result=[]):
    result.append(value)
    return result

return_list('apple')
['apple']

return_list('banana')
['apple', 'banana']
```

함수가 실행되는 시점에 기본 매개변수값을 계산하기 위해, 아래와 같이 바꿔준다.

```python
def return_list(value, result=None):
    if result is None:
        result = []
    result.append(value)
    return result

return_list('apple')
['apple']

return_list('banana')
['banana']
```

## 위치인자 묶음

함수에 위치인자로 주어진 변수들의 묶음은 `*매개변수명`으로 사용할 수 있다.<br>
관용적으로 `*args`를 사용한다.

```python
def print_args(*args):
  print(args)
```
## 키워드인자 묶음

함수에 키워드인자로 주어진 변수들의 묶음은 `**매개변수명`으로 사용할 수 있다. 관용적으로 `**wargs`를 사용한다.
```python
def print_kwargs(**kwargs):
  print(kwargs)
```

## docstring

함수를 정의한 문서 역할을 한다.<br>
함수 정의 후, 몸체의 시작부분에 문자열로 작성하며, 여러줄로도 작성 가능하다.

```python
def print_args(*args):
    '이 함수는 무엇을 하기 위한 함수입니다.'
    print(args)

help(print_args)

Help on function print_args in module __main__:

print_args(*args)
    이 함수는 무엇을 하기 위한 함수입니다.
```

## 함수를 인자로 전달

파이썬에서는 함수 역시 다른 객체와 동등하게 취급 되므로, 함수에서 인자로 함수를 전달, 실행, 리턴하는 형태로 프로그래밍이 가능하다.

* 'call func'를 출력하는 함수를 정의하고, 함수를 인자로 받아 실행하는 함수를 정의하여 첫 번째에 정의한 함수를 인자로 전달해 실행해보자.
  ```python
  def func():
      print('call_func')

  def exec(f):
      return f()

  exec(func)
  call_func
  ```

## 내부 함수
함수 안에서 또 다른 함수를 정의해 사용할 수 있다.

* 문자열 인자를 하나 전달받는 함수를 만들고, 해당 함수 내부에 전달받은 문자열을 대문자화해서 리턴해주는 내부 함수를 구현한다.<br>
문자열을 전달받는 함수는 내부함수를 실행한 결과를 리턴하도록 한다.  
  ```python
  def upper(string):
    def exec(upper_string):
        return upper_string.upper()
    return exec(string)

  upper('hello')
  'HELLO'
  ```

## 스코프(영역)
파이썬에서는 코드 작성 시, 각 함수마다 독립적인 스코프(영역)을 가진다.<br>
메인 프로그램(현재 동작하는 프로그램의 최상위 위치)의 영역은 전역 영역(Global Scope)라고 하며, 전역 스코프 내부에서 독립적인 영역을 갖고 있는 경우에는 지역 영역(Local Scope)라고 부른다.

아래 코드의 경우, show_global_champion함수 내부의 영역은 별개의 로컬 스코프를 가지며, champion변수는 전역 영역의 것을 가져와 출력하는것을 볼 수 있다.

```python
champion = 'Lux'

def show_global_champion():
    print('show_global_champion : {}'.format(champion))

show_global_champion()
print('print champion : {}'.format(champion))
```
위 코드를 아래와 같이 변경 후 실행 해 본다.

```python
champion = 'Lux'

def show_global_champion():
    print('show_global_champion : {}'.format(champion))

def change_global_champion():
    print('before change_global_champion : {}'.format(champion))
    champion = 'Ahri'
    print('after change_global_champion : {}'.format(champion))

show_global_champion()
change_global_champion()
```

change_global_champion함수에서 오류가 발생한다.<br>
첫 번째 코드에서는 champion변수가 함수의 로컬 스코프에 존재하지 않기 때문에 글로블 스코프에서 해당 변수를 찾아 출력하였으나, 이번 코드에서는 내부에 또다른 champion변수가 존재하기 때문에 할당하기 전인 변수를 사용한 것으로 판단하여 프로그램에서 오류를 발생시킨다.<br>
이름이 같은 두 변수가 다른 객체임을 내장함수 id를 사용해 확인해보자.<br>
또한, 각 영역에 해당하는 데이터들은 locals()함수를 사용해 확인 할 수 있으며, 전역 영역의 데이터들은 globals()함수를 사용한다.

## 스코핑 룰
스코프는 지역(Local), 전역(Global)외에도 내장(Built-in)영역이 존재하며, 내장영역이 가장 바깥, 그 내부에 전역, 그 내부에 지역 순으로 정의된다.<br>
분리된 영역에서, 외부 영역에서는 내부 영역의 데이터를 사용할 수 없지만 내부 영역에서는 자신의 외부 영역에 있는 데이터를 참조할 수 있다.<br>
(반대의 경우에는 함수의 인자로 데이터를 전달한다)

## 내장 함수와 내장 영역

print, dict등 지정하지 않고 사용했던 내장 함수들은 위 스코핑 룰의 내장 스코프에 존재하는 함수들이다.<br>
전역스코프의 `__builtin__`변수에 할당되어 있으며, 전역 스코프에서는 해당 변수의 내부를 참조할 수 있도록 파이썬이 시작될 때 자동으로 처리된다.<br>
확인시 dir함수를 사용하며, dir함수는 해당 객체가 사용 가능한 속성 및 함수들을 리스트 형태로 나타내준다.

## 로컬 스코프에서 글로벌 스코프의 변수를 사용

```python
champion = 'Lux'

def change_global_champion():
    champion = 'Ahri'
    print('after change_global_champion : {}'.format(champion))

change_global_champion()
print('print global champion : {}'.format(champion))
```

이 경우, 위의 show_global_champion함수와는 다르게 change_global_champion함수는 champion변수에 새로운 값을 대입한다.<br>
만약 로컬 스코프에서 글로벌 스코프의 변수를 변경해야 한다면, 해당 변수가 로컬 스코프에 생성되는 것이 아닌 글로벌 영역에 이미 존재하는 값을 사용함을 명시해주어야 한다.

```python
champion = 'Lux'

def change_global_champion():
    global champion
    champion = 'Ahri'
    print('after change_global_champion : {}'.format(champion))

change_global_champion()
print('print global champion : {}'.format(champion))
```
파이썬에서는 한 스코프에서 동일한 이름을 가진 두 스코프의 변수를 사용할 수 없음을 기억해야 한다.

## 내부함수에서의 로컬 스코프(nonlocal)
```python
champion = 'Lux'

def local1():
    champion = 'Ahri'
    print('local1 locals() : {}'.format(locals()))

    def local2():
        champion = 'Ezreal'
        print('local2 locals() : {}'.format(locals()))
    local2()

print('global locals() : {}'.format(locals()))
local1()
```

로컬 스코프 내부에는 또 다른 로컬 스코프가 존재할 수 있다.<br>
전역 스코프가 아닌, 자신의 바로 바깥 영역의 로컬 스코프(자신보다 한 단계 위의 로컬 스코프)의 데이터를 참조하고자 한다면, nonlocal키워드를 사용한다.

```python
champion = 'Lux'

def local1():
    champion = 'Ahri'
    print('local1 locals() : {}'.format(locals()))

    def local2():
        nonlocal champion
        champion = 'Ezreal'
        print('local2 locals() : {}'.format(locals()))
    local2()
    print('local1 locals() : {}'.format(locals()))

print('global locals() : {}'.format(locals()))
local1()
```

## global키워드와 인자(argument)전달의 차이

--인자로 전달
```python
global_level = 100
def level_add(value):
    value += 30
    print(value)

level_add(global_level)
print(global_level)
```

--global키워드 사용
```python
global_level = 100
def level_add():
    global global_level
    global_level += 30
    print(global_level)

level_add()
print(global_level)
```
인자로 전달한 경우, 같은 객체를 가리키는 글로벌 변수 global_level과 매개변수 value가 존재한다.<br>
이 때, 매개변수인 value의 값을 변경하는 것은 global_level에는 영향을 주지 않는다.<br>
global키워드의 경우 둘은 같은 변수이다.

## 람다함수
한 줄 짜리 표현식으로 이루어지며, 반복문이나 조건문 등의 제어문은 포함될 수 없다.<br>
또한, 함수이지만 정의/호출이 나누어져 있지 않으며 표현식 자체가 바로 호출된다.

```python
lambda <매개변수> : <표현식>
```

```python
In [15]: def multi(x):
    ...:     return x*x
    ...:
    ...:
In [16]: multi(5)
Out[16]: 25
In [17]: (lambda x:x*x)(5)
Out[17]: 25
In [18]: f=(lambda x:x*x)
In [19]: f(5)
Out[19]: 25
```
## 클로져 (Closure)
함수가 정의된 환경을 말하며, 파이썬 파일이 여러개일 경우 각 파일은 하나의 모듈역할을 하고, 각 모듈은 독립적인 환경을 가진다.<br>
독립된 환경은 각자의 영역을 전역 영역으로 사용한다.

## closure/module_a.py

```python
level = 100
def print_level():
    print(level)
```
## closure/module_b.py
```python
import module_a
level = 50
def print_level():
    print(level)

module_a.print_level()
print_level()
```
python module_b.py로 module_b를 실행한다.

```
(fc-python) ➜  closure git:(master) ✗ python module_a.py
100
(fc-python) ➜  closure git:(master) ✗ python module_b.py
100
100
50
```
함수의 전역 영역은 해당 함수가 정의된 모듈의 전역 영역으로, 전역변수는 모듈의 영역에 영향을 받는다.

## 내부함수의 클로져
```python
level = 0
def outer():
    level = 50
    def inner():
        nonlocal level
        level += 3
        print(level)
    return inner
f= outer()
```
위의 경우, outer함수는 inner함수를 반환하여 결과를 func전역변수에 할당한다.<br>
inner함수의 호출 결과가 아닌 함수 자체를 반환하기 때문에, func변수는 실행할 수 있는 함수객체이다.<br>
이 때 inner함수가 사용하는 level변수는 nonlocal키워드를 사용했기 때문에 outer에 새로 정의된 지역변수 level을 사용한다.<br>
반복적으로 func함수를 실행하면 inner의 외부(outer)에 존재하는 level변수의 값을 증가시키고 print시키기 때문에, 값은 계속해서 증가한다.<br>

## 데코레이터 (decorator)
함수를 받아 다른 함수를 반환하는 함수. 예를 들면, 기존에 존재하던 함수를 바꾸지 않고 전달된 인자를 보기위한 디버깅 print함수를 추가한다던가 하는 기능을 할 수 있다.

  1. 기능을 추가할 함수를 인자로 받음
  2. 데코레이터 자체에 추가할 기능을 함수로 정의
  3. 인자로 받은 함수를 데코레이터 내부에서 적절히 호출
  4. 위 2가지를 행하는 내부 함수를 반환

아래와 같이 함수 2개를 만들고, 새 구문을 추가해본다.

  * 인자로 문자열 변수를 받아 출력해주는 함수 print_string구현
  * 인자로 정수형 변수를 받아 출력해주는 함수 print_int구현
  * 각 함수에 대해 자신이 전달받은 인자에 대한 type을 출력하는 구문을 추가

  ```python
  def print_args(original_function):
    def decorated_function(*args):
        print('args_type: {}'.format(type(args[0])))
        return original_function(*args)
    return decorated_function

  def print_string(x):
    return str(x)     

  def print_int(x):
    return int(x)  

  f=print_args(print_string)
  f('hello')
  args_type: <class 'str'>
  'hello'

  f2 = print_args(print_int)
  f2(12)
  args_type: <class 'int'>
  12
  ```

여러 함수에 대해 같은 기능을 추가할 경우, 데코레이터를 사용한다.
```python
def print_debug(func):
    def inner_func(*args, **kwargs):
        print('args :', args)
        print('kwargs :', kwargs)
        result = func(*args, **kwargs)
        return result
    return inner_func
```

데코레이터함수(인자로 전달할 함수) 형태로도 사용이 가능하지만, 데코레이터를 사용할 경우에는 함수 위에 데코레이터를 추가해서 사용가능하다.

```python
@print_debug
def any_func():
    pass
```
또한 데코레이터는 여러개를 가질 수 있으며, 함수에서 가장 가까운 것 부터 실행한다.

## 제네레이터 (generator)

제네레이터는 함수는 파이썬의 시퀀스 데이터를 생성하는데 사용된다. 실제 시퀀스 데이터와 다른 점은, 시퀀스 전체를 가지고 있는 것이 아니라 시퀀스 데이터를 생성하기 위한 어떠한 루틴만을 가지고 있는 것이다.<br>
이 방식을 택했을 때의 장점은, 전체 크기만큼의 메모리를 가지고 있는 시퀀스 데이터와는 달리 메모리를 적게 사용할 수 있다.<br>
제네레이터는 마지막으로 호출한 위치(항목)에 을 기억하고 있으며, 한 번 순회할 때 마다 그 다음 값을 반환한다.<br>
제네레이터는 함수를 통해서 만들어지며, 함수 내부의 반복문에서 yield키워드를 사용하면 제네레이터가 된다.    

```python
def range_gen(num):
  i = 0
  while i < num:
    yield i
    i += 1

gen = range_gen(10)
gen
<generator object range_gen at 0x10b682168>
type(gen)
<class 'generator'>
gen.__next__()
0
gen.__next__()
1
gen.__next__()
2
gen.__next__()
3
gen.__next__()
4
gen.__next__()
5
gen.__next__()
6
gen.__next__()
7
gen.__next__()
8
gen.__next__()
9
gen.__next__()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```
함수 내부에 yield키워드가 사용되어 제네레이터 함수가 되었으며, 함수를 실행하면 제네레이터 객체를 반환한다.<br>
yield부분에서 멈춘 제네레이터 객체를 순회하기 위해서는 `__next__()` 함수를 실행해준다.

## 실습
1.매개변수로 문자열을 받고, 해당 문자열이 red면 apple을, yellow면 banana를, green이면 melon을, 어떤 경우도 아닐 경우 I don't know를 리턴하는 함수를 정의하고, 사용하여 result변수에 결과를 할당하고 print해본다.

```python
def find(x):
  find_dict ={'red':'apple', 'yellow':'banana', 'green':'melon'}
  if x in find_dict:
      result = find_dict[x]
  else:
      result = "I don't know"
  print(result)

find('yellow')
banana

find('blue')
I don't know
```

2.1번에서 작성한 함수에 docstring을 작성하여 함수에 대한 설명을 달아보고, help(함수명)으로 해당 설명을 출력해본다.

```python
def find(x):
  '이 함수는 dict안에 값이 있으면 리턴해 주는 함수 입니다.'
  find_dict ={'red':'apple', 'yellow':'banana', 'green':'melon'}
  if x in find_dict:
      result = find_dict[x]
  else:
      result = "I don't know"
  print(result)

help(find)
Help on function find in module __main__:

find(x)
  이 함수는 dict안에 값이 있으면 리턴해 주는 함수 입니다.
```  

3.한 개 또는 두 개의 숫자 인자를 전달받아, 하나가 오면 제곱, 두개를 받으면 두 수의 곱을 반환해주는 함수를 정의하고 사용해본다.
```python
def cal(*args):
  if len(args) == 1:
    return args[0]**2
  else:
    return args[0]*args[1]

cal(5)
25

cal(5,2)
10
```
4.두 개의 숫자를 인자로 받아 합과 차를 튜플을 이용해 동시에 반환하는 함수를 정의하고 사용해본다.
```python
def sum_and_subtraction(*args):
    print(args[0]+args[1])
    print(args[0]-args[1])

sum_and_subtraction(10,4)
14
6
```    
5.위치인자 묶음을 매개변수로 가지며, 위치인자가 몇 개 전달되었는지를 print하고 개수를 리턴해주는 함수를 정의하고 사용해본다.
```python
def how_many(*args):
    print(len(args))
    return '위치인자의 개수: {}'.format(len(args))

how_many(1,2,3,4,5,6,7,8)
8
'위치인자의 개수: 8'
```    
6.람다함수와 리스트 컴프리헨션을 사용해 한 줄로 구구단의 결과를 갖는 리스트를 생성해본다.
```python
f=[(lambda x,y:x*y)(i,j) for i in range(2,10) for j in range(1,10)]

print(f)

[2, 4, 6, 8, 10, .... ,32, 40, 48, 56, 64, 72, 9, 18, 27, 36, 45, 54, 63, 72, 81]
```

## 알고리즘
* 순차검색(Sequential Search)
  * 문자열과 키 문자 1개를 받는 함수 구현
  * while문을 이용, 문자열에서 키 문자가 존재하는 index위치를 검사 후 해당 index를 리턴
  * 찾지 못했을 경우 -1을 리턴

```python
def sequrntial_search(string,key):
  index = 0
  while True:
      if key in string:
          return string.index(key)
          break
      else:
          return -1
          break

sequrntial_search('hello','o')
4

sequrntial_search('hello','i')
-1
```

* 선택정렬(Selection sort)
  * [9, 1, 6, 8, 4, 3, 2, 0, 5, 7] 를 정렬한다.
  * 정렬과정
    1. 리스트 중 최소값을 검색
    2. 그 값을 맨 앞의 값과 교체
    3. 나머지 리스트에서 위의 과정을 반복

```python
def selection_sort(x):
    a=0
    index = 0
    for i in range(len(x)):
        if x.index(min(x[i:])) == x.index(x[i]):
            x[i] = min(x[i:])
        else:
            a=x[i]
            index = x.index(min(x[i:]))
            x[i]=min(x[i:])
            x[index]=a

test_list = [9, 1, 6, 8, 4, 3, 2, 0, 5, 7]

selection_sort(test_list)

test_list
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```
