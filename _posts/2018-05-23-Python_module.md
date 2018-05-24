---
title: Python 모듈
description: <center>python function</center><br><center>-이 글은 fastcampus에서의 수강 후 쓴 글 입니다.-<center>
categories:
 - python
tags:
---
# 모듈
지금까지 셸에서 진행한 실습의 경우, 하나의 모듈 내부에서 작업한 것으로 취급된다.<br>
파이썬 파일은 각각 하나의 모듈로 취급되며, 실행이나 함수의 정의, 단순 변수의 모음 등등 여러 역할을 한다.

## 모듈 불러오기(import)
기본 모듈에서 부가적인 기능들을 불러와서 사용하는 형태로 코드를 작성한다.<br>
**module/shop.py**
```python
def buy_item():
  print('Buy item!')

buy_item()
```

**module/game.py**
```python
def play_game.py:
  print('Play game!')

play_game()
```

**module/lol.py**
```python
import game
import shop

print('= Turn on game =')
game.play_game()
shop.buy_item()
```

## __name__변수
`lol.py`가 실행될 떄, `game`과 `shop`이 import되는 순간 해당 코드가 실행되어 버리는 문제가 있다.<br>
이 때, 파이썬 인터프리터를 이용해 실행한 코드인지를 확인하여 단순히 `import`한 모듈의 경우 실행을 막는 방식을 사용할 수 있다.<br>
각 모듈은 자신의 이름을 가지며, 모듈 이름은 모듈의 전역변수 `__name__` 에서 확인 할 수 있다.

```python
print(__name__)
```
파이썬 인터프리터가 실행한 모듈의 경우, `__main__`이라는 이름을 가진다. 따라서 `python <파일명>`으로 실행한 경우에만 동작할 부분은 if문으로 감싸준다.<br>

**module/shop.py**
```python
def buy_item():
  print('Buy item!')

if __name__ == '__main__':
  buy_item()
```

**module/game.py**
```python
def play_game():
  print('Play game!')

if __name__ == '__main__':
  play_game()
```
## lol.py 리펙토링

```python
import game
import shop

def turn_on():
    print('= Turn on game =')

    while True:
        choice = input('What would you like to do?\n  1: Go to Shop, 2: Play Game, 0: Exit\n    Input : ')
        if choice == '0':
            break
        elif choice == '1':
            shop.buy_item()
        elif choice == '2':
            game.play_game()
        else:
            print('Choice not exist')
        print('-----------------------')

    print('= Turn off game =')

if __name__ == '__main__':
    turn_on()
```
    
