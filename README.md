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


## JDBC 드라이버

<br>
JDBC 드라이버는 JDBC API를 이용하여 데이터베이스와 연동할 수 있도록,
<br>
특정 데이터베이스 관리 시스템(DBMS)에 대한 드라이버를 제공하는 소프트웨어 모듈입니다.
<br>


각각의 DBMS는 자체적인 네트워크 프로토콜과 API를 가지므로, <br>
JDBC API를 사용하여 DBMS와 연결하려면 해당 DBMS에 맞는 드라이버가 필요합니다.<br>
예를 들어, MySQL 데이터베이스와 연결하려면 MySQL JDBC 드라이버가 필요하고,<br>
Oracle 데이터베이스와 연결하려면 Oracle JDBC 드라이버가 필요합니다.<br>
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



## 1.드라이버 로딩 

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
  => [Build path] -> [Configure Build Path] -> 라이브러리탭 -> class path > Add external Jars 로 드라이버를 넣어준다.<br>
  => 참조 라이브러리로 드라이버가 추가됨.<br>



## 2.DB서버에 연결하기

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
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class ConnectionTest {

	public static void main(String[] args) throws SQLException {
		//String url = "jdbc:mysql://localhost:3306/jdbc?serverTimezone=UTC";
		String url = "jdbc:oracle:thin:@localhost:1521:xe";
		String user = "유저명";
		String password = "비번";
		
		try {
			//1. 드라이버 로딩
			//Class.forName("com.mysql.cj.jdbc.Driver");
			Class.forName("oracle.jdbc.driver.OracleDriver");
			System.out.println("드라이버 로딩 성공");
			//2. DB 서버에 접속
			Connection conn = DriverManager.getConnection(url,user,password);
			
		} catch (ClassNotFoundException e) {
			System.out.println("드라이버로딩실패");
			e.printStackTrace();
		}
	}

}
```

<br>

## 3.Statement 객체 생성

<br>
SQL문을 실행할 수 있는 기능을 구현한 클래스<br>
Connection 객체의 메소드를 이용해서 생성<br>
<br>

[상속구조] <br>
  +---------------+<br>
  | Statement	  |		-정적 SQL문을 실행할때 사용 (보안취약)<br>
  +---------------+<br>
 	^<br>
	|<br>
+--------------------+<br>
| PreparedStatement  |		-동적 SQL문을 실행할때 사용 (시큐어코딩에 적합한 방식, 캐시사용)<br>
+--------------------+<br>
	 ^<br>
	 |<br>
+--------------------+<br>
| CallableStatement  |		-각 DBMS에 특화된 SQL문을 실행하기 위해 사용하는 객체<br>
+--------------------+<br>
<br>
<br>


### 1) Statement 객체를 이용하기

<br>

```java
Statement stmt = conn.createStatement();
```
<br>
Statement객체는 어떤 드라이버가 로딩되어 있냐에 따라 다른 객체 리턴.<br>

<br>

### -executeUpdate<br>

insert , update , delete  명령문을 실행<br>
매개변수에 전달된 sql문을 실행 <br>
실행 결과로 몇 개의 row에 되었는지 리턴<br>
<br>

```java
int result = stmt.executeUpdate("sql문");
```

<br>

<details>
    <summary style="color:blue">연습 코드 (insert)</summary>
	
```java

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class InsertTest {

	public static void main(String[] args) {
		String url = "jdbc:mysql://localhost:3306/jdbc?serverTimezone=UTC";
		String user = "exam";
		String password = "exam";
		String sql = "insert into customer values('jang','1234','장동건','서울',sysdate(),1000,'배우')";
		
		try {
			// 1. 드라이버 로딩
			Class.forName("com.mysql.cj.jdbc.Driver");
			System.out.println("드라이버 로딩 성공!");
			
			// 2. DB서버 접속
			Connection conn = DriverManager.getConnection(url,user,password);
			System.out.println("커넥션 성공"+conn);
			
			// 3. SQL을 실행하기 위해서 Statement객체를 생성하기
			Statement stmt = conn.createStatement();
			System.out.println("Statement객체"+stmt);
			
			// 4. SQL문을 실행
			int result = stmt.executeUpdate(sql);
			
			// 5. 결과 처리
			System.out.println(result);
			
		}catch(ClassNotFoundException e) {
			System.out.println("드라이버 로딩 실패");
			e.printStackTrace();
		}catch(SQLException e) {
			e.printStackTrace();
		}
	}

}
```
	
</details>

<br>

<details>
    <summary>연습 코드 2 (update)</summary>
	
```java
package Jdbc.basic;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class UpdateTest {

	public static void main(String[] args) {
		String url = "jdbc:mysql://localhost:3306/jdbc?serverTimezone=UTC";
		String user = "exam";
		String password = "exam";
		String sql = "update customer set addr = '서울특별시' where addr = '서울'";

		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			System.out.println("driver loading success.");

			Connection conn = DriverManager.getConnection(url, user, password);
			System.out.println("connection success");

			Statement sm = conn.createStatement();

			int result = sm.executeUpdate(sql);
			System.out.println(result);
		} catch (ClassNotFoundException e) {
			System.out.println("driver loading failed.");
			e.printStackTrace();
		} catch (SQLException e) {
			e.printStackTrace();
		}

	}

}

