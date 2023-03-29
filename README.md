# JDBC
<img src="https://capsule-render.vercel.app/api?type=waving&color=auto&height=200&section=header&text=JDBC&fontSize=90" />

JDBC는 "Java Database Connectivity"의 약어로, 자바 언어를 사용하여 데이터베이스와 연동하기 위한 API<br>
자바 프로그램에서 데이터베이스와의 연결,<br>
데이터베이스로부터 데이터를 쿼리하거나 업데이트하는 작업을 수행하기 위한 <br>
일련의 메서드를 제공합니다.
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

MySQL 드라이버 => https://dev.mysql.com/downloads/connector/j/



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



