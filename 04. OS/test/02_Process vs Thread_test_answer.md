CS 스터디 4주차 시험지
OS - Process vs Thread

<br>

1. 다음 그림을 완성하시오.




<img width="531" alt="image" src="https://user-images.githubusercontent.com/66426083/162187716-4816f727-3ac6-47e8-826c-11ed78510e95.png">







<br>

2. 멀티 프로세스의 장단점을 서술하시오


장점: 안전성 (하나의 프로세스가 죽어도 다른 프로세스에 영향을 미치지 않음, 메모리 침범X)


단점: 많은 메모리 공간과 CPU 시간 필요, 문맥교환 시 캐시 매모리 초기화로 인한 성능 저하




<br>



3. 멀티 스레드의 장단점을 서술하시오


장점: 프로세스에 비해 빠른 문맥교환, 공유 메모리로 자원 소모 감소 (Throughput 향상, 응답 시간 단축)


단점: 공유 메모리로 인한 안전성 문제(동기화 작업 필요 but 과도한 동기화는 병목현상 야기(성능저하))

![image](https://user-images.githubusercontent.com/66426083/162187625-fb4448c1-d8fa-4f78-89a4-c480071275b7.png)
