---
title: SQL Database
description: <center>SQL Database</center>  <center>-개인으로 공부하는거라 사실과 다를 수 있음.-<center>
categories:
 - SQL
tags:
---

# SQL Database

## CREATE DATABASE
---

새 데이터베이스를 만드는 것이다.
```python
CREATE DATABASE databasename;
```
>데이터베이스를 만들기 전에 관리자 권한이 있어야 한다.

## DROP DATABASE
---

기존의 데이터베이스를 삭제하는 것이다.
```python
DROP DATABASE databasename;
```
>`CREATE DATABASE`와 마찬가지로 관리자 권한이 있어야하며, 삭제 시 모든 정보가 없어지므로 주의해야 한다.

## CREATE TABLE
---

데이터베이스의 새로운 `TABLE`을 만드는데 사용한다.
```python
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
);
```
`column`의 위치에서는 `column`이름을 지정한다.
`datatype`은 varchar, integer, date 등의 type을 지정한다.

## DROP TABLE
---

기존 테이블을 삭제하는데 이용한다.
```python
DROP TABLE table_name;
```

테이블의 내용만 삭제하기 위해서는 아래와 같은 코드를 이용한다.
```python
TRUNCATE TABLE table_name;
```

## ALTER TABLE
---

기존의 테이블의 `column` 추가, 삭제 또는 수정하는데 사용한다.

**ALTER TABLE - ADD**  
열 추가
```python
ALTER TABLE table_name
ADD column_name datatype;
```

**ALTER TABLE - DROP COLUMN**  
열 삭제
```python
ALTER TABLE table_name
DROP COLUMN column_name;
```

**ALTER TABLE - ALTER / MODIFY COLUMN**  
열의 형식을 변경

SQL Server / MS Access:
```python
ALTER TABLE table_name
ALTER COLUMN column_name datatype;
```

My SQL / Oracle (prior version 10G):
```python
ALTER TABLE table_name
MODIFY COLUMN column_name datatype;
```

Oracle 10G and later:
```python
ALTER TABLE table_name
MODIFY column_name datatype;
```

## Create Constraints
---

`CREATE TABLE`으로 테이블이 작성 될 때 또는 `ALTER TABLE`으로 테이블이 작성된 후에 제한 조건을 지정할 수 있습니다.
```python
CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    column3 datatype constraint,
    ....
);
```

|        조건        |        설명         |
|:-----------------:|:------------------:|
| NOT NULL | 열이 `NULL` 값을 가질 수 없음을 보장한다. |
| UNIQUE | 열의 모든 값이 서로 다른지 확인한다. |
| PRIMARY KEY | `NOT NULL`과 `UNIQUE`의 조합. 테이블의 각 행을 고유하게 식별한다. |
| 외부 키 | 다른 테이블의 행 / 레코드를 고유하게 식별한다. |
| CHECK | 열의 모든 값이 특정 조건을 충족하는지 확인한다. |
| DEFAULT | 값이 지정되지 않은 경우 열의 기본값을 설정한다. |
| INDEX | 데이터베이스에서 데이터를 매우 신속하게 생성 및 검색하는 데 사용된다. |

## NOT NULL
---

`NULL` 값을 포함 할 수 있다. `NOT NULL` 조건은 열이 `NULL` 값을 허용하지 않도록 강제한다.  
이렇게하면 필드에 항상 값이 포함될 수 있다. 즉, 새 레코드를 삽입하거나이 필드에 값을 추가하지 않고 레코드를 업데이트 할 수 없습니다.

Ex)
```python
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);
```

## UNIQUE
---
**CREATE TABLE에 대한 SQL UNIQUE**

`UNIQUE` 조건은 열의 모든 값이 서로 다른지 확인합니다. `UNIQUE` 및 `PRIMARY KEY` 조건은
열 또는 열 집합의 고유성을 보장합니다.  
`PRIMARY KEY` 조건에는 자동으로 `UNIQUE` 조건이 있습니다.  
그러나 테이블 당 많은 `UNIQUE` 조건을 가질 수 있지만 테이블 당 하나의 `PRIMARY KEY` 조건 만 가질 수 있습니다.

SQL Server / Oracle / MS Access
```python
CREATE TABLE Persons (
    ID int NOT NULL UNIQUE,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);
```

MySQL
```python
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    UNIQUE (ID)
);
```

`UNIQUE` 조건의 이름을 지정하고 여러 열에 `UNIQUE` 제약 조건을 정의하려면 아래의 코드를 사용.

MySQL / SQL Server / Oracle / MS Access
```python
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CONSTRAINT UC_Person UNIQUE (ID,LastName)
);
```

