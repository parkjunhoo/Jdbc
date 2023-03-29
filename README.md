# JDBC
<img src="https://capsule-render.vercel.app/api?type=waving&color=auto&height=200&section=header&text=JDBC&fontSize=90" />

JDBC는 "Java Database Connectivity"의 약어로, 자바 언어를 사용하여 데이터베이스와 연동하기 위한 API<br>
자바 프로그램에서 데이터베이스와의 연결,<br>
데이터베이스로부터 데이터를 쿼리하거나 업데이트하는 작업을 수행하기 위한 <br>
일련의 메서드를 제공합니다.
<br>
<br>
JDBC API를 사용하여 자바 프로그램에서 데이터베이스를 조작할 수 있으며,<br>
이를 통해 다양한 데이터베이스와 연동이 가능합니다.<br>
JDBC는 표준화된 인터페이스를 제공하므로, 다양한 데이터베이스 관리 시스템(DBMS)과 호환되며, <br>
이식성이 뛰어난 솔루션을 제공합니다.

JDBC를 사용하여 데이터베이스에 접근하면, <br>
자바 애플리케이션에서 데이터베이스와의 연결이 유지됩니다. <br>
이를 통해 데이터베이스에 대한 쿼리와 업데이트가 실시간으로 반영될 수 있습니다.
<br>
<hr>


### JDBC 드라이버

<br>
JDBC 드라이버는 JDBC API를 이용하여 데이터베이스와 연동할 수 있도록,
<br>
특정 데이터베이스 관리 시스템(DBMS)에 대한 드라이버를 제공하는 소프트웨어 모듈입니다.
<br>


각각의 DBMS는 자체적인 네트워크 프로토콜과 API를 가지므로, <br>
JDBC API를 사용하여 DBMS와 연결하려면 해당 DBMS에 맞는 드라이버가 필요합니다.<br>
예를 들어, MySQL 데이터베이스와 연결하려면 MySQL JDBC 드라이버가 필요하고,<br>
Oracle 데이터베이스와 연결하려면 Oracle JDBC 드라이버가 필요합니다. =====> 다형성<br>
<br>
JDBC 드라이버는 JDBC API의 표준 인터페이스를 구현합니다.<br>
즉, JDBC API를 호출하면 드라이버가 해당 DBMS와 통신하고, 결과를 JDBC API로 반환합니다.<br>
따라서 JDBC 드라이버는 JDBC API와 DBMS 사이의 중개자 역할을 합니다.<br>
<br>

JDBC 드라이버는 주로 DBMS 제조사에서 제공됩니다. <br>
따라서 각각의 DBMS에 맞는 드라이버를 다운로드하여 설치해야 합니다.<br>
또한, JDBC 드라이버는 다양한 버전이 존재하므로, 사용하는 DBMS 버전에 맞는 드라이버를 선택하여 사용해야 합니다.<br>
<br>
일반적으로 JDBC 드라이버는 JDBC API와 함께 제공되므로,<br>
JDBC API를 사용하려면 드라이버를 추가로 설치할 필요가 없습니다.<br>
그러나, 해당 DBMS에 맞는 드라이버가 시스템 클래스 패스(classpath)에 설정되어 있어야 하므로,<br>
드라이버를 설치하여 설정하는 작업이 필요합니다.<br>
<br>



<hr>



### 1.드라이버 로딩 

드라이버 안에 클래스들이 패키지에 저장되어 있으므로 모두 로딩하지 않고 핵심 클래스만 메모리에 로딩<br>
java.lang패키지의 class라는 클래스의 forName이라는 메소드를 이용해서 jdbc드라이버의 핵심 클래스를 메모리에 로딩 <br>
핵심 클래스는 드라이버 클래스라 하며 이 드라이버 클래스는 어떤 DBMS(버전에 따라서도 달라짐)를 이용하냐에 따라 달라짐<br>

[mySQL]
구버전 -> com.mysql.jdbc.Driver <br> 
신버전 -> com.mysql.cj.jdbc.Driver <br>

[오라클]
oracle.jdbc.driver.OracleDriver

[문법]
Class.forName("핵심클래스명") <br>
<br>
ex:) <br>
Class.forName("com.mysql.cj.jdbc.Driver") <br>
Class.forName("orcle.jdbc.driver.OracleDriver") <br>

(수업시간엔 수동으로 추가했찌만 자바에도 Nuget같은 Maven Gradle이 있다고 들엇다 아마 이걸로 하지않을까는 나중에는)<br>

-드라이버를 제조사 홈페이지에서 다운로드
MySQL 드라이버 => https://dev.mysql.com/downloads/connector/j/

-오라클 드라이버=> C:\oraclexe\app\oracle\product\11.2.0\server\jdbc\lib <br>
설치폴더에서 사용하거나 오라클 사이트에서 다운로드<br>
<br>

JVM이 인식할 수 있는 위치로 드라이버를 가져오기(app - web 다르게 작업)<br>
  jdbc코드를 실행하기 위해서 JVM이 찾을 수 있는 위치에 있어야한다.<br>
  => [Build path] -> [Configure Build Path] -> 라이브러리탭탭 -> 클래스패스에 Add Jars 로 드라이버를 넣어준다.<br>
  => 참조 라이브러리로 드라이버가 추가됨.<br>



### 2.DB서버에 연결하기

java.sql 패키지의 DriverManager 클래스를 이용해서 DB서버에 연결<br>
DriverManager클래스는 JDBC드라이버를 관리하고 DB와 연결해서 Connection 객체를 생성함 <br>
[ 어떤 DBMS 드라이버가 로딩 되어 있냐에 따라 다른 Connection 객체가 리턴(다형성 적용) ] <br>
<br>
Connection 인터페이스는 Statement , PreparedStatement , CallableStatement 객체를 생성하며, <br>
주로 변경되지 않는 정적 SQL문을 실행할때 사용<br>
커넥션 객체를 만들때는 <br>
1. dbms가 설치된 컴퓨터 ip 주소 <br>
2. dbms가 허용하는 포트 번호 <br>
3. db계정 및 비밀번호<br>
4. 사용하려는 db 이름<br>

위 4가지 정보가 필요하다. <br>
```java
Connection conn = DriverManager.getConnection("연결문자열","사용자","비밀번호");
//연결문자열
//oracle  =>  jdbc:oracle:thin:@IP주소:포트/DB이름
//mysql   =>  jdbc:mysql://ip주소:포트/DB
//타입존 설정 jdbc:mysql://localhost:3306/jdbc?serverTimezone=UTC
```
<br>

ex:<br>

```java
public static void main(String[] args) throws SQLException {
		String url = "jdbc:mysql://localhost:3306/jdbc?serverTimezone=UTC";
		String user = "유저명,,,,";
		String password = "비밀번호,.,.";
		
		try {
			//1. 드라이버 로딩
			Class.forName("com.mysql.cj.jdbc.Driver");
			System.out.println("드라이버 로딩 성공");
			//2. DB 서버에 접속
			Connection conn = DriverManager.getConnection(url,user,password);
			
		} catch (ClassNotFoundException e) {
			System.out.println("드라이버로딩실패");
			e.printStackTrace();
		}
	}
```

<br>

