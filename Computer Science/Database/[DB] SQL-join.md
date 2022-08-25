# SQL을 알기 전에...

Database의 백그라운드부터 알고 가보자 <br/>

## 데이터베이스(DB)란?

데이터베이스를 한 마디로 정의하면 '데이터의 집합'이라고 할 수 있다.  
데이터베이스에는 일상생활 대부분의 정보가 저장되고 관리됨.
* ex) 카카오 메시지, 인스타그램 업로드 사진, 교통카드 등등...  <br/>

## DBMS(Database Management System)란?

데이터베이스를 '데이터의 집합'이라고 정의한다면, 이런 데이터 베이스를 관리하고 운영하는 소프트웨어를 DBMS라고 한다.
다양한 데이터가 저장되어 있는 데이터베이스는 여러 명의 사용자나 응용 프로그램과 공유하고 동시에 접근이 가능해야 한다.
* ex) 여러 명의 은행 예금 계좌 정보 -> 데이터베이스
* ex) 은행이 가지고 있는 예금 계좌 데이터베이스에 여러 명이 동시 접근 가능.(예금 계좌 주인, 은행 직원, ATM 등) -> DBMS가 있기에 가능

### DBMS의 종류

데이터베이스를 사용하기 위해 소프트웨어, 즉 DBMS를 설치해야하는데 대표적으로 MySQL, 오라클, SQL 서버, MariaDB 등이 있다.

|DBMS|제작사|작동 운영체제|기타|
|----|----|----------|---|
|MySQL|Oracle|Unix, Linux, Windows, Mac|오픈 소스(무료), 상용|
|MariaDB|MariaDB|Unix, Linux, Windows|오픈 소스(무료), MySQL 초기 개발자들이 독립해서 만듬|
|PostgreSQL|PostgreSQL|Unix, Linux, Windows, Mac|오픈 소스(무료)|
|Oracle|Oracle|Unix, Linux, Windows|오픈 소스(무료), 상용 시장 점유율 1위|
|SQL Server|Microsoft|Windows|오픈 소스(무료), 주로 중/대형급 시장에서 사용|
|DB2|IBM|Unix, Linux, Windows|오픈 소스(무료), 메인프레임 시장 점유율 1위|
|Access|Microsoft|Windows|오픈 소스(무료), PC용|
|SQLite|SQLite|Android, iOS|오픈 소스(무료), 모바일 전용, 오픈 소스(무료)|
<br/>
  
## DBMS의 분류

DBMS의 유형은 계층형, 망형, 관계형, 객체지향형, 객체관계형 등으로 분류된다. 현재 사용되는 DBMS 중에는 관계형 DBMS가 가장 많은 부분을 차지하며, MySQL도 관계형 DBMS에 포함된다.  

### 계층형 DBMS

계층형 DBMS는 처음으로 등장한 DBMS 개념으로 1960년대에 시작되었다. 아래 그림과 같이 각 계층은 트리 형태를 갖는다.
계층형 DBMS의 문제는 처음 구성을 완료한 후에 이를 변경하기가 상당히 까다롭다는 것이다. 또한 다른 노드를 찾아가는 것이 비효율적이다. 근래는 사용하지 않는 형태이다.
  
  <img width="691" alt="계층형 DBMS" src="https://user-images.githubusercontent.com/66079439/184584078-af3af1e1-cd10-4436-bdc7-3710bf640d98.png">

### 망형 DBMS
 
망형 DBMS는 계층형 DBMS의 문제점을 개선하기 위해 1970년대에 등장했다. 각 노드끼리도 연결된 유연한 구조다.
하지만 망형 DBMS를 잘 활용하려면 프로그래머가 모든 구조를 이해해야만 프로그램 작성이 가능하다는 단점이 존재한다.
  
  <img width="684" alt="망형 DBMS" src="https://user-images.githubusercontent.com/66079439/184584088-79948789-63e3-4c5f-acb2-235e913e584d.png">

### 관계형 DBMS

MySQL 뿐만 아니라, 대부분의 DBMS가 RDBMS 형태로 사용된다. RDBMS의 데이터베이스는 테이블(table)이라는 최소 단위로 구성되며, 이 테이블은 하나 이상의 열과 행으로 이루어져 있다.
RDBMS에서는 모든 데이터가 테이블에 저장된다. 이 구조가 가장 기본적이고 중요한 구성이기 때문에 RDBMS는 테이블로 이루어져 있으며, 테이블은 열과 행으로 구성되어 있다.  
  
  <img width="688" alt="관계형 DBMS" src="https://user-images.githubusercontent.com/66079439/184584099-54e6e64a-c7fb-4aa1-af75-395a7005e35b.png">
<br/>

## SQL이란?

SQL은 DBMS에서 사용하는 언어이다.  

SQL은 특정 회사에서 만드는 것이 아니라 국제표준화기구에서 SQL에 대한 표준을 정해서 발표하고 있다. 이를 표준 SQL이라고 부른다. 그런데 문제는 SQL을 사용하는 DBMS를 만드는 회사가 여러 곳이기 때문에 표준 SQL이 각 회사 제품의 특성을 모두 포용하지 못한다는 점이다. 그래서 DBMS를 만드는 회사에서는 되도록 표준 SQL을 준수하되, 각 제품의 특성을 반영한 SQL을 사용한다.

