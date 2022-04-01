5. 다음은 I/O 작업의 진행 과정이다. a번과 b번은 Blocking I/O와 Non-Blocking I/O 중 각각 어디에 해당하는가?

   1. 유저가 커널에게 read 작업 요청 (: recvfrom 함수 호출)
   2. a. 입력 데이터가 없다는 결과 메시지 "EWOULDBLOCK"을 return, read 작업 요청
      b. 데이터 입력될 때까지 대기
   3. 입력 데이터가 있으면 유저에게 결과 전달

   → 1번은 Non-Blocking, 2번은 Blocking
