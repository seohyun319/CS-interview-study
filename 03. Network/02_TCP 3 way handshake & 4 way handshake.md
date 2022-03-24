## TCP 3 way handshake & 4 way handshake
> 연결을 성립하고 해제하는 과정

<br>
<br>

### 3 way handshake

- 연결 성립 (Connection Establishment)
- TCP는 정확한 전송을 보장해야 함으로 통신에 앞서 논리적인 접속을 보장하기 위해 연결 성립 과정 진행

<br>

<image width=500 src="https://user-images.githubusercontent.com/66426083/159830474-13b9fdb0-9849-489a-ae48-bb7fa396ee5d.png" />
<br>

1) 클라이언트가 서버에게 접속을 요청하는 SYN(x) 패킷을 보냄
2) 서버가 SYN(x)을 받고, 클라이언트로 받았다는 신호인 ACK(x+1)와 SYN(y) 패킷을 보냄
3) 클라이언트는 서버의 수락 응답인 ACK(x+1)와 SYN(y) 패킷을 받고, ACK(y+1)를 서버로 보내며 연결이 성립됨

<br>
-> 3번의 통신을 통해 연결 성립(3 way handshake)


<br>
<br>

---

<br>

### 4 way handshake

- 연결 해제 (Connection Termination)
- 모든 통신이 끝난 후에는 연결을 해제해야 함

<br>

<image width=500 src="https://user-images.githubusercontent.com/66426083/159831183-7e3c8ea7-4e9d-47d1-86c1-e29b304107b8.png" />
<br>

1) 클라이언트가 서버에게 연결을 종료하겠다는 FIN 플래그를 보냄

2) 서버는 FIN을 받고, 확인했다는 ACK를 클라이언트에게 보냄 (이때 데이터를 모두 보낼 때까지 CLOSE_WAIT 상태가 됨)

3) 데이터를 모두 보냈다면, 연결이 종료되었다는 FIN 플래그를 클라이언트에게 보냄

4) 클라이언트는 FIN을 받고, 확인했다는 ACK를 서버에게 보냄 (아직 서버로부터 받지 못한 데이터가 있을 수 있으므로 TIME_WAIT을 통해 기다림)

    - 서버는 ACK를 받은 이후 소켓 연결을 닫음(Closed)

    - TIME_WAIT 시간이 끝나면 클라이언트도 닫음 (Closed)

<br>
-> 4번의 통신을 통해 연결 해제 (4 way handshake)


<br>
<br>
<br>
참고 https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/TCP%203%20way%20handshake%20%26%204%20way%20handshake.md / https://asfirstalways.tistory.com/356

