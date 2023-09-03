## Transaction Isolate
* Read Uncommitted
    - 트랜잭션이 커밋되지 않아도 다른 트랜잭션이 데이터를 읽을 수 있는 레벨
    - dirty read 발생
        - 한 트랜잭션이 변경 사항을 커밋을 하지 않았느데, 다른 트랜잭션이 변경 사항을 바로 읽을 수 있는 문제
    - Non-Repeatable, Phantom Read 현상도 발생
    - 예시
        - A 트랜잭션이 어떤 데이터를 변경했을 때 B 트랜잭션이 해당 데이터를 조회
        - A 트랜잭션이 커밋전에 어떤 오류에 의해 롤백처리가 되었는데, B 트랜잭션은 변경된 데이터로 계속 작업을 진행함
* Read Committed
    - 어떤 트랜잭션의 변경 내용이 커밋되어야만 다른 트랜잭션에서 읽을 수 있는 레벨
    - 커밋이 되지 않으면 트랜잭션 시작 전 데이터를 읽는다.
    - dirty read 현상 해결
    - Non-Repeatable 발생
        - 하나의 트랜잭션에서 항상 같은 데이터를 반환하지 않는 문제
    - Phantom Read 현상도 발생
    - 예시
        - A 트랜잭션이 시작하고, B 트랜잭션이 시작했다.
        - B 트랜잭션이 어떤 데이터를 조회한다.
        - A 트랜잭션에서 해당 데이터를 변경하고 커밋하였다.
        - B 트랜잭션에서 다시 해당 데이터를 조회하면 다른 값이 조회된다.
* Repeatable Read
    - 트랜잭션이 시작되기 전 커밋된 내용에 대해서만 조회할 수 있는 레벨
    - MySQL 의 default 격리 수준
    - MySQL 에서는 트랜잭션 id 를 부여해서 id 가 작은 트랜잭션에서 커밋된 데이터만 읽을 수 있다. -> 변경되기 전 레코드는 undo 영역에 저장
    - Non-Repeatable 현상 해결
    - Phantom Read 발생
        - 한 트랜잭션 내에서 같은 쿼리를 두 번 실행했는데, 첫 번째 쿼리에 없던 레코드가 두 번째 쿼리에서 나타나는 현상
        - Insert 에서만 발생
    - 예시 코드
      ```sql
      START TRANSACTION; -- transaction id : 1
      SELECT * FROM MEMBER WHERE MEMBER.Gender = 'Male'; -- 0건 조회
      
        START TRANSACTION; -- transaction id : 2
        INSERT INTO MEMBER VALUES(1,'hongyeongjune', 27, 'Male');
        COMMIT;
      
      SELECT * FROM MEMBER WHERE MEMBER.Gender = 'Male'; -- 1건 조회
      COMMIT;
  ```
  - MySQL 의 실행 엔진 중 하나인 InnoDB 는 내부적으로 next-key lock 때문에 Phantom Read 를 허용하지 않는다.
* Serializable
    - 이는 트랜잭션이 완료될 때까지 다른 트랜잭션은 해당 데이터의 수정 및 삽입을 허용하지 않는다.
    - 읽기 작업을 할때조차 Lock 을 건다.
    - 가장 엄격하고 확실하게 일관성을 보장하나 동시처리가 안되기 때문에 성능이 낮다.

## Lock
* InnoDB 의 Row-level 은 Shared Lock 과 Exclusive Lock 두 가지가 존재한다.
* Shared Lock
    - 읽을 때 사용되는 Lock
    - shared lock 끼리는 동시에 접근이 가능하다. -> 즉, 하나의 row 를 여러 트랜잭션이 읽을 수 있다.
    - 하지만, shared lock 이 설정된 row 에는 exclusive lock 을 걸 수 없다.
    - 일반적인 select 문에는 shared lock 이 걸리지 않는다.
* Exclusive Lock
    - 특정 row 를 변경하고자 할 때 사용
    - 특정 row 에 exclusive lock 이 해제될 때 까지 shared lock 이나, 쓰기 작업을 위해 exclusive lock 을 걸 수 없다.
* Record Lock
    - 테이블에 인덱스가 생성되어 있지 않더라도 테이블 생성시에 함께 생성되는 default Clustered Index 의 레코드에 Lock 을 걸어, 항상 인덱스 레코드에 Lock 을 설정한다.
    - row 가 아닌 DB index 에 걸리는 lock
    - 특정 레코드에 shared lock 혹은 exclusive lock 을 걸 때 사용한다.
    - exclusive lock 예시
      ```sql
      (Transaction A)
      SELECT column FROM table WHERE column = 10 FOR UPDATE;
      (Transaction B)
      DELETE FROM table WHERE column = 10;
      ```
        - 이렇게 하면, table.column 의 값이 10인 index 에 exclusive lock 이 걸린다.
        - 그래서 table.column 이 10인 row 를 삭제할 수 없다.
    - shared lock 예시
      ```sql
      (Transaction A)
      SELECT * FROM table WHERE column=10 LOCK IN SHARE MODE
      ```
    - 이렇게 하면, table.column 의 값이 10인 index 에 shared lock 이 걸린다.
* Gap Lock
    - index record 에 직접 lock 을 거는 것이 아니라 gap 에 거는 lock 이다.
    - gap 이란 index 중 db 에 실제 없는 값이다.
    - 예를들어, id column 만 있는 테이블이 있고 이 column 에 index 가 설정되었고 현재 테이블엔 id = 3, id = 7 만 저장되어있다.
    - 여기서 gap 은 2 <= id, 4 <= id <= 6, id <= 8 이다.
    - gap lock 은 해당 gap 에 접근하려는 다른 쿼리를 막는다.
    - 예시
      ```sql
      (Transaction A)
      SELECT columnn FROM table WHERE column BETWEEN 1 AND 10 FOR UPDATE;
      ```
        - 이 테이블에는 3, 7의 값이 저장되어있다고 하자
        - 1<= column <= 2, 4 <= column <= 6, 8 <= column <= 10 에 gap lock 이 걸린다.
* next-key lock
    - record lock + gap lock 동시 사용
    - 예시
      ```sql
      (Transaction A)
      SELECT * WHERE id > 100 FOR UPDATE
      ```
        - 이 테이블에는 1, 3, 90, 101, 107 값이 저장되어있다고 하자
        - id > 100 을 만족하는 첫 레코드 101을 발견하면 첫 인덱스 발견 직전 레코드부터 gap lock 이 걸린다.
        - 해당 조건절을 만족하는 레코드에 record lock 이 걸린다.
        - gap lock
            - 90 <= id <= 100, 102 <= id <= 106, 108 <= id
        - record lock
            - 101, 107
