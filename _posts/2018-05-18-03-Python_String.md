---
title: Python 문자열
description: <center>python 문자열</center><br><center>-이 글은 fastcampus에서의 수강 후 쓴 글 입니다.-<center>
categories:
 - python
tags:
---

## 문자열
python3 에서는 문자열에서 기본적으로 유니코드를 사용하며 불변하다.

## 문자열 표현
작은 따옴표 또는 큰 따옴표를 이용한다
```python
In [49]: '패스트 캠퍼스'
Out[49]: '패스트 캠퍼스'
In [50]: "패스트 캠퍼스"
Out[50]: '패스트 캠퍼스'
```
작은 따옴표 또는 큰 따옴표를 사용했을 떄, 사용하지 않는 인용 부호는 문자열 내부에서 사용 가능
```python
In [51]: '패스트 캠퍼스"웹프로그래밍 스쿨"'
Out[51]: '패스트 캠퍼스"웹프로그래밍 스쿨"'
```
세 개의 작은 따옴표 또는 큰 따옴표는 여러줄에 걸친 문자열을 나타낼 때 사용
```python
'''환사 여러분.
    ...:
    ...: 7.1 패치를 소개합니다.
    ...: 앞으로 있을 여러 번의 패치에 대해서는 차차
    ...: 하지만 그렇다고 이번 패치가 하향
    ...: 정의의 전장에서 승리를 기원합니다.'''
```
## 문자열 더하기
문자열을 더라게 되면 뒤에 더하여 붙게된다.
```python
In [53]: '패스트'+'캠퍼스'
Out[53]: '패스트캠퍼스'
```

## 형변환
내장함수 str을 사용한다.
```python
In [54]: str(124)
Out[54]: '124'
```
## 이스케이프 문자
특수문자, 또는 특별한 역할을 하는 의미를 나타내는 문자를 뜻한다.

|   이스케이프 문자   |      설명     |
|:---------------:|:------------:|
| /a |  비프음 발생  |
| \t |    탭(tab)  |
| \n | 줄바꿈   |
| \\ | \(역슬래시) 입력 |  
| \' | 작은따옴표(') 입력 |  
| \" | 큰따옴표(") 입력  |

## 인덱스 연산
문자열에서 문자를 추출하기 위해 대괄호와 오프셋을 지정할 수 있다.<br>
가장 왼쪽은 0이며, 가장 오른쪽은 -1로 시작한다.

```python
In [55]: name = '패스트캠퍼스'
In [56]: name[0]
Out[56]: '패'
In [57]: name[-1]
Out[57]: '스'
In [58]: name[20]
---------------------------------------------------------------------------
IndexError                                Traceback (most recent call last)
<ipython-input-58-5b0788fe6a0f> in <module>()
----> 1 name[20]

IndexError: string index out of range
```
문자열은 불변이므로 인덱싱한 부분에 새 값을 대입할 수 없다.
```python
In [59]: name[0]='크'
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-59-599f1f7b383a> in <module>()
----> 1 name[0]='크'

TypeError: 'str' object does not support item assignment
```
## 슬라이스 연산
`[start:end:step]` 형식을 사용한다.

* `[:]`- 처음부터 끝까지
* `[start:]` -- start오프셋부터 마지막까지
* `[:end]` -- 처음부터 end오프셋까지
* `[start:end]` -- start오프셋부터 end오프셋까지
* `[start:end:step]` -- start오프셋부터 end오프셋까지, step만큼씩 뛰어넘은 부분

## 길이
내장함수 len을 사용한다.

## 문자열 나누기(split)
내장함수 split을 사용하여 주어진 구분자를 기준으로 문자열을 리스트로 변환해준다.
```python
In [60]: girlsday = "민아,유라,소진,혜리"
In [61]: girlsday.split(',')
Out[61]: ['민아', '유라', '소진', '혜리']
```
split함수에 인자를 주지 않을 경우, 공백을 구분자로 사용한다.

## 문자열 결합(join)
split과는 반대로 문자열 리스트를 하나의 문자열로 결합해준다.
```python
In [62]: girlsday_list = girlsday.split(',')
In [63]: girlsday_str = ', '.join(girlsday_list)
In [64]: print(girlsday_str)
민아, 유라, 소진, 혜리
```

## 문자열 포맷
옛 스타일(%)

|   변환타입   |      설명     |
|:---------------:|:------------|
| %s |  문자열  |
| %d |    10진수  |
| %x | 16진수   |
| %o | 8진수 |  
| %f | 10진수 부동소수점수 |  
| %e | 지수로 나타낸 부동소수점수  |
| %g | 10진 부동소수점수 혹은 지수로 나타낸 부동소수점수  |
| %% | 리터럴 %  |

```python
In [66]: '%s' % 42
Out[66]: '42'
```

## 정렬
```%[정렬기준(-,없음)][전체글자수].[문자길이 또는 소수점 이후 문자길이][변환타입]```
```python
In [67]: d=37
In [68]: f=3.14
In [69]: s = 'Fastcampus'
In [70]: '%d %f %s' % (d, f, s)
Out[70]: '37 3.140000 Fastcampus'
In [71]: '%10d %10f %10s' % (d, f, s)
Out[71]: '        37   3.140000 Fastcampus'
In [72]: '%-14d %-14f %-14s' % (d, f, s)
Out[72]: '37             3.140000       Fastcampus    '
```

## 새 스타일({}, format)
```{}.format(변수)```
```python
In [73]: '{} {} {}'.format(d, f, s)
Out[73]: '37 3.14 Fastcampus'
In [74]: '{1} {2} {0}'.format(d, f, s)
Out[74]: '3.14 Fastcampus 37'
```

## 실습
1. 여러 줄의 텍스트를 multi_lines변수에 할당하고, print()함수로의 출력과 인터프리터의 자동 출력(변수명 입력)을 비교해보시오.
```python
In [76]: multi_lines = '''그대여
    ...: 아무 걱정
    ...: 하지 말아요'''
In [77]: multi_lines
Out[77]: '그대여\n아무 걱정\n하지 말아요'
In [78]: print(multi_lines)
그대여
아무 걱정
하지 말아요
```
2. str1, str2변수에 각각 문자열을 할당하고, 두 변수를 결합해 str3변수에 할당해보시오.
```python
In [79]: str1 = '그대여'
In [80]: str2 = '아무걱정'
In [81]: str3 = str1+str2
In [82]: str3
Out[82]: '그대여아무걱정'
```
3. str1변수에 `*` 연산자를 사용한 결과를 출력해보시오.
```python
In [83]: str1*3
Out[83]: '그대여그대여그대여'
```
