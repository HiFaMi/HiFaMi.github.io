---
title: Python
description: <center>python 시퀀스</center><br><center>-이 글은 fastcampus에서의 수강 후 쓴 글 입니다.-<center>
categories:
 - python
tags:
---

# 리스트
리스트는 순차적인 데이터를 나타내는 데 유용하며, 문자열과는 달리 내부 항복을 변경할 수 있다.

## 리스트 생성
```python
In [84]: empty_list1 = []
In [85]: empty_list2 = list()
In [86]: sample_list = ['a', 'b', 'c', 'd']
In [87]: sample_list2 = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
```
## 다른 데이터를 리스트로 변환
```python
In [88]: list('League of legends')
Out[88]:
['L', 'e', 'a', 'g', 'u', 'e', ' ', 'o', 'f', ' ', 'l', 'e', 'g', 'e', 'n', 'd', 's']
```
## 인덱스 연산
sample_list2를 이용해서 실습. 5월, 7월을 인덱스연산을 통해 추출해보자.
```python
In [89]: sample_list2[4]
Out[89]: 'May'
In [90]: sample_list2[6]
Out[90]: 'Jul'
```
## 내부항복 변경
sample_list를 이용, 3번째 요소인 'c'를 대문자 'C'로 바꿔본다.
```python
In [91]: sample_list[2] ='C'
In [92]: sample_list
Out[92]: ['a', 'b', 'C', 'd']
```
## 슬라이스 연산
* sample_list2를 이용, 1월부터 3월씩 건너뛴 결과를 quarters에 할당
```python
In [93]: quarters = sample_list2[::3]
In [94]: quarters
Out[94]: ['Jan', 'Apr', 'Jul', 'Oct']
```
* sample_list2를 이용, 끝에서부터 3번째 요소까지를 last_three에 할당
```python
In [97]: last_three = sample_list2[:8:-1]
In [98]: last_three
Out[98]: ['Dec', 'Nov', 'Oct']
```
* sample_list2를 이용, 끝에서부터 처음까지(거꾸로) 2월씩 건너뛴 결과를 reverse_two_steps에 할당
```python
In [99]: reverse_two_steps = sample_list2[::-1]
In [100]: reverse_two_steps
Out[100]:
['Dec', 'Nov', 'Oct', 'Sep', 'Aug', 'Jul',
 'Jun', 'May', 'Apr', 'Mar', 'Feb', 'Jan']
```

## 리스트 항목 추가
```python
In [101]: sample_list.append('e')
In [102]: sample_list
Out[102]: ['a', 'b', 'C', 'd', 'e']
```

## 리스트 병합(extend, +=)
```python
In [103]: fruits = ['apple', 'banana', 'melon']
In [104]: colors = ['red', 'green', 'blue']
In [105]: fruits.extend(colors)
In [106]: fruits
Out[106]: ['apple', 'banana', 'melon', 'red', 'green', 'blue']
```

## 특정 위치에 리스트 항목 추가(insert)
리스트 함수 insert 사용
* fruits리스트의 1번째 위치에 'mango'를 추가해보자
  ```python
  In [106]: fruits
  Out[106]: ['apple', 'banana', 'melon', 'red', 'green', 'blue']
  In [107]: fruits.insert(0, 'mango')
  In [108]: fruits
  Out[108]: ['mango', 'apple', 'banana', 'melon', 'red', 'green', 'blue']
  ```
* fruits리스트의 100번째 위치에 'pineapple'을 추가해보자
  ```python
  In [109]: fruits.insert(100, 'mango')
  In [110]: fruits
  Out[110]: ['mango', 'apple', 'banana', 'melon', 'red', 'green', 'blue', 'mango']
  ```

## 특정 위치 리스트 항목 삭제 (del)
파이썬 구문 del사용<br>
```del은 리스트 함수가 아닌, 파이썬 구문으로 `del <리스트>[오프셋]` 형식을 사용한다.```

```python
In [110]: fruits
Out[110]: ['mango', 'apple', 'banana', 'melon', 'red', 'green', 'blue']
In [111]: del fruits[1]
In [112]: fruits
Out[112]: ['mango', 'banana', 'melon', 'red', 'green', 'blue']
```
값으로 리스트 항목 삭제(remove)
```python
In [113]: fruits.remove('mango')
In [114]: fruits
Out[114]: ['banana', 'melon', 'red', 'green', 'blue']
```
## 리스트 항목 추출 후 삭제 (pop)
```python
In [116]: fruits.pop()
Out[116]: 'blue'
In [117]: fruits.pop(-3)
Out[117]: 'melon'
```
## 값으로 리스트 항목 오프셋 찾기 (index)
```python
In [118]: fruits.index('red')
Out[118]: 1
In [119]: fruits
Out[119]: ['banana', 'red', 'green']
```
## 존재여부 확인 (in)
```python
In [120]: 'red' in fruits
Out[120]: True
In [121]: 'mango' in fruits
Out[121]: False
```
## 값 세기(count)
```python
In [122]: fruits.append('red')
In [123]: fruits.append('red')
In [124]: fruits.count('red')
Out[124]: 3
In [125]: fruits
Out[125]: ['banana', 'red', 'green', 'red', 'red']
```
## 정렬하기(sort, sorted)

* sort는 리스트 자체를 정렬
* sorted는 리스트의 정렬 복사본을 반환

## 리스트 복사(copy)

* copy함수
* list함수
* 슬라이스 연산[:]

# 튜플
튜플은 리스트와 비슷하나, 정의 후 내부 항목의 삭제나 수정이 불가능하다.

## 튜플 생성
```python
In [127]: color = 'red',
In [128]: fruits = 'apple', 'banana'
In [130]: fruits
Out[130]: ('apple', 'banana')
In [132]: color
Out[132]: ('red',)
```
튜플을 정의할 때는 괄호가 없어도 무관하나, 괄호로 묶는것이 좀 더 튜플임을 구분하기 좋다.<br>
또한, 튜플의 요소가 1개일 때는 요소의 뒤에 쉼표(,)를 붙여야 한다.

## 튜플 언패킹
```python
In [133]: f1,f2 = fruits
In [134]: f1
Out[134]: 'apple'
In [135]: f2
Out[135]: 'banana'
```
## 튜플을 사용하는 이유
* 리스트보다 적은 메모리 사용
* 정의후에는 변하지 않는 내부 값

# 실습
1. 문자열 'Fastcampus'를 리스트, 튜플 타입으로 형변환하여 새 변수에 할당한다.
```python
In [136]: list_type =list ('Fastcampus')
In [137]: list_type
Out[137]: ['F', 'a', 's', 't', 'c', 'a', 'm', 'p', 'u', 's']
In [138]: tuple_type = ('Fastcampus',)
In [139]: tuple_type
Out[139]: ('Fastcampus',)
```
2. 1번에서 할당한 리스트, 튜플 변수를 이용해 다시 문자열을 만든다.
```python
In [142]: ''.join(list_type)
Out[142]: 'Fastcampus'
In [143]: ''.join(tuple_type)
Out[143]: 'Fastcampus'
```
