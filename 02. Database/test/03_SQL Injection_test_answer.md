1. 해커는 PW input 란에 논리적 에러를 이용해 로그인 우회를 하고자 한다. 이때 해커가 입력할 문장을 작성하시오.

    ![https://user-images.githubusercontent.com/76686872/158479771-9d0f60f3-91e7-4ee9-afdc-cb334bc97c6a.png](https://user-images.githubusercontent.com/76686872/158479771-9d0f60f3-91e7-4ee9-afdc-cb334bc97c6a.png)
    
    → **' OR '1'='1**
    

1. 해커는 게시글 조회 요청에 user 테이블을 삭제하는 쿼리문을 같이 넣고자 한다. 해커가 입력할 문장을 작성하시오. 

    ![https://user-images.githubusercontent.com/76686872/158479892-1bf855f1-6183-4f92-b50e-e80ee9e5b11d.png](https://user-images.githubusercontent.com/76686872/158479892-1bf855f1-6183-4f92-b50e-e80ee9e5b11d.png)
    
    → **9999;DROP TABLE user**
    
2. SQL Injection을 방어하는 방법 중에는 사용자가 입력하는 값을 검증하는 방법이 있다. 이때, 상대적으로 덜 안전한 방식의 명칭과 방어하는 방법을 쓰시오.
    
    → **블랙 리스트 방식, HTTP 요청을 통해 전달되는 사용자 데이터에 SQL 구문으로 해석될 수 있는 문자나 공격에 사용되는 SQL 구문의 포함 여부를 검사하여 포함 시 요청을 차단하거나 해당 문자를 제거함.**
    
3. 사용자의 입력값을 문자열로 취급해 공격 쿼리를 무효화하는 구문의 명칭은?
    
    → ****매개변수화된 쿼리(Prepared Statement)****
    
    ---