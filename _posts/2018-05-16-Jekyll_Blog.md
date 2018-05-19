---
title: Jekyll 블로그
description: <center>rbenv환경에서 jekyll 블로그 생성하고 GitHub에 배포하기</center><br><center>-이 글은 fastcampus에서의 수강 후 쓴 글 입니다.-<center>
categories:
 - Set
tags:
---


## Homebrew 설치
```c
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install
/master/install)"
```
위의 코드를 터미널에 입력하여 Homebrew를 설치하여준다.<br>
이미 Homebrew가 설치되어 있을 경우 ```update homebrew```를 입력하여 최신버전으로 업데이트 해준다.

## rbenv 설치

`brew install rbenv ruby-bild`를 입력하여 rbenv를 설치한다.

## rbenv를 위한 설정을 셸 설정파일에 추가

`zsh`를 이용할 경우 `~/.zshrc`, 기본 `bash`를 쓰는경우 `~/.bash_profile`에 작성한다.<br>
ex) `vi .zshrc`, `vi .bash_profile` 또는 `open .zshrc`, `open .bash_profile`를 입력하여 수정


```c
# rbenv
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(rbenv init -)"
```
설정파일을 작성하고 저장 한 후 새 터미널을 열어준다.<br>

## Ruby 설치

rbenv를 이용하여 ruby를 설치하고, 사용할 버전을 지정한다.
```c
rbenv install 2.4.1
rbenv global 2.4.1
rbenv version
  system
*2.4.1(set by /Users/mac/.rbenv/version)
```
`*`은 적용되어 있는 버전을 보여준다  

Ruby 설치 후 `rehash` 작업을  `rbenv rehash`를 입력하여 실행하여 준다.<br>
rehash는 rbenv가 관리하는 루비 명령어들을 `~/.rbenv/shims`디렉토리에 셸 스크립트 파일로 복사해주는 역할을 한다.

## RubyGems, Gem, bundler

RubyGems는 Ruby패키지 관리자이며, 각 패키지는 Gem이라고 불린다. 설치해야 할 Gem은 jekyll과 bundler, github-pages이다.
설치코드는 아래와 같다.
```c
gem install jekyll bundle github-pages
```
## Jekyll 블로그 생성 후 로컬 실행

위에서 필요한 `gem`을 설치하였다면 이제 jekyll블로그를 생성할 차례이다.<br>
`jekyll`블로그를 생성하고 싶은 곳의 상위 폴더에서 아래의 코드를 실행시키면 된다.
```c
➜jekyll new 블로그명
➜cd 블로그명
ls -al
```
위에 나온 코드대로 실행하였다면 아래와 같은 목록이 나올것이다.
```c
➜ls -al
total 56
drwxr-xr-x  10 mac  staff   340  5 16 18:25 .
drwxr-xr-x   3 mac  staff   102  5 16 18:25 ..
-rw-r--r--   1 mac  staff    35  5 16 18:25 .gitignore
-rw-r--r--   1 mac  staff   398  5 16 18:25 404.html
-rw-r--r--   1 mac  staff  1039  5 16 18:25 Gemfile
-rw-r--r--   1 mac  staff  1692  5 16 18:25 Gemfile.lock
-rw-r--r--   1 mac  staff  1652  5 16 18:25 _config.yml
drwxr-xr-x   3 mac  staff   102  5 16 18:25 _posts
-rw-r--r--   1 mac  staff   539  5 16 18:25 about.md
-rw-r--r--   1 mac  staff   175  5 16 18:25 index.md
```
jekyll패키지 대신 `github-page`를 사용하도록 `gemfile`의 내용을 수정하여준다.
`gem "jekyll", "~> 3.8.1"`부분을 주석처리<br>
`# gem "github-pages", group: :jekyll_plugins`부분의 주석을 해제<br>
하여 아래와 같게 만들어준다.
```c
source "https://rubygems.org"

# Hello! This is where you manage which Jekyll version is used to run.
# When you want to use a different version, change it below, save the
# file and run `bundle install`. Run Jekyll with `bundle exec`, like so:
#
#     bundle exec jekyll serve
#
# This will help ensure the proper Jekyll version is running.
# Happy Jekylling!
#gem "jekyll", "~> 3.8.1"

# This is the default theme for new Jekyll sites. You may change this to anything you like.
gem "minima", "~> 2.0"

# If you want to use GitHub Pages, remove the "gem "jekyll"" above and
# uncomment the line below. To upgrade, run `bundle update github-pages`.
 gem "github-pages", group: :jekyll_plugins

# If you have any plugins, put them here!
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.6"
end
```
저장하고 난 다음 실행하기 전에 `bundle`로 관리되는 패키지를 업데이트 시켜준다.

```c
bundle install
bundle update
```
만약 install시 오류 메세지가 보인다면 `bundle update`를 먼저 실행 후 `bundle install`을 다시한번 실행한다.<br>
실제 정적 사이트를 생성하고, 테스트를하기 위한 로컬 서버를 실행한다.
```c
bundle exec jekyll serve
```

실행 후 <http://127.0.0.1:4000>로 접속하면 아래와 같이 생성된 사이트를 볼 수 있다.

<img src="{{ site.url }}/assets/images/blog_test.png" alt="블로그 테스트">