**ALTER TABLE에 대한 SQL UNIQUE**

테이블이 이미 만들어 졌을 때 `ID`열에 `UNIQUE` 조건을 만들려면 아래의 코드를 사용.

MySQL / SQL Server / Oracle / MS Access
```python
ALTER TABLE Persons
ADD UNIQUE (ID);
```

`UNIQUE` 조건의 이름을 지정하고 여러 열에 `UNIQUE` 조건을 정의하려면 아래의 코드를 사용.

MySQL / SQL Server / Oracle / MS Access
```python
ALTER TABLE Persons
ADD CONSTRAINT UC_Person UNIQUE (ID,LastName);
```

**UNIQUE 조건 삭제**

MySQL
```python
ALTER TABLE Persons
DROP INDEX UC_Person;
```

SQL Server / Oracle / MS Access
```python
ALTER TABLE Persons
DROP CONSTRAINT UC_Person;
```

## PRIMARY KEY
---

`PRIMARY KEY` 조건은 데이터베이스 테이블의 각 레코드를 고유하게 식별한다.  
기본 키는 `UNIQUE` 값을 포함해야하며 `NULL` 값을 포함 할 수 없다.  
테이블에는 기본 키가 하나만있을 수 있다. 기본 키는 하나 또는 여러 개의 필드로 구성 될 수 있다.

**CREATE TABLE의 SQL PRIMARY KEY**

다음 코드는 `Person`테이블이 생성 될 때 `ID`열에 `PRIMARY KEY`를 만든다.

MySQL
```python
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    PRIMARY KEY (ID)
);
```

SQL Server / Oracle / MS Access
```python
CREATE TABLE Persons (
    ID int NOT NULL PRIMARY KEY,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);
```

`PRIMARY KEY` 조건의 이름 지정을 허용하고 여러 열에 대해 `PRIMARY KEY` 조건을 정의하려면 아래의 코드를 사용한다.

MySQL / SQL Server / Oracle / MS Access
```python
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CONSTRAINT PK_Person PRIMARY KEY (ID,LastName)
);
```
>위의 예에서는 오직 하나의 `PRIMARY KEY` (PK_Person) 만 있다.
그러나 기본 키의 `VALUE`는 두 개의 `COLUMNS` (ID + 성)로 구성된다.

**ALTER TABLE에 대한 SQL PRIMARY KEY**  

테이블이 이미 만들어 졌을 때 `ID`열에 `PRIMARY KEY` 조건을 만들려면 아래의 코드를 사용.

MySQL / SQL Server / Oracle / MS Access
```python
ALTER TABLE Persons
ADD PRIMARY KEY (ID);
```

`PRIMARY KEY` 조건의 이름 지정을 허용하고 여러 열에 대해 `PRIMARY KEY` 조건을 정의하려면 아래의 코드를 사용.

MySQL / SQL Server / Oracle / MS Access :
```python
ALTER TABLE Persons
ADD CONSTRAINT PK_Person PRIMARY KEY (ID,LastName);
```
>`ALTER TABLE` 문을 사용하여 기본 키를 추가하는 경우 기본 키 열은 (테이블이 처음 작성되었을 때)
`NULL` 값을 포함하지 않도록 이미 선언되어 있어야한다.

**PRIMARY KEY 조건 삭제**

MySQL
```python
ALTER TABLE Persons
DROP PRIMARY KEY;
```

SQL Server / Oracle / MS Access
```python
ALTER TABLE Persons
DROP CONSTRAINT PK_Person;
```

## FOREIGN KEY
---

두 테이블을 서로 연결하는 데 사용되는 키.
`FOREIGN KEY`는 다른 테이블의 `PRIMARY KEY`를 참조하는 테이블의 필드 (또는 필드 모음)입니다.  
`FOREIGN KEY`가 들어있는 테이블을 하위 테이블이라고하고 `Candidate Key`가 들어있는 테이블을 참조 된 테이블 또는 상위 테이블이라고한다.

**CREATE TABLE의 SQL FOREIGN KEY**

아래의 코드는 `orders`테이블을 만들 때 `PersonID`열에 `FOREIGN KEY`를 만든다.

MySQL
```python
CREATE TABLE Orders (
    OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)
);
```

SQL Server / Oracle / MS Access
```python
CREATE TABLE Orders (
    OrderID int NOT NULL PRIMARY KEY,
    OrderNumber int NOT NULL,
    PersonID int FOREIGN KEY REFERENCES Persons(PersonID)
);
```

`FOREIGN KEY` 조건의 이름 지정 및 여러 열의 `FOREIGN KEY` 조건 정의를 허용하려면 아래의 코드를 사용.