<img width="684" alt="SQL 종류" src="https://user-images.githubusercontent.com/66079439/184584109-c2c4574c-26d3-468d-bc7a-8ce79063b5ed.png">


* SQL은 구조화된 쿼리 언이이며, 데이터베이스에 쿼리를 보내 원하는 데이터를 가져오거나 삽입할 수 있다.
* 쿼리란? : 쿼리는 '질의문'이라는 뜻을 지님. 쿼리는 저장되어 있는 데이터를 필터링하기 위한 질의문으로 볼 수 있음.
* SQL을 사용할 수 있는 데이터베이스와 달리, 데이터의 구조가 고정되어 있지 않은 데이터베이스를 NoSQL이라고 한다. 관계형 데이터베이스와는 달리, 테이블을 사용하지 않고 데이터를 다흔 형태로 저장한다. NoSQL의 대표적인 예시는 MongoDB와 같은 문서 지향 데이터베이스이다.
<br/>

## SQL Join

하나의 테이블에 원하는 데이터가 모두 있다면 좋겠지만, 두 개의 테이블을 엮어야 원하는 결과가 나오는 경우도 있다. 조인을 쓰면 두개의 테이블을 엮어서 원하는 데이터를 추출할 수 있다.  
  
두 테이블의 조인을 위해서는 기본키(Primary Key)와 외래키(Foreign Key)관게로 맺어져야 하고, 이를 일대다 관계라고 한다. 조인은 네가지 형태로 이루어져있다. Inner Join, Outer Join, Cross Join, Self Join.  
  
### 1. Inner Join(내부 조인)

두 테이블을 연결할 때 가장 많이 사용하는 것이 내부 조인. 보통 그냥 조인이라고 부른다.

```
SELECT <열 목록>
FROM <첫 번째 테이블>
    INNER JOIN <두 번째 테이블>
    ON <조인될 조건>
[WHERE 검색 조건]
```

![Inner-Join-Graph](https://user-images.githubusercontent.com/66079439/184588021-b3493daf-b9ad-43e0-a25c-1a16fd78aea5.png)


### 2. Outer Join(외부 조인)

내부 조인은 두 테이블에 모두 데이터가 있어야만 결과가 나오지만, 외부 조인은 한쪽에만 데이터가 있어도 결과가 나온다.

```
SELECT <열 목록>
FROM <첫 번째 테이블(LEFT 테이블)>
    <LEFT|RIGHT|FULL>OUTER JOIN <두 번째 테이블(RIGHT 테이블)>
    ON <조인될 조건>
[WHERE 검색 조건]
```

#### OUTER JOIN의 종류
  - LEFT OUTER JOIN: 왼쪽 테이블의 모든 값이 출력되는 조인
  - RIGHT OUTER JOIN: 오른쪽 테이블의 모든 값이 출력되는 조인
  - FULL OUTER JOIN: 왼쪽 또는 오른쪽 테이블의 모든 값이 출력되는 조인

![Outer-Join-Graph2](https://user-images.githubusercontent.com/66079439/184588046-abb9d341-abf9-41ea-842a-9f8b3cfc6dc2.png)

### 3. CROSS JOIN(상호 조인)

한쪽 테이블의 모든 행과 다른 쪽 테이블의 모든 행을 조인시키는 기능. 상호 조인 결과의 전체 행 개수는 두 테이블의 각 행의 개수를 곱한 수만큼 된다. 카디션 곱(Cartesian Product)라고도 한다.

```
SELECT *
FROM <첫 번째 테이블>
    CROSS JOIN <두 번째 테이블>
```

![Cross-Join-Graph](https://user-images.githubusercontent.com/66079439/184588080-7acf121b-fd2c-4674-85c8-da40f55963c7.png)

### 4. SELF JOIN(자체 조인)

자체 조인은 자기 자신과 조인하므로 1개의 테이블을 사용한다. 별도의 문법이 있는 것은 아니고 1개로 조인하면 자체 조인이 된다.

```
SELECT <열 목록>
FROM <테이블> 별칭A
    INNER JOIN <테이블> 별칭B
    ON <조인될 조건>
[WHERE 검색 조건]
```

![Self-Join-Graph](https://user-images.githubusercontent.com/66079439/184588093-0ae54436-a99b-4eec-ba64-81a9ef002bed.png)

<br/> <br/>

## Reference
 - https://hongong.hanbit.co.kr/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-databasedb-dbms-sql%EC%9D%98-%EA%B0%9C%EB%85%90/
 - https://velog.io/@estell/SQL-1-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4DB-SQL%EC%9D%B4%EB%9E%80
 - https://hongong.hanbit.co.kr/sql-%EA%B8%B0%EB%B3%B8-%EB%AC%B8%EB%B2%95-joininner-outer-cross-self-join/

