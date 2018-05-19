---
title: Python Setting
description: <center>pyenv에서 python 설치하기</center><br><center>-이 글은 fastcampus에서의 수강 후 쓴 글 입니다.-<center>
categories:
 - Set
tags:
---


## Pyenv 설치

python의 버전을 따로 관리할 수 있도록 도와주는 라이브러리이다. python 버전간의 충돌을 막아주기 위해 설치하고 사용한다.<br>
`brew install pyenv`<br>
`brew install pyenv-virtualenv`<br>
아래의 `virtualenv`의 경우 pyenv를 사용하기 쉽게 virtualenv를 사용할 수 있도록 만든 라이브러리 이다.


## Pyenv 설정
설치 후 pyenv 관련 설정을 shell 설정에 추가 <br>
`vi ~/.zshrc`를 이용해서 연 다음 그 문서 제일 마지막에 아래와 같은 문구를 넣는다.<br>
```c
export PYENV_ROOT=/usr/local/var/pyenv
if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi
```
shell의 설정을 기록 후 터미널을 재시작 하거나 `source ~/.zshrc` 또는 `source ~/.zshrc_profile`을 실행

파이썬 설치 전에 관련 유틸리티를 설치한다.(readline, xz)
```c
brew install readline xz
```
pyenv를 사용하여 파이썬 3.6.5버전 설치
```c
pyenv install 3.6.5
```

## Pyenv 사용

가상환경 생성을 위해 아래의 형식과 같이 입력한다.<br>
`pyenv virtualenv <version> <env_name>`
```c
pyenv virtualenv 3.6.5 fc-python
```
사용할 폴더로 이동
```c
cd project
mkdir python
cd python
```
Tip: `take python`을 하게되면 python폴더 생성과 동시에 위치가 python폴더로 이동한다.<br>

local에 가상환경 지정<br>
`pyenv local fc-python`<br>
-가상환경 지우기<br>
`pyenv uninstall <env_name>`

## Ipython
기본 파이썬 셸보다 다양한 기능을 사용할 수 있도록 해주는 셸을 제공해준다.

## Ipython 설치
`pip install ipython`<br>
커맨드라인에서 `ipython`을 입력하여 실행
