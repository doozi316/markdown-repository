## 📣 들어가며

최근 JDBC로 (정확히는 node-jdbc) 테이블 목록을 가져올 일이 있었는데,  
`getTables` api 를 요청해도 빈 배열만 반환됐다. 분명 테이블들이 있는데도...

  
한참의 삽질 끝에 `getCatalogs` 또는 `getSchemas` api 를 사용 후,  
스키마나 카탈로그 정보로 테이블 목록을 가져와야한다는 걸 알 수 있었다.  
그런데 카탈로그가 있는 DB가 있고, 없는 DB가 있었다.  
때문에 카탈로그가 없다면 스키마를 적절히 조회해서 그 조회 정보로 테이블을 가져왔어야했는데,  
도통 감이 잡히지 않아 이번 포스팅을 작성해본다. 

사실 이런 의문점은 DBeaver를 쓸 때부터 갖고 있던 생각이었다.

(다른 DB 툴도 비슷하리라고 생각된다.)

[##_Image|kage@SGxSU/btszI1koen8/FL1vKmf89sn7wBjeBHeF0K/img.png|CDM|1.3|{"originWidth":213,"originHeight":129,"style":"alignCenter","caption":"MySQL(데이버베이스 명과 테이블 명은 가림)"}_##]

[##_Image|kage@cIL3l6/btszJ1j9DlP/K5b1OHeoEJuZtM4GFYlMpK/img.png|CDM|1.3|{"originWidth":348,"originHeight":167,"style":"alignCenter","caption":"PostgreSQL(데이버베이스 명과 테이블 명은 가림)"}_##]

DBeaver를 사용하다보면 어떤 DB는 Databases 아래에 테이블 목록이 바로 있는 반면 

어떤 DB는 Databases 목록 하위에 Schemas 하위에 Tables 가 보이는 등 구조가 달랐기 때문이다.

이번 포스팅에선 스키마와 카탈로그의 개념 및 DB 계층에 대해 다뤄본다. 

## 📘 스키마란?

Database Schema.  
스키마는 직역하면 개요, 계획, 도식을 나타낸다.  
데이터베이스에서 자료의 구조, 자료의 표현 방법, 자료 간의 관계를 형식 언어로 정의한 구조이다.  
**데이터베이스 관리자(DBA)/유저**에 의해 생성 및 관리된다.

### 📒 스키마 예

-   테이블 정보(테이블 이름, 컬럼 이름, 컬럼 데이터 타입 등)
-   테이블 간의 관계(relationship)
-   제약 조건(NOT NULL, UNIQUE, PRIMARY KEY, FOREINKEY, DEFAULT, INDEX 등)

### 📒 스키마 구조

[##_Image|kage@E1gXq/btszLsOxoEQ/iTaDAWugqZT2EvRyCEhk3k/img.png|CDM|1.3|{"originWidth":1440,"originHeight":810,"style":"alignCenter"}_##]

스키마는 크게 개념 스키마, 외부 스키마, 내부 스키마로 나눌 수 있다.  
(뭔가 대학 전공 수업때 들었던거 같은 기억이...)

#### 개념 스키마

일반적으로 '스카마' 라고 했을 때, 개념 스키마를 의미한다.  
개념 스키마는 DB의 전체 구조를 나타낸다.  
모든 데이터베이스 객체 및 객체 간의 관계를 포괄적으로 정의한다.  
사용자 관점에서 데이터베이스를 전반적으로 이해할 수 있는 논리적인 설계를 제공한다.  
데이터베이스의 고수준 뷰를 정의하는 데 사용된다.

#### 외부 스키마

외부 스키마는 데이터베이스의 부분적인 뷰 또는 사용자 관점을 나타낸다.  
때문에 일부만 볼 수 있다는 의미에서 '서브 스키마'라고도 한다.  
특정 사용자 그룹이나 응용 프로그램에 의해 볼 수 있는 데이터베이스 부분을 정의한다.  
각 사용자 그룹이 필요로 하는 데이터에 액세스할 수 있도록한다.  
데이터베이스의 특정 부분을 개별적으로 제어 및 사용자 지정할 수 있다.  
쉽게 설명하자면, 권한 별 접근 가능 부분을 정의해둔 것이라 생각하면 될 듯 하다.  
하나의 데이터베이스 시스템에는 여러 개의 외부 스키마가 존재할 수 있다.

#### 내부 스키마

내부 스키마는 데이터베이스의 물리적 구조와 저장 방법을 정의한다.  
데이터베이스 관리 시스템(DBMS) 내부에서 데이터가 어떻게 저장되고 관리되는지를 나타낸다.  
주로 데이터 압축, 색인 구조, 파일 구성 및 기타 물리적인 세부 사항을 다룬다.  
개발자나 일반 사용자가 직접 접근하는 것이 아니라 DBMS가 내부적으로 처리하는 영역이다.

## 📘 카탈로그란?

Database Catalog.  
데이터 사전이라고도 불린다.

데이터베이스 카탈로그는 메타데이터들로 구성된 데이터베이스 내의 인스턴스이다.  
즉, 카탈로그에 저장된 데이터 = 메타데이터 인것이다.

메타데이터는  
기본 테이블, 뷰 테이블, 동의어(synonym)들, 값 범위들, 인덱스들, 사용자들, 사용자 그룹 등등과 같은 데이터베이 개체의 정의를 의미한다.

> **💡 메타데이터**  
> 메타 데이터는 데이터에 관한 구조화된 데이터이다.  
> 대량의 정보 가운데에서 확인하고자 하는 정보를 효율적으로 검색하기 위해 원시데이터(Raw data)를 일정한 규칙에 따라 구조화 혹은 표준화한 정보를 의미한다.  
>   
> 쉽게 얘기하자면 다른 데이터를 설명해 주는 데이터이다.  
> 메타(Meta)는 일반적으로 '~에 관한', '~에 대한' 이라고 해석된다.  
>   
> 예를 들어, 과일 정보를 저장하고 있는 테이블이 있다.여기서 테이블 내의 '사과', '오렌지', '맛있음'의 데이터 따위가 아니라테이블 이름, 열(컬럼) 이름, 데이터 타입(숫자타입, 문자타입 등) 등을 메타 데이터라고 할 수 있다.

카탈로그는 DB 종류에 따라 다른 구조를 가진다.

  
**데이터베이스 관리 시스템(DBMS, database management system)**에 의해 스스로 생성 및 관리된다.

## 📘 스키마 VS 카탈로그

스키마든 카탈로그든 테이블 정보, 인덱스 등 정의하는 데이터가 비슷한 것 같은데,  
스키마와 카탈로그는 서로 어떤 차이점이 있을까?

[##_Image|kage@pNc9O/btszHHsWpV8/9UG3VXUkACiXv54Y9F06PK/img.png|CDM|1.3|{"originWidth":1440,"originHeight":810,"style":"alignCenter"}_##]

일단 한마디로 정리하자면,  
카탈로그가 스키마 정보를 포함하고 있다.  
카탈로그가 스키마보다 더 큰 개념인 것이다.

스키마는 유저(DBA)에 의해 생성/관리 되고, 카탈로그는 DBMS에 의해 생성/관리된다.  
카탈로그는 모든 종류의 스키마를 가진 공간이다.  
카탈로그는 한 개 이상의 스키마를 가질 수 있으며 `INFORMATION_SCHEMA` 라는 이름의 스키마는 항상 가지고 있다.  
카탈로그는 보통 데이터베이스의 동의어로 사용된다.

## 📘 DB 계층 구조

카탈로그가 스키마를 포함한 것이라는 걸 이해했다.  
그렇다면 아래 이미지처럼 스키마가 없는 DB가 있었던 이유는 뭘까?

[##_Image|kage@SGxSU/btszI1koen8/FL1vKmf89sn7wBjeBHeF0K/img.png|CDM|1.3|{"originWidth":213,"originHeight":129,"style":"alignCenter","caption":"Schemas 가 없는 MySQL(데이버베이스 명과 테이블 명은 가림)"}_##][##_Image|kage@cIL3l6/btszJ1j9DlP/K5b1OHeoEJuZtM4GFYlMpK/img.png|CDM|1.3|{"originWidth":348,"originHeight":167,"style":"alignCenter","caption":"Schemas 가 있는 PostgreSQL(데이버베이스 명과 테이블 명은 가림)"}_##]

일단 정확하게 말하자면 말하자면,

스키마가 없는게 아니라 카탈로그가 없는 것이다.

MySQL 에선 Database 를 Schema 와 동의어로 쓰이고 있다. ([공식문서](https://dev.mysql.com/doc/refman/8.2/en/glossary.html#glos_schema))

그리고 위에서 설명한 것 처럼, 일반적으로 Catalog 와 Database 를 동의어로 사용된다.

따라서 위 이미지의 PostgreSQL 은 Catalog(Database) 와 Schemas 가 둘 다 있는 것이고,

MySQL은 Schemas(Databse) 만 존재하는 것이다. 

그렇다면 MySQL 에 카탈로그가 없는 이유가 대체 뭘까?

이를 이해하려면 DB별 계층 구조에 대해 알아야한다.

DB는 서로 다른 계층 구조를 가지는데,  
크게 4계층과 3계층 구조로 나눌 수 있다.

대표적인 3계층 구조 DB엔 MySQL 이 있고,  
4계층 구조 DB 엔 PostgreSQL이 있다.

그리고 3계층인지 4계층인지 아리송 하지만 결국은 4계층인 Oracle 이 있다. 

## 📘 4계층 구조

## 📘 3계층 구조

더보기

[https://junhyunny.github.io/database/database-schema-and-catalog/](https://junhyunny.github.io/database/database-schema-and-catalog/)  
[https://ko.wikipedia.org/wiki/메타데이터](https://ko.wikipedia.org/wiki/메타데이터)  
[https://ko.wikipedia.org/wiki/데이터베이스\_카탈로그](https://ko.wikipedia.org/wiki/데이터베이스_카탈로그)  
[https://ko.wikipedia.org/wiki/데이터베이스\_스키마](https://ko.wikipedia.org/wiki/데이터베이스_스키마)

[https://spidyweb.tistory.com/181](https://spidyweb.tistory.com/181)

[https://hue9010.github.io/db/mysql\_schema/](https://hue9010.github.io/db/mysql_schema/)

[https://stackoverflow.com/questions/7942520/relationship-between-catalog-schema-user-and-database-instance](https://stackoverflow.com/questions/7942520/relationship-between-catalog-schema-user-and-database-instance)