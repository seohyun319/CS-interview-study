CS 스터디 2주차 시험지
Network - TCP 3 way handshake & 4 way handshake

<br>

1. 3 way handshake와 4 way handshake의 목적에 대해 서술하시오.


- 3 way handshake : 연결 성립



- 4 way handshake : 연결 해제


<br>

2. 보기를 참고해 3 way handshake의 과정을 완성하시오. (단, 모든 보기를 활용할 것)


1) 클라이언트 -> (        SYN(x)        ) -> 서버

2) 서버 -> (.      ACK(x+1), SYN(y),      ) -> 클라이언트

3) 클라이언트 -> (         ACK(y+1)        ) -> 서버


<br>


3. 보기를 참고해 4 way handshake의 과정을 완성하시오.


1) 클라이언트 -> (     FIN 플래그     ) -> 서버

2) 서버 -> (      ACK         ) -> 클라이언트

3) 서버 -> (     FIN 플래그        ) -> 클라이언트

4) 클라이언트 -> (      ACK         ) -> 서버