```
	
</details>

</details>

<br>

<details>
    <summary>연습 코드 3 (delete)</summary>
	
```java
package Jdbc.basic;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

public class DeleteTest {

	public static void main(String[] args) {
		String url = "jdbc:mysql://localhost:3306/jdbc?serverTimezone=UTC";
		String user = "exam";
		String password = "exam";
		String sql = "delete from customer where addr = '제천'";
		
		try {
			// 1. 드라이버 로딩
			Class.forName("com.mysql.cj.jdbc.Driver");
			System.out.println("드라이버 로딩 성공!");
			
			// 2. DB서버 접속
			Connection conn = DriverManager.getConnection(url,user,password);
			System.out.println("커넥션 성공"+conn);
			
			// 3. SQL을 실행하기 위해서 Statement객체를 생성하기
			Statement stmt = conn.createStatement();
			System.out.println("Statement객체"+stmt);
			
			// 4. SQL문을 실행
			int result = stmt.executeUpdate(sql);
			
			// 5. 결과 처리
			System.out.println(result);
			
		}catch(ClassNotFoundException e) {
			System.out.println("드라이버 로딩 실패");
			e.printStackTrace();
		}catch(SQLException e) {
			e.printStackTrace();
		}
	}

}

```
	
</details>


#### -executeQuery<br>

select 명령문을 실행 <br>
실행한 후 조회된 테이블을 리턴<br>
DBMS에서 조회된 테이블을<br>
자바에서 사용할 수 있도록 만들어서 제공되는 객체 (ResultSet)<br>
실제로는 어떤 DBMS가 사용되냐에 따라 다른 ResultSet의 하위 객체가 리턴된다.
<br>

```java
ResultSet rs = stmt.executeQuery(sql);
```


### 2) PreparedStatement 객체를 이용하기

Connection 객체에 정의된 preparedStatement메소드를 이용해서 생성 <br>
캐시사용 <br>

[실행흐름] <br>
쿼리 문장분석 -> 컴파일 -> 실행 <br>
<br>
[사용방법]<br>
Statement는 SQL문을 실행하는 과정에서 위의 실행흐름에 명시되어 있는 과정을<br>
매번 반복해서 처리하고 있지만,<br>
PreparedStatement객체는 한번만 작업한다.<br>
캐시에서 꺼내서 사용한다. <br>
PreparedStatement객체가 sql문을 실행하는 방식이 미리 SQL문을 파싱해놓고 <br>
외부에서 입력 받는 값들을 전달해서 최종 코드가 실행될 수 있도록 처리 <br>
<br>
1. sql문을 전달하며 PreparedStatement 객체를 생성 <br>
=> Connection 객체의 preparedStatement메소드를 호출할 때 sql문을 전달해야한다.<br>

```java
PreparedStatement ptmt = con.preparedStatement(sql);
```

<br>
2. sql문을 작성할떄, 외부에서 입력 받아서 처리할 부분을 ?로 대체하여 표시한다. <br>
(?는 컬럼명에 줄 수 없고 값의 자리에만 사용할 수 있다.)<br>

```java
String sql = "insert into customer values('?','?','?','?',sysdate(),1000,'?')";
```

3. ?에 대한 값을 설정 <br>
PreparedStatement의 setXXX 메소드를 이용해서 설정 <br>
setXXX 메소드는 컬럼의 타입과 맞는 setter 메소드를 선택해서 작업 <br>
(ResultSet의 getter메소드 타입 매칭과 동일)

```java
ptmt.setString(1, "bts") //=> 첫번째 물음표 자리에 "bts"를 셋팅 (인덱스 1부터 시작)
```

```java
ptmt.setInt(2, 2000) //=> 두번째 물음표 자리에 2000를 셋팅
```


<br>

executeUpdate , executeQuery  <br>
=> Statement 객체와 메소드명은 동일하지만 매개변수가 없는 메소드를 사용 <br>
(이미 SQL을 객체 생성과 동시에 전달하기 떄문에 다시 전달하지 않는다.) <br>


<br><br>
<details>
    <summary>수업시간 PreparedStatement 연</summary>
	
```java
package Jdbc.basic;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.Scanner;

