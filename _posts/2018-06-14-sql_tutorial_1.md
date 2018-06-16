---
title: SQL tutorial - 1
description: <center>SQL tutorial</center>  <center>-개인으로 공부하는거라 사실과 다를 수 있음.-<center>
categories:
 - SQL
tags:
---

# SQL tutorial - 1
---
**SQL 이란?**

* 구조화된 커리언어
* SQL을 이용하여 데이터베이스에 엑세스하고 조작 할 수 있다.

## SQL Syntax

데이터베이스에서 행하는 대부분은 SQL 문으로 된다.  
Ex)

```python
SELECT * FROM Customers;
```

SQL 키워드는 **대소문자를 구분하지 않는다.** SELECT와 select는 같은 키워드이다.  
SQL 문에 끝에는 `;(세미콜론)`이 필요하다.

**SQL 명령어**

| 명령어 | 설명 |
|:----:|:----|
| SELECT | 데이터베이스 데이터를 추출 |
| UPDATE | 데이터베이스 데이터를 업데이트 |
| DELETE | 데이터베이스 데이터를 삭제 |
| INSERT INTO | 새로운 데이터를 데이터베이스에 삽입 |
| CREATE DATABASE | 새 데이터베이스 만듬 |
| ALTER DATABASE | 데이터베이스 수정 |
| CREATE TABLE | 새 테이블 만듬 |
| ALTER TABLE | 테이블 수정 |
| DROP TABLE | 테이블 삭제 |
| CREATE INDEX | index(검색 키) 작성 |
| DROP INDEX | index 삭제 |

## SELECT
---
데이터베이트에서 데이터를 선택하는 데 사용한다.

```python
SELECT column1, column2, ...
FROM table_name;
```
column1, column2는 데이터를 선택할 테이블 필드의 이름이다.  
데이터베이스에서 사용 가능한 모든 필드를 선택하기 위해서는 아래와 같이 사용한다.

```python
SELECT * FROM table_name;
```

**SELECT DISTINCT**

SELECT DISTINCT는 고유의 값 즉 중복 값을 포함하지 않고 값을 넘겨주게 된다.

```python
SELECT DISTINCT column1, column2, ...
FROM table_name;
```
## WHERE

WHERE은 레코드를 필터링 하는데 사용한다.  
지정된 조건을 충족하는 레코드 만을 추출한다.
WHERE은 SELECT만이 아닌 UPDATE, DELETE에서도 사용된다.

```python
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

전체 테이블에서의 조건에 충족하는 레코드 만을 추출하고 싶다면 아래와 같이 사용한다.

```python
SELECT * FROM table_name
WHERE condition;
```

WHERE 연산자

| Operator |	Description |
|:--------:|:------------:|
| `=` |	Equal |
| `<>` |	Not equal(다른 SQL 버전에서는 `!=`를 사용하기도 함) |
| `>` |	Greater than |
| `<` |	Less than |
| `>=` |	Greater than or equal |
| `<=` |	Less than or equal |
| BETWEEN |	Between an inclusive range |
| LIKE |	Search for a pattern |
| IN |	To specify multiple possible values for a column |

## AND, OR, NOT

**AND**

```python
SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2 AND condition3 ...;
```

**OR**

```python
SELECT column1, column2, ...
FROM table_name
WHERE condition1 OR condition2 OR condition3 ...;
```

**NOT**

```python
SELECT column1, column2, ...
FROM table_name
WHERE NOT condition;
```

## ORDER BY
---

결과의 집합을 오름차순 또는 내림차순으로 설정할 떄 사(기본적으로는 오름차순으로 설정)

```python
SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC;
```
위의 코드에서 `ASC`는 오름차순 `DESC`는 내림차순 이다.

## INSERT INTO
---

테이블에 새 레코드를 삽입하는데 사용한다. 삽입하는데는 두가지 방법이 있다

1. 삽입 할 열 이름과 값을 모두 지정
```python
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

2. 모든 열의 값을 추가하는 경우
```python
INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```

첫번째 방법의 경우 `ID`에 해당하는 값은 자동으로 증가하지만 포함되어 있지 않은 값은  `null`값으로 처리된다.  
두번쨰의 경우 해당 값을 전부 입력해야 하기 때문에 `ID`값 또한 입력해야한다.

`null`값은 필드에 값이 없는것을 의미한다. 이 `null`값은 비교연산자(`>`,`<`,`=`)는 사용이 안되며  
비교하기 위해서는 `IS NULL`또는 `IS NOT NULL`로 비교 가능하다.

## UPDATE
---

UPDATE의 경우 테이블의 기존의 레코드를 수정하는데 사용한다.

```python
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

`WHERE`문을 사용하여 해당 조건에 맞는 값만 수정할 수 있다. 하지만 `WHERE`값을 넣어주지 않고 할 경우 모든 값이 바뀌어 버리니 주의 하여야 한다.

## DELETE
---

기존의 테이블의 레코드 값을 삭제하는데 사용한다.

```python
DELETE FROM table_name
WHERE condition;
```

**`WHERE`을 생략할 경우 모든 레코드 값이 사라지니 주의 해야한다.**

모든 레코드 삭제의 경우 아래의 코드처럼 입력한다.

```python
DELETE FROM table_name;
```
또는
```python
DELETE * FROM table_name;
```

## SELECT TOP
---

리턴 할 레코드의 수를 지정하는데 사용한다. 큰 테이블에서 유용하나 레코드의 수가 많으면 성능에 영향이 미칠 수 있다.  
>모든 데이터베이스 시스템이 SELECT TOP을 지원하는 것은 아니다. MYSQL은 LIMIT, Oracle은 ROWNUM을 지원한다.

SQL Server / MS Access

```python
SELECT TOP number|percent column_name(s)
FROM table_name
WHERE condition;
```

MySQL

```python
SELECT column_name(s)
FROM table_name
WHERE condition
LIMIT number;
```

Oracle

```python
SELECT column_name(s)
FROM table_name
WHERE ROWNUM <= number;
```

## MAX, MIN
---

`MIN()`의 경우 선택된 column의 가장 작은 값을, `MAX()`는 가장 큰 값을 반환한다.

```python
SELECT MIN(column_name)
FROM table_name
WHERE condition;
```
```python
SELECT MAX(column_name)
FROM table_name
WHERE condition;
```

## COUNT, AVG, SUM
---

COUNT

```python
SELECT COUNT(column_name)
FROM table_name
WHERE condition;
```

AVG

```python
SELECT AVG(column_name)
FROM table_name
WHERE condition;
```

SUM

```python
SELECT SUM(column_name)
FROM table_name
WHERE condition;
```

## LIKE
---

`LIKE`는 `WHERE`문 안에서의 지정된 패턴을 검색하는데 사용한다.

* `%` -> 0 또는 1 (정규표현식의 `*`과 비슷)
* `_` -> 하나의 문자 (MS Access는 `_`대신 `?`를 사용)

| LIKE Operator |	Description |
|:-------------:|:-----------:|
| WHERE CustomerName LIKE 'a%' | 'a'로 시작하는 모든 값 |
| WHERE CustomerName LIKE '%a' |	'a'로 끝나는 모든 값 |
| WHERE CustomerName LIKE '%or%' |	중간에 'or'이 이는 모든 값 |
| WHERE CustomerName LIKE '_r%' |	문자하나 뒤에 r로 시작하는 모든 값 |
| WHERE CustomerName LIKE 'a_%_%' |	'a'로 시작하고 길이가 3자 이상인 모든 값 |
| WHERE ContactName LIKE 'a%o' |	'a'로 시작하고 'o'로 끝나는 모든 값 |
