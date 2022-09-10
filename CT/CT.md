# 목차
<!-- TOC -->

- [목차](#목차)
- [1. 집합과 맵](#1-집합과-맵)
  - [1.1 HashMap](#11-hashmap)
  - [1.2 HashSet](#12-hashset)
- [2. String](#2-string)
  - [2.1 자르기](#21-자르기)
- [3. Stack](#3-stack)

<!-- /TOC -->
# 1. 집합과 맵

## 1.1 HashMap
* Map 인터페이스를 구현한 컬렉션
* hash 테이블로 키와 값으로 된 객체를 저장한다.
  * 키는 고유한 값을 가진다
  * HashMap<keyElement,valueElement> 이름 = new HashMap<>();
  * put(key, value), get(key), reMove(key), size(), entrySet(), keySet(), values(), replace(key, value), containsKey(key) / containsValue(value), clear()
    * entrySet(): HashMap의 모든 요소를 'key = value' 형태로 Set으로 반환
    * keySet(): HashMap의 모든 key를 Set으로 반환
    * values(): HashMap의 모든 값을 Collection으로 반환

## 1.2 HashSet
<<<<<<< HEAD:CT.md
* Set(집합) 인터페이스를 구현한 컬렉션
  * 중복을 허용하지 않고, 순서대로 입력되지 않음
* HashSet<Element> 이름 = new HashSet<>();
* add(value), remove(value), size(), clear(), contains(value), iterator(); 

# 2. String

## 2.1 자르기
* substring()
  * substring(int)
    * int부터(포함) 끝까지 문자열 반환
  * substring(int1, int2)
    * int1 부터(포함) int2전 까지(미포함) 문자열 반환
* split(char)
  * char을 기준으로 문자열 분할해서 Array로 반환
  
# 3. Stack
* List 인터페이스를 상속받는 컬렉션
* Queue와 함께 자바에서 사용되는 대표적인 자료 구조
* 마지막의 추가된 데이터가 가장 먼저 나오는 후입선출(LIFO) 구조
* 재귀함수 호출, 인터럽트 처리, 깊이 우선 탐색(DFS)등 에서 주로 사용
* Stack<Element> stack = new Stack<>();
* push(value), pop(value), peek(value), contains(value), size(), empty(), clear()
=======
  * Set(집합) 인터페이스를 구현한 컬렉션
    * 중복을 허용하지 않고, 순서대로 입력되지 않음
  * HashSet<제네릭> 이름 = new HashSet<>();
  * add(value), remove(value), size(), clear(), contains(value), iterator(); 
>>>>>>> d763e81a9eea21bc3b7ad10a4a59e316503f72d4:CT/CT.md
