# 목차
<!-- TOC -->

- [목차](#목차)
- [1. Servlet](#1-servlet)
  - [1.1 개요](#11-개요)
    - [1.1.1 서블릿 컨테이너](#111-서블릿-컨테이너)
  - [1.2 Servlet 구동](#12-servlet-구동)
- [2. JSP](#2-jsp)
  - [2.1 개요](#21-개요)
  - [2.2 표기법](#22-표기법)
- [3. JDBC](#3-jdbc)
  - [3.1 개요](#31-개요)
  - [3.2 코딩 절차](#32-코딩-절차)

<!-- /TOC -->
# 1. Servlet
## 1.1 개요
* Sever + Applet
* Java 내부에 HTML 코드를 삽입하여 사용 할 수 있게 해준다(.java 파일)
* 모든 Servlet은 javax.servlet.Servlet 인터페이스를 상속 받아 구현
  * 웹을 다룰 수 있도록 해주는 "HttpServlet" 클래스를 상속받음
* Servlet 구현 시 Servlet 인터페이스와 ServletConfig 인터페이스를 javax.sevlet.GenericServlet에 구현
* HttpServlet 클래스를 상속받음(상속받지 않으면 HTML 코드 사용이 불가능)
* Dynamic Web Project의 src 폴더에 파일 생성(이클립스)
* 기본적으로 Servlet 파일 명 = URL(/프로젝트명/서블릿파일명)
  * Servlet 파일(.java) 생성시 URL mapping 값을 바꾸면 tomcat 설정도 바뀌면서 URL을 다르게 할 수 있다.
* 크게 보면 Servlet 인터페이스를 추상 클래스인 GenericServlet 이 구현,그리고 이 GenericServlet 을 HttpServlet 이 상속하고 있다.
  * HttpServletRequest, HttpServletResponse 인터페이스를 상속받는 HttpServlet 클래스를 Servlet 파일을 생성하면 기본적으로 상속받는다.
### 1.1.1 서블릿 컨테이너
* WAS의 일종(관점에 따라 부르는 명칭이 다를 뿐)
  * Web Application Server
  * 사용자가 요청한 서비스의 결과를 스크립트 언어로 가공하여 동적인 페이지를 제공
* 서블릿들의 생성, 실행, 파괴를 담당한다.(서블릿 생명주기(Life Cycle) 관리)
* 서버에 만들어진 서블릿이 스스로 작동하는 것이 아니라, 서블릿을 관리 해주는 것이 필요한데, 이러한 역할을 하는 것이 서블릿 컨테이너
* Clinet의 Request를 받아주고 Response할 수 있게, 웹 서버와 소켓을 만들어 통신
* 대표적으로 Tomcat
  * 톰캣은 웹 서버와 소켓을 만들어 통신하며 JSP(java server page)와 Servlet이 작동할 수 있는 환경을 제공
* 멀티 스레드 지원 및 관리
  * 서블릿 컨테이너는 요청이 올 때 마다 새로운 자바 쓰레드를 하나 생성
  * HTTP 서비스 메소드를 실행하고 나면, 쓰레드는 자동으로 소멸
  * 원래는 스레드를 관리해야 하지만 서버가 다중 스레드를 생성 및 운영해주니 스레드의 안정성에 대해서 걱정하지 않아도 된다.
* 웹 서버와 서블릿 컨테이너간 요청 처리 과정
  * 웹서버가 HTTP 요청을 받는다
  * 웹서버는 요청을 서블릿 컨테이너로 전달한다.
  * 서블릿이 컨테이너에 없다면, 서블릿을 동적으로 검색하여 컨테이너의 주소 공간에 로드한다.
  * 컨테이너가 서블릿의 init() 메소드를 호출하면, 서블릿이 초기화된다(서블릿이 처음 로드됬을 때 한번만 호출)
  * 컨테이너가 서블릿의 service() 메소드를 호출하여 HTTP 요청을 처리한다.
  * 웹서버는 동적으로 생성된 결과를 올바른 위치에 반환한다.

## 1.2 Servlet 구동
* Clint가 http 프로토콜 Requst -> Web Server
* Web Server가 Requst -> WAS
* WAS(서블릿 컨테이너)가 HttpServletRequest, HttpServletResponse 인터페이스 객체인 requst, response를 생성해서 service 메소드에 전달한다.
  * service() 메소드는 특정 HTTP 요청(GET, POST 등)을 처리하는 메서드 (doGet(), doPost() 등)를 호출한다.
    * 입력한 정보를 서버에 전송해주는 메소드
    * doGet
      * 보안이 중요하지 않은 데이터 : 보안에 취약함
      * 사용자가 입력한 값이 URL에 보여짐
        * URL창에 “?” 뒤에 데이터를 입력하는 방법(쿼리스트링)
      * 데이터 검색에 많이 사용
      * 기본 명령어
        * response.getWriter().append("Served at: ").append(request.getContextPath());
        * 실행 된 후의 결과 : 웹 브라우저에 "Served at: /프로젝트명"을 출력
    * doPost
      * 중요한 데이터는 URL에 노출하지 않음
      * 입력한 값이 HTTP 헤더 메모리 영역에 저장
* requst, response 객체 데이터로 응답 페이지를 작성한다. (WAS Response Clint)
* destroy() 메소드는 보통 서버가 종료되었을 때, 서블릿의 내용이 변경되어 재 컴파일 될 때 호출된다.

# 2. JSP
## 2.1 개요
* Java Server Page
* java를 이용한 사이드 스크립트 언어(.jsp 파일)
* HTML 내부에 Java 코드를 삽입하여 사용할 수 있게 해준다.
* Servlet과 기능의 차이는 없으며, Servlet으로는 인터페이스를 구현하기 까다로워 사용된다.
* 실행 시 javax.servlet.http.HttpServlet 클래스를 상속받은 Java 파일(Servlet)로 변환한 다음 컴파일되어 실행된다.
* 서블릿 컨테이너가 JSP 파일을 Servlet 파일로 변환하고 실행
* MVC 패턴의 View를 만들 때 이용
* Dynamic Web Project의 Web Content에 파일 생성(이클립스)
* form 태그의 action 속성으로 서블릿 호출(/프로젝트명/서블릿URL(기본적으로는 Servlet 파일명))
* form 태그의 method 속성으로 데이터 전송 방식 선택(doGet(), doPost())
  * method 값을 생략하면 기본으로 get

## 2.2 표기법
* Directive tag
  * <%@ 지시자 %>
  * JSP의 환경 설정
  * java의 import 명령어
* Declaration tag
  * <%! 선언문 %>
  * java의 클래스, 메서드 정의 혹은 변수, 상수 선언
* Scriptlet tag
  * <% 코드 %>
  * java의 명령어
* Expression tah
  * <%= 표현식 %>
  * 하나의 값을 웹 브라우저에 보여줄 때 사용하는 명렁어
* Comments tag
  * <%-- 주석 --%>

# 3. JDBC
## 3.1 개요
* Java DataBase Connectivity
* java에서 데이터베이스에 접근 할 수 있게 해주는 API
* java 소스코드 -> JDBC Interface(DriverManager) -> JDBC Driver -> DBMS 로 구성

## 3.2 코딩 절차
* Driver 로드
  * DriverManager
    * 데이터 원본에 JDBC Driver를 통하여 Connection을 만드는 역할
    * Class.forName() 메소드를 통해 생성되며 예외처리 필수
      * Class.forName("oracle.jdbc.driver.OracleDriver");
    
* DBMS 연결
  * Connection 객체 생성
      * 특정 데이터 원본과 연결된 커넥션을 나타냄
      * 직접적인 객체 생성 불가능, DriverManager의 getConnection() 메소드 사용
      * Connection refConn = DriverManager.getConnection("jdbc:oracle:thin:@localhost:1521:XE", "scott", "tiger");
  * Statement 객체 생성
    * Connection 클래스의 createStatement() 메소드를 사용하여 생성
    * String 객체 안에 쿼리문을 저장
    * 동적인 쿼리문을 사용할 시에는 PreparedStatement 객체 생성
      * PreparedStatement 클래스의 prepareStatement() 메소드를 사용해 동적인 쿼리문을 저장(변수 부분을 ?로 지정)
      *PreparedStatement setString(int, String) 메소드를 사용해 쿼리문 설정(위치(?), 변수)
  * SQL 전송
    * SELECT의 경우 Statement 클래스의 메소드 executeQuery(sql)를 사용하여 쿼리를 실행
      * executeQuery(sql) 메소드는 질의 결과로 테이블 형태의 결과를 반환
      * ResultSet 타입으로 결과 반환
    * create 또는 drop, insert, delete, update와 같이 테이블의 내용을 변경하는 경우 executeUpdate(sql) 메소드 사용
      * INT 타입으로 결과 반환
  * 결과 받기
    * ResultSet 인터페이스에는 질의 결과의 현재 행(row)을 가리키는 커서(cursor)라는 변수가 존재(배열의 인덱스와 유사)
      * 커서는 첫번째 이전 위치를 가지고 있음
      * next() 메소드를 사용해 커서를 다음 행으로 이동
        * while (rs.next())
    * ResultSet 인터페이스의 getString(), getInt() 등 메소드를 사용하여 컬럼의 자료를 참조
      * 커서가 가르키는 행(row)에서 컬럼의 숫자나 컬럼의 이름을 지정
      * getInt(1) = 커서가 가르키는 row에 첫번째 컬럼의 값을 인트로 가져온다
  * 닫기(객체 반환)
    * 생성된 Connection, Statement, ResultSet 객체를 생성된 역순으로 close()메소드를 사용하여 반환