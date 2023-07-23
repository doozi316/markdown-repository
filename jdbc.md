## 📢 들어가며

이번 포스팅에선 JDBC 에 대해 알아본다.

## 🤝 JDBC란?

**J**ava **D**ata**b**ase **C**onnectiviy 의 줄임말이다.
직역하면, 자바 데이터베이스 연결성이란 뜻이다.

결론적으로 JDBC는 Java 라이브러리이다.
Java와 여러 DB 간의 연결을 위한 Java API의 집합이다.

JDBC API 는 아래와 같은 역할을 한다.

1. 데이터 베이스에 연결
2. SQL 문 만들기
3. 데이터베이스에서 SQL 문 실행
4. SQL 실행 결과 보기

## 💡 참고) ODBC 와 JDBC 의 차이

ODBC는
**O**pen **D**ata**b**ase **C**onnectivity 의 약자이다.
JDBC 와 같은 기능을 하나, 아래와 같은 차이점이 있다.

|               | JDBC                                                | ODBC                                              |
| ------------- | --------------------------------------------------- | ------------------------------------------------- |
| 언어 지원     | 자바 언어에 특화되어 있다.                          | C/C++ 기반 언어를 지원한다.                       |
| 플랫폼 독립성 | Java 언어가 실행되는 모든 플랫폼에서 사용가능하다.  | Windows 운영체제에서 주로 사용된다.               |
| 드라이버 관리 | JDBC 드라이버를 사용하여 데이터베이스와 연결한다.   | ODBC 드라이버를 사용하여 데이터베이스와 연결한다. |
| 성능          | ODBC 에 비해 빠르다.                                | JDBC에 비해 느리다.                               |
| 보안          | 자바 플랫폼의 보안 기능을 활용하여 높은 수준의 보안 | C/C++ 기반으로 구현되어 플랫폼의 보안 기능에 의존 |

## 🤝 JDBC 구조

다소 허접하지만 그림으로 그려보았다 ^^
JDBC API는 JDBC API 와 JDBC DRIVER API 로 크게 두가지로 나눌 수 있다.

JDBC API 는 자바 응용 프로그램과 JDBC Manager 간 연결을 제공하는 기능을 담당하고,
JDBC DRIVER API 는 JDBC Manager 와 JDBC DRIVER 간의 연결을 지원한다.

JDBC DRIVER 는 DB 쪽에서 제공하는 흔히 아는 jar 파일이다.
이 파일을 통해 DB 와의 연결이 가능하다.

그럼 위 그림에서 JDBC Driver Manager는 무엇일까? (빨간 별표 부분)
JDBC Driver Manager 는 JDBC 라이브러리의 일부로,
JDBC API 가 사용하는 객체이다.
각 DB에 엑세스 올바른 JDBC Driver 가 사용되었는지 확인하는 역할을 한다.

## 🤝 JDBC 구성 객체

JDBC Driver Manager 처럼 JDBC 라이브러리엔
각종 Class 나 Interface 가 존재한다.
대표적인 몇가지 객체에 대해 알아보자.
아래에서 설명할 객체는 Java Application 구현 시,
JDBC 를 적용할 때 직접 코드에 써보게 될테니, 잘 알아두면 좋다.

### 🤚 DriverManager

방금 위에서 설명한 객체이다.
데이터 베이스 드라이버 목록을 관리하는 클래스이다.
통신 하위 프로토콜을 사용하여 Java 응용 프로그램 연결 요청을 적절한 데이터베이스와 일치시킨다.

### 🤚 Driver

데이터베이스 서버와의 통신을 처리한다.
이 객체를 직접 다루는 경우는 드물다.
대신 DriverManager 객체를 사용한다.

### 🤚 Connection

데이터베이스에 연결하기 위한 모든 메서드를 포함하는 인터페이스이다.
데이터베이스와의 모든 통신은 Connection 객체를 통해서만 수행된다.

### 🤚 Statement

SQL 문을 DB로 보낼때(실행할 때) 사용된다.

### 🤚 ResultSet

Statement 객체를 통해 SQL 쿼리를 실행한 후, 그 결과를 다룰 때 사용된다.

### 🤚 SQLException

DB와 관련된 모든 오류를 처리한다.
