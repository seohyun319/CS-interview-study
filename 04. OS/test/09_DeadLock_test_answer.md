## DeadLock 
---

1. 교착상태(DeadLock)과 무한 대기 상태의 차이점을 서술하시오.

* 교착상태는 제 3자의 도움이 존재해야 해당 상태를 빠져나올 수 있는 반면, 무한대기상태는 외부적 조치 없이 서비스를 언젠가 받을 수 있다.
<br>

2.  프로세스가 어떤 자원을 사용 중이고 어떤 자원을 기다리고 있는지 나타내는 방향성이 있는 그래프를 무엇이라 하는가? (한국어, 영어 약자, 영어 모두 가능)

* RAG, 자원 할당 그래프, Resource Allocation Graph 중 하나 작성
<br> 

3. 교착 상태가 되기 위한 네 가지 필요조건을 작성하시오.

* 상호배제(Mutual exclusion), 점유대기(Hold and wait), 비선점(No preemption), 순환대기(Circular wait)
<br>

4.	교착 상태 해결 방법 중, 교착 상태를 유발하는 네 가지 조건을 무력화해 방지하는 방법을 무엇이라 하는가? (00와 00)

* 예방과 회피
<br>

5.	4번의 단점을 하나만 작성하시오.

* 자원의 심각한 낭비와 특정 프로세스의 무한대기 가능성이 있다.
