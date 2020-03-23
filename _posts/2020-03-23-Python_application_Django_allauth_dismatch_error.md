---
title: Python application Django allauth dimatch error
description: <center>1. Django allauth dismatch</center>
categories:
 - Project
tags:
 - error
 - Django
 - Nginx
 - django-allauth
---

사이트의 구성은 `Nginx <-> gunicorn <-> Django` 이다.

사이트를 구성하는 도중에 `django-allauth`를 사용하여 `github`를 이용하여 로그인을 하도록
구성하였다. 하지만 사용도중 `500 internal server error`가 일어나고 이 문제를 해결해도
`Authorization callback URL`이 `mismatch` 되었다고 오류가 나와 이 문제를 해결한걸
정리해서 올린다.

### 500 internal server error

이 문제의 경우 `SITE_ID`를 잘못 지정해준 문제였다.

```python
from django.contrib.sites.models import Site
>>>Site.objects.all()
<QuerySet [<Site: example.com>, <Site: http://localhost:8000/>]>
>>> site = Site.objects.first()
>>> site.id
1
```

위의 코드에서와 같이 `Site`에 대한 `QuerySet`이 나오는것을 볼 수 있다.
`SITE_ID`의 경우 `Site`에 대한 `PK`의 값이고 이를 지정하는 것이다.

### Callback url mismatch

이 경우에는 `github`의 `Developer Setting`에서의 `Oauth Apps`에서 제대로 `callback url`을 지정하였는데도 `mismatch`가 나오는 오류였다.

이 오류에 관해 찾아본 결과

<a href='https://stackoverflow.com/a/19991275'>Stack overflow 원문</a>

```
I found that the issue occurs because the nginx proxy, which sits in front of the python app server, sets the HTTP Host header to localhost.
```

위의 링크를 타고 들어가면 원문을 확인 할 수 있다.
`header`를 `domain`이 아닌 `localhost`로 잡고있기 때문에 이러한 `mismatch`가 일어난다고 한다.

따라서 `nginx`의 설정에 아래와 같은 구문을 추가하였다.

```python
    location / {
            proxy_set_header HOST $http_host;
        }
```

`header`를 `host domain`으로 설정하여 제대로 접근하도록 하였다.