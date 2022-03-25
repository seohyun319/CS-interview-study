CS 스터디 2주차 시험지
Database - Transaction

<br>

1. 트랜잭션의 특징 4가지를 서술하시오.

- 원자성 (Atomicity): 트랜잭션이 DB에 모두 반영되거나, 혹은 전혀 반영되지 않아야 함 (all or nothing)
- 일관성 (Consistency): 트랜잭션의 작업 처리 결과는 항상 일관성 있어야 함 (각종 무결성 제약 조건 충족 필요)
- 독립성 (Isolation): 둘 이상의 트랜잭션이 동시에 병행 실행되고 있을 때, 어떤 트랜잭션도 다른 트랜잭션 연산에 끼어들 수 없음
- 지속성 (Durability): 트랜잭션이 성공적으로 완료되었으면 결과는 영구적으로 반영되어야 한다



<br>




2. UNDO와 REDO가 무엇인지 서술하시오.


- UNDO: 정상적으로 종료되지 않은 트랜잭션이 변경한 page들 복구 작업
- REDO: 이미 commit한 트랜잭션의 수정을 재반영하는 복구 작업



<br>


3. 다음 표의 빈칸을 채우고, 현재 대부분의 DBMS가 채택 중인 정책에 체크하시오.
<img width="726" alt="image" src="https://user-images.githubusercontent.com/66426083/160154940-ce4c221e-6c2d-459a-b2d0-3da552c31af7.png">

