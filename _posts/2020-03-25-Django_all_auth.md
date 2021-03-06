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

### 설치 및 settings.py

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
그 다음에 `urls.py`에 아래와 같이 입력한다.

```python
urlpatterns = [
    path('accounts/', include('allauth.urls)),
]
```


```python
python manage.py migrate
```
마지막으로 `migrate` 하면 `django admin` 페이지에 소셜에 관련된 것이 추가되어 있는것을 볼 수 있다.

이제 `guthub`, `kakao`등과 같은 사이트에 접속하여 `Client key`, `Secret key`를
발급 받아 `django admin`페이지의 `SocialApplication` 항목에 추가시켜주면 된다.
(`kakao`의 경우 `Secret key`없이 `Client key`만 입력하여주면 된다.)

### template

그 다음 `templates`에 `login`에 대한 `html`파일을 만든 후

{% raw %}
```python
{% load socialaccount %}
<a href="{% provider_login_url '<social>' method='oauth2' %}"></a>
```
{% endraw %}
위의 코드와 같이 입력하면 된다.


ex)
{% raw %}
```python
{% load socialaccount %}

<a href="{% provider_login_url 'kakao' method='oauth2' %}"></a>
<a href="{% provider_login_url 'github' method='oauth2' %}"></a>
<a href="{% provider_login_url 'google' method='oauth2' %}"></a>
<a href="{% provider_login_url 'discord' method='oauth2' %}"></a>
```
{% endraw %}


### django-allauth template custom

`allauth`를 사용하다 보면 `templates`이 기본으로 되어있다. 이러한 `templates`를 `custom`
하기 위해서는 아래와 같이 파일을 만들고

```bash
templates > socialaccount > signup.html
```

`settings.py`

```python
TEMPLATES = {
  'DIR': [
    os.path.join(BASE_DIR, 'templates'),
    os.path.join(BASE_DIR, 'templates', 'socialaccount'),
  ]
}
```
위 처럼 입력하면 된다.

만약 `social login`이 아닌 일반적인 `account login`일 경우

```bash
templates > account > signup.html
```

`settings.py`

```python
TEMPLATES = {
  'DIR': [
    os.path.join(BASE_DIR, 'templates'),
    os.path.join(BASE_DIR, 'templates', 'account'),
  ]
}
```
로 변경 해 주면 된다.
