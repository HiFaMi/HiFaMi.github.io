---
title: Django allauth
description: <center> 1. Django allauth </center>
categories:
 - Project
tags:
 - Django
 - django-allauth
---

Django 프로젝트 중에 `django-allauth`를 사용하여 소셜 로그인을 구현하려 한다.

`poetry`를 사용하기 때문에 아래처럼 작성하여 `django-allauth`를 다운받아 준다.
```python
poetry add django-allauth
```


`settings.py`에서 `INSTALLED_APPS`에 아래의 항목을 추가하여 준다
```python
    'allauth',
    'allauth.account',
    'allauth.socialaccount',

    'allauth.socialaccount.providers.github',
    'allauth.socialaccount.providers.kakao',
    'allauth.socialaccount.providers.google',
    'allauth.socialaccount.providers.discord',
```
그 다음에
```python
python manage.py migrate
```
를 입력하면 `django admin` 페이지에 소셜에 관련된 것이 추가되어 있는것을 볼 수 있다.

이제 `guthub`, `kakao`등과 같은 사이트에 접속하여 `Client key`, `Secret key`를
발급 받아 `django admin`페이지의 `SocialApplication` 항목에 추가시켜주면 된다.
(`kakao`의 경우 `Secret key`없이 `Client key`만 입력하여주면 된다.)

그 다음 `templates`에 `login`에 대한 `html`파일을 만든 후

```python
{% load socialaccount %}
<a href="{% provider_login_url '<social>' method='oauth2' %}"></a>
```
위의 코드와 같이 입력하면 된다. 꼭 `{% load socialaccount %}`를 처음줄에 입력하여야한다.

ex)
```python
{% load socialaccount %}

<a href="{% provider_login_url 'kakao' method='oauth2' %}"></a>
<a href="{% provider_login_url 'github' method='oauth2' %}"></a>
<a href="{% provider_login_url 'google' method='oauth2' %}"></a>
<a href="{% provider_login_url 'discord' method='oauth2' %}"></a>
```