public class PreparedStatementInsertTest {
	public static void main(String[] args) {
		
		Scanner key = new Scanner(System.in);
		InsertTest_Ver2 obj = new InsertTest_Ver2();
		
		System.out.print("아이디:");
		String id = key.next();
		
		System.out.print("패스워드:");
		String pass = key.next();
		
		System.out.print("이름:");
		String name = key.next();
		
		System.out.print("주소:");
		String addr = key.next();
		
		System.out.print("메모:");
		String memo = key.next();
		
		obj.insert(id,pass,name,addr,memo);
	}
	
	public void insert(String id , String pass ,String name, String addr , String memo) {
		String url = "jdbc:mysql://localhost:3306/jdbc?serverTimezone=UTC";
		String user = "exam";
		String password = "exam";
		String sql = "insert into customer values('?','?','?','?',sysdate(),1000,'?')";
		
		try {
			// 1. 드라이버 로딩
			Class.forName("com.mysql.cj.jdbc.Driver");
			System.out.println("드라이버 로딩 성공!");
			
			// 2. DB서버 접속
			Connection conn = DriverManager.getConnection(url,user,password);
			System.out.println("커넥션 성공"+conn);
			
			// 3. SQL을 실행하기 위해서 PreparedStatement객체를 생성하기
			PreparedStatement ptmt = conn.prepareStatement(sql);
			System.out.println("PreparedStatement객체"+ptmt);
			
			// ? 에 값 전달해주기.
			ptmt.setString(1, id);
			ptmt.setString(2, pass);
			ptmt.setString(3, name);
			ptmt.setString(4, addr);
			ptmt.setString(5, memo);
			
			// 4. SQL문을 실행
			int result = ptmt.executeUpdate();
			
			// 5. 결과 처리
			System.out.println(result);
			
		}catch(ClassNotFoundException e) {
			System.out.println("드라이버 로딩 실패");
			e.printStackTrace();
		}catch(SQLException e) {
			e.printStackTrace();
		}
	}



}

