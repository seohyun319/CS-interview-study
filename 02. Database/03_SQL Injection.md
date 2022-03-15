# SQL Injection

injection

1. 주사
2. (상황·사업 등의 개선을 위한 거액의) 자금 투입
3. (액체의) 주입

## **SQL Injection**

> 해커가 조작한 SQL 쿼리문을 주입하고 실행되게 하여 데이터베이스가 비정상적인 명령을 실행하도록 조작하는 공격 기법
> 
- 공격에 성공하게 되면 조직 내부의 민감한 데이터나 개인 정보를 획득 가능
- 심각한 경우에는 조직의 데이터 전체를 장악하거나 완전히 손상시킬 수 있음.

---

## SQL Injection의 동작 원리 및 공격 방법

### 1) 인증 우회 예시

- 정상적인 로그인 요청 수행 과정
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/73e6b775-99aa-47e3-a82d-6e955d3e99e1/Untitled.png)
    
- SQL Injection을 통한 로그인 우회
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ad87ee7d-e30c-44fe-8c75-93b0e767103d/Untitled.png)
    
- 논리적 에러 이용
    - 로그인 시 유저가 input 창에 아이디, 비밀번호 입력 시 다음 쿼리문 전송됨
        
        SELECT * FROM USER WHERE ID = ‘abc’ AND PASSWORD = ‘1234’;
        
    - 기본 쿼리문의 WHERE 절에 true문을 OR문으로 추가하여 무조건 적용되도록 수정한 뒤 DB를 마음대로 조작 가능
        1. 끝에 넣기 `' OR '1'='1`
            
            SELECT * FROM USER WHERE ID = ‘abc’ AND PASSWORD = ‘`' OR '1'='1`';
            
            앞의 값 또는 1과 1이 참인가 → OR로 연결돼있으니 무조건 TRUE인 1=1때문에 TRUE문 됨
            
        2. AND문 전에 넣기 `' OR 1=1--` (AND가 OR보다 우선순위 높음)
            
            SELECT * FROM USER WHERE ID = ‘`' OR 1=1--`' AND PASSWORD = ‘1234’;
            
            WHERE절을 닫아주는 싱글 쿼터와, OR 1=1이라는 TRUE문과, --를 이용해 뒤의 구문을 모두 없는 것으로 만들어주는 주석문으로 구성
            
        
        = SELECT * FROM USER
        
        USER 테이블의 모든 정보 조회 가능
        

### 2) 새로운 데이터베이스 명령문 실행

- 정상적인 게시글 조회 요청 수행 과정
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bb7bae14-2e1e-451c-85da-699153f08c67/Untitled.png)
    
- SQL Injection을 통한 악의적 명령 실행
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/581072a0-4692-4534-b477-7f873741813d/Untitled.png)
    
- 콜론(;)을 이용해 다른 쿼리문 함께 입력
    - 콜론으로 명령어 연결해 한 줄로 된 두 개 이상의 명령어 연속 기입 가능
        
        ‘ ; DELETE * USER FROM ID = ‘1’;
        
        SELECT * FROM USER WHERE ID = ‘`'; DELETE * USER FROM ID = ‘1’`’ AND PASSWORD = ‘1234’;
        
    
    ⇒ 보안이 완벽하지 않으면, 이처럼 비밀번호와 아이디가 일치해서 True가 되고 뒤에 작성한 DELETE 문도 데이터베이스에 영향을 줄 수도 있게 되는 치명적인 상황
    
    시스템 명령어를 실행 가능하면 해당 서버의 모든 자원에 접근, 데이터 유출 및 삭제 가능
    

### 3) 데이터 조작 및 유출

시스템에서 발생하는 에러 메시지를 이용해 공격하는 방법. 

e.g.) 해커는 **GET 방식으로 동작하는 URL의 쿼리 스트링을 추가해 에러를 발생**시킴. 이에 해당하는 오류가 발생하면, 해당 웹앱의 데이터베이스 구조를 유추 가능해 해킹에 활용

---

## **방어 방법**

### **1) 입력 값 검증**

- 화이트 리스트 방식: 입력된 값이 개발자가 의도한 값(유효값) 인지 검증. 지정된 문자만 허용 → 블랙 리스트 방식보다 보안에 좋음
- 블랙 리스트 방식: HTTP 요청을 통해 전달되는 사용자 데이터에 SQL 구문으로 해석될 수 있는 문자 또는 공격에 사용되는 SQL 구문들의 포함 여부를 검사, 포함시 요청을 차단하거나 해당 문자를 제거(또는 다른 문자로 대체)
    - SQL 기호: , –, ‘, “, ?, #, (, ), ;, =, /* 등
    - SQL 구문: SELECT, INSERT, UPDATE, DELETE, UNION, GROUP BY, HAVING, ORDER BY 등

### **2) 에러 메시지 노출 금지**

- 원본 데이터베이스 테이블에 접근 권한을 높여 일반 사용자는 view로만 접근하여 에러를 볼 수 없도록 만듦
- DB 에러 발생 시 에러가 발생한 쿼리문과 함께 에러 내용 반환 → 이때 테이블명, 컬럼명, 쿼리문 노출 가능성 있음 → 오류 발생시 사용자에게 보여줄 수 있는 페이지 제작하거나 메시지 박스 띄우도록 해야 함

### **3) 매개변수화된 쿼리(Prepared Statement) 사용하기**

Prepared Statement 구문: 외부 입력 값이 SQL 구문의 구조를 변경하지 못하게 정해진 구조로 처리. 사용자의 입력(?에 들어가는 데이터)을 문자열로 취급하여 공격 쿼리가 들어와도 단순 문자열로 인식되어 인젝션이 무효화됨. 

`INSERT INTO MyGuests VALUES(?, ?, ?)`

---

참고 링크

- [tech-interview-for-developer](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/SQL%20Injection.md)
- [https://m.mkexdev.net/427](https://m.mkexdev.net/427)
- [https://velog.io/@yanghl98/Database-SQL-Injection](https://velog.io/@yanghl98/Database-SQL-Injection)
- [https://noirstar.tistory.com/264](https://noirstar.tistory.com/264)
- [https://www.bugbountyclub.com/pentestgym/view/52](https://www.bugbountyclub.com/pentestgym/view/52)’