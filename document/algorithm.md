## 목차

<!-- 목차 -->
-   [목차](#목차)
-   [시간 복잡도](#시간-복잡도)
-   [시간 복잡도 계산](#시간-복잡도-계산)
-   [O(logN) 시간 복잡도 분석](#ologn-시간-복잡도-분석)
-   [피보나치](#피보나치)
-   [선형, 비선형 자료구조](#선형-비선형-자료구조)
-   [정렬의 종류](#정렬의-종류)
-   [선택정렬](#선택정렬)
-   [삽입정렬](#삽입정렬)
-   [버블정렬](#버블정렬)
-   [합병정렬](#합병정렬)
-   [퀵정렬](#퀵정렬)
-   [합병정렬 vs 퀵정렬](#합병정렬-vs-퀵정렬)
-   [힙정렬](#힙정렬)
-   [위상 정렬](#위상-정렬)
-   [안정 정렬, 불안정 정렬](#안정-정렬-불안정-정렬)
-   [빠른 선택 알고리즘](#빠른-선택-알고리즘)
<!-- /목차 -->

## 시간 복잡도
* 알고리즘을 구성하는 명령어들이 몇번이나 실행되었는지 센 결과(frequency count) + 각 명령어의 실행시간(execution time)을 곱한 합계를 의미
* 얼마나 걸리는지 구하는 것
* 연산 1억번에 1초정도
* 공간복잡도는 메모리를 얼마나 사용하는지 구하는 것
* [참고 자료](https://skmagic.tistory.com/164)

## 시간 복잡도 계산
* 실행 횟수를 구한다.
* Big O, O(N)은 최악의 시간을 구하는 것
  ![image](https://user-images.githubusercontent.com/25604495/66132758-896dbd80-e630-11e9-80bb-0ab100211cef.png)
    - 1 : 입력자료의 수에 관계 없이 일정한 실행 시간을 갖는 알고리즘
        - 2회 결려도 O(1) 이다.
        - 즉, N에 관계없이 상수 시간이 걸렸을 때는 O(1)이다.
    - log N : N이 증가함에 따라 실행시간이 조금씩 늘어난다.
        - 주로 커다란 문제를 일정한 크기를 갖는 작은 문제로 쪼갤 때 나타나는 유형
        - N개를 계속해서 절반으로 나누는 연산(ex. 이진 탐색)
        - 빠른 탐색 알고리즘
    - N log N : N이 두배로 늘어나면 실행 시간은 2배보다 약간 더 많이 늘어난다.
        - 커다란 문제를 독립적인 작은 문제로 쪼개어 각각에 대해 독립적으로 해결하고, 나중에 다시 그것들을 하나로 모으는 경우
        - 빠른 정렬 알고리즘
* [참고 자료](https://skmagic.tistory.com/164)

## O(logN) 시간 복잡도 분석
* 시간복잡도는 자료의 개수가 N일 때 실행 횟수를 구하는 것
* 이진 탐색 - O(log N)
    - [참고 자료](https://zelord.tistory.com/11)
* 퀵정렬 - O(N log N)
    - Pivot 과 비교횟수 N번 -> 반을 나눠서, 각각 반을 동일한 연산을 수행
    - 즉, 전체 수행기간은 N번 더하기 반에대한 동일연산을 두 번 수행 한것과 같다.
    - T(N) = N + 2T(N/2)
    - = 2(2T(N/4) + N/2) + N
    - = 4T(N/4) + N + N
    - = 4(2T(N/8) + N/4) + 2N
    - = 8T(N/8) + N + 2N
    - ...
    - = 2<sup>log<sub>2</sub>N</sup> + N log<sub>2</sub>N
    - [참고 자료](https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html)
    - [참고 자료](https://m.blog.naver.com/PostView.nhn?blogId=devace&logNo=220539413241&proxyReferer=https:%2F%2Fwww.google.com%2F)

## 피보나치
```java
// 재귀
// 시간 복잡도 2의 N승
int fibonacchi(int n) {
    if(n == 0) return 0;
    if(n == 1) return 1;

    return fibonacchi(n - 1) + fibonacchi(n - 2);
}

//반복문
//시간 복잡도 N
int[] array = new int[n];
array[0] = 0;
array[1] = 1;
for(int i=2; i<=n; i++) {
    array[i] = array[i-1] + array[i-2];
}
```

## 선형, 비선형 자료구조
* 선형 구조
    - 자료를 구성하는 데이터를 순차적으로 나열시킨 형태를 의미
    - 배열(Arrays), 연결 리스트(Linked List), 스택(Stack), 큐(Queue)
* 비선형 구조
    - 하나의 자료 뒤에 여러개의 자료가 존재할 수 있는 것을 의미
    - 트리(Tree), 그래프(Graph)

## 정렬의 종류
* 선택정렬
* 삽입정렬 - 안정
* 버블정렬 - 안정
* 합병정렬 - 안정
* 퀵정렬
* 힙정렬
* 정렬의 시간 복잡도  
  ![image](https://user-images.githubusercontent.com/25604495/66103164-d8dfc980-e5ef-11e9-906d-f07fbd425e74.png)
* 알고리즘 및 정렬 시간 복잡도

Algorithm|Best Time Complexity|Average Time Complexity|Worst Time Complexity|Worst Space Complexity
---|---|---|---|---
선형탐색(Linear Search)|O(1)|O(N)|O(N)|O(1)
이진탐색(Binary Search)|O(1)|O(logN)|O(logN)|O(1)
버블정렬(Bubble Sort)|O(N<sup>2</sup>)|O(N<sup>2</sup>)|O(N<sup>2</sup>)|O(1)
선택정렬(Selection Sort)|O(N<sup>2</sup>)|O(N<sup>2</sup>)|O(N<sup>2</sup>)|O(1)
삽입정렬(Insertion Sort)|O(N)|O(N<sup>2</sup>)|O(N<sup>2</sup>)|O(1)
합병정렬(Merge Sort)|O(NlogN)|O(NlogN)|O(NlogN)|O(N)
퀵정렬(Quick Sort)|O(NlogN)|O(NlogN)|O(N<sup>2</sup>)|O(logN)
힙정렬(Heap Sort)|O(NlogN)|O(NlogN)|O(NlogN)|O(N)
버킷정렬(Bucket Sort)|O(N+K)|O(N+K)|O(N<sup>2</sup>)|O(N)
기수정렬(Radix Sort)|O(N*K)|O(N*K)|O(N*K)|O(N+K)
팀정렬(Tim Sort)|O(N)|O(NlogN)|O(NlogN)|O(N)
셸정렬(Shell Sort)|O(N)|O((NlogN)<sup>2</sup>)|O((NlogN)<sup>2</sup>)|O(1)

## 선택정렬
* 회차마다 가장 작은 것을 찾아 앞에서부터 하나씩 정렬
* 앞에서부터 정렬된다.
* (n-1) + (n-2) + ... + 2 + 1 => n(n-1)/2 -> O(n<sup>2</sup>)
* 불안정 정렬이다.
    - 예를 들어, [B1, B2, C, A] (A < B1 = B2 < C) 로 되어있다고 가정하자
    - 순서대로 순회하면서 정렬하면 다음과 같다.
    - round 1 : [A, B2, C, B1]
    - round 2 : [A, B2, C, B1]
    - round 3 : [A, B2, B1, C]
    - 초기의 B1, B2의 순서가 뒤 바뀐 것을 확인할 수 있고 이를 불안정 정렬이라 한다
* [참고 자료](https://gmlwjd9405.github.io/2018/05/06/algorithm-selection-sort.html)
```java
public int[] solution(int[] arr) {
    int[] answer = arr;
    
    for(int i=0; i<answer.length-1; i++) {
        int minIndex = i;
        for(int j=i+1; j<answer.length; j++) {
            if(answer[minIndex] > answer[j]) {
                minIndex = j;
            }   
        }
        swap(answer, minIndex, i);   
    }
}

public void swap(int[] array, int x, int y) {
    int temp = array[x];
    array[x] = array[y];
    array[y] = temp;
}
``` 

## 삽입정렬
* 회차마다 각 숫자를 적절한 위치에 삽입
* 두 번째 인덱스부터 시작
* 자신보다 작은 값이 나올때까지 비교하므로 이미 정렬되어 있을 경우 효율적
```java
public int[] solution(int[] arr) {
    for(int i=1; i<arr.length; i++) {
        int temp = arr[i];
        int j = i -1;
        // 현재 선택된 것보다 크기 전까지 반복
        while(j >= 0 && temp < arr[j]) {
            arr[j + 1] = arr[j];    // 한칸씩 뒤로 미룬다.
            j--;
        }
        // 위 반복문에서 탈출하는 경우 앞의 원소가 temp 보다 작다는 의미
        // temp 는 j번째 원소 뒤에 와야한다.
        arr[j+1] = temp;
    }
}
```
* [참고 자료](https://gmlwjd9405.github.io/2018/05/06/algorithm-insertion-sort.html)

## 버블정렬
* 회차마다 인접한 값끼리 비교
* 뒤에서 부터 정렬된다.
* [참고 자료](https://gmlwjd9405.github.io/2018/05/06/algorithm-bubble-sort.html)
```java
public void solution(int[] arr) {
    int temp = 0;
    for(int i=arr.length; i>0; i--) {
        for(int j=0; j<i; j++) {
            if(arr[j] > arr[j+1]) {
                temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }   
    }   
}
```

## 합병정렬
* 배열의 크기가 1이 될 때까지 계속 반으로 나눈 후, 나눠진 배열을 합병하면서 정렬
* [참고 자료](https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html)
```java
public static int[] temp;

public void solution(int[] arr) {
    temp = new int[arr.length];
    mergeSort(arr, 0, arr.length-1);
}

public void mergeSort(int[] arr, int left, int right) {
    
    //더 이상 나눌 수 없으므로 return
    if(left == right) return;
    
    int mid = (left + right) / 2;
    mergeSort(arr, left, mid);
    mergeSort(arr, mid+1, right);
    
    merge(arr, left, mid, right);
}

public void merge(int[] arr, int left, int mid, int right) {
    //왼쪽 부분 리스트 시작점
    int leftIndex = left
    //오른쪽 부분 리스트 시작점
    int rightIndex = mid + 1;
    //임시로 담을 배열 시작점
    int index = left;
    
    while(leftIndex <= mid && rightIndex <= right) {
        if(arr[leftIndex] <= arr[rightIndex]) {
            temp[index++] = arr[leftIndex++];
        }
        else {
            temp[index++] = arr[rightIndex++]; 
        }
    }
    
    //왼쪽 부분 리스트가 먼저 채워졌을 경우
    //즉, 오른쪽 부분 리스트에 아직 값이 남아 있을 경우
    if(leftIndex > mid) {
        while(rightIndex <= right) {
            temp[index++] = arr[rightIndex++];
        }   
    }
    
    //오른쪽 부분 리스트가 먼저 채워졌을 경우
    //즉, 왼쪽 부분 리스트에 아직 값이 남아 있을 경우
    else {
        while(leftIndex <= mid) {
            temp[index++] = arr[leftIndex++];
        }
    }

    //정렬된 배열을 새 배열에 옮겨준다.
    for(int i=left; i<=right; i++) {
        arr[i] = temp[i];
    }
}
```

## 퀵정렬
* pivot 값 선택 후 작은 것은 왼쪽으로, 큰 것은 오른쪽으로 분할(partition)
* 분할한 왼쪽과 오른쪽을 위의 과정 반복
* pivot 선택 방식
    - 첫 번째 요소
    - 중간 요소
    - 마지막 요소
    - 랜덤 요소
    - 첫 번째 요소나 마지막 요소를 선택하면 최악의 경우 O(n<sup>2</sup>)이 나올 수 있다.
    - 따라서 중간 요소를 선택하여 해결할 수 있다.
    - 자바의 내장 함수인 Arrays.sort()는 퀵 정렬이다.
* [참고 자료](https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html)
```java
//중간 요소 퀵 정렬
public void solution(int[] arr) {
    quickSort(arr, 0, arr.length-1);
}

public void quickSort(int[] arr, int low, int high) {
    //low 가 high 보다 크거나 같다면 원소가 1개 이므로 종료
    if(low >= high) return;

    int pivot = partition(arr, low, high);
    quickSort(arr, low, pivot);
    quickSort(arr, pivot+1, high);
}

public int partition(int[] arr, int left, int right) {
    //시작은 배열에서 벗어난 위치에서 한다.
    int low = left - 1;
    int high = right + 1;
    int pivot = arr[(low + right) / 2];

    while(true) {
        // pivot 보다 작으면 low 증가
        do {
            low++;
        } while(arr[low] < pivot);
    
        // pivot 보다 크면 high 감소
        // low 가 high 보다 작거나 같을 때 까지
        do {
            high--;
        } while(arr[high] > pivot && low <= high);
    

        //low 가 high 보다 크거나 같다면(엇갈린다면) 그대로 Swap 하지 않고 종료
        if(low >= high) return high;
        swap(arr, low, high);
    }
    
    public void swap(int[] arr, int low, int high) {
        int temp = arr[low];
        arr[low] = arr[high];
        arr[high] = arr[low];
    }
}
```

## 합병정렬 vs 퀵정렬
* 합병정렬
    - 쪼갤 수 있는 만큼 쪼갠 후 합병하여 정렬한다
    - 장점
        - 안정적이다.(최악과 최선의 경우 모두 N log N 이다.)
    - 단점
        - 배열을 정렬할 때 임시 배열이 필요하다.
* 퀵 정렬
    - Pivot 을 선택하는 과정에서 정렬을 하면서 쪼갠다.
    - 장점
        - 일반적으로 속도가 가장 빠르다.(시간복잡도가 O(N log<sub>2</sub>N)을 가지는 다른 정렬 알고리즘과 비교해도 빠르다.)
        - 추가 메모리 공간이 필요 없다.(O(logN) 만큼의 메모리를 필요로 한다.)
    - 단점
        - 정렬된 리스트에 대해서는 퀵정렬의 불균형 분할(리스트가 계속 불균형하게 나눠짐)에 의해 수행시간이 오래 걸린다.
        - 순차 정렬, 역순 정렬 시 최악의 시간 복잡도
        - Pivot 을 중간 요소로 선택하여 문제 해결
* 같은 O(N log<sub>2</sub>N)이지만 퀵정렬이 더 빠른 이유
    - 코드적으로 생각해보면 Swap 의 횟수가 더 적다.
    - 즉, 합병정렬은 모든 배열을 쪼개고 Swap 을 진행 하는데, 퀵 정렬은 Pivot 을 기준으로 좌우의 값을 Swap 하기 때문에 Swap 의 횟수가 더 적다.
* LinkedList
    - 합병정렬은 LinkedList 정렬이 필요할 떄 유용
    - 퀵정렬을 이용해 LinkedList 를 정렬하면 성능이 좋지 않다.
        - 정렬을 할 때 Index 기반으로 정렬을 하기 때문
        - 퀵정렬은 순차적 접근이 아닌 임의적 접근이기 때문이다.
            - 즉, 배열의 경우에는 인덱스를 통해 접근하기 떄문에 시간복잡도가 O(1)이지만, LinkedList는 Head부터 탐색해야 하기 떄문에 O(n)이다.
            - 즉, 임의적으로 접근할 때마다 오버헤드가 발생한다.
* [참고 자료](https://mygumi.tistory.com/309?category=677288)

## 힙정렬
* 완전 이진 트리를 기본으로 하는 힙 자료 구조 기반 정렬방식
    - 완전 이진 탐색 트리가 아닌, 완전 이진 트리
    - 최대 힙 or 최소 힙을 이용하기 때문에 부모는 자식노드보다 크거나 작아야 한다.
    - 이진 탐색 트리처럼 왼쪽 노드는 작은 값, 오른쪽 노드는 큰 값이 아니다.
* 최대 힙 트리나 최소 힙 트리를 이용하여 정렬
* 퀵정렬 또는 합병정렬의 성능이 좋기 때문에 힙정렬을 많이 사용하지는 않는다.
* 유용한 경우
    - 가장 크거나 가장 작은 값을 구할 때
    - 최대 K 만큼 떨어진 요소들 정렬
* Heap 에서 최댓/최솟 값(Root Node)을 하나씩 추출하면서 정렬
* [참고 자료](https://st-lab.tistory.com/225)
```java
public void solution(int[] arr) {
    heapSort(arr);
}

public int getParent(int child) {
    return (child - 1) / 2;
}

public void heapify(int[] arr, int parentIndex, int lastIndex) {
    int leftChildIndex = 2 * parentIndex + 1;
    int rightChildIndex = 2 * parentIndex + 2;
    int largestIndex = parentIndex;

    // 왼쪽 자식 노드와 비교
    if(leftChildIndex < lastIndex && arr[largestIndex] < arr[leftChildIndex]) {
        larestIndex = leftChildIndex;
    }
    
    // 오른쪽 자식 노드와 비교
    if(rightChildIndex < lastIndex && arr[largestIndex] < arr[rightChildIndex]) {
        largestIndex = rightChildIndex;
    }

    // largestIndex 노드와 부모 노드가 다르다면 부모노드보다 큰 노드가 존재하다는 으미
    // 바꿔주소 그에 해당하는 서브 트리를 Heap 으로 만들어준다.
    if(largestIndex != parentIndex) {
        swap(arr, larestIndex, parentIndex);
        heapify(arr, larestIndex, lastIndex);
    }
}

public void heapSort(int[] arr) {
    int size = arr.length;
    
    // 부모노드와 heapify 과정에서 음수가 발생하면 안된다.
    // 원소가 1개이거나 0개이면 정렬 할 필요가 없다.
    if(size < 2) return;

    // 가장 마지막 노드의 부모 노드 인덱스 구하기
    int parentIndex = getParent(size - 1);

    // 가장 마지막 노드의 부모 노드부터 차례대로 Max Heap 을 만든다.
    // 즉, 제일 작은 서브 트리부터 차례대로 Heap 의 조건을 만족하도록 만든다.
    for(int i=parentIndex; i>=0; i--) {
        heapify(arr, i, size - 1);
    }   

    // 정렬
    // Root Node 인 0번째 인덱스와 i 번째 인덱스를 교환해준다.
    // 0  ~ (i - 1) 까지의 부분트리에 대해 다시 Heap 을 만든다.
    for(int i=size-1; i>0; i--) {
        swap(arr, 0, i);
        heapify(arr, 0, i-1);
    }
}
```

## 위상 정렬
* 정해진 순서대로 실행하는 과정이 필요할 때
* 방향성이 있고, 사이클이 존재하면 안된다.
* Queue 와 Degree 배열을 이용한다.
    - Degree 배열은 어떠한 정점이 자기 자신한테 진입하는 차수를 계산한 배열이다.
    - 해당 Degree 의 값이 0이면 Queue 에 넣는다.
    - 해당 Degree 가 1 이상이면 자신의 순서 앞에 누군가가 먼저 나와야하므로 빼지 않는다.
* [참고 자료](https://www.crocus.co.kr/716)

## 안정 정렬, 불안정 정렬
* 안정 정렬
    - 동일한 값에 대해 기존의 순서가 유지
    - 삽입 정렬, 버블 정렬, 병합 정렬
    - 삽입 정렬이 안정 정렬인 이유
        - 정렬된 1 ~ N 배열에서 N+1번째 값이 자신의 위치를 찾아가는 방식이므로 Stable 하다.
    - 버블 정렬이 안정 정렬인 이유
        - index 제일 뒤쪽부터 두 개의 값을 비교해가며 작은 값을 큰 값과 Swap 한다.
        - 즉, 제일 작은 값이 앞으로 하나씩 올라가는 방식이므로 Stable 하다.
    - 병합 정렬이 안정 정렬인 이유
        - 크기가 N인 배열을 계속해서 divide 하는 단계에서는 index 가 변하지 않는다.
        - conquer 단계에서 인접한 Sub problem 들이 merge 되면서 swap 하는데, 같은 값이면 절대 swap 하지 않는다.
        - 따라서 Stable 하다.
* 불안정 정렬
    - 동일한 값에 대해 기존의 순서가 뒤바뀔 수 있다.
    - 선택 정렬, 퀵 정렬, 힙 정렬
    - 선택 정렬이 불안정 정렬인 이유
        - 예를 들어, [B1, B2, C, A] (A < B1 = B2 < C) 로 되어있다고 가정하자
        - 순서대로 순회하면서 정렬하면 다음과 같다.
        - round 1 : [A, B2, C, B1]
        - round 2 : [A, B2, C, B1]
        - round 3 : [A, B2, B1, C]
        - 초기의 B1, B2의 순서가 뒤 바뀐 것을 확인할 수 있고 이를 불안정 정렬이라 한다
        - [참고 자료](https://stackoverflow.com/questions/4601057/why-is-selection-sort-not-stable)
    - 퀵 정렬이 불안정 정렬인 이유
        - pivot 을 기준으로 swap 하기 때문에 같은 값의 위치가 바뀔 수 있다.
        - [참고 자료](https://stackoverflow.com/questions/21106766/why-quick-sort-is-unstable)
    - 힙 정렬이 불안정 정렬인 이유
        - 최대 힙을 만들 때 불안정 정렬 상태에서 최댓값만 가지고 정렬을 하기 때문에 안정정렬이 아니다.

## 빠른 선택 알고리즘
* K 번째로 큰 값 혹은 K 번째로 작은 값을 구할 때 사용
* 퀵 정렬을 응용
* O(N)의 시간 복잡도인 이유
    - N + N/2 + N/4 + ...
* 퀵 정렬을 모두 한 후 찾는 것이 아닌 퀵 정렬을 하면서 찾는 방식이다.
* 주의
    - K 번째와 Pivot 값을 잡을 때 K 번째는 관계 없다.
    - 결국 정렬된 후의 Pivot 값 인덱스를 반환하기 때문이다.
* [참고 자료](https://hackability.kr/entry/Quick-Selection%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%9C-On-%EC%84%A0%ED%83%9D-%EB%B0%A9%EB%B2%95)  
