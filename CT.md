# 목차
<!-- TOC -->

- [목차](#목차)
- [1. 집합과 맵](#1-집합과-맵)
  - [1.1 HashMap](#11-hashmap)
  - [1.2 HashSet](#12-hashset)
- [2. String](#2-string)
  - [2.1 자르기](#21-자르기)
- [3. Stack](#3-stack)
- [4. Queue](#4-queue)
  - [4.1 Deque](#41-deque)
- [5. Heap](#5-heap)

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
  * 정규식 검사, 빈문자열 포함
* StringToknizer(str, char)
  * str을 char 기준으로 분할
  * 정규식 검사가 아님.
  * "[]," 식으로 구분자 여러개 사용 가능
  
# 3. Stack
* List 인터페이스를 상속받는 컬렉션
* Queue와 함께 자바에서 사용되는 대표적인 자료 구조
* 한쪽에서만 삽입과 삭제가 가능
* 마지막의 추가된 데이터가 가장 먼저 나오는 후입선출(LIFO) 구조
* 재귀함수 호출, 인터럽트 처리, 깊이 우선 탐색(DFS)등 에서 주로 사용
* Stack<Element> stack = new Stack<>();
* push(value), pop(value), peek(value), contains(value), size(), empty(), clear()

# 4. Queue
* Deque, BlockingDeque, BlockingQueue, TransferQueue 인터페이스가 Queue 인터페이스를 상속받는다
* 한쪽에서는 삽입만, 한쪽에서는 삭제만 가능
* 처음 추가된 데이터가 가장 먼저 나오는 선입선출(FIFO) 구조
* BFS 알고리즘, 프로세스 관리, 대기 순서 관리 등 에서 주로 사용
* Queue<Element> queue = new LinkedList<Element>(); (다른 자식들도 가능)
* offer(value), poll(value), peek(value), contains(value), size(), empty(), clear()

## 4.1 Deque
* Double - Ended Queue
* 한쪽에서만 삽입, 다른 한쪽에서만 삭제가 가능했던 큐와 달리 양쪽에서 삽입, 삭제가 가능
* Deque 인터페이스는 Queue 인터페이스를 상속받는다.
  * Deque의 구현 클래스에는 ArrayDeque, LinkedBlockingDeque, ConcurrentLinkedDeque, LinkedList가 있다.
* 데이터의 삽입 삭제가 빠르고 앞, 뒤에서 삽입 삭제가 모두 가능하다
* index 를 통해 임의의 원소에 바로 접근이 가능하고
* 데이터를 앞, 뒤쪽에서 모두 삽입 삭제하는 과정이 필요한 경우, 데이터의 크기가 가변적일 때 사용
* offer(value), offerFirst(value), offerLast(value), poll(value), pollFirst(value), pollLast(value), peekFirst(value), peekLast(value), peek(value), contains(value), size(), empty(), clear(), remove(), removeFirst(), removeLast()

# 5. Heap
* 2진 트리의 일종
* 반정렬 상태(느슨한 정렬 상태)의 트리
* 중복값을 허용한다.
* 우선순위 큐를 구현하는데 많이 사용
* 부모 노드가 자식 노드보다 크냐 작냐에 따라 최대힙, 최소힙으로 구분
* 보통 배열을 사용하며 편의를 위해 0번 인덱스는 사용하지 않음
  * 1번 인덱스가 Root Node
* 부모 노드의 인덱스가 N 이라면 왼쪽 자식 노드의 인덱스는 N * 2 오른쪽 자식 노드의 인덱스는 N * 2 + 1 을 가진다.
* 삽입시 마지막 노드에 삽입한 후 부모와 값을 비교하면서 교체해간다.
* 삭제시 루트노드를 삭제 후 마지막 노드를 루트 노드에 삽입하고 자식 노드와 값을 비교하면서 교체해 간다.