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

위 객체들은 아래와 같이 사용될 수 있다.
DB 연결 Java 프로그램을 구현해 본 사람이라면 눈에 익숙할 것이다.

```
import java.sql.*;

public class FirstExample {
   static final String DB_URL = "jdbc:mysql://localhost/TUTORIALSPOINT";
   static final String USER = "guest";
   static final String PASS = "guest123";
   static final String QUERY = "SELECT id, first, last, age FROM Employees";

   public static void main(String[] args) {
      // Open a connection
      try(Connection conn = DriverManager.getConnection(DB_URL, USER, PASS);
         Statement stmt = conn.createStatement();
         ResultSet rs = stmt.executeQuery(QUERY);) {
         // Extract data from result set
         while (rs.next()) {
            // Retrieve by column name
            System.out.print("ID: " + rs.getInt("id"));
            System.out.print(", Age: " + rs.getInt("age"));
            System.out.print(", First: " + rs.getString("first"));
            System.out.println(", Last: " + rs.getString("last"));
         }
      } catch (SQLException e) {
         e.printStackTrace();
      }
   }
}
```

## 🤝 JDBC 데이터 베이스 연결 방법

JDBC로 데이터 베이스를 연결하려면 크게 6가지 과정을 거쳐야한다.

1. DB 선택하기 (ex. MySQL, PostgreSQL 등)
2. 선택한 DB 공식 홈페이지에서 JDBC 드라이버를 다운로드한다.
3. Java 프로젝트 코드 단에서 JDBC 라이브러리를 import 한다.
4. 다운로드한 JDBC 드라이버를 코드 단에서 등록한다.
5. 연결할 DB를 가리키는 URL을 등록한다.
6. DriverManager 객체의 getConnectio() 메소드로 호출을 코딩하여 실제 데이터 베이스 연결을 설정한다.

위 과정을 차근차근 설명해보겠다.

### 🤚 Import JDBC Package

1, 2번 과정은 크게 더 설명할 부분이 없으니 3번으로 넘어가자.

JDBC 라이브러리를 프로젝트에 주입하는 부분이다.
`import` 문으로 JDBC 라이브러리를 아래와 같이 JAVA 소스 코드 단에서 작성해주면 된다.

```
import java.sql.*; // 표준 JDBC
import java.math.*; // BigDecimal, BigInteger 지원
```

### 🤚 JDBC 드라이버 등록

DB 홈페이지에서 다운로드 받은 JDBC 드라이버를 프로젝트에 주입하는 과정이다.
프로젝트에서 한번만 수행하면 된다.
방법은 `Class.forName()`, `DriverManager.registerDriver()` 를 쓰는 방법 총 두가지이다.

#### Class.forName()

동적으로 JDBC 드라이버 클래스 파일을 메모리에 자동 등록 및 로드할 수 있다.
이 방법을 사용하면 드라이버 구성과 이동이 편해 보편적으로 사용되는 편이다.

#### DriverManager.registerDriver()

Microsoft 에서 제공하는 것과 같은 비 JDK 호환 JVM을 사용하는 경우 사용된다.

### 🤚 DB URL 등록

JDBC 로 어떤 DB에 접근할 것인지 설정하는 단계이다.
JDBC 드라이버를 로드한 후 `DriverManager.getConnection()` 메소드를 사용하여 설정할 수 있다.
`DriverManager.getConnection()` 메소드 인자로 각 DB의 JDBC URL 을 입력해서 등록하면 된다.
아래와 같이 DB 마다 JDBC 용 DB URL 이 다르다.

| RDBMS  | JDBC 드라이버 이름              | URL 형식                                                |
| ------ | ------------------------------- | ------------------------------------------------------- |
| MySQL  | com.mysql.jdbc.Driver           | **jdbc:mysql://** \*/hostname/ databaseName             |
| ORACLE | oracle.jdbc.driver.OracleDriver | **jdbc:oracle:thin:@**hostname:port Number:databaseName |
| DB2    | COM.ibm.db2.jdbc.net.DB2Driver  | **jdbc:db2:**hostname:port Number/databaseName          |
| Sybase | com.sybase.jdbc.SybDriver       | **jdbc:sybase:Tds:**hostname: port Number/databaseName  |

진하게 칠해진 글씨 부분이 고정된 JDBC URL 값이고, 나머지 부분만 각 DB 환경에 맞게 작성해주면 된다.

TODO: https://www.tutorialspoint.com/jdbc/jdbc-db-connections.htm - Using a Database URL with a username and password