```
	
</details>


<br>

## 5.결과에 대한 처리

#### 1) insert , delete , update

<br>
-모두 int를 리턴하므로 동일한 방법으로 처리<br>
-리턴 되는 값이 0이면 처리되지 않았다는 의미<br>
<br>

#### 2) select 

<br>
select문을 실행하고 보여지는 2차원 표의 데이터를 자바에서 사용할 수 있도록 만들어진 객체인 ResultSet <br>
ResultSet 내부에 있는 테이블 데이터를 읽기 위해서 ResultSet이 제공하는 메소드를 이용해서 작업<br>
ResultSet 객체 내부에서 위차값에 대한 정보를 갖고 있는 Cursor 객체를 다음 레코드로 이동하면서 데이터를 읽어야한다<br>

-레코드의 갯수만큼 반복 작업을 수행<br>
-ResultSet의 next메소드를 이용해서 다음 레코드로 커서를 이동하여 작업. next메소드는 Cursor를 이동하고<br>
다음 레코드가 있으면 true를 리턴하고 없으면 false를 리턴한다.<br>

```java
while(rs.next)){
	System.out.print(rs.getString("id")); //컬럼명이 id인 데이터를 조회
	System.out.println(rs.getString(1)); //컬럼 인덱스가 1인 데이터를 조회
}
```

<br>
- 한 번에 하나의 컬럼만 읽을 수 있다.<br>
ResultSet의 getXXXX메소드를 이용해서 컬럼값을 읽는다. 컬럼의 타입에 따라 다른 메소드를 이용 <br>
<br>

(index는 정의된 컬럼의 순서가 아닌 조회 결과로 만들어진 컬럼의 순서이다. 1부터 시작)<br>

#### getString()

char , varchar => String <br>
getString("컬럼명") or getString(컬럼의 순서를 나타내는 index) <br>



#### getInt()

int => int <br>
getInt("컬럼명") or getInt(컬럼의 순서를 나타내는 index) <br>

#### getdate()

date => java.sql.Date <br>
getDate("컬럼명") or getDate(컬럼의 순서를 나타내는 index) <br>


<br><br>
<details>
    <summary>수업시간 연습과제 간단한 로그인처리 만들어보기</summary>
	
```java
package Jdbc.basic;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;



public class LoginTest {

	public static void main(String[] args) throws Exception{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		System.out.println("아이디를 입력하세요:");
		String userId = br.readLine();
		System.out.println("비번을 입력하세요:");
		String userPass = br.readLine();
		
		
		String url = "jdbc:mysql://localhost/jdbc?serverTimezone=UTC";
		String user = "exam";
		String password = "exam";
		String sql = String.format("select * from customer where id = '%s' and pass = '%s' limit 1", userId , userPass);
		System.out.println(sql);
		Class.forName("com.mysql.cj.jdbc.Driver");
		Connection con = DriverManager.getConnection(url,user,password);
		Statement stmt = con.createStatement();
		ResultSet rs = stmt.executeQuery(sql);
		if(rs.next()) {
			String id = rs.getString("id");
			System.out.printf("%s님 로그인 되었습니다." , id);
		}else {
			System.out.println("일치하는 회원 정보가 없습니다.");
		}
	}

}

```
	
</details>

<br><br><br>


<br><br>
<details>
    <summary>수업시간 연습과제 간단한 crud 만들어보기</summary>
	
```java
package Jdbc.basic;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Scanner;

public class InsertTest_Ver2 {
	public static void main(String[] args) {
		
		Scanner key = new Scanner(System.in);
		InsertTest_Ver2 obj = new InsertTest_Ver2();
		
		System.out.print("아이디:");
		String id = key.next();
		
		System.out.print("패스워드:");
		String pass = key.next();
		
		System.out.print("이름:");
		String name = key.next();
		
		System.out.print("주소:");
		String addr = key.next();
		
		System.out.print("메모:");
		String memo = key.next();
		
		obj.insert(id,pass,name,addr,memo);
	}
	
