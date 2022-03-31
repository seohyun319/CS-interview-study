## TLS handshake 
---

1. 
    (1). SSL인증서에는 서버의 개인키가 담기고, 이 인증서는 CA의 개인키로 암호화된다. (O, X)  
    (2). TCP 3 way handshake보다 TLS handshake가 선행된다. (O, X)  

<br>

2.  (1) :  
    (2) :  
    (4) :  
    (8) :  
    ![image](https://user-images.githubusercontent.com/65678579/161054076-f6ab245d-48c7-4999-8520-a186b31750ca.png)  

<br> 

3. CA 인증서에 대한 신뢰성이 확보되었다면, 클라이언트 난수 바이트를 생성하여 서버의 공개키로 암호화한다. 이 난수 바이트는 대칭키를 정하는데 사용이 되고, 앞으로 서로 메세지를 통신할 때 암호화하는데 사용한다.

