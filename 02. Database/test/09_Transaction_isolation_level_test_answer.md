## Transaction Isolation Level  

------

1.	다음 중 대부분 DBMS가 채택하고 있는 기본 트랜잭션 격리성 수준(Transaction Isolation Level)인 것은?  

     A.	Read Uncommitted  
  
     B.	Read Committed  
  
     C.	Repeatable Read  
  
     D.	Serializable   
     
-  대부분 DBMS가 Read Commtted를 기본 트랜잭션 격리성 수준으로 채택하고 있으므로 Dirty Read가 발생할 위험은 적지만, Non-Repeatable Read, Phantom Read 현상에 대해선 주의가 필요하다.  
     <br>
  
2.	O, X 문제  

     A.	트랜잭션 격리성 수준(Transaction Isolation Level)을 Serializable로 상향 조정하면 일반적으로 동시성과 일반성이 같이 높아진다. (O, X)  
     
- 격리 레벨이 높아질수록(상향 조정할수록) 일관성은 높아지지만 동시성은 낮아진다.  
     <br>
  
3.  아래 그림은 000방식을 사용할 때 발생할 수 있는 문제 상황을 나타낸 것이다. 그림에서 발생한 문제를 하고 000에 들어갈 격리 수준의 이름을 쓰시오.    
    
    ![image](https://user-images.githubusercontent.com/65678579/160237379-ff698b9d-2455-42f7-a634-5cb6cff4f087.png)


 - Read Committed, 실제 테이블 값을 가져오는 것이 아니라 Undo 영역에 백업된 레코드에서 값을 가져오는 방식이다. 그림에서 트랜잭션 -1 이 커밋한 이후 아직 끝나지 않은 트랜잭션 -2가 테이블 값을 읽으면 값이 변경된단느 문제가 발생한다. 하나의 트랜잭션 내에서 똑같은 SELECT 쿼리를 실행했을 때 같은 결과를 가져와야하는 정합성에 어긋나며, 입금, 출금 처리가 진행되는 금전적인 처리에 불리하다.  
     <br>
