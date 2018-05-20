---
title: Python 딕셔너리
description: <center>python 딕셔너리</center><br><center>-이 글은 fastcampus에서의 수강 후 쓴 글 입니다.-<center>
categories:
 - python
tags:
---

# 딕셔너리 (Dictionary)
Key-Value 형태로 항목을 가지는 자료구조.

## 딕셔너리 생성
```python
In [144]: empty_dict1 = {}
In [145]: empty_dict2 = dict()
In [146]: champion_dict = {
     ...:  'Lux': 'the Lady of Luminosity',
     ...:  'Ahri': 'the Nine-Tailed Fox',
     ...:  'Ezreal': 'the Prodigal Explorer',
     ...:  'Teemo': 'the Swift Scout',
     ...:  }
```

## 형변환
dict 함수를 사용하여 두 값의 시퀀스(리스트 또는 튜플)을 딕셔너리로 변환 한다.
```python
In [147]: sample = [[1,2], [3,4], [5,6]]
In [149]: dict(sample)
Out[149]: {1: 2, 3: 4, 5: 6}
```

## 항목 찾기/ 추가/ 변경[key]
```python
In [151]: champion_dict['Lux']
Out[151]: 'the Lady of Luminosity'
In [152]: champion_dict['Sona'] = 'Maven of the Strings'
In [153]: champion_dict
Out[153]:
{'Lux': 'the Lady of Luminosity',
 'Ahri': 'the Nine-Tailed Fox',
 'Ezreal': 'the Prodigal Explorer',
 'Teemo': 'the Swift Scout',
 'Sona': 'Maven of the Strings'}
In [154]: champion_dict['Lux'] = 'Demacia'
In [155]: champion_dict
Out[155]:
{'Lux': 'Demacia',
 'Ahri': 'the Nine-Tailed Fox',
 'Ezreal': 'the Prodigal Explorer',
 'Teemo': 'the Swift Scout',
 'Sona': 'Maven of the Strings'}
 ```
## 결합(update)
```python
In [156]: item_dict = {
     ...: 'Doran\'s Ring': 400,
     ...: 'Doran\'s Blade': 450,
     ...: 'Doran\'s Shield': 450,
     ...: }
In [157]: com_dict = {}
In [158]: com_dict.update(champion_dict)
In [159]: com_dict.update(item_dict)
In [160]: com_dict
Out[160]:
{'Lux': 'Demacia',
 'Ahri': 'the Nine-Tailed Fox',
 'Ezreal': 'the Prodigal Explorer',
 'Teemo': 'the Swift Scout',
 'Sona': 'Maven of the Strings',
 "Doran's Ring": 400,
 "Doran's Blade": 450,
 "Doran's Shield": 450}
 ```
 서로 같은 키가 있을 경우에는 update에 주어진 딕셔너리의 값이 할당된다.

## 삭제(del)
```python
In [161]: del com_dict['Doran\'s Blade']

In [162]: del com_dict['Doran\'s Ring']

In [163]: del com_dict['Doran\'s Shield']

In [164]: com_dict
Out[164]:
{'Lux': 'Demacia',
 'Ahri': 'the Nine-Tailed Fox',
 'Ezreal': 'the Prodigal Explorer',
 'Teemo': 'the Swift Scout',
 'Sona': 'Maven of the Strings'}
```
## Else
전체삭제 : clear <br>
in으로 키 검색 : True/False를 반환<br>
keys() : 키값 반환<br>
values() : 벨류값 반환<br>
items() : 모든 값 얻기<br>
복사 : copy()

# 셋 (Set)
셋은 키만 있는 딕셔너리와 같으며, 중복된 값이 존재할 수 없다.

## 셋 생성
```python
In [165]: empty_set = set()
In [166]: champions = {'lux', 'ahri', 'ezreal'}
```

## 형변환
문자열, 리스트, 튜플, 딕셔너리를 셋으로 변환 할 수 있으며, 중복된 값이 있으면 사라진다.
```python
In [167]: set('ezreal')
Out[167]: {'a', 'e', 'l', 'r', 'z'}
In [168]: set(champion_dict)
Out[168]: {'Ahri', 'Ezreal', 'Lux', 'Sona', 'Teemo'}
```
딕셔너리는 키값만 남게 된다.

## 집합 연산

|   연산자   |      설명      |
|:----------:|:-------------:|
| \| |  합집합 |
| & |    교집합   |
| - | 차집합 |
| ^ | 대칭차집합 |  
| <= | 부분집합 |
| < | 진부분집합 |
| >= | 상위집합 |
| > | 진상위집합 |

# 실습
1. apple은 사과, banana는 바나나, cherry는 체리의 key-value를 갖는 fruits라는 이름의 사전을 만든다.
```python
In [169]: fruits = {'apple' : '사과', 'banana' : '바나나', 'cherry' : '체리'}
In [170]: fruits
Out[170]: {'apple': '사과', 'banana': '바나나', 'cherry': '체리'}
```
2. fruits를 Set으로 만들어 fruits_set변수에 할당한다.
```python
In [171]: fruits_set = set(fruits)
In [172]: fruits_set
Out[172]: {'apple', 'banana', 'cherry'}
```
3. fruits_set에 durian이 존재하는지 확인한다.
```python
In [174]: 'durian' in fruits_set
Out[174]: False
```
4. fruits사전에서 apple키에 해당하는 값을 출력한다.
```python
In [175]: fruits['apple']
Out[175]: '사과'
```
5. girlgroups라는 이름의 2차원 사전을 만들고 출력해본다.
  * 최상위 키는 girlsday와 redvelvet이 있으며, 각각 자식으로 사전을 갖는다.
  * girlsday키의 자식사전에는 korean과 members키가 있으며, 각각 '걸스데이'라는 문자열과 ['민아', '혜리', '소진', '유라']라는 리스트를 갖는다.
  * redvelvet키의 자식사전에도 korean과 members키가 있으며, 각각 '레드벨벳'이라는 문자열과 ['아이린', '슬기', '웬디', '조이', '예리']라는 리스트를 갖는다.
  ```python
  In [176]: girlgroups = {
     ...: 'girlsday' :{'korean':'걸스데이' , 'members' : ['민아', '혜리', '소진', '유라']},
     ...: 'redvelvet' :{'korean' : '레드벨벳' , 'members' : ['아이린', '슬기', '웬디', '조이',
     ...: '예리']},
     ...: }
  ```
6. girlgroups사전의 최상위 키 목록을 출력해본다.
```python
In [177]: girlgroups.keys()
Out[177]: dict_keys(['girlsday', 'redvelvet'])
```
7. girlgroups['girlsday']의 모든 키를 출력해본다.
```python
In [178]: girlgroups['girlsday'].keys()
Out[178]: dict_keys(['korean', 'members'])
```
8. girlgroups['redvelvet']의 모든 값을 출력해본다.
```python
In [179]: girlgroups['redvelvet'].values()
Out[179]: dict_values(['레드벨벳', ['아이린', '슬기', '웬디', '조이', '예리']])
```

9. x = {1,2,3,4,5,6,8}, y={4,5,6,9,10,11}, z={4,6,8,9,7,10,12}일 때,
  * x,y,z의 교집합에 해당하는 숫자는?
  ```python
  In [184]: x&y&z
  Out[184]: {4, 6}
  ```
  * y,z의 교집합이며 x에는 속하지 않는 숫자는?
  ```python
  In [185]: (y&z)-x
  Out[185]: {9, 10}
  ```
  * x에만 속하고 y,z에는 속하지 않는 숫자는?  
  ```python
  In [186]: x-(y|z)
  Out[186]: {1, 2, 3}
  ```
