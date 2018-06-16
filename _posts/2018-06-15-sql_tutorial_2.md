---
title: SQL tutorial - 2
description: <center>SQL tutorial</center>  <center>-개인으로 공부하는거라 사실과 다를 수 있음.-<center>
categories:
 - SQL
tags:
---

# SQL tutorial - 2
## IN
---

`IN` 연산자를 사용하여 `WHERE`절에 여러값을 지정할 수 있다.
`IN` 연산자는 여러 `OR`의 줄임말이다.

```python
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1, value2, ...);
```

또는

```python
SELECT column_name(s)
FROM table_name
WHERE column_name IN (SELECT STATEMENT);
```

`IN`값에서 벗어난 값을 얻기 위해서는 아래와 같이 입력한다.

```python
SELECT column_name(s)
FROM table_name
WHERE column_name NOT IN (value1, value2, ...);
```

## BETWEEN
---
`BETWEEN`은 주어진 범위의 값을 가져온다. 그 값이 텍스트, 숫자, 날짜일 수 있다.  
`BETWEEN`은 시작 값과 끝 값이 존재한다.

```python
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```
범위에 벗어난 값을 사용하기 위해서는 아래와 같은 값을 입력한다.

```python
SELECT column_name(s)
FROM table_name
WHERE column_name NOT BETWEEN value1 AND value2;
```

## Alias

테이블 또는 `column`에 임시로 이름을 지정하는데 사용한다.(python의 as와 비슷함)

열의 경우

```python
SELECT column_name AS alias_name
FROM table_name;
```

테이블의 경우
```python
SELECT column_name(s)
FROM table_name AS alias_name;
```

## JOIN
---

두 개 이상의 테이블에 있는 행을 결합하는데 사용한다.  

* (INNER) JOIN : 두 테이블에서 값이 일치하는 레코드를 반환합니다.
  ```python
  SELECT Orders.OrderID, Customers.CustomerName
  FROM Orders
  INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
  ```
  <img style='border:0' src="{{ site.url }}/assets/images/img_innerjoin.gif" alt="innerjoin" >

* LEFT (OUTER) JOIN : 왼쪽 테이블에서 모든 레코드를 반환하고 오른쪽 테이블에서 일치하는 레코드를 반환합니다.
  ```python
  SELECT column_name(s)
  FROM table1
  LEFT JOIN table2 ON table1.column_name = table2.column_name;
  ```
  <img style='border:0' src="{{ site.url }}/assets/images/img_leftjoin.gif" alt="leftjoin" >

* RIGHT (OUTER) JOIN : 오른쪽 테이블에서 모든 레코드를 반환하고 왼쪽 테이블에서 일치하는 레코드를 반환합니다.
  ```python
  SELECT column_name(s)
  FROM table1
  RIGHT JOIN table2 ON table1.column_name = table2.column_name;
  ```
  <img style='border:0' src="{{ site.url }}/assets/images/img_rightjoin.gif" alt="rightjoin" >

* FULL (OUTER) JOIN : 왼쪽 또는 오른쪽 테이블에 일치하는 항목이 있으면 모든 레코드를 반환합니다.
  ```python
  SELECT column_name(s)
  FROM table1
  FULL OUTER JOIN table2 ON table1.column_name = table2.column_name;
  ```
  <img style='border:0' src="{{ site.url }}/assets/images/img_fulljoin.gif" alt="fulljoin" >


<p style='text-align:right'>출처:https://www.w3schools.com/sql/</p>

## UNION
---

두 개 이상의 SELECT 문의 과 집함을 결합하는데 사용한다.

* UNION 내의 각 SELECT 문은 같은 수의 열을 가져야한다.
* `column`은 유사한 데이터 형식을 가져야한다.
* 각 SELECT 문의 열은 같은 순서로 있어야한다.

UNION
```python
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
```

UNION ALL(UNION은 기본적으로 고유 값만을 선택한다. 중복 허용하기 위해서는 `ALL`을 사용한다.)
```python
SELECT column_name(s) FROM table1
UNION ALL
SELECT column_name(s) FROM table2;
```

## GROUP BY
---

`COUNT`, `MAX`, `MIN`, `SUM`, `AVG`와 함께 사용되어 결과 집합을 하나 이상의 열로 그룹화한다.
```python
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
ORDER BY column_name(s);
```

