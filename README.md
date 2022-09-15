# 목차
<!-- TOC -->

- [목차](#목차)
- [1. Servlet](#1-servlet)
  - [1.1 개요](#11-개요)
    - [1.1.1 서블릿 컨테이너](#111-서블릿-컨테이너)
  - [1.2 Servlet 구동](#12-servlet-구동)
  - [1.3 페이지 이동](#13-페이지-이동)
    - [1.3.1 포워딩(forwarding) 기법](#131-포워딩forwarding-기법)
    - [1.3.2 리다이렉트 방법](#132-리다이렉트-방법)
- [2. JSP](#2-jsp)
  - [2.1 개요](#21-개요)
  - [2.2 표기법](#22-표기법)
  - [2.2.1 링크 이동](#221-링크-이동)
- [3. JDBC](#3-jdbc)
  - [3.1 개요](#31-개요)
  - [3.2 코딩 절차](#32-코딩-절차)
- [4. 디자인 패턴](#4-디자인-패턴)
  - [4.1 싱글톤(Singleton) 패턴](#41-싱글톤singleton-패턴)
    - [4.1.1 개요](#411-개요)
    - [4.1.2 사용례](#412-사용례)
    - [4.1.3 사용 형식](#413-사용-형식)

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
* Clint가 http 프로토콜 Request -> Web Server
* Web Server가 Request -> WAS
* WAS(서블릿 컨테이너)가 HttpServletRequest, HttpServletResponse 인터페이스 객체인 request, response를 생성해서 service 메소드에 전달한다.
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
      * a태그는 get 방식만 표현 가능
    * doPost
      * 중요한 데이터는 URL에 노출하지 않음
      * 입력한 값이 HTTP 헤더 메모리 영역에 저장
* request, response 객체 데이터로 응답 페이지를 작성한다. (WAS Response Clint)
* destroy() 메소드는 보통 서버가 종료되었을 때, 서블릿의 내용이 변경되어 재 컴파일 될 때 호출된다.

## 1.3 페이지 이동
### 1.3.1 포워딩(forwarding) 기법
* 페이지 주소(URL)은 바뀌지 않고 내용만 바뀐다.
  * 웹 컨테이너(Web Container) 차원에서만 페이지 이동
  * 클라이언트는 다른 페이지로 이동을 했는지 알 수 없다.
* 페이지가 바뀌어도 request는 바뀌지 않으므로 요청에 속성을 설정해서 이동할 페이지로 값을 가져 갈 수 있다.
* javax.servlet.RequestDispatcher 인터페이스를 사용해서 객체 생성
  * request 객체의 getRequestDispatcher("이동할 페이지")메소드를 사용
  * forward() 메소드를 호출해서 이동
  * javax.servlet.RequestDispatcher rd = request.getRequestDispatcher("이동할 페이지");
  * rd.forward(request, response);
* request, response 객체를 계속해서 사용 가능
  * 페이지 주소(URL)가 바뀌지 않았기 때문
* 특정 URL에 대해 외부에 공개되지 않아야 하는 부분을 사용하거나 조회를 위해 사용

### 1.3.2 리다이렉트 방법
* 페이지 주소(URL)와 내용이 바뀐다.
  * 추가적으로 발생한 처리 때문에 포워딩보다 느리다.
* response.sendRedirect("이동할 페이지")
* request, response 객체도 바뀌게 된다.
* 최초 요청을 받은 첫 번째 URL에서 클라이언트에 Redirect할 두 번째 URL을 리턴하고, 클라이언트는 전혀 새로운 요청을 생성하여 두 번째 URL에 다시 요청을 보낸다.
* 클라이언트의 요청에 따라 서버의 DB에 변화가 생기는 작업에 사용
  * 요청을 중복으로 보내는 것을 방지

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

## 2.2.1 링크 이동
* <a href="이동할 페이지.jsp?객체=값" id=""><a>
  * 이동할 페이지로 이동후 객체를 전달
  * doGet 방식
  * 받는 쪽 페이지 에서는 E 객체 = request.getParameter("객체명");을 사용하여 값 전달 받음

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
        * count = rs.executeUpdate()
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
      * 힙 메모리에 생성된 객체의 구조가 1차원 배열 형식이기 때문

# 4. 디자인 패턴
## 4.1 싱글톤(Singleton) 패턴
### 4.1.1 개요
* 자바에서 가장 단순한 디자인 패턴중 하나
* 하나의 클래스 만을 정의해서 사용(단독)
* 생성 패턴의 일부
  * 객체를 생성하는 가장 단순하고 편한 방법
* 다른 클래스와의 관계가 존재하지 않음
* 단일 객체만을 생성하는 단독 클래스가 포함
  * 하나의 객체만을 생성

### 4.1.2 사용례
* JDBC DB 연결 객체 생성 전용 클래스로 정의
  * Class.forName(): 드라이버 생성(로딩);
  * getConnection(): 자바와 DB를 서로 연결
  * 데이터 베이스 연괄 과정에서 시간을 절약
* static 으로 객체를 생성(주소 고정)
  * 하나의 객체만 관리하기 위해 사용


### 4.1.3 사용 형식
* 참조변수를 선언
   * 기본 형식
    * 참조변수 선언과 객체 생성을 동시에
  * 응용 형식
    * 참조변수 선언과 객체 생성을 분리
      * if(생성 객체 == null){} 안에 객체 생성 관련 내용 작성
      * 생성할 객체가 존재하면 새로운 객체를 생성하지 않음.
  * static 제한자 필수
    * 힙 메모리에 하나의 객체를 생성
  * private 접근 제한자 사용
    * 하나의 클래스 내부에서 사용
    * 객체의 수를 1개로 제한
* 기본 생성자를 private 접근 제한자로서 선언
* setter 사용 불가능
  * 현재 참조하는 객체의 주소를 유지 하기 위해서
  * 메모리 공간의 낭비를 막기 위함