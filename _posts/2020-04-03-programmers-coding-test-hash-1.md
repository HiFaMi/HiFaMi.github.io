---
title: Programmers coding test hash 1
description: <center> Programmers coding test hash 1 </center>
categories:
 - Project
tags:
 - Programmers
 - algorithm
---


## 1.완주하지 못한 선수

### 문제설명
수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

### 제한사항

* 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
* completion의 길이는 participant의 길이보다 1 작습니다.
* 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
* 참가자 중에는 동명이인이 있을 수 있습니다.

### 입출력 예


|participant|completion|return|
|:-----:|:-----:|:-----:|
|[leo, kiki, eden] |	[eden, kiki]|	"leo" |
|[marina, josipa, nikola, vinko, filipa]|	[josipa, filipa, marina, nikola]	|"vinko"|
|[mislav, stanko, mislav, ana]|[stanko, ana, mislav]	|"mislav"|

### 입출력 예 설명
* 예제 #1
leo는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

* 예제 #2
vinko는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

* 예제 #3
mislav는 참여자 명단에는 두 명이 있지만, 완주자 명단에는 한 명밖에 없기 때문에 한명은 완주하지 못했습니다.

### 풀이

```python
def solution(participant, completion):
    for person in completion:
        participant.remove(person)

    return participant[0]
```

이 방법의 경우에는 테스트 케이스는 다 통과하지만 효율성에서는 다 실패한다.  
`remove`가 앞에서부터 탐색하기 때문에 만약 `person`이 `participant`의 마지막에 위치하고
있다면 제일 뒤에까지 탐색해야 하기 때문이다.

```python
  def solution(participant, completion):
    participant.sort()
    completion.sort()

    for i in range(len(completion)):
      if participant[i] != completion[i]:
        return participant[i]
    return participant[-1]
```
위의 방법은 테스트 케이스와 효율성 둘 다 통과하였다. `sort()`를 이용하여 `list` 내에서
알파벳순으로 정렬을 시킨 후 조건에서 "항상 `completion`의 길이는 `participant`의 길이보다 1이 작다."
를 이용하여 `completion`의 길이로 `for`루프를 돌려 만약 같지 않을떄 `participant`의 값을 리턴하고
만약 없을 경우 `participant`의 마지막 값이기 때문에 마지막 값을 `return`한다.

첫번째의 경우는 `sort()`를 한다고 해도 `remove`가 리스트를 전체를 다 도는 `for`와 같기 때문에
복잡도가 `n^2`이 된다고 한다.

```python
from collections import Counter
    def solution(participant, completion):
      answer = Counter(participant) - Counter(completion)

      return list(answer.keys())[0]
```

위의 경우는 `collections`의 `Counter`를 사용한 경우이다.  
이 경우 `Counter`는 테스트 1의 경우 `	Counter({'leo': 1, 'kiki': 1, 'eden': 1})`와 같이 나타난다.
리스트 안의 중복인 값을 `key`로 중복 횟수를 `value`값으로 보여준다. `Counter`의 흥미로운 점은 연산이 된다는 점이다. 그래서 `Counter(participant) - Counter(completion)`을 하게 되면 같은 `key`에 대한 `value`값을 빼주게 된다. 따라서 하나의 값만 남아있게되기 때문에 그 값을 `list`로 변환한 후 `return`해준다.(가장 좋은 방법이라고 생각된다.)
