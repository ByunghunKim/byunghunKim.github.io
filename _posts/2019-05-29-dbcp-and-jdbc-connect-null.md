
DBCP 란

마트에서 물건을 계산 할때를 생각해 봅시다.(놀이동산, 영화관에서 표를 구매하는 행위도 유사)
손님 1명이 계산을 요청할 때 마다 계산대를 설치하고 직원이 계산을 해준다면
여기에는 다음의 큰 행위가 발생합니다.

1. 계산대 설치
2. 직원 배치
3. 물건 계산 및 결제
4. 계산대 철수

이런 일련의 행위가 계산을 할 때 마다 일어난다면 업무의 난이도가 매우 높아집니다.

이를 효율적으로 바꾸어보면 
1. 계산대를 미리 설치(효율화. 계산을 위한 준비 시간 절약)
2. 직원은 상시 대기(효율화. 상시 처리로 업무시간 절약)
3. 물건 계산 및 결제(효율화 비대상. 손님마다 구매 물품이 다르므로 효율화 대상 아님)
4. 계산대 철수(효율화. 폐점하기 전까지 해당 행위 불필요)

위와 같이 반복적이고 중복적인 업무를 사전에 준비해두어 매장 운영의 효율성을 높이는 작업과 같다고 보시면 됩니다.

DBCP는 위와같이 DB와의 연결이 필요한 작업이 발생할 때
DB와의 연결방법을 미리 만들어두었다가, 사용자의 요청이 있을때만 만들어둔 pool을 사용하고 다시 반납하는 기법입니다.
미리 만들어두기 때문에 전체적으로는 데이터베이스의 부하를 줄이고, 서버의 자원을 효율적으로 활용할 수 있는 기술입니다.


웹프로그램을 개발할 때 connection pool 을 설정할 필요가 있는데
아래와 같은 에러가 발생할 때 다음의 사항을 참고해보세요.


> java.sql.SQLException: Cannot create JDBC driver of class '' for connect URL 'null'  
> at org.apache.tomcat.dbcp...


JDBC 환경설정 확인

1. 라이브러리 확인
  - tomcat 6.0 이전 버전 : commons-dbcp.jar , commons-pool.jar , commons-collections.jar
  - tomcat 6.0 이후 버전 : tomcat-dbcp.jar
  버전에 맞는 jar 파일을 webContent/WEB-INF/lib 폴더에 추가시켜 줍니다.
  
2. PC에 설치해둔 tomcat경로/conf/context.xml 파일에 다음의 설정을 추가합니다.
  - '<context></context>' 태그 내부에
  ```xml
	<Resource 
	  name="jdbc/dbname" #(데이타베이스이름 , JNDI로 호출될 이름을 설정) 
	  auth="Container" #(Container 거나 Application이거나 - DBCP를 관리할 관리자) 
	  type="javax.sql.DataSource" #(해당 resource의 return type) 
	  factory="org.apache.tomcat.dbcp.dbcp2.BasicDataSourceFactory" #(dbcp를 유용하는 관리 클래스) 
	  driverClassName="com.mysql.jdbc.Driver" #(dbcp를 이용하기 위한 드라이버클래스) 
	  url="jdbc:mysql://localhost:3306/basicjsp" #(db 접속 url) 
	  username="test" #(db 접속 id) 
	  password="test" #(db 접속 password) 
	  maxActive="100"  
	  maxIdle="30" 
	  maxWait="10000" 
	  removeAbandoned="true" 
	  removeAbandonedTimeout="60"/> 
  ```

3. WEB-INF/web.xml 설정에 다음의 설정을 추가합니다.
  - '<web-app></web-app>' 태그 내부에
  ```html
	<resource-ref>
	  <description>My SQL Resource</description><!-- 리소스 설명 -->
	  <res-ref-name>jdbc/basicjsp</res-ref-name><!-- 리소스 이름(JNDI명) -->
	  <res-type>javax.sql.DataSource</res-type><!-- 리턴 Type -->
	  <res-auth>Container</res-auth><!-- 관리 계층 -->
	</resource-ref>
  ```


좀 더 많은 DBCP 참조.
[네이버 Commons DBCP 이해하기] (https://d2.naver.com/helloworld/5102792 "네이버 Commons DBCP 이해하기");





