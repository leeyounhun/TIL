# 목차
<!-- TOC -->

- [목차](#%EB%AA%A9%EC%B0%A8)
- [JSP](#jsp)
  - [개요](#%EA%B0%9C%EC%9A%94)
  - [WAS](#was)
  - [표기법](#%ED%91%9C%EA%B8%B0%EB%B2%95)
- [JDBC](#jdbc)

<!-- /TOC -->
# 1. JSP

## 1.1 개요
* Java Server Page
* java를 이용한 사이드 스크립트 언어.
* HTML 내부에 Java 코드를 삽입하여 사용할 수 있게 해준다.
* Servlet과 기능의 차이는 없으며, Servlet으로는 인터페이스를 구현하기 까다로워 사용된다.
* 실행 시 javax.servlet.http.HttpServlet 클래스를 상속받은 Java 파일(Servlet)로 변환한 다음 컴파일되어 실행된다.
* JSP 파일을 Servlet 파일로 변환하고 실행하는 프로그램을 서블릿 컨테이너라고 한다. 대표적으로는 톰캣
* MVC 패턴의 View를 만들 때 이용
## 1.2 WAS
* Web Application Server
* 사용자가 요청한 서비스의 결과를 스크립트 언어로 가공하여 동적인 페이지를 제공
* tomcat 등
## 1.3 표기법
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
 * <%= 표현신 %>
 * 하나의 값을 웹 브라우저에 보여줄 때 사용하는 명렁어
* Comments tag
  * <%-- 주석 --%>
# 2. JDBC