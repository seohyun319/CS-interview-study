## TLS handshake  
---

1.	X, X  

    (1). SSL인증서에는 서버의 공개키가 담기고, 이 인증서는 CA의 개인키로 암호화 된다.    
    (2). TCP 3 way handshake 이후 TLS handshake가 진행된다.
    <br>

2.	
    (1) : Client hello  
    (2) : Server hello  
    (4) : Client key exchage   
    (8) : Server “finished” 
    <br> 
3. 4번 Client key exchage에 대한 설명이다.  
