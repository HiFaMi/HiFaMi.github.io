---
title: Programmers coding test hash 2
description: <center> Programmers coding test hash 2 </center>
categories:
 - Algorithm
tags:
 - Programmers
 - algorithm
---

## 전화번호 목록

### 문제설명
전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.

* 구조대 : 119
* 박준영 : 97 674 223
* 지영석 : 11 9552 4421

전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.

### 제한사항
* phone_book의 길이는 1 이상 1,000,000 이하입니다.
* 각 전화번호의 길이는 1 이상 20 이하입니다.

### 입출력 예제

|phone_book|	return|
|:-------:|:--------:|
|[119, 97674223, 1195524421]|	false|
|[123,456,789]|	true|
|[12,123,1235,567,88]|	false|

### 입출력 설멍

* 입출력 예 #1
앞에서 설명한 예와 같습니다.

* 입출력 예 #2
한 번호가 다른 번호의 접두사인 경우가 없으므로, 답은 true입니다.

* 입출력 예 #3
첫 번째 전화번호, “12”가 두 번째 전화번호 “123”의 접두사입니다. 따라서 답은 false입니다.

### 풀이

```python
def solution(phone_book):
    phone_book.sort()
    for i in range(1, len(phone_book)):
        if phone_book[0] == phone_book[i][:len(phone_book[0])]:
          return False
    return True
```
가장 작은 숫자가 접두사로 추가되는거 같다. 따라서 `sort()`를 통해 `phone_book`을 정렬한 후
접두사가 들어있는 경우만 판단하면 되기 떄문에 `indexing`을 이용해서 비교하고 만약 있을경우
`False`를 리턴하고 없을경우 `True`를 리턴한다.

```python
def solution(phone_book):
    phone_book = sorted(phone_book)

    for p1, p2 zip(phone_book, phone_book[1:]):
        if p2.startswith(p1):
            return False
    return True

```

`startswith`로 `p1`의 문자열이 `p2`에 있을 경우 `True`를 리턴하고 아닐경우에는 `False`를
리턴한다.  
