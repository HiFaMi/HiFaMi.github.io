---
title: Queryset API
description: <center>Queryset API</center>  <center>-개인으로 공부하는거라 사실과 다를 수 있음.-<center>
categories:
 - Django
tags:
---

# Queryset API

`models_class_name.objects.all()` - 데이터베이스의 모든 값을 Queryset 형식으로 반환

`len()` - 길이를 반환

`count()` - 테이블의 레코드 수를 반환

`list(models_class_name.objects.all())` - Queryset을 리스트 형식으로 반환

`bool()` -적어도 한개 이상의 경우가 있을 경우 사용(하나의 결과 만 존재하는지 찾을 경우에는 `exists()`가 더 효율적)

`pickle` - 모든 결과가 메모리에 강제적으로 로드  
Ex)
```python
import pickle
query = pickle.loads(s)   
qs = MyModel.objects.all()
qs.query = query          
```

`filter()` - 지정된 매개변수와 일치 하는 객체를 반환

`exclude()` - 지정된 매개변수를 제외한 나머지 값을 반환

`annotate()` - 각 개체에 쿼리식을 목록으로 주석을 추가

`order_by()` - 주어진 순서에 의해 정렬(`-`의 경우 내림차순)

`reverse()` - Queryset이 역순으로 반환

`distinct()` - 중복을 제거하여 반환

`values()` - 인스턴스로 반환하는 것이 아닌   `dict`타입으로 반환

`values_list()` - `dict`타입 대신 튜플을 반환

`dates(field, kind, order='ASC')` - 특정 종류의 모든 날짜를 반환  

* `year` - 모든 연도 값의 목록을 반환
* `month` - 모든 연도 / 월 값의 목록을 반환
* `day` - 모든 연도 / 월 / 일 값의 목록을 반환

`datetimes(field_name, kind, order = 'ASC', tzinfo = None)` - 특정 종류의 모든 날짜를 반환

`none()` - 빈 `Queryset`을 반환하는 새로운 `Queryset`이 만들어짐

```python
Entry.objects.none()
>><QuerySet []>
from django.db.models.query import EmptyQuerySet
isinstance(Entry.objects.none(), EmptyQuerySet)
>>True
```

`union(*other_qs, all='False')` - 두 개 이상의 `Queryset`을 결합

`intersection(*other_qs)` - 두 개 이상의 공유 요소를 반환

`difference(*other_qs)` - 두 개 이상과 다른 요소를 반환

`extra(elect = None , where = None , params = None , tables = None , order_by = None , select_params = None )` - `sql`의 `WHERE`절을 간단하게 표

`only(*field)` - `field`값만 우선 호출

`using()` - 별명 설정(두 개 이상의 데이터베이스를 사용하는 경우 유용)

`select_for_update(nowait = False, skip_locked = False, of())` - transaction이 끝날 때까지 행을 잠그게 된다.

`raw( raw_query , params = None , translations = None )` - `django.db.models.query.RawQuerySet`인스턴스를 반환

**QuerySets를 돌려주지 않는 메소드**

`get()` - 지정된 매개변수와 일치하는 값을 반환

`create()` - 객체를 작성해 저장까지 하는 메소드

`get_or_create()` - `get()`으로 호출 하였을 때 없는 경우에는 그 값을 가지고 `create()`하게 된다.

`update_or_create()` - `get()`으로 해당 조건을 찾고 그 값이 있을 경우 새로운 값으로 `update()`되고 없는 경우에는 `create()`한 다음 `update()`된다.

`bulk_create(objs, batch_size = None)` - 객체 목록을 효율적인 방법으로 데이터베이스에 삽입

**주의사항**
* 모델의 `save()`메서드는 호출되지 않고 `pre_save`및 `post_save`신호는 전송되지 않는다.
* 다중 테이블 상속 시나리오에서 하위 모델에서는 작동하지 않는다.
* 모델의 기본 키가 `AutoFieldtrue save()`이면 데이터베이스 백엔드가 지원하지 않는 한 (현재 `PostgreSQL`) 기본 키 속성을 검색 및 설정하지 않는다 .
* 다 대다 관계에서는 작동하지 않는다.

`count()` - 데이터베이스의 객체 수를 반환

`in_bilk(id_list = None, field_name = 'pk')` - 필드 값(`id_list`) 및 해당 값에 대한 목록을 가져와 `field_name` 지정된 값으로 객체의 인스턴스 값을 반환

`latest(*field)`, `earliest(*field)` - 테이블의 최신 객체를 반환

`first()` - `QuerySet`와 일치하는 첫번째 객체를 반환, 없을경우 `None`값을 반환

`last()` - `first()`와 동일하지만 마지막 객체를 반환

`aggregate( * args , ** kwargs )` - 계산된 평균, 합계등을 `dict`값으로 반환

`exists()` - 결과를 포함하고 있는 경우 `True`값을 반환

`update()` - 지정된 필드에 대해 `SQL` 업데이트 쿼리를 수행하고 일치하는 행 수를 반환한다. 일부 행에 이미 새 값이있는 경우 업데이트 된 행 수와 다를 수 있다.

`delete()` - 삭제를 수행하고 삭제된 `QuerySet`의 개체 수 및 삭제 당한 인스턴스를 `dict`형식으로 보여줌

**Field 조회**

`exact` - 정확히 일치(값이 `None`일 경우 `Null`값으로 해석된다.)

`iexact` - 대소문자를 구분하지 않는 값의 일치를 비교(값이 `None`일 경우 `Null`값으로 해석된다.)

`contains` - 대소문자를 구분하여 값의 일치를 비교

`icontains` - 대소문자를 구별하지 않고 값을 비교

`in` - `in`에 해당하는 값을 반환

**비교**

|   표현식     |    설명    |
|:----------:|:--------:|
|    `gt`    |    보다 큰    |
|    `gte`    |    크거나 같음   |
|    `lt`    |    미만    |
|    `lte`    |    보다 작거나 같음    |

`startswith` - 대소문자를 구분하여 시작

`istartswith` - 대문자와 소문자 구분하지 않고 끝남

`endswith` - 대소문자 구분하면서 끝남

`iendswith` - 대소문자 구분하지 않고 끝남

`range` - 범위

`date` - 날짜 시간 필드의 경우, 값을 날짜로 변환

`year` - 해당하는 년에 값을 반환

`month` - 해당하는 달의 값을 반환

`day` - 해당하는 날짜의 값을 반환

`week` - 날짜 및 시간 필드의 경우 주 번호를 반환

`week_day` - 요일과 일치하는 값을 반환

`quarter` - 분기의 값을 반환

`time` - `datetime`필드의 경우 값을 시간으로 변환

`hour` - 일치하는 시간에 해당하는 값을 반환

`minute` - 일치하는 분에 해당하는 값을 반환

`second` - 일치하는 초에 해당하는 값을 반환

`isnull` - 값이 없는 경우 `True`값을 반환

`regex` - 대소문자를 구분하는 정규식의 일치를 판단

`iregex` - 대소문자를 구분하지 않는 정규식의 일치를 판단