## HAVING
---

`WHERE`을 aggregate functions와 같이 사용할 수 없기 때문에 `HAVING`을 사용

```python
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING condition
ORDER BY column_name(s);
```

## EXISTS
---

하위 쿼리에 레코드가 있는지를 판단한다. 레코드가 하나 이상일 경우 `True`를 반환한다.

```python
SELECT column_name(s)
FROM table_name
WHERE EXISTS
(SELECT column_name FROM table_name WHERE condition);
```

## ANY, ALL
---
`ANY`, `ALL`은 `WHERE`, `HAVING`과 함꼐 사용한다.  
`ANY`의 경우 하위 쿼리에서 해당하는게 하나라도 있을 경우 `Ture`를 반환한다.  
`ALL`의 경우 하위 쿼리에서 모두 해당하여야 지만 `True`를 반환한다.

**ANY**
```python
SELECT column_name(s)
FROM table_name
WHERE column_name operator ANY
(SELECT column_name FROM table_name WHERE condition);
```

**ALL**
```python
SELECT column_name(s)
FROM table_name
WHERE column_name operator ALL
(SELECT column_name FROM table_name WHERE condition);
```

## SELECT into
---

한 데이터 테이블을 새 테이블로 복사한다.

모든 열을 복사 할 경우 아래의 코드를 사용한다.
```python
SELECT *
INTO newtable [IN externaldb]
FROM oldtable
WHERE condition;
```

일부 열만 새 테이블로 복사하려면 아래의 코드를 사용한다.
```python
SELECT column1, column2, column3, ...
INTO newtable [IN externaldb]
FROM oldtable
WHERE condition;
```

## INSERT INTO SELECT
---

한 테이블의 데이터를 복사하여 다른 테이블에 삽입한다.
* 소스 및 목표 테이블의 데이터 타입과 같아야 한다.
* 목표 테이블의 기존 레코드 값은 영향을 받지 않는다.

한 테이블의 모든 열을 다른 테이블로 복사
```python
INSERT INTO table2
SELECT * FROM table1
WHERE condition;
```

한 테이블의 일부 열을 다른 테이블로 복사
```python
INSERT INTO table2 (column1, column2, column3, ...)
SELECT column1, column2, column3, ...
FROM table1
WHERE condition;
```

## NULL
---

레코드의 값이 `NULL`일 경우 만약 계산식을 하게되면 `NULL`값이 나오게 됩니다.  
이 `NULL`값을 다른 값으로 대체하기 위해서는 다음과 같은 코드를 이용 할 수 있습니다.

MYSQL - `IFNULL()`, `COALESCE()`
```python
SELECT ProductName, UnitPrice * (UnitsInStock + IFNULL(UnitsOnOrder, 0))
FROM Products
```
```python
SELECT ProductName, UnitPrice * (UnitsInStock + COALESCE(UnitsOnOrder, 0))
FROM Products
```

SQL Server - `ISNULL()`
```python
SELECT ProductName, UnitPrice * (UnitsInStock + ISNULL(UnitsOnOrder, 0))
FROM Products
```

MS Access - `IsNull()`(`null`값일 경우에는 `True`, 아닐 경우에는 `False`를 반환 합니다.)
```python
SELECT ProductName, UnitPrice * (UnitsInStock + IIF(IsNull(UnitsOnOrder), 0, UnitsOnOrder))
FROM Products
```

Oracle - `NVL()`
```python
SELECT ProductName, UnitPrice * (UnitsInStock + NVL(UnitsOnOrder, 0))
FROM Products
```

## Comments

SQL 문의 섹션을 설명하거나 SQL 문의 실행을 막는 데 사용됩니다.

**한 줄 주석**  
`--`를 사용하며 사용하였을 경우 `--`를 시작점으로 이용하여 행의 끝까지를 주석처리 하게된다.

**여러 줄 주석**  
`/*`로 시작하고 `*/`롤 끝을 낸다. 위의 사이의 모든 텍스트는 무시된다.  
이를 이용하여 명령문의 일부만 무시가 가능하다.

Ex)
```python
SELECT CustomerName, /*City,*/ Country FROM Customers;
```
