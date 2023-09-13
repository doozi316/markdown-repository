## 📢 들어가며

이번 포스팅에선 JDBC 에 대해 알아본다.

## 🤝 JDBC란?

**J**ava **D**ata**b**ase **C**onnectiviy 의 줄임말이다.
직역하면, 자바 데이터베이스 연결성이란 뜻이다.

결론적으로 JDBC는 Java <u>라이브러리</u>이다.
Java와 여러 DB 간의 연결을 위한 Java API의 집합이다.
라이브러리, API 개념을 잘 모르겠다면 아래 두 포스팅을 참고.

-   [프레임워크(Framework), 라이브러리(Library), 플러그인(Plug-in), 모듈(Module)의 차이](https://doozi0316.tistory.com/entry/%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%ACFramework-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%ACLibrary-%ED%94%8C%EB%9F%AC%EA%B7%B8%EC%9D%B8Plug-in-%EB%AA%A8%EB%93%88Module%EC%9D%98-%EC%B0%A8%EC%9D%B4)
-   [SDK, API의 개념과 차이점](https://doozi0316.tistory.com/entry/SDK-API%EC%9D%98-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%B0%A8%EC%9D%B4%EC%A0%90)

JDBC API 는 아래와 같은 역할을 한다.

1. 어플리케이션과 DB 간의 연결
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

JDBC API는 **JDBC API** 와 **JDBC DRIVER API** 크게 두가지로 나눌 수 있다.

JDBC API 는 자바 응용 프로그램과 JDBC Manager 간 연결을 제공하는 기능을 담당하고,
JDBC DRIVER API 는 JDBC Manager 와 JDBC DRIVER 간의 연결을 지원한다.

JDBC DRIVER 는 DB 공식 홈페이지에서 제공하는 jar 파일이다.
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

방금 위에서 설명한 객체이다. (빨간 별표 부분)
데이터 베이스 드라이버(jar 파일)를 관리하는 클래스이다.
Java 어플리케이션으로부터 온 DB 연결 요청을 적절한 데이터베이스와 연결시킨다.

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
DB 연결 Java 프로그램을 구현해 본 사람이라면 눈에 익숙할지도.

### 🤚 예제

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
2. 선택한 DB 공식 홈페이지에서 JDBC 드라이버를 다운로드
3. Java 프로젝트 코드 단에서 JDBC 라이브러리를 import
4. 다운로드한 JDBC 드라이버를 코드 단에서 등록
5. 연결할 DB를 가리키는 URL을 등록
6. DriverManager 객체의 getConnectio() 메소드로 호출을 코딩하여 실제 데이터 베이스 연결을 설정

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

| RDBMS  | JDBC 드라이버                   | URL 형식                                                 |
| ------ | ------------------------------- | -------------------------------------------------------- |
| MySQL  | com.mysql.jdbc.Driver           | **jdbc:mysql://** hostname/databaseName                  |
| ORACLE | oracle.jdbc.driver.OracleDriver | **jdbc:oracle:thin:@** hostname:port Number:databaseName |
| DB2    | COM.ibm.db2.jdbc.net.DB2Driver  | **jdbc:db2:** hostname:port Number/databaseName          |
| Sybase | com.sybase.jdbc.SybDriver       | **jdbc:sybase:Tds:** hostname: port Number/databaseName  |

진하게 칠해진 글씨 부분이 고정된 JDBC URL 값이고, 나머지 부분만 각 DB 환경에 맞게 작성해주면 된다.

```
DriverManager.getConnection(String url);
```

### 🤚 User, Password 등록

`DriverManager.getConnection()` 메소드 인자로 JDBC URL 을 넣어 어떤 DB에 연결할건지 설정해줄 수 있다고 앞서 설명했는데,
사실 이 정보만으로는 DB에 연결하기 어렵다.
DB에 접속하기위해선 이 DB에 접근 가능한 권한이 있어야한다.
즉, User와 Password 정보를 `DriverManager.getConnection()` JDBC URL과 함께 인자로 넘겨야한다.

아래 예시와 같이 여러 방법으로 `DriverManager.getConnection()` 에 JDBC URL 과 User, Password를 인자로 넘길 수 있다.

**문자열 하나로 통째로 넘기기**

```
String URL = "jdbc:oracle:thin:username/password@amrood:1521:EMP";
Connection conn = DriverManager.getConnection(URL);
```

**각각 인자로 넘기기**

```
String URL = "jdbc:oracle:thin:@amrood:1521:EMP";
String USER = "username";
String PASS = "password"
Connection conn = DriverManager.getConnection(URL, USER, PASS);
```

**Properties 객체 사용하기**

💡 **Properties**

키, 값으로 이뤄진 객체

```
import java.util.*;

String URL = "jdbc:oracle:thin:@amrood:1521:EMP";
Properties info = new Properties( );
info.put( "user", "username" );
info.put( "password", "password" );

Connection conn = DriverManager.getConnection(URL, info);
```

## 🤝 JDBC 데이터 베이스 연결 닫기

JDBC 프로그램이 끝나면 DB 연결을 명시적으로 종료시켜줘야한다.
그러나, 이를 까먹을 경우 Java 의 가비지 콜렉터가 DB 연결을 닫고 비운다.
그렇다고 가비지 콜렉터에 의존하면 좋지못한 프로그램이니 명시적으로 꼭 종료시켜주자.

가비지 콜렉터의 개념을 잘 모르겠다면 아래 포스팅을 참고.

-   [[JAVA] JVM이란? 개념 및 구조 (JDK, JRE, JIT, 가비지 콜렉터...)](https://doozi0316.tistory.com/entry/1%EC%A3%BC%EC%B0%A8-JVM%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EB%A9%B0-%EC%9E%90%EB%B0%94-%EC%BD%94%EB%93%9C%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%8B%A4%ED%96%89%ED%95%98%EB%8A%94-%EA%B2%83%EC%9D%B8%EA%B0%80)

DB 연결은 아래와 같이 작성해 닫아줄 수 있다.

```
conn.close();
```

이렇게 명시적으로 연결을 닫으면 DBMS 자원을 아낄 수 있어 DB 관리하기 용이하다.
