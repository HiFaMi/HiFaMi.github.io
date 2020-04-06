---
title: Programmers coding test stack/queue 2
description: <center> Programmers coding test stack/queue 2 </center>
categories:
 - Algorithm
tags:
 - Programmers
 - algorithm
---

## 다리를 지나는 트럭

### 문제설명

트럭 여러 대가 강을 가로지르는 일 차선 다리를 정해진 순으로 건너려 합니다. 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 알아내야 합니다. 트럭은 1초에 1만큼 움직이며, 다리 길이는 `bridge_length`이고 다리는 무게 `weight`까지 견딥니다.
※ 트럭이 다리에 완전히 오르지 않은 경우, 이 트럭의 무게는 고려하지 않습니다.

예를 들어, 길이가 2이고 10kg 무게를 견디는 다리가 있습니다. 무게가 `[7, 4, 5, 6]kg`인 트럭이 순서대로 최단 시간 안에 다리를 건너려면 다음과 같이 건너야 합니다.

|경과 시간|	다리를 지난 트럭	|다리를 건너는 트럭	|대기 트럭|
|:-------:|:--------------:|:----------------:|:------:|
|0|	[]|	[]	|[7,4,5,6]|
|1~2|	[]|	[7]|	[4,5,6]|
|3|	[7]	|[4]	|[5,6]|
|4	|[7]|	[4,5]|	[6]|
|5	|[7,4]|	[5]	|[6]|
|6~7|	[7,4,5]|	[6]|	[]|
|8	|[7,4,5,6]|	[]|	[]|

따라서, 모든 트럭이 다리를 지나려면 최소 8초가 걸립니다.

`solution` 함수의 매개변수로 다리 길이 `bridge_length`, 다리가 견딜 수 있는 무게 `weight`, 트럭별 무게 `truck_weights`가 주어집니다. 이때 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 `return` 하도록 `solution` 함수를 완성하세요.

### 제한조건

- bridge_length는 1 이상 10,000 이하입니다.
- weight는 1 이상 10,000 이하입니다.
- truck_weights의 길이는 1 이상 10,000 이하입니다.
- 모든 트럭의 무게는 1 이상 weight 이하입니다.

### 입출력 예

|`bridge_length`|	`weight`|	`truck_weights`|	`return`|
|:-----------:|:------:|:----------:|:--------:|
|2|	10|	[7,4,5,6]|	8|
|100|	100|	[10]|	101|
|100|	100|	[10,10,10,10,10,10,10,10,10,10]|	110|

### 풀이

1.
```python
def solution(bridge_length, weight, truck_weights):
    q=[0]*bridge_length
    sec=0
    while q:
        sec+=1
        q.pop(0)
        if truck_weights:
            if sum(q)+truck_weights[0]<=weight:
                q.append(truck_weights.pop(0))
            else:
                q.append(0)
    return sec
```
차가 다리에 올라갈 수 있는 개수는 `bridge_length`가 되기 때문에 그 만큼의 값이 `0`인 빈 리스트를 만든다.
그 다음에 `q`의 값이 존재 할 경우 무한루프를 돌리며 `q`에서 제일 앞의 값을 `pop()`을 이용하여 가져오고 가져오게되면 `sec`의 값이 하나하나 증가하게 된다. 만약 `q`의 총값 즉 `sum(q)`와 `truck_weights`의 첫번째 값의 합이 `weight`를 넘지 않는다면 `truck_weights`의 첫번째 값을 `q`에 `append`시켜주고 아닐 경우 `0`을 넣어준다.

`q`에 대한 값을 테스트1의 경우로 보게되면 아래와 같이 나오게 된다.
```bash
[0, 7]
[7, 0]
[0, 4]
[4, 5]
[5, 0]
[0, 6]
[6]
[]
```

하지만 위의 경우 `sum()`이 `for`문을 도는거기 때문에 시간복잡도가 `n^2`이 되기 때문에 효율성에서는 문제가 생기는 걸로 나타난다.

2.
```python
def solution(bridge_length, weight, truck_weights):
    q=[0]*bridge_length
    sec=0
    sq = 0
    while q:
        sec+=1
        value = q.pop(0)
        if value != 0:
            sq -= value
        if truck_weights:
            if sq+truck_weights[0]<=weight:
                temp = truck_weights.pop(0)
                q.append(temp)
                sq+=temp
            else:
                q.append(0)
    return sec
```
1번째와는 다르게 `sum()`함수를 이용하지 않고 `sq`라는 기본값이 `0`인 변수를 만든 후, 만약 `q.pop(0)`의 값이 0이 아닐경우에는 `sq`에서 값을 빼게되며 아래의 조건문에서 `sq`와 `truck_weights[0]` 값의 합이 `weight`를 안넘길 경우에 `sq`에 값을 더하는 방식으로 `sum()`함수를 대체하였다.