MySQL / SQL Server / Oracle / MS Access
```python
CREATE TABLE Orders (
    OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    CONSTRAINT FK_PersonOrder FOREIGN KEY (PersonID)
    REFERENCES Persons(PersonID)
);
```

**ALTER TABLE에 대한 SQL FOREIGN KEY**

`orders`테이블이 이미 생성 된 경우 `PersonID`열에 `FOREIGN KEY` 조건을 만들려면 아래의 코드를 사용.

MySQL / SQL Server / Oracle / MS Access
```python
ALTER TABLE Orders
ADD FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
```

`FOREIGN KEY` 조건의 이름 지정 및 여러 열의 `FOREIGN KEY` 조건 정의를 허용하려면 아래의 코드를 사용.

MySQL / SQL Server / Oracle / MS Access
```python
ALTER TABLE Orders
ADD CONSTRAINT FK_PersonOrder
FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
```

**FOREIGN KEY 조건 삭제**

MySQL
```python
ALTER TABLE Orders
DROP FOREIGN KEY FK_PersonOrder;
```

SQL Server / Oracle / MS Access
```python
ALTER TABLE Orders
DROP CONSTRAINT FK_PersonOrder;
```

## CHECK
---

열에 배치 할 수있는 값 범위를 제한하는 데 사용된다.  
단일 열에 `CHECK` 조건을 정의하면이 열에 대해 특정 값만 허용된다.  
테이블에 `CHECK` 조건을 정의하는 경우가 행의 다른 `column`의 값에 따라 특정 열의 값을 제한 할 수 있다.

**CREATE TABLE에 대한 SQL CHECK**

아래의 코드는 `Person`테이블이 작성 될 때 `Age` `column`에 `CHECK`조건을 작성한다.  
`CHECK` 조건은 18 세 미만의 사람을 가질 수 없도록 보장한다.

MySQL
```python
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CHECK (Age>=18)
);
```

SQL Server / Oracle / MS Access
```python
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int CHECK (Age>=18)
);
```

`CHECK` 조건의 이름 지정 및 여러 열에 대한 `CHECK` 조건 정의를 허용하려면 아래의 코드를 사용.

MySQL / SQL Server / Oracle / MS Access
```python
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    City varchar(255),
    CONSTRAINT CHK_Person CHECK (Age>=18 AND City='Sandnes')
);
```

**ALTER TABLE에 대한 SQL CHECK**

테이블이 이미 생성 된 경우 `Age`열에 `CHECK` 조건을 만들려면 아래의 코드를 사용.

MySQL / SQL Server / Oracle / MS Access
```python
ALTER TABLE Persons
ADD CHECK (Age>=18);
```

`CHECK` 조건의 이름 지정 및 여러 열에 대한 `CHECK` 조건 정의를 허용하려면 아래의 코드를 사용.

MySQL / SQL Server / Oracle / MS Access :
```python
ALTER TABLE Persons
ADD CONSTRAINT CHK_PersonAge CHECK (Age>=18 AND City='Sandnes');
```

**CHECK 조건을 삭제**

MySQL
```python
ALTER TABLE Persons
DROP CHECK CHK_PersonAge;
```

SQL Server / Oracle / MS Access
```python
ALTER TABLE Persons
DROP CONSTRAINT CHK_PersonAge;
```

## DEFAULT
---

`DEFAULT` 조건은 열의 기본값을 제공하는 데 사용된다.  
다른 값을 지정하지 않으면 기본값이 모든 새 레코드에 추가된다.

**CREATE TABLE의 SQL DEFAULT**

아래의 코드는 `Person`테이블을 만들 때 `City`열의 `DEFAULT` 값을 설정.

MySQL / SQL Server / Oracle / MS Access
```python
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    City varchar(255) DEFAULT 'Sandnes'
);
```

`DEFAULT` 조건은 `GETDATE()`와 같은 함수를 사용하여 시스템 값을 삽입하는 데에도 사용할 수 있다.
```python
CREATE TABLE Orders (
    ID int NOT NULL,
    OrderNumber int NOT NULL,
    OrderDate date DEFAULT GETDATE()
);
```

**ALTER TABLE에 대한 SQL DEFAULT**

테이블이 이미 만들어 졌을 때 `도시`열에 `DEFAULT` 조건을 만들려면 아래의 코드를 사용.

MySQL
```python
ALTER TABLE Persons
ALTER City SET DEFAULT 'Sandnes';
```

SQL Server / MS Access
```python
ALTER TABLE Persons
ALTER COLUMN City SET DEFAULT 'Sandnes';
```

