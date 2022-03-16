## 트랜잭션 (Transaction)

<br>

- 데이터베이스의 상태를 변화시키기 위해 수행하는 작업 단위
  - 상태 변화: SQL 질의어(SELECT, INSERT, DELETE, UPDATE)를 통해 DB에 접근
  - 작업 단위: 기준에 따라 정한 SQL 명령문 묶음
  - ex) 계좌에서 만 원 출금 후 만 원 입금하는 DB 작업 -> 두 개의 UPDATE문을 묶어 하나의 트랜잭션이라고 함.
  - 하나의 작업(트랜잭션)이 완료되려면 트랜잭션 속의 모든 쿼리문이 성공적으로 완료되어야 함 (Commit)
  - 작업 단위에 속하는 쿼리 중 하나라고 실패하면 모든 쿼리문을 취소하고 이전 상태로 돌려놓아야 함 (Rollback)
    <br>

---

<br>

### **트랜잭션의 특징 (ACID 성질)**

- 원자성 (Atomicity)
  - 트랜잭션이 DB에 모두 반영되거나, 혹은 전혀 반영되지 않아야 함 (all or nothing)
- 일관성 (Consistency)
  - 트랜잭션의 작업 처리 결과는 항상 일관성 있어야 함 (각종 무결성 제약 조건 충족 필요)
- 독립성 (Isolation)
  - 둘 이상의 트랜잭션이 동시에 병행 실행되고 있을 때, 어떤 트랜잭션도 다른 트랜잭션 연산에 끼어들 수 없음
- 지속성 (Durability)
  - 트랜잭션이 성공적으로 완료되었으면 결과는 영구적으로 반영되어야 한다

<br>

---

<br>

### **Transaction의 상태**

<br>
<image width=500 src="https://user-images.githubusercontent.com/66426083/158584329-ac4ca19c-0fee-4694-a62a-a749184c3e32.png" />
<br>

- Commit: 하나의 트랜잭션이 성공적으로 끝났을 때 변경된 데이터를 디스크에 영구적으로 반영하는 것
- Rollback: 하나의 트랜잭션이 비정상적으로 종료되어 원자성이 깨진 경우 이전 Savepoint로 되돌아가는 것

<br>

---

<br>

### **Transaction 관리를 위한 DBMS의 전략**

- **DBMS의 구조**
  <br><br>
  <image width=400 src="https://user-images.githubusercontent.com/66426083/158551992-98ad6d44-c979-4fb3-bfb2-2e169d3079e6.png" />
  <br>

  - 질의 처리기(Query Processor) + 저장 시스템(Storage System)
  - 데이터를 고정 길이의 page 단위로 비휘발성 저장 장치인 디스크에 저장, 일부분을 메인 메모리에 저장

- **버퍼 관리자(Buffer Manager)**

  - DBMS의 Storage System에 속하는 모듈 중 하나로 메인 메모리애 유지하는 페이지들을 관리하는 모듈
  - 버퍼 관리 정책에 따라 UNDO 복구와 REDO 복구가 요구되거나 그렇지 않게 되므로 트랜잭션 관리에 매우 중요

- **UNDO**
  - 정상적으로 종료되지 않은 트랜잭션이 변경한 page들 복구 작업
  - 버퍼 관리자의 버퍼 교체 알고리즘에 따라 트랜잭션과 무관하게 버퍼 교체(수정된 페이지들을 디스크에 )가 일어날 수 있기 때문에 필요
    1. STEAL : 수정된 페이지를 언제든지 디스크에 쓸 수 있는 정책
       - 대부분의 DBMS가 채택
       - UNDO logging과 복구를 필요로 함
    2. NO-STEAL : 수정된 페이지들을 EOT(End Of Transaction)까지는 버퍼에 유지하는 정책
       - UNDO 작업이 필요하지 않지만 매우 큼 메모리 버퍼 필요
- **REDO**
  - 이미 commit한 트랜잭션의 수정을 재반영하는 복구 작업
    1. FORCE : 수정했던 모든 페이지를 트랜잭션 commit 시점에 디스크에 반영하는 정책
       - 커밋되었을 때 수정된 페이지들이 디스크에 반영되므로 REDO 불필요
    2. NO-FORCE : 수정했던 페이지를 commit 시점에 디스크에 반영하지 않는 정책
       - 대부분의 DBMS가 채택
       - 트랜잭션이 디스크상의 DB에 반영되지 않을 수 있어 REDO 필요
       - 커밋 시 로그(log)만 기록

<br><br>

<table>
  <tr>
    <th colspan="2">트랜잭션이 완료되지 않은 상태에서 데이터를 디스크에 기록할 것인가?</th>
  </tr>
  <tr>
    <td>STEAL</td>
    <td>기록한다 (중간에 디스크로 데이터 스틸!)</td>
  </tr>
  <tr>
    <td>NO-STEAL</td>
    <td>기록하지 않는다</td>
  </tr>
  </table>

<br>

<table>
  <tr>
    <th colspan="2">트랜잭션이 완료된 후 바로 데이터를 디스크에 기록할 것인가?</th>
  </tr>
  <tr>
    <td>FORCE</td>
    <td>기록한다 (강제로 바로 디스크에 저장!)</td>
  </tr>
  <tr>
    <td>NO-FORCE</td>
    <td>기록하지 않는다</td>
  </tr>
  </table>

<Br><br>
_DBMS는 버퍼 관리 정책으로 STEAL과 NO-FORCE 정책 채택 -> UNDO, REDO 모두 필요_

<br>
<br>
  <br>
  <br>
  참고  https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/Transaction.md / https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Database#transaction
