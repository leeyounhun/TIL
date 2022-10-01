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
  - [4.2 Priority Queue(우선순위 큐)](#42-priority-queue우선순위-큐)
- [5. Heap](#5-heap)
- [6. Greedy Algorithm(욕심쟁이 알고리즘)](#6-greedy-algorithm욕심쟁이-알고리즘)
  - [6.1 개요](#61-개요)
  - [6.2 조건](#62-조건)
  - [6.3 사용례](#63-사용례)
- [7. Binary Search(이분 탐색)](#7-binary-search이분-탐색)
  - [7.1 개요](#71-개요)
  - [7.2 구현방법](#72-구현방법)
  - [7.3 활용](#73-활용)
    - [7.3.1 Upper Bound & Lower Bound](#731-upper-bound--lower-bound)
    - [7.3.2 Parametric Search](#732-parametric-search)
    - [7.3.3 LIS(Longest Increasing Subsequence)](#733-lislongest-increasing-subsequence)
- [8. Graph](#8-graph)
  - [8.1 개요](#81-개요)
  - [8.2 구성요소](#82-구성요소)
  - [8.3 구현](#83-구현)
  - [8.4 DFS(Depth First Search)](#84-dfsdepth-first-search)
    - [8.4.1 개요](#841-개요)
    - [8.4.2 특징](#842-특징)
    - [8.4.3 장점](#843-장점)
    - [8.4.4 단점](#844-단점)
  - [8.5 BFS(Breadth First Search)](#85-bfsbreadth-first-search)
    - [8.5.1 개요](#851-개요)
    - [8.5.2 특징](#852-특징)
    - [8.5.3 장단점](#853-장단점)
- [9. BackTracking](#9-backtracking)
- [10. DP](#10-dp)

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
  * hasNext() 사용 불가 -> hasMoreToken() 사용
  
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

## 4.2 Priority Queue(우선순위 큐)
* 일반적인 큐의 구조 FIFO(First In First Out)를 가지면서, 데이터가 들어온 순서대로 나가는 것이 아닌 우선순위가 높은 데이터가 먼저 나가는 자료구조
* 우선순위 큐에 저장할 객체는 필수적으로 Comparable Interface를 구현해야한다.
  * Comparable Interface는 compareTo() 메서드를 통해 객체 간의 순서를 비교할 수 있도록 해준다.
    * Comparable Interface를 구현한 클래스는 각 인스턴스간 순서가 존재한다.
    * 자바에서 같은 타입의 인스턴스를 서로 비교해야만 하는 클래스들은 모두 Comparable 인터페이스를 구현하고 있다.
* Heap을 이용하여 구현하는 것이 일반적이다.
  * 힙으로 구성되어 있기에 시간 복잡도는 O(NLogN)이다.
* PriorityQueue<Element> priorityQueue = new PriorityQueue<>();(최소힙)
* PriorityQueue<Element> priorityQueue = new PriorityQueue<>(Collections.reverseOrder());(최대힙)
  
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

# 6. Greedy Algorithm(욕심쟁이 알고리즘)
## 6.1 개요
* 최적해를 구하기 위해 사용되는 근사적인 방법
* 현재상태에서 당장 그 순간에 대해서 최적인 선택을 해 나가는 방법
  * 최종적인 결과 도출에 대한 최적해를 보장하지 않음
  * 그리디 알고리즘을 사용하려면 조건을 만족해야 한다. 
  
## 6.2 조건
* 탐욕스러운 선택 조건 (greedy choice property)
  * 앞의 선택이 이후의 선택에 영향을 주지 않아야 한다.
* 최적 부분 구조(Optimal Substructure)
  * 문제에 대한 최종 해결 방법은 부분 문제에 대한 최적 문제 해결 방법으로 구성된다.
* 이러한 조건이 성립하지 않는 경우에는 그리디 알고리즘은 최적해를 구하지 못한다.

## 6.3 사용례
* 매트로이드 구조인 경우
* AI에 있어서 결정 트리 학습법(Decision Tree Learning)
* 활동 선택 문제(Activity selection problem)
* 거스름돈 문제
* 최소 신장 트리(Minimum spanning tree)
* 다익스트라 알고리즘
  * DP의 일종

# 7. Binary Search(이분 탐색)
## 7.1 개요
* 정렬되어 있는 배열에서 데이터를 찾으려 시도할 때, 혹은 결정문제(답이 Y or N으로 정해지는 문제)의 답이 이분적일 때 사용하는 알고리즘이다.
* 데이터의 중간값을 기준으로 찾으려는 데이터를 찾는 기법이다.
* 반드시 배열 내부의 데이터가 정렬되어 있어야 사용이 가능하다.
* 시간 복잡도는 O(logN)이다.

## 7.2 구현방법
* 최소값, 최대값, 중간값을 사용한다.
* 찾으려는 값과 중간값을 비교한다.
* 찾으려는 값이 더 작으면 최대값을 중간값 - 1 으로 바꾸고 다시 중간값을 구해 비교한다.
* 단계마다 탐색 범위를 반으로(÷2) 나누는 것과 동일하므로 시간 복잡도가 크게 줄어든다.

## 7.3 활용
### 7.3.1 Upper Bound & Lower Bound
* 원하는 값을 단순히 찾는게 아닌 원하는 값 이상/초과가  처음으로 나오는 위치를 찾는 과정이다.
* 최대값을 배열의 크기 - 1 이 아닌 배열의 크기로 지정한다.
  * 찾으려는 값 이상/초과인 값이 처음으로 나오는걸 리턴해야 하기 때문이다.
* 탐색한 값이 찾으려는 값보다 크거나 같은 경우(Lower) 혹은 큰 경우(Upper) 최대값을 중간값으로 지정하여 범위를 더 좁히면서 찾아간다
* 최대 n일 때 최대값 = n으로 선언하거나, 출력할 답이 최소 0일 때 lo = 0으로 선언하면 안된다. 
  * (hi = n + 1, lo = -1로 선언)
* 찾고자 하는 값과 같거나 큰 수가 있는 첫 번째 인덱스를 찾는 Lower-Bound
  * if(value <= mid)
    * hi = mid;
  * return lo
* 찾고자 하는 값보다 큰 수가 있는 첫 번째 인덱스를 찾는 Upper-Bound
  * if(value < mid)
    * hi = mid;
  * return lo - 1
### 7.3.2 Parametric Search
* 최적화 문제를 결정 문제로 바꾸어 푸는 것이다.
* 일련의 값들이 아니라 주어진 범위 내에서 원하는 값 또는 원하는 조건에 가장 일치하는 값을 찾아내는 알고리즘이다.
* 범위 내에서 조건을 만족하는 값을 찾으려는 최적화 문제라면 이분 탐색으로 결정 문제를 해결하면서 범위를 좁혀가며 탐색한다.

### 7.3.3 LIS(Longest Increasing Subsequence)
* 최장 증가 부분수열
* 부분 수열 중 가장 긴 증가 수열을 찾는 알고리즘
* DP를 이용해서 찾는 방법(O = N^2)와 이분탐색을 이용해서 찾는 방법(O = nlogn)이 있다.
  * 이분 탐색을 사용하면 LIS의 길이만을 구할 수 있다.
  * 이분 탐색의 Lower Bound를 사용한다.
  * 수열 외 새로운 배열은 만든다.
  * 첫 자리에는 수열의 첫 숫자를 넣는다
  * 수열의 다음 수가 현재 배열의 마지막 수보다 크면 배열에 추가한다.
  * 수열의 다음 수가 현재 배열의 마지막 수보다 작으면 이분 탐색으로 수열의 수가 처음으로 커지는 지점에 넣는다.
  * 이를 끝까지 반복해서 만들어진 배열의 길이는 LIS의 길이와 같다.

# 8. Graph
## 8.1 개요
* 노드(Node)와 노드를 연결하는 간선(Edge)으로 연결관계를 표현하는 자료구조
  * 노드는 정점(Vertex) 이라고도 한다.
* 무방향 그래프, 가중치가 있는 무방향 그래프, 가중치가 있는 유방향 그래프가 있다.
* 두 지점 간의 최단 경로를 구하는 데 자주 이용된다.
* 순환하지 않는 그래프를 트리(Tree)라고 한다.
## 8.2 구성요소
* 노드(node): 정점 (vertex)이라고도 하며 데이터가 저장되는 그래프의 기본 원소
* 간선 (edge): 링크(link)라고도 하며 노드 간의 관계
* 인접 노드: (adjacent node): 하나의 노드에서 간선에 의해 직접 연결되어 있는 노드
* 차수(degree): 노드에 연결된 간선의 수
* 진입 차수(in-degree): 외부에서 오는 간선의 수
* 진출 차수(out-degree): 외부로 향하는 간선의 수
* 경로 (path): 간선을 따라갈 수 있는 길
* 경로의 길이 (length): 경로를 구성하는 데 사용된 간선의 수
* 단순 경로 (simple path): 경로 중에서 반복되는 간선이 없는 경로
* 사이클 (cycle): 시작 노드와 종료 노드가 같은 단순 경로
## 8.3 구현
*  그래프를 구현하는 방법에는 인접 행렬(Adjacency Matrix)을 이용하는 방법과 인접 리스트(Adjacency List)를 이용하는 방법이 있다.
* 인접 행렬(Adjacency Matrix)
  * 노드의 개수가 n이라면 n*n 형태의 2차원 배열로 그래프의 연결 관계를 표현한다.
  * 2차원 배열에 모든 노드들의 간선 정보를 저장해서 두 노드를 연결하는 간선을 조회할 때 O(1) 시간복잡도를 가진다.
  * 메모리 공간이 낭비된다.
  * 간선의 수를 알아내려면 O(n²)의 시간이 소요된다.
* 인접 리스트(Adjacency List)
  * 그래프의 각 노드에 인접한 노드들을 연결리스트(Linked List)로 표현한다.
  * 존재하는 간선만 관리하므로 보다 메모리 사용이 효율적이다.
  * 간선을 조회하거나 노드의 차수를 알기 위해서는 노드의 인접 리스트를 탐색해야 하므로 노드의 차수만큼의 시간이 필요하다.
  
## 8.4 DFS(Depth First Search)
### 8.4.1 개요
* 깊이 우선 탐색
* 그래프 탐색의 일종
* 루트 노드에서 시작해서 다음 분기로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방법
* 구조상 스택 오버플로우를 유의해야 한다.
### 8.4.2 특징
* 자기 자신을 호출하는 순환 알고리즘의 형태를 가지고 있다.
* 어떤 노드를 방문했었는지 여부를 반드시 검사 해야 한다.
* 단순 검색 속도 자체는 BFS에 비해서 느리다.
* 분기가 나타날 때마다 기록하면서 자신이 지나간 길을 지워나간다.
* 재귀호출을 사용하여 구현하지만, 단순한 스택 배열로 구현하기도 한다.
### 8.4.3 장점
* 단지 현 경로상의 노드들만을 기억하면 되므로 저장 공간의 수요가 비교적 적다.
* 목표 노드가 깊은 단계에 있을 경우 해를 빨리 구할 수 있다.
### 8.4.4 단점
* 해가 없는 경로에 깊이 빠질 가능성이 있다.
* 얻어진 해가 최단 경로가 된다는 보장이 없다. 

## 8.5 BFS(Breadth First Search)
### 8.5.1 개요
* 너비 우선 탐색
* 루트 노드부터 시작해 인접 노드를 먼저 탐색하는 방법
*  노드 사이의 최단 경로 혹은 임의의 경로를 찾고 싶을 때 이 방법을 선택한다.
### 8.5.2 특징
* 재귀적으로 동작하지 않는다.
* 어떤 노드를 방문했었는지 여부를 반드시 검사 해야 한다
* 큐를 사용한다.
### 8.5.3 장단점
* 출발노드에서 목표노드까지의 최단 길이 경로를 보장한다.
* 경로가 매우 길 경우에는 탐색 가지가 급격히 증가함에 따라 보다 많은 기억 공간을 필요로 하게 된다.
* 해가 존재하지 않는다면 유한 그래프(finite graph)의 경우에는 모든 그래프를 탐색한 후에 실패로 끝난다.
* 무한 그래프(infinite graph)의 경우에는 결코 해를 찾지도 못하고, 끝내지도 못한다.

# 9. BackTracking
* 완전 탐색중 이번 탐색 분기가 유망하지 않다고 판단되면 탐색을 멈추고 다음 분기로 넘어가는 방식
* 불필요한 경로를 조기에 차단할 수 있게 되어 경우의 수가 줄어들지만, 만약 N!의 경우의 수를 가진 문제에서 최악의 경우에는 여전히 지수함수 시간을 필요로 하므로 처리가 불가능 할 수도 있다.
* 모든 가능한 경우의 수 중에서 특정한 조건을 만족하는 경우만 살펴보는 것
* DFS 등으로 모든 경우의 수를 탐색하는 과정에서, 조건문 등을 걸어 답이 절대로 될 수 없는 상황을 정의하고, 그러한 상황일 경우에는 탐색을 중지시킨 뒤 그 이전으로 돌아가서 다시 다른 경우를 탐색한다.

# 10. DP
* 동적 프로그래밍
* 큰 문제를 부분 문제로 나누고 부분 문제의 정답으로 큰 문제의 답을 찾아가는 알고리즘
* 중복되는 부분 문제(Overlapping Subproblem)
  * 큰 문제의 해를 찾기 위해 여러 부분 문제를 풀어야 하고 부분 문제는 반드시 중복해서 나타난다.
* 최적 부분 구조(Optimal Substructure)
  * 큰 문제의 해를 찾기 위한 연산과 부분 문제의 해를 찾기 위한 연산이 동일해야 하며 부분 문제의 해를 조합해 큰 문제의 해를 찾을수 있는 구조이다.
* 메모이제이션
  * 중복되는 부분 문제들을 반복해서 계산하면 시간과 메모리가 낭비되기 때문에 이전에 구한 부분 문제의 해를 메모리에 저장해 둔다.