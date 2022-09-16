# 0. 목차
<!-- TOC -->

- [0. 목차](#0-목차)
- [1. 개요](#1-개요)
- [2. 특징](#2-특징)
- [3. 기본 구조](#3-기본-구조)

<!-- /TOC -->
# 1. 개요
* HTML
  * 하이퍼 텍스트를 구현하기 위한 뼈대가 되는 핵심적인 기술
  * 마크업 언어
* CSS
  * HTML을 꾸미기 위한 기능
* jQuery
  * JavaScript의 라이브러리중 하나
  * 더 적게 쓰고(write) 더 많이 쓴다(use)
* 자바와는 관련이 없음
# 2. 특징
* 로컬의 브라우저에서 실행되는 인터프리터 방식의 프로그래밍 언어
  * 인터프리터: 명령어를 한 줄씩 번역해 바로 실행
* 객체기반 스크립트 언어
  * 스크립트 언어는 빠르게 배우고 작성하기 위해 고안됨
    * 혼자서는 독립적으로 실행 불가능하다.
    * 짧은 소스 코드 파일이나 REPL(Read Eval Print Loop)로 상호작용함.
    * 주로 기본 프로그램 동작을 사용자 요구에 맞게 수행하는 용도로 사용 = 보조적
  * 클라이언트 사이드 스크립트 언어
    * 사용자 컴퓨터에서 처리되는 스크립트 언어
* ECMA 스크립트 표준을 따르는 대표적인 웹 기술
  * ECMA 자바 스크립트 표준화 기구
  * 모질라(https://developer.mozilla.org/ko/docs/Web/JavaScript)에서 한글도 제공

# 3. 기본 구조
* HTML에서 제공하는 <script></script> 태그를 사용
* 작성방식
  * inline 방식
    * JS의 양의 적을때 사용
    * 태그에 이벤트 핸들러 속성을 이용하여 직접 실행 코드 작성
  * internal 방식
    * 가장 일반적인 방식
    * html 파일 내 <head> 나 <body> 태그 안에 스크립트 소스 작성
  * external 방식
    * 자바 스크립트의 양이 많을 경우 코드 부분을 외부 파일로 저장하여 작성
    * 가장 많이 쓰는 방식
* 데이터 출력
  * document.write(내용);
    * 브라우저 화면 상의 페이지에 값 출력
  * window.alert(내용);
    * 내용을 메시지 창에 출력
  * innerHTML = 내용;
    * 태그 엘리먼트의 내용을 변경하여 출력
  * console.log(내용);
    * 개발자 도구 화면의 콘솔에 출력