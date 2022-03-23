# **Blocking I/O & Non-Blocking I/O**

---

## **I/O 작업**

- : Kernel level에서만 수행 가능 → 유저 Process(or Thread)는 커널에게 I/O 요청해야.(==시스템 콜 보내기)
- 시스템 콜 보내는 순간 커널로 제어권 넘어가고 (context-switch), 유저 Process(or Thread)는 제어권 돌아오기 전까지 block됨(다른 작업 못함). 커널이 반환하는 결과 기다림.

## **Blocking I/O**

- I/O 작업이 진행되는 동안 Kernel이 제어권 갖고 있어, user Process(Thread) 는 자신의 작업을 중단한 채 대기
- 과정
    1. 유저가 커널에게 read 작업 요청 (: recvfrom 함수 호출)
    2. 데이터 입력될 때까지 block돼 대기
    3. 데이터 입력되면 커널이 유저에게 결과 전달(커널에서 유저로 데이터 복사) → 유저는 하던 일 복귀
    
    ![image](https://user-images.githubusercontent.com/76686872/159688813-f74113e1-b2c5-4b2c-9041-5280d650fd4c.png)
    

## **Non-Blocking I/O**

I/O 작업이 진행되는 동안 User Process의 작업을 중단하지 않음.

- 진행 순서
    1. 유저가 커널에게 read 작업 요청 (: recvfrom 함수 호출)
    2. 요청 즉시 결과 반환: Kernel은 곧바로 recvBuffer를 채워서 보내지 못하므로, 입력 데이터가 없다는 결과 메시지 "EWOULDBLOCK"을 return함.
    3. 입력 데이터가 있을 때까지 1, 2번 과정 반복
        
        > Blocking 방식과 달리, User Process는 그동안 다른 작업을 진행할 수 있음.
        > 
    4. 입력 데이터가 있으면 유저에게 결과 전달
        
        > 입력 데이터가 있으면(recvBuffer에 user가 받을 수 있는 데이터가 있는 경우), recvfrom 함수는 Kernel에 있는 Buffer에서 데이터를 복사해서 유저로 받아옴.
        > 
    
    ![image](https://user-images.githubusercontent.com/76686872/159688851-5a935856-c562-48f3-9768-ac1acb118350.png)
    

참고 링크

- [https://ju3un.github.io/network-basic-1/[](https://ozt88.tistory.com/20)](https://ju3un.github.io/network-basic-1/)
- [https://ozt88.tistory.com/20](https://ozt88.tistory.com/20)