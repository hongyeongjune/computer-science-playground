## 목차

<!-- 목차 -->
-   [목차](#목차)
-   [자료구조 시간 복잡도](#자료구조-시간-복잡도)
-   [List](#list)
-   [ArrayList vs LinkedList](#arraylist-vs-linkedlist)
-   [Hash](#hash)
-   [Set](#set)
-   [Map](#map)
-   [HashSet vs HashMap](#hashset-vs-hashmap)
-   [HashTable](#hashtable)
-   [HashMap 의 내부적인 동작 원리](#hashmap-의-내부적인-동작-원리)
-   [HashMap vs HashTable](#hashmap-vs-hashtable)
-   [Stack](#stack)
-   [Queue](#queue)
-   [Tree](#tree)
-   [이진 트리](#이진-트리)
-   [Heap](#heap)
-   [이진 탐색 트리](#이진-탐색-트리)
-   [균형 이진 탐색 트리](#균형-이진-탐색-트리)
-   [레드 블랙 트리](#레드-블랙-트리-red-black-tree)
-   [AVL 트리](#avl-트리)
-   [B-Tree](#b-tree)
-   [B+Tree](#btree)
-   [B-Tree vs B+Tree](#b-tree-vs-btree)
-   [Graph](#graph)
-   [Graph vs Tree](#graph-vs-tree)
<!-- /목차 -->

## 자료구조 시간 복잡도
Data Structure|Average TimeComplexity|-|-|-|Worst TimeComplexity|-|-|-|Worst Space Complexity
---|---|---|---|---|---|---|---|---|---
-|접근(Access)|탐색(Search)|삽입(Insertion)|제거(deletion)|접근(Access)|탐색(Search)|삽입(Insertion)|제거(deletion)|
배열(Array)|O(1)|O(N)|O(N)|O(N)|O(1)|O(N)|O(N)|O(N)|O(N)
스택(Stack)|O(N)|O(N)|O(1)|O(1)|O(N)|O(N)|O(1)|O(1)|O(N)
단일 연결 리스트(Singly-Linked List)|O(N)|O(N)|O(1)|O(1)|O(N)|O(N)|O(1)|O(1)|O(N)
이중 연결 리스트(Doubly-Linked List)|O(N)|O(N)|O(1)|O(1)|O(N)|O(N)|O(1)|O(1)|O(N)
스킵 리스트(Skip List)|O(logN)|O(logN)|O(logN)|O(logN)|O(N)|O(N)|O(N)|O(N)|O(N logN)
해쉬 테이블(Hash Table)|-|O(1)|O(1)|O(1)|-|O(N)|O(N)|O(N)|O(N)
이진 탐색 트리(Binary Search Tree)|O(logN)|O(logN)|O(logN)|O(logN)|O(N)|O(N)|O(N)|O(N)|O(N)
직계 트리(Cartesian Tree)|-|O(logN)|O(logN)|O(logN)|-|O(N)|O(N)|O(N)|O(N)
비-트리(B-Tree)|O(logN)|O(logN)|O(logN)|O(logN)|O(logN)|O(logN)|O(logN)|O(logN)|O(N)
레드-블랙 트리(Red-Black Tree)|O(logN)|O(logN)|O(logN)|O(logN)|O(logN)|O(logN)|O(logN)|O(logN)|O(N)
스플레이 트리(Splay Tree)|-|O(logN)|O(logN)|O(logN)|O(-)|O(logN)|O(logN)|O(logN)|O(N)
AVL 트리(AVL Tree)|O(logN)|O(logN)|O(logN)|O(logN)|O(logN)|O(logN)|O(logN)|O(logN)|O(N)

## List
* ArrayList
* LinkedList
* Stack, Queue
* Vector

## ArrayList vs LinkedList
Class|add|remove|get|contains
---|---|---|---|---
ArrayList|O(N)|O(N)|O(1)|O(N)
LinkedList|O(1) or O(N)|O(1) or O(N)|O(N)|O(N)

* ArrayList
    - ArrayList 가 검색은 유리하다. -> Index 기반이기 때문
    - 논리적 순서와 물리적 순서가 일치한다.
    - index 값을 통한 원소 접근이 용이하다. -> O(1)
    - 삽입, 삭제의 경우 배열에 shift 연산을 해야하기 때문에 비용이 높다.
* LinkedList
    - LinkedList 가 삽입 삭제의 경우 유리
    - 논리적으로 순서대로 되어있으나 물리적으로는 그렇지 않다.
    - 노드가 다음 원소의 주소를 가지고 있다.
    - 맨 앞 혹은 맨 뒤에 삽입/삭제를 하면 O(1)이지만, 그 외는 O(N)
    - 삽입, 삭제 시 데이터를 Shift 하지 않고 다음 원소의 주소를 바꿔주는 식으로 할 수 있다.
    - Shift 를 하지 않기 때문에 ArrayList 와 같은 O(N)이 나와도 더 빠르다.

## Hash
* 기본적으로 데이터를 고정된 크기의 데이터로 변환시키는 것
* Hashing : 변환하는 과정
* Hash 값 : 변환된 값
* Hash 함수 : 수행하는 함수

## Set
Class|add|contains
---|---|---
HashSet|O(1)|O(1)
LinkedHashSet|O(1)|O(1)
EnumSet|O(1)|O(1)
TreeSet|O(logN)|O(logN)

* 특징
    - 인덱스로 객체를 가져올 수 없다.
    - Key Value 형식
* HashSet
    - 내부적으로 자바의 HashMap 으로 구현되어 있다.
    - 즉, contains 함수가 List 보다 빠르다.
    - 중복을 허용하지 않고, 순서가 존재하지 않는다.
* LinkedHashSet
    - 순서가 존재하는 HashSet
* TreeSet
    - 이진 탐색 트리 형태이다.
    - 데이터를 저장할 때부터 정렬을 한다.
    - 즉, HashSet 에 비해 속도가 느리다.

## Map
Class|get|containsKey
---|---|---
HashMap|O(1)|O(1)
LinkedHashMap|O(1)|O(1)
TreeMap|O(logN)|O(logN)

* 특징
    - Key Value 형식을 가진 자료구조
    - Key 는 중복일 수 없고, Value 는 중복이 가능하다.
* HashMap
    - 내부적으로 Entry<K, V>[] entry 의 배열로 되어 있다.
    - 해당 배열에 인덱스는 내부 해시 함수를 통해서 계산된다.
    - 검색 성능이 O(1)로 가장 좋다.
* TreeMap
    - 내부적으로 Red Black Tree 로 저장된다.
    - 키 값에 대한 Comparator 구현으로 정렬 순서를 바꿀 수 있다.
    - 이진 탐색 트리 형태로 데이터 저장, 검색과 정렬에 특화되어있다.
    - 키 값이 알파벳 순서대로 정렬된다.
    - 트리에 저장되므로 키 값은 일정 기준으로 정렬된 상태로 출력한다.
    - Iterator 하려면 TreeMap 이 좋지만 O(logN)의 성능을 지니므로 데이터가 많아지면 좋지 않을 수 있다.

## HashSet vs HashMap
-|HashSet|HashMap
---|---|---
Implements|Set|Map
Duplicates|No|Yes, Duplicate values but no duplicate key
Dummy values|Yes|No
Adding or Storing mechanism|HashMap Object| Hashing Technique
Insertion method|add()|put()

* Dummy Value
    - Set 은 내부적으로 Map 사용
    - Map 의 Key 를 이용한다.
    - Set 에서 Map 의 Value 에는 Dummy Value 가 들어간다.
    ```java
      private static final Object PRESENT = new Object();
      
      public boolean add(E e) {
          return map.put(e, PRESENT) == null;
      }        
    ```

* 속도
    - 내부적으로 HashSet 은 HashMap 으로 구현되어 있기 때문에 속도에 차이가 없다.

## HashTable
* HashTable 에서 인덱스 값을 설정하는 Hash 함수
    - Division Method : 입력값을 테이블의 크기로 나눈 나머지를 인덱스로 사용한다. (주소 = 입력값 % 테이블의 크기)
    - Digit Folding : 각 Key 의 문자열을 ASCII 코드로 바꾸고 값을 합한 데이터를 테이블 내의 주소로 사용한다.
    - Multiplication Method : Key 값과 0과 1사이의 상수를 곱한 뒤 소수 부와 테이블의 크기를 곱한 값을 주소로 사용한다.
* 특징
    - 내부적으로 배열을 사용하며 평균적으로 빠른 탐색 속도(O(N))를 가진다.
    - 평균적으로의 의미는 충돌을 고려하지 않았을 때 이다.
    - Key 값을 해시 함수를 통해서 인덱스로 변환한 후 그 인덱스에 Key 값을 집어넣는다.
    - 만약 다른 Key 값을 해시 함수에 통과시켰는데 같은 인덱스가 나온다면 그걸 충돌이라고 한다.
* 충돌 해소법
    - 개방 주소법
        - 충돌 발생 시 비어 있는 다른 인덱스를 찾는다.
    - 분리 연결법(Chaining)
        - 다른 인덱스를 찾는 것이 아니라 그 인덱스에 연결하는 방법
        - 즉, 연결 리스트를 이용하여 연결하는 방법을 말한다.
        - 정리하면, 동일한 버킷 데이터에 대해 자료구조를 활용해 추가 메모리를 사용하여 다음 데이터의 주소를 저장한다.
          ![images](https://blog.kakaocdn.net/dn/bTF67c/btqL7xx3OGw/DM8KEKU5x7dx6Nks4JR7K1/img.png)

## HashTable equals 와 hashCode
* put
    - HashTable 에 같은 객체가 이미 있다면 기존 객체를 덮어쓴다. (equals -> true)
    - HashTable 에 같은 객체가 없다면 해당 엔트리를 LinkedList 에 추가 (equals -> false)
* get
    - 값이 같은 객체가 있다면 그 객체를 리턴 (equals -> true)
    - 값이 같은 객체가 없다면 null 리턴 (equals -> false)
* equals 와 hashCode 를 재정의 해야하는 이유
    - hashCode 를 재정의하지 않으면 같은 값 객체라도 해시 값이 다르기 때문에 찾을 수 없다.
    - equals 를 재정의하지 않으면 hashCode() 가 만든 해시 값을 이용해 객체가 저장된 버킷을 찾을 수 있지만 해당 객체가 자신과 같은 객체인지 비교할 수 가없다.

## HashMap 의 내부적인 동작 원리
* HashMap 의 내부는 Entry 의 배열로 선언되어 있다.
* Key 와 Value 를 HashMap 에 put 하게 되면 Key 를 내부 해시 함수를 통해서 인덱스로 만들어준다.
* 해시 함수를 사용하여 인덱스를 구하는 과정에 동일한 값이 발생할 수 있다.
* 이를 해시 충돌이라 하며 이를 방지 하기 위해 개방 주소법 혹은 분리 연결법을 사용한다.
* Java 의 HashMap 의 경우 분리 연결법(Chaining)을 사용한다.
* 즉, 분리 연결법을 사용하여 해시 값이 같은 데이터에 대한 연산을 하게 되면 연결 리스트를 탐색하여 equals 를 통해 보장된 value 를 return 한다.
* 연결리스트가 너무 길어질 경우, 탐색하는데 시간이 너무 오래걸린다.
* Java8 에서는 위의 문제를 해결하는 방식으로 리스트를 레드 블랙 트리(TreeMap)으로 변경하여 관리한다.
* LinkedList 와 Tree 의 사용 기준은 하나의 해시 버킷에 할당된 Key-Value 쌍의 개수이다.
* 즉, 8개의 Key-Value 쌍이 모이면 LinkedList 를 Tree 로 변경한다.
* 만약 해당 버킷에 있는 데이터를 삭제하여 개수가 6개 이르면 다시 LinkedList 로 변환한다.
* 8과 6으로 2이상의 차이를 둔 것은 만약 1차이로 인해 어떤 Key-Value 한 쌍이 반복되어 삽입/삭제되는 경우 불필요하게 Tree 와 LinkedList 를 변경하는 일이 반복되어 성능 저하가 발생할 수 있기 때문이다.
* Java 8 HashMap 에서는 Entry 의 배열 대신에 Node 배열을 사용한다.
* 사실상 Java 7 까지의 Entry 클래스와 내용이 같지만, LinkedList 대신 Tree 를 사용할 수 있도록 하위 클래스인 TreeNode 가 있다는 점이 다르다.
* 배열은 초기 사이즈를 초기화해놓고 사용해야한다는 특징이 있기 때문에 Map 에 데이터를 많이 넣게 되면 배열의 범위를 넘어가는 문제가 발생할 수 있다.
* 위의 문제를 해결하기 위해 내부적으로 resize 메서드를 호출하여 배열의 사이즈를 늘리는 방식으로 구현되어있다.
 ```java
public class HashMap <K, V> extends java.util.AbstractMap<K,V> implements java.util.Map<K,V>, java.lang.Cloneable, java.io.Serializable {
    static final int TREEIFY_THRESHOLD = 8;
    static final int UNTREEIFY_THRESHOLD = 6;
    ...
}
```
* [참고 자료](https://d2.naver.com/helloworld/831311)

## HashMap vs HashTable
* 특징
    - 모두 Key 와 Value 를 쌍으로 저장하는 자료구조
    - Map 인터페이스를 상속받아 구현
* 차이
    - 동기화의 제공 유무
    - HashMap : 동기화를 지원하지 않는다.
    - HashTable : 동기화를 지원한다. (대부분 연산에 synchronized 키워드를 붙여서 동기화 수행)
    - 멀티 스레드 환경에서는 HashTable 이 HashMap 에 비해서 Thread-safe 를 보장할 수 있지만, HashMap 보다 낮은 성능을 보인다.

## Stack
* 선형 자료구조의 일종으로 FILO(First In, Last Out - 선입 후출) 의 대표적인 예
* 먼저 들어갔다가 나중에 나오는 구조
* 보통 미로찾기나 괄호 유효성 체크에서 활용된다.

## Queue
Class|offer|peak|poll|size
---|---|---|---|---
PriorityQueue|O(logN)|O(1)|O(logN)|O(1)
LinkedList|O(1)|O(1)|O(1)|O(1)
ArrayDequeue|O(1)|O(1)|O(1)|O(1)

* 선형 자료구조의 일종으로 FIFO(First In, First Out - 선입 선출)의 대표적인 예
* 먼저 들어가서 먼저 나오는 구조
* 작업 우선순위를 정하거나 Heap 구현, BFS 등에 사용된다.
* 우선순위 큐(PriorityQueue)
    - Heap 으로 구현, 따라서 정렬은 HeapSort 로 된다.
    - 들어온 순서대로 나가는 큐 대신, 어떠한 우선순위를 두고 먼저 나가는 큐 방식이 필요할 때 사용

## Tree
* 비선형 자료구조로 계층적 자료 구조를 표현하는 자료구조
* 구성요소
    - 노드 : 트리를 구성하고 있는 원소
    - 간선 : 노드와 노드사이를 연결하는 선
    - 루트 : 트리의 최상위 노드
    - 터미널 : 트리의 최하위 노드
    - 인터널 : 트리의 최하위 노드를 제외한 모든 노드
    - 리프 노드 : 자식 노드가 없는 노드
* 탐색방법
    - 전위 : Root -> Left -> Right
    - 중위 : Left -> Root -> Right
    - 후위 : Left -> Right -> Root

## 이진 트리
* 모든 자식 노드가 최대 두개인 트리
* 완전 이진 트리
    - 위에서 아래로, 왼쪽에서 오른쪽 순서대로 채워진 트리
* 포화 이진 트리
    - 마지막 레벨을 제외하고 모든 레벨이 두 개의 자식 노드로 채워진 경우

## Heap
* 완전 이진 트리이면서 우선순위 큐를 위하여 만들어진 자료구조
* 주의 : 완전 이진 탐색 트리가 아니다.
* 여러 개의 값들 중에서 최댓값이나 최솟값을 빠르게 찾아내도록 만들어짐
* 힙은 반 정렬 상태(느슨한 정렬 상태)를 유지한다.
    - 큰 값이 상위 레벨이 있고, 작은 값이 하위 레벨에 있다.(반대의 경우도 됨)
* 중복된 값을 허용 한다.
* 종류
    - 최대 힙(Max Heap) : 부모가 자식보다 크거나 같은 완전 이진 트리
    - 최소 힙(Min Heap) : 부모가 자식보다 작거나 같은 완전 이진 트리


## 이진 탐색 트리
* Binary Search Tree 는 이진 트리이며, 데이터를 저장하는 특별한 규칙이 존재한다.
* 노드에 저장된 값은 유일한 값이다.
* 왼쪽 서브트리는 현재 노드 값보다 작으며, 오른쪽 서브트리는 현재 노드 값보다 크다.
* 탐색에 특화되어 있다.
* 장점
    - 최적의 경우 O(logN)의 시간 복잡도를 나타낸다.
* 단점
    - 최악의 경우(편향트리) O(N)의 시간 복잡도를 나타낸다.
* 편향 이진 트리
    - 모든 노드가 왼쪽 자식 혹은 오른쪽 자식으로만 편향되어있는 경우
    - 이를 해결하는 방법으로 Rebalancing 기법이 있다.

## 균형 이진 탐색 트리
* 이미 정렬된 데이터를 이진 탐색 트리로 만들 경우 한쪽으로 편향된 편향 트리가 되어 O(N)이라는 시간 복잡도를 발생한다.
* 이를 위해 균형을 이루도록 Rebalancing 기법을 사용하여 만든 트리를 균형 이진 탐색 트리라 한다.
* 대표적인 예
    - 레드 블랙 트리(Red-Black Tree)
    - AVL 트리

## 레드 블랙 트리 Red-Black Tree
* Rebalancing 기법의 하나로 기존 이진 탐색 트리의 삽입, 삭제, 탐색의 비효율성을 개선한 방법
* 규칙
    - 각 노드의 색은 Red 혹은 Black
    - Root Node 는 Black
    - 각 말단 노드는 Black
    - 어떤 노드의 색이 Red 이면 자식들은 모두 Black
    - 어느 한 노드로부터 리프노드까지의 Black 수는 리프노드를 제외하면 모두 같다.
    - 삽입되는 노드의 색은 무조건 Red 이다.
* 삽입시 문제
    - 삽입할 때 무조건 Red 를 하게 되면 Double Red 가 발생할 수 있다.
    - 해결 방법
        - Restructuring(회전)
        - Recoloring(색상변환)
* Restructuring
    - When ?
        - 부모 노드가 Red 이고, 부모 노드의 형제 노드가 없거나 Black 일 경우
    - 삽입된 노드, 부모 노드(parent node), 부모의 부모 노드(grand parent)를 오름차순으로 정렬
    - 가운데 있는 값을 부모로 만들고 나머지 둘을 자식으로 만든다.
    - 올라간 값을 Black 으로 만들고 그 두 자식들을 Red 로 만든다.
* Recoloring
    - When ?
        - 부모 노드가 Red 이고, 부모 노드의 형제 노드가 Red 일 경우
    - 삽입된 노드의 부모와 그 형제 노드를 Black 으로 하고, 부모의 부모 노드(grand parent)를 Red 로 한다.
    - Problem
        - 부모의 부모 노드(grand parent)가 Root node 가 아니었을 시 Double Red 가 다시 발생할 수 있다.
        - 그럼 다시 Restructuring 혹은 Recoloring 을 수행
* 특징
    - 이진 탐색 트리의 모든 특징을 가진다.
    - 노드에 자식이 없을 경우 자식을 가리키는 포인터에 null 값을 저장하고, 이러한 노드를 말단 노드로 간주하며 Black 을 준다.
* [참고 자료](https://zeddios.tistory.com/237)

## AVL 트리
* 각 트리의 왼쪽 서브 트리와 오른쪽 서브 트리의 깊이 차이가 1을 넘지 않는 것이 특징인 트리
* LL, RR, RL, LR 이란 4가지 상황이 발생하면 Left Rotate 와 Right Rotate 연산을 통해 균형을 맞춘다.
* LL
    - ![images](https://cdn.filepicker.io/api/file/SaR6jSSTYKuPCyuuGxlR)
    - 부모의 부모노드(grand parent)를 Right Rotate 합니다.
* RR
    - ![images](https://cdn.filepicker.io/api/file/njRUhO6MSZm0rn3Hv0l0)
    - 부모의 부모노드(grand parent)를 Left Rotate 합니다.
* RL
    - ![images](https://cdn.filepicker.io/api/file/DQYwAvUlQ1mXC4MfW8eb)
    - 부모 노드를 Left Rotate 한 후, 부모의 부모노드(grand parent)를 Right Rotate 합니다.
* LR
    - 부모 노드를 Right Rotate 한 후, 부모의 부모노드(grand parent)를 Left Rotate 합니다.
* [참고 자료](https://www.zerocho.com/category/Algorithm/post/583cacb648a7340018ac73f1)

## B-Tree
* 인덱스를 이루고 있는 자료구조의 일종
* MySQL 의 DB Engine 인 InnoDB 는 B+Tree 로 이루어져있는데 B-Tree 의 확장된 개념이다.
* 노드의 데이터의 수가 N 개 라면 자식 노드의 개수는 N+1 개
* 노드의 데이터는 반드시 정렬된 상태이어야 한다.
* 루트 노드를 제외한 모든 노드는 적어도 차수/2 개 이상의 데이터를 가지고 있어야한다.
* 데이터는 중복될 수 없다.
* 탐색시 높은 성능을 보여준다.
* 어떠한 값에 대해서도 같은 시간 복잡도를 가진다.
* [참고 자료](https://hyungjoon6876.github.io/jlog/2018/07/20/btree.html)
* [참고 자료](https://zorba91.tistory.com/293)

## B+Tree
* B-Tree 의 확장개념으로, B-Tree 의 경우, Internal 또는 Branch 노드에 Key 와 Data 를 담을 수 있다.
* B+Tree 의 경우, Branch 노드에 Key 만 담아두고, 오직 리프 노드에만 Key 와 Data 를 저장한다.
* 즉, 리프 노드끼리 Linked List 로 연결되어 있다.
* 리프 노드를 제외하고, 데이터를 담아두지 않기 때문에 메모리를 더 확보함으로써 더 많은 Key 를 수용할 수 있다.
* 하나의 노드에 더 많은 Key 를 담을 수 있기 때문에 트리의 높이가 낮아진다.(Cache Hit 를 높일 수 있다.)
* 풀 스캔 시, B+Tree 는 리프 노드에 데이터가 있기 때문에 한 번의 선형 탐색만 하면 돼서 속도가 B-Tree 보다 빠르다.
* 즉, B-Tree 의 경우 모든 노드를 확인해야 한다.
* [참고 자료](https://zorba91.tistory.com/293)

## B-Tree vs B+Tree
구분|B-Tree|B+Tree
---|---|---
데이터 저장|리프 노드, 브랜치 노드 모두 데이터 저장 가능|오직 리프노드에만 가능
트리의 높이|높음|낮음
풀 스캔 시 검색 속도|모든 노드 탐색|리프 노드에서 선형탐색
키 중복|불가능|있음(리프노드에 모든 데이터가 있기 때문에)
검색|자주 access 되는 노드를 루트 노드 가까이 배치 가능, 루트 노드에 가까울 경우, 브랜치 노드에도 데이터가 존재하기 때문에 빠름|리프 노드까지 가야 데이터 존재
LinkedList|없음|리프 노드끼리 LinkedList 로 연결
* [참고 자료](https://zorba91.tistory.com/293)

## Graph
* 단순히 노드와 그 노드를 연결하는 간선을 하나로 모아 놓은 자료 구조
* 특징
    - 네트워크 모델이다.
    - 2개 이상의 경로가 가능하다.
    - 루트 노드의 개념이 없다.
    - 순환 혹은 비순환이다.
    - 방향 그래프와 무방향 그래프로 나눌 수 있다.
* 구현 방법
    - 인접 리스트(Adjacency List)
        - 리스트를 사용하여 구현
        - 정점간 연결 여부 파악이 오래 걸린다. -> 공간 복잡도(O(E+V)) / E : Edge 간선 / V : Vertex 정점
    - 인접 행렬(Adjacency Matrix)
        - 정방 행렬을 사용하여 구현
        - 연결 관계를 O(1)로 파악이 가능하다. -> 공간 복잡도(O(2V)) / E : Edge 간선 / V : Vertex 정점
* [참고 자료](https://gmlwjd9405.github.io/2018/08/13/data-structure-graph.html)

## Graph vs Tree
-|Graph|Tree
---|---|---
방향성|방향, 무방향 그래프|방향 그래프
사이클|가능|불가능
자체 간선|가능|불가능
순환|가능|불가능
루트 노드|존재 하지 않음|한 개의 루트 노드만 존재
모델|네트워크 모델|계층 모델
* [참고 자료](https://gmlwjd9405.github.io/2018/08/13/data-structure-graph.html)
