---
title: Python 예외처리
description: <center>python exception</center>  <center>-이 글은 fastcampus에서의 수강 후 쓴 글 입니다.-<center>
categories:
 - python
tags:
---
# 예외처리
---
오류가 발생하면 프로그램은 에러를 출력하며 강제종료되거나, 원하지 않는 동작을 한다.

이러한 오류를 안전하게 처리하고, 바로 강제종료 되지 않고 오류 발생 후 처리할 루틴을 실행하고자 할 때 예외처리를 사용한다.

가장 기본적인 형태
```python
try:
	시도할 코드
except:
	에러가 발생했을 경우 실행할 코드
```
* 리스트 범위를 넘어간 에러

```python
sample_list = list('apple')
try:
    print(sample_list[5])
    print('List index출력완료')
except IndexError:
    print('list index를 참조하려 했는데 오류가 났음')

print('try-except구문 끝')

>>list index를 참조하려 했는데 오류가 났음
>>try-except구문 끝
```

여러가지 예외를 구분할 경우

```python
try:
	시도할 코드
except <예외 클래스1>:
	에러클래스 1에 해당할 때 실행할 코드
except <예외 클래스2>:
	...
except <예외 클래스3>:
	...
```

* 리스트의 범위를 넘어간 경우, IndexError를 명시적으로 처리해본다
* 딕셔너리의 키가 없는 경우, KeyError를 명시적으로 처리해본다

```python
sample_list = list('apple')
sample_dict={'red':'apple', 'yellow':'banana'}

try:
    print(sample_list[3])
    print(sample_dict['yellow'])

except IndexError as e:
    print('list index를 참조하려 했는데 오류가 났음')
    print(e)
except KeyError as e:
    print('dict index를 참조하려 했는데 오류가 났음')
    print(e)
else:
    print('예외없이 잘 끝났음')
finally:
    print('어쨌든 끝났음')

>>l
>>banana
>>예외없이 잘 끝났음
>>어쨌든 끝났음
```

예외사항을 변수로 사용할 경우

```python
try:
	시도할 코드
except <예외클래스> as <변수명>:
	<변수명>을 사용한 코드
```
## try ~ else
---
`else`문은 `try`이후 예외가 발생하지 않을 경우 실행된다.
```python
try:
	시도할 코드
except:
	예외 발생시 실행 코드
else:
	예외가 발생하지 않았을 시 실행할 코드
```
## try ~ finally
---
`finally`문은 `try`이후 예외가 발생하건, 하지않건 무조건 마지막에 실행된다.

## 예외 발생시키기
---
예외를 발생시킬때는 `raise`구문을 사용한다.

## 예외 만들기
---
내장 클래스 `Exception`을 상속받아 커스텀 예외를 만들 수 있다. 초기화 메서드에서 예외에서 처리할 데이터를 받고, `print`문으로 사용되고 싶다면 `__str__`메서드를 오버라이드 해준다.
