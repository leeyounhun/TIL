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
  - [1.4 Cookie & Session](#14-cookie--session)
    - [1.4.1 개요](#141-개요)
    - [1.4.2 쿠키](#142-쿠키)
    - [1.4.3 세션](#143-세션)
- [2. JSP](#2-jsp)
  - [2.1 개요](#21-개요)
  - [2.2 표기법](#22-표기법)
    - [2.2.1 링크 이동](#221-링크-이동)
  - [2.3 표준 액션 태그](#23-표준-액션-태그)
  - [2.4 EL / JSTL](#24-el--jstl)
    - [2.4.1 EL](#241-el)
  - [2.5 Scope](#25-scope)
  - [2.6 표준 액션 태그](#26-표준-액션-태그)
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
- [6. Spring Framework](#6-spring-framework)
  - [6.1 개요](#61-개요)
  - [6.2 특징](#62-특징)
    - [6.2.1 POJO(Plain Old Java Object)](#621-pojoplain-old-java-object)
    - [6.2.2 DI(Dependency Injection)](#622-didependency-injection)
    - [6.2.3 AOP(Aspect Oriented Programming)의 지원](#623-aopaspect-oriented-programming의-지원)
    - [6.2.4 IOC(Inversion Of Control)](#624-iocinversion-of-control)
  - [6.3 스프링 컨테이너](#63-스프링-컨테이너)
  - [6.4 Maven Project](#64-maven-project)
  - [6.5 Log4j](#65-log4j)
  - [6.6 Spring 구성 모듈](#66-spring-구성-모듈)
  - [6.7 Spring JDBC Template](#67-spring-jdbc-template)
    - [6.7.1 개요](#671-개요)
    - [6.7.2 커넥션 풀](#672-커넥션-풀)
    - [6.7.3 사용법](#673-사용법)
  - [6.8 Spring Transaction](#68-spring-transaction)
  - [6.9 XML](#69-xml)
  - [6.10 Spring MVC](#610-spring-mvc)
  - [6.11 Spring Security](#611-spring-security)
- [7. Mybatis](#7-mybatis)
  - [7.1 개요](#71-개요)
  - [7.2 사용법](#72-사용법)
    - [7.2.1 Session](#721-session)
    - [7.2.2 매퍼 설정 파일(config)](#722-매퍼-설정-파일config)
    - [7.2.3 Mapper XML 파일](#723-mapper-xml-파일)
  - [7.3 mybatis-spring](#73-mybatis-spring)

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

## 1.4 Cookie & Session 
### 1.4.1 개요
* HTTP 프로토콜의 특징이자 약점을 보완하기 위해서 사용한다.
  * HTTP는 TCP 3 Way-Handshake / 4 Way-Handshake를 통해 세션(연결)을 수립한다 
    * 한번의 세션안에서 클라이언트는 서버로 Request를 보내고, 서버로부터 Response를 받으면 세션(연결)이 끊어진다.
  * 연결을 끊는 순간 클라이언트와 서버의 통신이 끝나며 상태 정보는 유지하지 않는다 (무상태성)
  * 리소스 낭비가 줄어드는 것은 큰 장점이지만 통신 시 마다 새로운 세션(연결)을 열어야하는 작업은 클라이언트가 서버에게 요청을 할 때마다 인증을 해야하는 단점이 생겼다.
  * HTTP는 이 2가지 특성을 보완하기 위해서 쿠키와 세션을 사용하게 되었다.
    * 만약 쿠키와 세션이 없다면 어떤 페이지에서 옮겨다닐 때마다 로그인을 다시해야 한다.
    * TCP Session != JSP Session
* 웹 브라우저가 서버로 요청을 하면, 서버는 알맞은 동작을 한 후 웹브라우저에 응답하고 연결을 종료한다.
  * 연결이 끊겼을 때 정보들을 지속적으로 유지하기 위한 수단으로 세션과 쿠키를 사용한다.

### 1.4.2 쿠키
  * 쿠키는 서버에서 생성하고 클라이언트측에 저장된다.
  * 서버에 요청할 때마다 쿠키의 속성값이 변경, 참조될 수 있다.
    * 첫 요청때 쿠키가 클라이언트에 저장된다.
  * 보안에 취약하다
  * 쿠키가 웹 브라우저에 저장되면 웹 브라우저는 해당 서버로 웹 페이지를 요청할 때 마다 쿠키를 함께 전송한다.
    * 응답전송(response), 서버->브라우저 쿠키 전송은 한번만 일어난다.
    * 요청전송(request), 일단 웹 브라우저에 쿠키가 저장되면 삭제되가 전까지 매번 웹 서버로 전송된다.
  * 쿠키 부스러기 처럼 가벼운 정보만을 다룬다.
    * 보안적으로 중요하거나 큰 정보는 세션 사용
    * 쿠키는 하나의 웹 사이트 당 20개 까지만 저장된다.
    * 한 쿠키당 데이터 값은 4096을 넘을 수 없다.
  * 쿠키 생성 
    * Cookie cookie = new Cookie("cookieName",  "cookieValue");
    * response.addCookie(cookie);
      * 클라이언트에 전송
      * 톰캣 8.5에서 새로 추가된 기본 쿠키 규칙
        * 세미콜론, 콤마, 이콜 사인, 그리고 공백은 쿠키 값으로 이용될 수 없다. 
        * ';' , ',', '=' , ' '
  * 쿠키 사용
    * getName()
    * setValue(String value) / getValue()
    * setDomain(String uri) / getDonmain()
    * setPath(String uri) / getPath()
    * setMaxAge(int time) / getMaxAge()
      * 기본값은 -1 -> 따로 설정하지 않으면 웹 브라우저를 닫을때 같이 삭제
### 1.4.3 세션
* 쿠키와 마찬가지로 서버와의 연결이 끊겼을 때 데이터를 유지하는 수단이다.
  * 쿠키와는 달리 서버상에 객체로 저장하게 된다.
  * 클라이언트의 요청이 발생하면 자동으로 생성된다.
  * 세션 내부객체의 메소드를 이용하여 속성을 설정한다.
  * 세션은 서버에서만 접근이 가능하여 보안이 쿠키보다 강하고, 데이터의 용량에 제한이 없다.
  * 세션은 지정한 유효시간만큼 접근하지 않게 되면 웹컨테이너에 의해 자동으로 종료된다.
    * web.xml에서 유효기간 설정
      * <session-timeout>100</session-timeout>(분단위)
    * session의 메소드 사용
      * session.setMaxInactiveInterval(100 * 60)(초단위)
* javax.servlet.http.HttpSession으로 세션 데이터를 다룰 수 있다.
  * setAttribute() :  세션에 데이터를 저장
  * getAttribute() : 해당하는 세션을얻음 (반환형 : Object)
* session을 사용한 로그인 처리과정
  * HTML 폼으로부터 로그인 정보를 받는다.
  * 로그인에 성공하면(= DB에 저장돤 정보와 form으로 입력받은 정보가 같으면) session 기본 객체의 속성에 데이터를 기록한다(session.setAttribute("키", 값);)
  * 이후 각 JSP/Servlet에서 선생 작업으로 session 객체에 접근하여 지정한 속성이 있는지 검사한다.
  * 지정한 속성이 존재한다면 로그인 상태로 간주한다.
  * 사용자가 로그아웃 할 경우 특성 속성을 지우거나 세션을 종료한다.
    * session.invalidate();
    * session.removeAttribute(키);

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
    * <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
  * Core Tags
    * 접두어: c
    * 일반 프로그램 언어에서 제공하는 변수 선언, 조건, 제어 반복문 등의 기능 제어
    * 변수 선언 <c:set var="" name=""/>
    * 변수 출력 <c:out value=""/>
      * escapXML 속성의 값을 true로 지정하면 <>기호를 코드 값으로 변환(lt)
    * 조건문 <c:if test="조건식">
      * else문은 없음
    * switch문 <c: choose> case <c:when test="조건식"> defult<c: otherwise>
    * 반복문 <c: forEach var="변수명" items="배열" begin="시작인덱스" end="종료인덱스">
    * <c:forToken>
      * 문자열을 구분자로 나눠 토큰을 분리해 처리
      * items 속성에 토큰을 포함하는 문자열을 지정
      * delims 속성에 구분자 지정
    * <c:url>
      * url 경로를 설정하고 해당 url의 param 속성을 선언하여 쿼리 스트링을 정의 하는 태그
      * <c:url var="" value="">
  * Formatting Tags
    * 접두어: fmt
    * 메시지의 형식이나 숫자, 날짜 형식과 관련된 포맷 제공
    * <fmt:formatNumber type="" value="" maxIntegerDigits="">
      * type: number, currency, percent
      * 출력 형식을 설정하는 태그
      * 표시하고자 하는 수의 단위 표현 가능
      * 초과하면 해당 자릿수만큼 표시
    * <fmt:setLocal value="">
      * 지역 설정을 통해 통화기호나 시간 대역을 설정
  * Function
  * XML Tags
  * SQL Tags

## 2.5 Scope
* JSP에서는 page, request, session, application 등의 네가지 객체 범위를 제공한다
* 만약 같은 이름의 변수가 page, request에 저장되어 있는 경우, 그 변수를 부르면 작은 범위에 있는 page에 저장 되어있는 변수가 불러진다.
* Application : 웹 어플리케이션이 시작되고 종료될 때까지 변수가 유지되는 경우 사용한다.
* Session : 웹 브라우저 별로 변수가 관리되는 경우 사용한다.
* Request : http요청을 WAS가 받아서 웹 브라우저에게 응답할 때까지 변수가 유지되는 경우 사용한다.
* Page : 페이지 내에서 지역변수처럼 사용한다

## 2.6 표준 액션 태그
* XML 기술을 사용해서 기존 JSP 문법을 확장하는 태그
* 웹 브라우저에서 실행되는게 아닌 컨테이너에서 실행되고 결과만 브라우저로 보냄
* 표준 액션 태그
  * JSP 페이지에서 바로 사용
  * 접두어 jsp: (<jsp:~~>)
* 커스텀 액션 태그
  * 별도의 라이브러리 필요
  * 라이브러리 선언에 따른 접두어 사용 (<c:set>)
* <jsp:include>
  * <%@ include file=“파일 명” %>과 쓰임이 동일하나  jsp파일이 java파일로 변환될 때 삽입되는 <%@ include %>와는 달리 jsp파일이 java파일로 바뀌고 컴파일이 완료되어 런타임 시 삽입
  * 페이지에 다른 페이지를 포함 시킬때 사용
    * 광고 등 동적 페이지에 많이 사용
    * 여러 페이지를 모아 하나의 페이지 구성
* <jsp:forward>
  * 하나의 jsp에서 다른 jsp 페이지로 요청처리를 전달할 때 사용
  * request, response 객체가 같이 전달됨  

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

# 6. Spring Framework
## 6.1 개요
* EJB의 단점들을 극복하기 위해 만들어짐
  * 구조가 복잡하다.
  * 실행속도가 느리다
  * 유지보수에 많은 시간/노력/비용이 든다.
* Framework
  * 프로그램 기본 흐름 및 구조를 정의
  * 라이브러리, 인터페이스, 설정 정보등의 집합
  * 개발 구조를 미리 구성하고 필요한 부분을 조립하는 형태
    * 생산성 상승
* 복잡함에 반기를 들어서 만들어즌 프레임워크
* 개발 생산성과 개발 도구의 지원
* 다른 프레임 워크들의 포용
*  스프링을 사용하기 위해서는 Maven의 의존 설정에 대한 이해가 요구된다.
## 6.2 특징
### 6.2.1 POJO(Plain Old Java Object)
* 일반 java 코드를 이용하여 객체를 구성하는 방식
* 코드 개발시 개발자가 특정 라이브러리나 기술에 종속되지 않음
  * 생산성과 테스트 작업에 유리

### 6.2.2 DI(Dependency Injection)
* 의존성 주입
  * A가 B에 의존하면, B가 변할 때 A도 변한다.
* 의존관계를 외부에서 결정하고 주입하는 것이 DI(의존관계 주입)이다.
  * 즉, 필요한 객체를 직접 생성하는 것이 아닌 외부로 부터 필요한 객체를 받아서 사용하는 것이다.
  * 객체를 외부(Spring)에서 생성해서 사용하려는 주체 객체(A)에 주입시켜주는 방식이다.
    * 참조할 객체를 매개변수로 받는다.
  * 메소드 외부에서 매개변수에 값을 대입한다.
  * 생성자를 통해 주입하거나 Setter 메소드를 이용해 주입한다.
    * 생성자를 통해 주입하면 new를 사용해 만들 때 한번만 주입 가능하다.
      * 컨테이너가 빈을 조립할 때 한번만 호출되고 변경되기 때문에 안정적이다.
      * 가장 많이 사용된다.
    * setter를 사용하면 자기가 원하는 시점에 자유롭게 주입이 가능하다.
      * public으로 setter을 열어둬야 하기 때문에 문제가 생길 수 있다. 
    * 필드에 직접 주입하는것도 가능하지만 변경이 불가능 하기에 자주 사용하지 않는다.
* 클래스 간의 의존관계를 스프링 컨테이너가 자동으로 연결해준다.
* 강하게 결합된 클래스들을 분리하고, 객체 간의 관계를 결정해 줌으로써 결합도를 낮추고 유연성을 확보해준다.
* 한 객체가 다른 객체를 주입받으려면 반드시 DI 컨테이너에 의해 관리되어야 한다.
* 주로 인터페이스를 사이에 둬 클래스 레벨에서는 의존관계가 고정되지 않게 한다.
* XML이나 어노테이션을 사용한다.
  * XML
    * Bean 태그 사용
    * <bean id="" class=" "> 태그로 컨테이너가 생성할 객체를 지정한다.
      * id 속성 값은 <bean> 태그를 이용해서 생성하는 스프링 빈 객체의 고유한 이름으로 사용한다.
      * class 속성은 스프링 컨테이너가 생성할 객체의 클래스 이름을 값으로 갖는다.
    * <property>(setter), <constructor-arg>(생성자)로 빈 객체의 값을 설정한다 (의존성 주입)
      * <value> 태그, value 속성, <ref> 태그, ref 속성을 사용해서 프로퍼티 값을 지정할 수 있다.
    * application.xml 파일에 Bean을 직접 등록하는 것은 고전적인 방법이다.
  * 어노테이션
    * XML을 사용하는 방법 대신 최근에 자주 사용하는 방법이다.
    * @ComponentScan을 사용하는 방법과 자바 코드로 직접 등록하는 방법이 있다.
    * Bean은 @Bean, @Component, @Service, @Repository와 같은 어노테이션으로 생성될 수 있다.
    * @Controller, @Service, @Repository 어노테이션들은 @Component 어노테이션을 상속받고 있다
    * 특정 타입을 리턴하는 메서드를 만들고 @Bean 어노테이션을 붙여주면 자동으로 해당 타입의 Bean이 생성된다.
    * @ComponentScan
      * 해당 어노테이션이 붙어있는 클래스가 Component를 Scan할 시작 지점임을 나타내는 어노테이션이다.
      * 해당 패키지를 포함한 하위 패키지만 대상이 된다.
      * @Component 어노테이션들을 스캔하여 IOC 컨테이너에 적재한다.
      * @Autowired 어노테이션을 사용해 의존성을 연결(주입)한다.
        * IoC컨테이너에 존재하는 빈(Bean)을 찾아 주입하는 역할을 한다.
        * 의존성 주입의 대상이 되는 클래스는 Bean으로 등록된 상태여야 한다.
        * 스프링 빈으로 등록하지 않고 직접 생성한 객체에서는 동작하지 않는다.
    * 자바 코드
      * @configration을 사용하여 XML 파일과 같은 역할을 하는 Bean 설정 파일로서 사용한다.
      * @Bean를 사용한다.
      * 상황에 따라 구현 클래스를 변경해야 하는 경우에 사용한다.
    * 어노테이션으로 Bean을 등록하고 사용하기 위해서는 AnnotationConfigApplicationContext를 사용해야 한다.
  * 스프링 컨테이너는 생성자의 매개변수 뿐 아니라 생성자의 반환형도 검사하기 때문에 중복이 있어선 안된다.
  
### 6.2.3 AOP(Aspect Oriented Programming)의 지원
* 관심 지향 프로그래밍
  * 일종의 개발 방법론
* 어떤 로직을 기준으로 핵심적인 관점, 부가적인 관점으로 나누어서 보고 그 관점을 기준으로 각각 모듈화하는 것
* 소스 코드상에서 다른 부분에 계속 반복해서 쓰는 코드들을 발견할 수 있는 데 이것을 흩어진 관심사 (Crosscutting Concerns)라 부른다.
* 흩어진 관심사를 Aspect로 모듈화하고 핵심적인 비즈니스 로직에서 분리하여 재사용하는 것
* AOP 주요 개념
  * Aspect : 설명한 흩어진 관심사를 모듈화 한 것. 주로 부가기능을 모듈화함.
  * Target : Aspect를 적용하는 위치 (클래스, 메서드 .. )
  * Advice : 실질적으로 어떤 일을 해야할 지에 대한 것, 실질적인 부가기능을 담은 구현체
  * JointPoint : Advice가 적용될 위치, 끼어들 수 있는 지점. 메서드 진입 지점, 생성자 호출 시점, 필드에서 값을 꺼내올 때 등 다양한 시점에 적용가능
  * PointCut : JointPoint의 상세한 스펙을 정의한 것. 'A란 메서드의 진입 시점에 호출할 것'과 같이 더욱 구체적으로 Advice가 실행될 지점을 정할 수 있음
  * 관점
    * Before (이전) : 어드바이스 타겟 메소드가 호출되기 전에 어드바이스 기능을 수행
    * After (이후) : 타겟 메소드의 결과에 관계없이(즉 성공, 예외 관계없이) 타겟 메소드가 완료 되면 어드바이스 기능을 수행
    * AfterReturning (정상적 반환 이후)타겟 메소드가 성공적으로 결과값을 반환 후에 어드바이스 기능을 수행
    * AfterThrowing (예외 발생 이후) : 타겟 메소드가 수행 중 예외를 던지게 되면 어드바이스 기능을 수행
    * Around (메소드 실행 전후) : 어드바이스가 타겟 메소드를 감싸서 타겟 메소드 호출전과 후에 어드바이스 기능을 수행
    * @관점(execution[접근제한자][반환타입]packge.class.method())      
* 스프링 빈에만 AOP를 적용 가능
* 모든 AOP 기능을 제공하는 것이 아닌 스프링 IoC와 연동하여 엔터프라이즈 애플리케이션에서 가장 흔한 문제(중복코드, 프록시 클래스 작성의 번거로움, 객체들 간 관계 복잡도 증가 ...)에 대한 해결책을 지원하는 것이 목적
* 프록시 패턴을 사용
  * 어떤 객체를 사용하고자 할때, 객체를 직접적으로 참조하는 것이 아닌 해당 객체를 대항하는 객체를 통해 대상 객체에 접근하는 방식
  * 장점
    * 사이즈가 큰 객체가 로딩되기 전에도 프록시를 통해 참조를 할 수 있다.
    * 실제 객체의 public, protected 메소드를 숨기고 인터페이스를 통해 노출시킬 수 있다.
    * 로컬에 있지 않고 떨어져있는 객체를 사용할 수 있다.
    * 원래 객체에 접근에 대해 사전처리를 할 수 있다.
  * 단점
    * 객체를 생성할 때 한 단계를 거치게 되므로, 빈번한 객체 생성이 필요한 경우 성능이 저하될 수 있다.
    * 프록시 내부에서 객체 생성을 위해 스레드가 생성, 동기화가 구현되어야 하는 경우 성능이 저하될 수 있다.
    * 로직이 난해해져 가독성이 떨어질 수 있다.
    
### 6.2.4 IOC(Inversion Of Control)
* 제어의 역전
  * 제어는 실행 흐름을 의미
* 객체의 생성을 특별한 관리 위임 주체에게 맡긴다. 이 경우 사용자는 객체를 직접 생성하지 않고, 객체의 생명주기를 컨트롤하는 주체는 다른 주체(컨테이너)가 된다.
  * 클래스 내부의 객체 생성 -> 의존성 객체의 메소드 호출이 아닌, 스프링에게 제어를 위임하여 스프링이 만든 객체를 주입 -> 의존성 객체의 메소드 호출 구조
* 개발자가 프로그램 전체 흐름을 제어하는게 아닌 스프링 프레임워크가 흐름을 제어
* 객체의 생성과 생명주기를 컨테이너가 관리
* 의존 관계를 스프링에서 처리
* 소스코드 자체에 객체를 생성하지 않고 Bean을 이용하여 의존성 주입을 하여 의존 관계를 낮춤


## 6.3 스프링 컨테이너
* 스프링은 객체를 생성하고 각 객체를 연결해주는 조립기의 역할을 수행한다.
* 기본적으로 Bean을 등록할때 싱글톤으로 등록한다.
  * 유일하게 하나만 등록해서 공유
  * 설정으로 싱글톤이 아니게 할 수 있지만 대부분의 경우 싱글톤으로 사용한다.
* 자바 객체 - 빈(Bean)들을 관리하는 공간
  * 빈의 생명 주기를 관리
  * XML, 어노테이션을 사용하여 관리
* IOC나 AOP, DI에 대해서 관리한다.
* Bean Factory와 이를 상속한 ApplicationContext 2가지 유형이 존재한다.
  * Bean Factory는 스프링 설정파일에 등록된 Bean 객체를 생성하고 관리하는 기본적인 기능만 제공한다.
  * 그렇기 때문에 BeanFactory 계열을 사용하기 보단 ApplicationContext 계열을 사용하는 것이 일반적이다.
* 스프링 컨테이너 생성 과정
  * 비어있는 스프링 컨테이너를 생성한다.
  * 스프링 설정 파일(Java, XML 등)을 기반으로 컨테이너에 스프링 빈을 등록한다.
  * 스프링 설정 파일(Java, XML 등)을 기반으로 스프링 빈의 의존관계를 주입(DI)한다
* 서블릿 컨테이너와는 다르게 자동으로 생성되지 않는다.
  * GeericXmlApplicationContext 클래스를 사용하여 메모리에 컨테이너 객체를 생성해야 한다.
    * xml 파일에서 빈 관련 정보를 읽어와 클래스에 저장
* 기본적으로 빈을 생성할때 싱글톤 형식으로 생성한다.
* 빈 객체를 생성한 후 메모리로 로딩한다
  * Laze-Loading
    * Bean Factory 인터페이스에서 사용한다.
    * XML 파일을 메모리에 로드하고 getBean 메소드에 의해 요청을 받는 시점에 인스턴스를 생성하고 로드한다.
    * 자주 사용되지 않는 빈 객체를 사용할때 사용
  * Pre-Loading
    * ApplicationContext 인터페이스에서 사용
    * 모든 빈 객체와 XML 설정 파일들이 ApplicationContext에 의해 로드 요청이 될 때 인스턴스를 생성하고 로드한다.
    * getBean 메소드를 쓰기 전에 이미 빈 객체가 메모리에 로딩
* 트랜잭션의 지원
  * 트랜잭션의 관리를 어노테이션 또는 XML로 설정 가능
  
## 6.4 Maven Project
* 프로젝트에 필요한 의존적인 라이브러리 자동으로 관리
* 자바 패키지를 만들때 aa.bb.cc 3단계로 만들던 것을 추가로 2 분류로 나눈다.
  * Group id
  * Artifact id
* dependencies 태그의 구조
  * 하위에 하나 이상의 dependecny 태그로 구성
  * dependecny 태그 하위에는 groupid, artifactid, version 태그가 반드시 필요
  * 작성 후 접속하면 Maven이 Repository에 접속하여 STS 프로젝트에 파일을 저장
  * 의존관계에 있는 라이브러리를 자동으로 추가 다운로드
  * Springframework 라이브러리 설치시 버젼을 동일하게 해야 한다.

## 6.5 Log4j
로깅(logging)
시스템 동작(실행) 시에 시스템 상태/작동 정보를 시간의 경과에 따라 기록하는 것
사용자의 패턴(유형) 또는 시스템 동작 자체의 분석에 사용
해킹 또는 침입 등의 사고가 발생한 경우 비정상 동작의 기록을 통해 감사 추적 수행
* Log for Java의 약어
* 로그문의 출력을 다양한 대상으로 할 수 있도록 도와주는 도구
* 오픈 소스
* 속도에 최적화
* thread-safe(멀티스레드 환경에서 사용해도 안전)
* 설정 파일은 properties 파일과 XML 형식으로 실행 중 수정 적용 가능
* 다음 6단계의 장애 레벨을 사용. 
  * < TRACE(추가), DEBUG, INFO, WARN, ERROR, FATAL >
  * FATAL: 아주 심각한 에러가 발생한 상태. 
    * 시스템적으로 심각한 문제가 발생해서 어플리케이션 작동이 불가능할 경우
    * 최악은 컴퓨터가 꺼진 상태 또는 문제가 발생해서 제대로 프로그램이 실행이 안되는 상태
    * 프로그램에서는 예외가 발생 -> 강제 종료
    * 일반적으로는 어플리케이션에서는 사용할 일이 없음
  * ERROR(에러: 오류)
    * 요청을 처리하는 중 문제가 발생한 상태를 나타냄
    * 시스템도 멈춤
    * 화면에는 빨간색의 텍스트가 표시
    * 프로그램에서는 구문 오류(문법 오류)
    * 프로그램이 실행되지 않음
  * WARN(경고)
    * 처리 가능한 문제이지만, 향후 시스템 에러의 원인이 될 수 있는 경고성 메시지를 나타냄
    * 현재는 프로그램 실행에는 문제는 없지만 시간이 지나면 문제가 발생할 가능성이 높음
    * 주의사항: 경고 메시지를 보고 원인을 파악 -> 해결책을 찾아서 해결해야 한다.
  * INFO(정보)
    * 로그인, 상태 변경과 같은 정보성 메시지를 나타냄
    * 단순한 알림 메시지
    * 문제가 없는 상태
  * DEBUG
    * 개발시 디버그 용도로 사용한 메시지를 나타냄
    * 예) System.out.println("메시지");


## 6.6 Spring 구성 모듈
* spring-beans 스프링 컨테이너를 이용하여 객체를 생성하는 기본 기능을 제공
  * 스프링 컨테이너: 톰켓 서버를 모델로 하여 새롭게 만든 서버 프로그램
* spring-context
  * 객체 생성, 생명주기 처리, 스키마 확장 등의 기능을 제공

## 6.7 Spring JDBC Template
### 6.7.1 개요
* Spring에서 제공하는 class
* JDBC API에서 반복되는 코드를 거의 제거해 주나 SQL은 직접 작성해야 한다.
* 데이터베이스와 통신을 위해 하는 드라이버 로딩, DB연결, 자원 해제 같은 작업을 스프링 프레임워크에 맡기고, 개발자는 쿼리문을 가지고 질의 응답만을 할 수 있다.
* 데이터베이스 연결과 관련된 정보를 가지고 있는 DataSource 클래스는 스프링 또는 c3p0에서 제공하는 클래스를 이용할 수 있다. 
  * private final JdbcTemplate jdbcTemplate;
  @Autowired
  public JdbcTemplate(DataSource dataSource) {
    jdbcTemplate = new JdbcTemplate(dataSource);
  }
* JdbcTemplate를 사용하기 위해선 레파지토리 의존 설정(pom.xml) 을 미리 해주어야 한다.

### 6.7.2 커넥션 풀
* 요청마다 매번 DB 연결을 새로 하는 것은 서버에 부하를 줄 수 있기 때문에 DB 연결을 미리 준비해놓고 사용하는 방법이다.
* 프로그램 시작 후 여러 연결 객체를 미리 생성한다.
* 대표적인 커넥션풀을 지원하는 오픈소스는 아파치 DBCP와 c3p0가 있으며 spring, mybatis, hibernate 등과 통합되어 DataSource를 구성하여 사용한다.

### 6.7.3 사용법
* queryForObject
  * SQL 쿼리를 사용 할 때 사용
  * Object jdbcTemplate.queryForObject(SQL구문, 반환 타입, 인자);
  * queryForObject의 반환형은 기본 데이터형만 가능
* RowMapper 인터페이스
  * RowMapper를 사용하면 원하는 형태의 결과값을 반환할 수 있다.
  * mapRow 메소드는 ResultSet을 사용한다.
    * User mapRow(ResultSet rs, int count);
    * ResultSet에 값을 담아와서 User 객체에 저장하는 것을 count만큼 반복한다.

## 6.8 Spring Transaction
* 스프링에서는 트랜잭션을 처리하는 방법을 2가지 제공해준다.
* 직접 코드 구현 방식
  * TransactionTemplate
  * 직접 PlatformTransactionManager 구현하기.
  * 트랜잭션 관리 부분이 비즈니스 로직과 함께 위치하기 때문에 자주 쓰이지 않는다.
* 선언적 방식
  * 트랜잭션 처리를 컨테이너가 자동으로 처리하도록 설정할 수 있다.
  * Spring AOP가 사용된다.
    * AOP를 이용한 트랜잭션을 분리한다.
  * xml이나 @Transactional 어노테이션을 사용한다.
    * @Transactional 어노테이션을 사용하면 내부적으로 if문을 만들어서 처리한다(autocommit).
    * 클래스 단위 혹은 메소드 단위 선언
      * 우선순위: 클래스 메소드 > 클래스 > 인터페이스 메소드> 인터페이스
    * @Transactional이 선언되면 해당 클래스에 트랜잭션이 적용된 프록시 객체 생성
    * 프록시 객체는 트랜잭션을 실행하고 rollback나 commit을 수행
## 6.9 XML
* 웹에서 구조화한 문서를 표현하고 전송하도록 설계한 마크업 언어
  * 문서의 본문 내용 의외에 첨가되는 부가적인 정보를 기술하는 언어
  * HTML, XML 등
* 문서 내용에 대한 구조와 의미를 기술하기 위한 언어
  * 일반 문서에서 "이름" 이란 표현이 있으면 XML을 사용해 이름에 의미를 부여한 표현이 가능하다
* 컴퓨터 분야 뿐만 아니라 학술 분야와 산업 분야에서 사용하고 있는 표준화된 문서를 다루는데 필수적인 기술이다.
  * W3C(World Wide Wed Consortium)에서 XML을 표준화 한다.
* HTML과 다르게 보안과 제한사항을 추가할 수 있다.

## 6.10 Spring MVC

## 6.11 Spring Security
* 스프링 기반 앱에서 보안을 담당하기 위해 만들어진 하위 프레임워크
* 접근주체, 인증, 권한, 인가 등을 관리한다.
  * 인증(Authentication): 해당 사용자가 본인이 맞는지를 확인하는 절차
  * 인가(Authorization): 인증된 사용자가 요청한 자원에 접근 가능한지를 결정하는 절차
* 주로 서블릿 필터와 필터 체인으로 위임 모델을 사용한다.
  * '인증'과 '권한'에 대한 부분을 Filter 흐름에 따라 처리한다.
    * 스프링 시큐리티는 필터를 거쳐 서블릿 서비스에 도착한다. 
  * Filter는 Dispatcher Servlet으로 가기 전에 적용되므로 가장 먼저 URL 요청을 받지만, Interceptor는 Dispatcher와 Controller사이에 위치한다는 점에서 적용 시기의 차이가 있다. 
  * 스프링 시큐리티는 필터를 체인처럼 엮어논다. 이를 필터 체인이라고 하고, 모든 request는 이 필터 체인을 반드시 거쳐야만 서블릿에 도달할 수 있다. 
  * 스프링 시큐리티의 필터에는 아주 다양한 필터들이 존재한다. 각각의 필터는 각기 서로 다른 관심사를 해결한다.


# 7. Mybatis
## 7.1 개요
* 데이터의 CRUD를 보다 편하게 하기 위해 xml로 구조화한 Mapper 설정 파일을 통해서 JDBC를 구현한 영속성 프레임워크
  * SQL을 별도 파일(mapper.xml)로 분리한다.
  * 유지보수와 재사용이 용이하다.
* 기존 JDBC를 통해 구현하던 코드의 파라매터 설정 및 결과 매핑을 xml설정을 통해 쉽고 간단하게 구현할 수 있다.
  * sql 실행 결과를 Map 객체에 매핑한다.
    * sql 구문과 객체를 연결하는것을 매핑이라 한다.
  * 매핑 작업을 자동으로 수행된다.
* 데이터베이스 레코드에 원시타입과 Map 인터페이스 그리고 자바 POJO 를 설정해서 매핑하기 위해 XML과 애노테이션을 사용할 수 있다.
* 데이터소스 기능과 트랜잭션 처리 기능을 제공한다.

## 7.2 사용법
* 마이바티스를 사용하기 위해선 mybatis-x.x.x.jar 파일을 클래스패스에 두거나 메이븐 dependency를 설정해야 한다.
* 마이바티스가 제공하는 대부분의 기능은 XML을 통해 매핑 기법을 사용한다. 
* 한 개의 매퍼 XML 파일에는 많은 수의 구문을 매핑할 수 있다.
* DTO 파일과 DAO 파일(java), Config파일과 Mapper파일(xml)을 사용한다

### 7.2.1 Session
* 모든 마이바티스 애플리케이션은 SqlSessionFactory 인스턴스를 사용한다.
* Session 클래스는 CRUD를 위한 다양한 메서드를 제공한다.
* 세션을 한번 생성하면 매핑구문을 실행하거나 커밋 또는 롤백을 하기 위해 세션을 사용할수 있다. 
* SqlSessionFactoryBuilder는 XML설정파일에서 SqlSessionFactory인스턴스를 생성한다.
* SqlSession 은 데이터베이스에 대해 SQL명령어를 실행하기 위해 필요한 모든 메소드를 가지고 있다.
* 마이바티스는 클래스패스와 다른 위치에서 자원을 로드하는 것으로 좀더 쉽게 해주는 Resources 라는 유틸성 클래스를 가지고 있다.
  * String resource = "config.xml";
InputStream inputStream = Resources.getResourceAsStream(resource);
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
* 생성된 SqlSession 인스턴스를 통해 SQL 구문을 실행할 수 있다. 
  * List selectList(query_id)	id에 대한 select문을 실행한 후 레코드를 List로 반환한다.
  * List selectList(query_id, '조건')	id에 대한 select문을 실행하면서 조건(쿼리문에서 사용할 인자)를 전달한다.
  * T selectOne(query_id)	id에 대한 select문을 실행한 후 한개의 레코드를 지정한 타입으로 반환한다.
  * T selectOne(query_id, '조건')	id에 대한 select문을 실행하면서 조건(쿼리문에서 사용할 인자)를 전달한다.

### 7.2.2 매퍼 설정 파일(config)
* 마이바티스 XML 설정파일은 다양한 설정과 프로퍼티를 가진다.
* configuration
  properties
  * settings
  * typeAliases
  * typeHandlers
  * objectFactory
  * plugins
  * environments
    * environment
      * transactionManager
      * dataSource
        * 프로그램에서 사용할 DB관련 정보
        * 
  * databaseIdProvider
  * mappers

### 7.2.3 Mapper XML 파일
* cache - 해당 네임스페이스을 위한 캐시 설정
* cache-ref - 다른 네임스페이스의 캐시 설정에 대한 참조
* resultMap - 데이터베이스 결과데이터를 객체에 로드하는 방법을 정의하는 엘리먼트
  * 복잡한 결과 매핑을 간편하게 만들어주기 위해 만들어진 태그다.
* sql - 다른 구문에서 재사용하기 위한 SQL 구문
* insert - 매핑된 INSERT 구문.
* update - 매핑된 UPDATE 구문.
* delete - 매핑된 DELEETE 구문.
* select - 매핑된 SELECT 구문.
  * 대부분의 애플리케이션은 데이터를 수정하기보다는 조회하는 기능이 많기 때문에 마이바티스는 데이터를 조회하고 그 결과를 매핑하는데 집중하고 있다.
  * 각각의 구문이 처리하는 방식에 대해 세부적으로 설정하도록 많은 속성을 설정할 수 있다.
    * id - 구문을 찾기 위해 사용될 수 있는 네임스페이스내 유일한 구분자
    * parameterType - 구문에 전달될 파라미터의 패키지 경로를 포함한 전체 클래스명이나 별칭
    * resultType - 이 구문에 의해 리턴되는 클래스명 전체 또는 alias를 입력, 즉 매핑하려는 자바 클래스의 전체 경로를 입력한다.
    * resultMap - 외부 resultMap 선언 당시 참조로 사용한 이름을 입력한다. 사용하면 자동으로 매핑된다.
    * flushCache - 이 값을 true 로 셋팅하면 구문이 호출될때마다 캐시가 지워진다. 디폴트는 false
    * useCache - 이 값을 true 로 셋팅하면 구문의 결과가 캐시된다. 디폴트는 true.
    * timeout - 예외가 던져지기 전에 데이터베이스의 요청 결과를 기다리는 최대시간을 설정한다.
    * fetchSize - 지정된 수만큼의 결과를 리턴하도록 하는 드라이버 힌트 형태의 값이다
    * statementType - STATEMENT, PREPARED, CALLABLE 중 하나를 선택할 수 있다. 마이바티스에게 Statement, PreparedStatement 또는 CallableStatement를 사용하게 한다. 디폴트는 PREPARED.
    * resultSetType - FORWARD_ONLY, SCROLL_SENSITIVE, SCROLL_INSENSITIVE, DEFAULT중 하나를 선택할 수 있다.
    * databaseId - 설정된 databaseIdProvider가 있는 경우 마이바티스는 databaseId 속성이 없는 모든 구문을 로드하거나 일치하는 databaseId와 함께 로드된다
    * resultOrdered - 결과를 조회하는 구문에서만 적용이 가능하다. true로 설정하면 내포된 결과를 가져오거나 새로운 주요 결과 레코드를 리턴할때 함께 가져오도록 한다. 이전의 결과 레코드에 대한 참조는 더 이상 발생하지 않는다.

## 7.3 mybatis-spring
* MyBatis를 Spring Framework에 녹여내 좀 더 쉽게 사용하고자하는 연동 모듈
* 마이바티스로 하여금 스프링 트랜잭션에 쉽게 연동되도록 처리한다.
* SqlSessionFactoryBean과 SqlSession을 Spring Framework의 Bean으로 등록하여 관리한다.
* 마이바티스 예외를 스프링의 DataAccessException로 변환하기도 하고 마이바티스, 스프링 또는 마이바티스 스프링 연동모듈에 의존성을 없애기도 한다.