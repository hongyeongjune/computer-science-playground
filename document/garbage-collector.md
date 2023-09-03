## Garbage Collection
* 프로그램이 동적으로 할당했던 메모리 영역(Heap) 중 필요 없게 된 영역을 해제하는 작업
* Mark and Sweep
    - Root Space 에서 부터 접근 가능한지를 해제의 기준으로 정한다.
    - Mark
        - Root Space 부터 탐색을 통해 연결된 객체를 찾아낸다.
        - 연결된 객체는 Reachable Object
        - 연결이 끊어진 객체는 Unreachable Object
    - Sweep
        - 연결이 끊어진 객체를 지운다.
    - Mark and Sweep Compaction
        - 유효한 객체들이 연속되게 쌓이도록 힙의 가장 앞 부분부터 채워져 객체가 존재하는 부분과 존재하지 않는 부분으로 나눈것
        - Sweep 이후 분산되어 있던 메모리를 정리
* Stop The World
    - GC 를 실행하기 위해 JVM 이 애플리케이션 실행을 멈추는 것
* GC 의 동작
    - Heap 영역에 존재하는 객체들에 대해 접근 가능한지 확인한다.
    - Root Space 에서 부터 시작하여 참조 값을 따라가며 접근 가능한 객체들에 Mark 하는 과정을 진행
    - Mark 되지 않은 객체 즉, 접근할 수 없는 객체는 Sweep(제거) 된다.
* Root Space 가 되는 조건
    - Stack 영역에 있는 데이터 (지역변수 혹은 파라미터)
    - method area 의 static 데이터
    - Native Method Stack 의 JNI 에 의해 생성된 객체들
        - Java Native Interface: 자바가 아닌 다른 언어로 만들어진 애플리케이션과 상호 작용 할 수 있는 인터페이스를 제공하는 것
* 영 영역
    - Minor GC
    - 새로운 객체들이 할당되는 영역
    - 순서
        - 처음 생성된 객체는 Eden 영역에 할당
        - Eden 영역이 꽉차면 Minor GC 수행
        - Eden 영역에서 살아남은 객체는 Survivor 0 영역으로 이동하면서 age 값이 1 증가한다.
        - 다시 Eden 영역이 꽉차면 다시 Minor GC 수행하고 이번에 살아남은 객체들은 다른 Survivor 1 영역으로 이동하고 age 값이 마찬가지로 1 증가한다.
        - 참고로 Survivor 영역은 하나에 객체가 있으면 다른 Survivor 에는 객체가 존재하면 안된다.
        - 위의 과정을 반복하고 age 가 특정 임계점이 되면 old 영역으로 이동한다.
        - 참고로 자바 8 병렬 GC 사용 기준 age 값이 15가 되면 old 영역으로 이동한다.
* 올드 영역
    - Major GC
    - Young 영역에서 살아남은 객체가 여기로 복사
    - Old 영역에 있다가 미사용된다고 식별되는 객체들은 Major GC 를 통해 메모리에서 제거
* STW 를 줄이는 GC 알고리즘
    - Serial GC
        - GC 를 처리하는 스레드가 1개 (싱글 스레드)
        - 다른 GC 에 비해 STW 시간이 길다
        - Mark and Sweep Compaction 사용
    - Parallel GC
        - Java 8 의 default GC
        - young 영역의 GC 를 멀티 스레드로 수행
        - Serial GC 보다 STW 감소
    - Parallel Old GC
        - Parallel GC 개선
        - Old 영역에서도 멀티 스레드로 GC 수행
    - CMS GC
        - Concurrent Mark and Sweep 의 줄임말 STW 시간을 줄이기 위해 고안
        - Compaction 과정이 없다.
        - Reachable 객체를 한 번에 찾지 않고 순차적으로 찾는다.
        - Initial Mark : Root Station 이 참조하는 객체만 마킹 (STW 발생)
        - Concurrent Mark : 참조하는 객체를 따라가며, 지속적으로 마킹 (STW 없이 발생)
        - Remark : concurrent Mark 과정에서 변경된 사항이 없는지 다시 한번 더 마킹하며 확인 (STW 발생)
        - Concurrent Sweep : 접근할 수 없는 객체를 제거하는 과정 (STW 없이 발생)
        - 위 처럼 STW 가 최대한 덜 발생하도록 하여, 자바 애플리케이션이 멈추는 현상을 줄임
        - 문제점
            - 기본적으로 Compaction 이 없어서 메모리 단편화가 일어날 수 있음 -> Compaction 작업을 넣어주면 STW 시간이 더 길어질 수 있는 문제 발생
            - 다른 GC 보다 메모리, CPU 를 더 많이 사용하는 단점이 있다. -> GC 대상을 파악하는 과정이 여러 단계로 수행되기 때문에 CPU 사용량이 높음
        - Compaction 해결법
            - Free List 방법
                - Promotion 할당을 할 때 Young 영역에서 승격된 Object 와 크기가 비슷한 Old 영역의 Free space 를 Free List 에서 탐색하게 된다.
                - 또한 Promotion 되는 Object 크기를 계속 통게화하여 Free Memory 블럭들을 붙이거나 쪼개서 적절한 Size 의 Free Memory Chunk 에 Object 를 할당한다.
                - 이런 작업은 Young 영역에 부담을 주는데, Free List 에서 적절한 Chunk 크기를 찾아 할당 해야되기 때문에 시간이 오래 걸린다.
    - G1 GC
        - CMS GC 의 메모리 단편화를 개선한 GC
        - Java 9 의 default GC
        - Eden, Survivor, Old 영역이 존재하지만, 해당 영역은 고정된 크기가 아니고 전체 heap 메모리 영역을 Region 이라는 특정한 크기로 나눈 것
        - Region 상태에 따라 그 Region 의 역할(Eden, Survivor, Old)가 동적으로 변동함
        - 전체 Heap 이 아닌 Region 단위로 탐색하며 mark and sweep 을 한다.
        - Compaction 을 수행한다.
        - Young GC 동작 과정
            - 멀티 스레드로 동작
            - Eden/Survivor 영역에서 수행
            - GC 후 살아있는 객체를 다른 Survivor Region 으로 이동시키고, 비워진 Region 을 Available Region 으로 변경
        - Old GC 동작 과정
            - Initial Mark : Survivor Region 중에서 Old 영역의 객체를 참조하고 Region 을 식별한다. (STW 발생)
            - Root Region Scan : Initial Mark 에서 찾은 Survivor Region 에 대한 GC 스캔 작업을 진행한다. (STW 없이 발생)
            - Concurrent Mark : 전체 Heap 영역에 대한 스캔으로, 살아있는 객체가 존재하는 Region 만 식별한다. (STW 없이 발생)
            - Remark : 최종적으로 살아남은 객체를 식별한다. (STW 발생)
            - Clean up
                - 살아남은 객체가 가장 적은 Region 의 GC 대상을 제거한다. (STW 발생)
                - STW 를 끝내고 GC 로 제거되어 빈 영역은 Available Region 으로 변경된다. (STW 없이 발생)
            - Copy
                - 살아남은 객체들을 Available Region 에 복사하여 Compaction 수행 (STW 없이 발생)