	public void insert(String id , String pass ,String name, String addr , String memo) {
		String url = "jdbc:mysql://localhost:3306/jdbc?serverTimezone=UTC";
		String user = "exam";
		String password = "exam";
		String sql = String.format("insert into customer values('%s','%s','%s','%s',sysdate(),1000,'%s')", id,pass,name,addr,memo);
		
		try {
			// 1. 드라이버 로딩
			Class.forName("com.mysql.cj.jdbc.Driver");
			System.out.println("드라이버 로딩 성공!");
			
			// 2. DB서버 접속
			Connection conn = DriverManager.getConnection(url,user,password);
			System.out.println("커넥션 성공"+conn);
			
			// 3. SQL을 실행하기 위해서 Statement객체를 생성하기
			Statement stmt = conn.createStatement();
			System.out.println("Statement객체"+stmt);
			
			// 4. SQL문을 실행
			int result = stmt.executeUpdate(sql);
			
			// 5. 결과 처리
			System.out.println(result);
			
		}catch(ClassNotFoundException e) {
			System.out.println("드라이버 로딩 실패");
			e.printStackTrace();
		}catch(SQLException e) {
			e.printStackTrace();
		}
	}



}

```
	
	
```java
package Jdbc.basic;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Date;

public class SelectTest_Ver2 {

	public void select(String addr) {
		
		String url = "jdbc:mysql://localhost:3306/jdbc?serverTimezone=UTC";
		String user = "exam";
		String password = "exam";
		String sql = String.format("select * from customer where addr = '%s'",addr);

		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			System.out.println("driver loading success.");

			Connection conn = DriverManager.getConnection(url, user, password);
			System.out.println("connection success");
			
			Statement sm = conn.createStatement();
			ResultSet rs = sm.executeQuery(sql);
			
			while(rs.next()) {
				System.out.print(rs.getString(1)+"\t");
				System.out.print(rs.getString(2)+"\t");
				System.out.print(rs.getString(3)+"\t");
				System.out.print(rs.getString(4)+"\t");
				System.out.print(rs.getDate(5)+"\t");
				System.out.print(rs.getInt(6)+"\t");
				System.out.println(rs.getString(7)+"\t");
			}
		} catch (ClassNotFoundException e) {
			System.out.println("driver loading failed.");
			e.printStackTrace();
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
	
	public static void main(String[] args) {
		
		SelectTest_Ver2 obj = new SelectTest_Ver2();
		obj.select("서울특별시");
		
	}

}

```
	
	
```java
package Jdbc.basic;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Date;

public class UpdateTest_Ver2 {

	public void update(String id) {
		
		String url = "jdbc:mysql://localhost:3306/jdbc?serverTimezone=UTC";
		String user = "exam";
		String password = "exam";
		String sql = String.format("update customer set addr = '%s' where id = '%s'" , id);

		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			System.out.println("driver loading success.");

			Connection conn = DriverManager.getConnection(url, user, password);
			System.out.println("connection success");

			Statement sm = conn.createStatement();

			int result = sm.executeUpdate(sql);
			System.out.println(result);
		} catch (ClassNotFoundException e) {
			System.out.println("driver loading failed.");
			e.printStackTrace();
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
	
	public static void main(String[] args) {
		
		UpdateTest_Ver2 obj = new UpdateTest_Ver2();
		obj.update("lee");
		
	}

}

```
	
	
```java
package Jdbc.basic;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Date;

public class DeleteTest_Ver2 {

	public void delete(String id) {
		
		String url = "jdbc:mysql://localhost:3306/jdbc?serverTimezone=UTC";
		String user = "exam";
		String password = "exam";
		String sql = String.format("delete from customer where id = '%s'" , id);

		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			System.out.println("driver loading success.");

			Connection conn = DriverManager.getConnection(url, user, password);
			System.out.println("connection success");

			Statement sm = conn.createStatement();

			int result = sm.executeUpdate(sql);
			System.out.println(result);
		} catch (ClassNotFoundException e) {
			System.out.println("driver loading failed.");
			e.printStackTrace();
		} catch (SQLException e) {
			e.printStackTrace();
		}
	}
	
	public static void main(String[] args) {
		
		DeleteTest_Ver2 obj = new DeleteTest_Ver2();
		obj.delete("id");
		
	}

}

```
	
	
</details>

<br><br><br>
