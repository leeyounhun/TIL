# 목차
<!-- TOC -->

- [목차](#목차)
- [1. 집합과 맵](#1-집합과-맵)
  - [1.1 HashMap](#11-hashmap)
  - [1.2 HashSet](#12-hashset)

<!-- /TOC -->
# 1. 집합과 맵

## 1.1 HashMap
  * Map 인터페이스를 구현한 컬렉션
  * hash 테이블로 키와 값으로 된 객체를 저장한다.
    * 키는 고유한 값을 가진다
  * HashMap<키 제네릭, 값 제네릭> 이름 = new HashMap<>();
  * put(key, value), get(key), reMove(key), size(), entrySet(), keySet(), values(), replace(key, value), containsKey(key) / containsValue(value), clear()
    * entrySet(): HashMap의 모든 요소를 'key = value' 형태로 Set으로 반환
    * keySet(): HashMap의 모든 key를 Set으로 반환
    * values(): HashMap의 모든 값을 Collection으로 반환

## 1.2 HashSet
  * Set(집합) 인터페이스를 구현한 컬렉션
    * 중복을 허용하지 않고, 순서대로 입력되지 않음
  * HashSet<제네릭> 이름 = new HashSet<>();
  * add(value), remove(value), size(), clear(), contains(value), iterator(); 