Oracle
```python
ALTER TABLE Persons
MODIFY City DEFAULT 'Sandnes';
```

**DEFAULT 조건 삭제**

MySQL
```python
ALTER TABLE Persons
ALTER City DROP DEFAULT;
```

SQL Server / Oracle / MS Access
```python
ALTER TABLE Persons
ALTER COLUMN City DROP DEFAULT;
```

## CREATE INDEX
---

테이블에 `index`를 만드는 데 사용됩니다.  
`index`는 데이터베이스에서 데이터를 빨리 검색하는 데 사용됩니다. 사용자는 `index`을 볼 수 없으며 검색, 쿼리 속도를 높이기 위해 사용된다.

CREATE INDEX - 테이블에 `index`를 만든다. 중복 된 값이 허용된다.
```python
CREATE INDEX index_name
ON table_name (column1, column2, ...);
```

CREATE UNIQUE INDEX - 테이블에 고유 `index`를 작성한다. 중복 값은 허용되지 않는다.
```python
CREATE UNIQUE INDEX index_name
ON table_name (column1, column2, ...);
```

>인덱스를 만드는 구문은 데이터베이스마다 다르다.

**DROP INDEX**

테이블의 `index`를 삭제하는 데 사용된다.

MS Access
```python
DROP INDEX index_name ON table_name;
```

SQL Server
```python
DROP INDEX table_name.index_name;
```

DB2 / Oracle
```python
DROP INDEX index_name;
```

MySQL
```python
ALTER TABLE table_name
DROP INDEX index_name;
```

## AUTO INCREMENT
---

새 레코드가 테이블에 삽입 될 때 고유 번호가 자동으로 생성되도록한다.

**MySQL**

`Person`테이블의 자동 증가 기본 키 필드로 `ID`열을 정의한다.
```python
CREATE TABLE Persons (
    ID int NOT NULL AUTO_INCREMENT,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    PRIMARY KEY (ID)
);
```

`AUTO_INCREMENT` 키워드를 사용하여 자동 증가 기능을 수행한다.  
기본적으로 `AUTO_INCREMENT`의 시작 값은 1이며 새 레코드마다 1 씩 증가한다.  
`AUTO_INCREMENT` 시퀀스를 다른 값으로 시작하려면 아래의 코드를 사용한다.

```python
ALTER TABLE Persons AUTO_INCREMENT=100;
```

**SQL Server**

`Person`테이블의 `AUTO INCREMENT` 기본 키 필드로 `ID`열을 정의한다.

```python
CREATE TABLE Persons (
    ID int IDENTITY(1,1) PRIMARY KEY,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);
```

`IDENTITY` 키워드를 사용하여 자동 증가 기능을 수행한다.  
위의 예에서 `IDENTITY`의 시작 값은 1이며 새 레코드마다 1 씩 증가한다.  
`ID`열이 값 10에서 시작하여 5 씩 증가하도록 지정하려면 `IDENTITY(10,5)`로 변경.

**MS Access**

`Person`테이블의 자동 증가 기본 키 필드로 `ID`열을 정의한다.

```python
CREATE TABLE Persons (
    ID Integer PRIMARY KEY AUTOINCREMENT,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);
```

`AUTOINCREMENT` 키워드를 사용하여 `AUTO INCREMENT` 기능을 수행합니다.  
기본적으로 `AUTOINCREMENT`의 시작 값은 1이며 새 레코드마다 1 씩 증가합니다.  
`ID`열이 값 10에서 시작하여 5 씩 증가하도록 지정하려면 자동 증가를 `AUTOINCREMENT(10,5)`로 변경하십시오.

**Oracle**

아래의 코드는 `seq_person`이라는 시퀀스 객체를 생성한다.  
`seq_person`은 1부터 시작하여 1 씩 증가한다. 또한 성능을 위해 최대 10 개의 값을 캐시한다.  
캐시 옵션은 더 빠른 액세스를 위해 얼마나 많은 순서 값이 메모리에 저장 될지 지정한다.

```python
CREATE SEQUENCE seq_person
MINVALUE 1
START WITH 1
INCREMENT BY 1
CACHE 10;
```

## Date

**Date Data Types**

MySQL
* DATE : YYYY-MM-DD
* DATETIME : YYYY-MM-DD HH : MI : SS
* TIMESTAMP : YYYY-MM-DD HH : MI : SS
* YEAR : YYYY 또는 YY

SQL Server
* DATE : YYYY-MM-DD
* DATETIME : YYYY-MM-DD HH : MI : SS
* SMALLDATETIME : YYYY-MM-DD HH : MI : SS
* TIMESTAMP : 고유 번호
