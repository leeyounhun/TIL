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
  - [2.3 표준 액션 태그](#23-표준-액션-태그)
  - [2.4 EL / JSTL](#24-el--jstl)
    - [2.4.1 EL](#241-el)
    - [2.4.2 JSTL](#242-jstl)
- [3. JDBC](#3-jdbc)
  - [3.1 개요](#31-개요)
  - [3.2 코딩 절차](#32-코딩-절차)
- [4. 디자인 패턴](#4-디자인-패턴)
  - [4.1 싱글톤(Singleton) 패턴](#41-싱글톤singleton-패턴)
    - [4.1.1 개요](#411-개요)
    - [4.1.2 사용례](#412-사용례)
    - [4.1.3 사용 형식](#413-사용-형식)
- [5. 다이어그램](#5-다이어그램)
  - [5.1 유스케이스 다이어그램](#51-유스케이스-다이어그램)
    - [5.1.1 개요](#511-개요)
    - [5.1.2 구성요소](#512-구성요소)
  - [5.2 시퀀스 다이어그램](#52-시퀀스-다이어그램)
    - [5.2.1 개요](#521-개요)
    - [5.2.2 구성요소](#522-구성요소)

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
  * 프로그램의 기능을 구현하는 복잡한 로직은 서블릿 클래스 안에 기술하고, 그 결과를 가져다가 출력하는 일만 JSP 페이지가 담당
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
* Expression tag
  * <%= 표현식 %>
  * 하나의 값을 웹 브라우저에 보여줄 때 사용하는 명렁어
* Comments tag
  * <%-- 주석 --%>

### 2.2.1 링크 이동
* <a href="이동할 페이지.jsp?객체=값" id=""><a>
  * 이동할 페이지로 이동후 객체를 전달
  * doGet 방식
  * 받는 쪽 페이지 에서는 E 객체 = request.getParameter("객체명");을 사용하여 값 전달 받음

## 2.3 표준 액션 태그
* JSP에서 기본적으로 제공하는 태그
* <jsp:useBean>
  * JavaBean 객체를 사용하기 위한 태그
    * JavaBean: 가장 저장 공간을 적게 사용하는 단순한 구조의 클래스
    * 자바의 재활용 가능한 컴포넌트 모델
    * 정보의 덩어리로, 데이터 저장소이다.
    * JSP에 보여주는 데이터를 데이터를 담기 위해 만들어 사용한다.
    * 필드, 기본 생성자, getter / setter 로만 이루어짐
  * <jsp:setProperty><jsp:getProperty>와 사용
    * <jsp:setProperty> : 자바 빈에 정보를 저장
    * <jsp:getProperty> : 자바 빈에서 정보를 얻음 
    * request.getParameter(); 명령어를 사용하지 않는다.
  * <jsp:useBean id="" class=".Bean">
      <jsp:setProperty name="" property=""></jsp:setProperty>
    </jsp:useBean>
* JSP에서 사용하는 VO, DTO, Entity와 동일
  * DTO(Data Transfer Object): 계층(Layer)간 데이터 교환을 위해 사용하는 객체
    * 데이터 교환만을 위해 사용하므로 로직을 갖지 않고, getter/setter 메소드만 갖는다.
  * VO(Value Object)는 값 그 자체를 표현하는 객체이다.
    * 로직을 포함할 수 있으며, 객체의 불변성(객체의 정보가 변경하지 않음)을 보장한다.
  * Entity: 실제 DB의 테이블과 매핑되는 객체이다. 

## 2.4 EL / JSTL
### 2.4.1 EL
* Expression Language
  * 표현식에 더 많은 형식을 추가
  * 자바 빈의 프로퍼티, 값을 jsp 표현식 <%=%>이나 액션태그 <jsp:useBean>를 사용하는것보다 쉽고 간결하게 꺼낼 수 있게하는 기술이다.
* 페이지의 가독성을 상승시키기 위해 사용
* 자바 빈 액션태그를 사용하는 것보다 관리가 쉽다.
* Parameter 형식
  * parameter : 브라우저(사용자) 요청에서 넘어온 값
  * <%= request.getParameter("name")%>
  * ${param.name} 동일
* Attribute 형식
  * attribute : 개발자가 코딩으로 설정하는 값
  * ${value} 형식으로 사용

### 2.4.2 JSTL
* JSP Standard Tag Library
* JSP 표준 태그 라이브러리
* JSP에서 자주 사용하는 기능을 구현하는 커스텀 태그 라이브러리
  * JPS 태그 명령어를 미리 정의해서 저장해 둔 것
* JSP를 보완하기 위해 등장
* EL을 기본으로 사용
* 개발속도 상승, 가독성 상승
  * JSTL을 사용하면 개발자는 HTML과 태그로만 구성된 일관된 소스를 볼 수 있다.
  * <% 기호(스크립틀릿) 없이 오로지 태그로만 구성이 가능해진다.
* WEB-INF/lib 폴더에 jstl.jar, standard.jar 첨부
* jsp 상단에 taglib 선언 및 사용
* Core Tag
  * 접두어: c
  * 일반 프로그램 언어에서 제공하는 변수 선언, 조건, 제어 반복문 등의 기능 제어
  * 변수 선언 <c:set var="" name=""/>
  * 변수 출력 <c:out value=""/>
    * escapXML 속성의 값을 true로 지정하면 <>기호를 코드 값으로 변환(lt)
  * 조건문 <c:if test="조건식">
    * else문은 없음
  * switch문 <c: choose> case <c:when test="조건식"> defult<c: otherwise>
  * 반복문 <c: forEach var="변수명" items="배열" begin="시작인덱스" end="종료인덱스">
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

# 5. 다이어그램
## 5.1 유스케이스 다이어그램
### 5.1.1 개요
* Use + case 다이어그램
* 시스템과 사용자의 상호작용을 다이어그램으로 표현한 것
* 사용자의 관점에서 시스템의 서비스 혹은 기능 및 그와 관련한 외부 요소를 보여주는 것
* 동적(행위) 다이어그램
* 여러 업무 프로세스를 설명하는데 자주 사용

### 5.1.2 구성요소
* 액터
  * 시스템과 상호작용을 하는 외부의 존재
    * 시스템 관점에서 바라본 사용자 혹은 타 시스템
* 유스케이스
  * 개발 대상이 되는 시스템이 제공하는 개별적인 기능
  * 사용자가 인지할 수 있는 시스템의 기능 단위
* 관계
  * 연관 관계
    * 유스케이스와 액터간 상호작용을 의미하는 관계
    * 유스케이스와 액터간 관계만 가능(액터-액터, 유스케이스-유스케이스 불가능)
  * 포함 관계
    * 한 유스케이스가 다른 유스케이스의 기능을 포함하는 관계
    * 어떤 기능을 수행하기 위해 필수적으로 필요한 기능
      * 개인정보조회 --<<include>>--> 로그인
      * 개인정보 조회를 위해선 필수적으로 로그인 필요
  * 확장 관계
    * 기본 유스케이스에서 특정 조건이나 선택에 따라 발생하는 유스케이스
      * 선택적으로 할 수 있는 관계
      * 파일업로드--<<extend>>-->게시글 등록
  * 일반화 관계
    * 유사한 유스케이스 또는 액터들을 추상화 하여 하나의 유스케이스로 그룹화 하여 이해도를 높인 관계
  * 액터 -> 유스케이스
    * 액터가 유스케이스를 활성화 시킴
  * 유스케이스 -> 액터
    * 유스케이스 결과게 액터에 통보됨
    * 외부 시스템에 서비스 실행을 요청함

## 5.2 시퀀스 다이어그램
### 5.2.1 개요
* Sequence Diagram
* 동적(행위) 다이어그램
* 시간에 따른 객체간의 상호작용을 표현
  * 객체 사이의 주고받는 메시지를 시간 순서대로 표현
* 객체 간 기능, 순서, 시간을 명확하게 표현
* 클래스 다이어그램 작성 후 작성
  * 유스케이스 -> 클래스 -> 시퀀스 순

### 5.2.2 구성요소
* 생명선
  * 액터, 클래스 객체, 컴포넌트 인스턴스 등 상효작용에 참여하는 구체적인 대상의 생명주기 표현
* 메시지
  * 생명선간 전달되어 상태의 행위에 대한 호출
  * 재귀 메시지
  * 답신 메시지
* 객체
* 제어 블록
* 활성화 블록