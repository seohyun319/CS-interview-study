## JWT(JSON Web Token)
> 선택적 서명 및 선택적 암호화를 사용하여 데이터를 만들기 위한 인터넷 표준

<br>

### 구성 요소
- . 을 구분자로 3가지의 문자열로 구성
- aaaa.bbbbb.ccccc 의 구조 -> 헤더(header), 정보(payload), 서명(signature)

<br>

#### 1) 헤더(Header)
  - typ: 토큰의 타입 지정
  - alg: 해싱 알고리즘 지정 
    - 기본적으로 HMAC, SHA256, RSA 사용

<br>

#### 2) 정보(payload)
  - 클레임(claim): 정보의 한 조각 (key-value의 쌍으로 이루어져 있음)
    - iss (issuer): 토큰 발급자
    - sub (subject): 토큰 제목
    - aud (audience): 토큰 대상자
    - exp (expiration): 토큰 만료 시간
    - nbf (Not before): 토큰 활성 날짜 (이 날짜가 지나기 전까지 토큰 처리X)
    - iat (issued at): 토큰 발급 시간 (토큰의 age 판단 가능)
    - jti: JWT의 도유 식별자 (일회용 토큰에 사용 시 유용)
    
  - 공개 클레임(public claim)
    - 충돌 방지된(collision-resistant) 이름을 가지고 있어야 함.
    - 클레임 이름: URI 형식
      ```
      {
        "https://chup.tistory.com/jwt_claims/is_admin" : true
      }
      ```
      
   - 비공개 클레임(private claim)
      - 서버와 클라이언트간 합의 하에 사용되는 클레임 이름들
      - 이름이 중복되어 충돌이 될 수 있어 유의해야 함
  
  <br>
  
  <img width="690" alt="image" src="https://user-images.githubusercontent.com/66426083/168664385-13d28020-2a23-44f7-a8af-e08cc72205c2.png">

  - 헤더와 정보는 json이 디코딩되어있을 뿐 암호화되어있지 않기 때문에 쉽게 인코딩 가능(jwt.io)
  - payload에 민감한 정보를 담지 않는 게 중요

<br>

#### 3) 서명(signature)
- 생성 방법: 헤더의 인코딩 값과 정보의 인코딩 값을 합친 후 주어진 비밀키로 해시
- base64 형태로 나타냄
  
  <img width="550" alt="image" src="https://user-images.githubusercontent.com/66426083/168663874-1115284c-e538-4d60-a65f-f016c99ce011.png">
 
 - 서버가 가지고 있는 개인키로 암호화되어있는 상태 -> 다른 클라이언트가 임의로 서명을 복호화할 수 없음


<br>

#### 인증 방법
1) 클라이언트가 서버로 JWT 토큰을 요청과 동시에 전달
2) 서버가 가지고 있는 개인키로 서명을 복호화한 다음 base64URlEncode(header)가 JWT의 헤더 값과 일치하는지, base64URlEncode(payload)와 일치하는지 확인하여 일치한다면 인증 허용

<br>

---

<br>

### 로그인 인증 시 JWT 사용
- 유효기간이 짧은 토큰 -> 로그인을 자주 해야 함
- 유효기간이 긴 토큰 -> 보안에 취약
- Refresh Token: Access Token의 유효기간이 만료되었을 때 Refresh Token이 새로 발급해주는 열쇠가 됨
  > ex) Refresh Token의 유효기간은 1주, Access Token의 유효기간은 1시간 -> 사용자는 Access Token으로 1시간동안 API요청을 하다가 시간이 만료되면 Refresh Token을 이용하여 새롭게 발급(1시간 동안 토큰을 탈취당할 가능성이 적다는 점을 이용) -> Refresh Token도 유효기간 만료 -> 새로 로그인


<image src="https://user-images.githubusercontent.com/66426083/168662434-9d5950ba-5c6c-44da-8759-633a69b38d0e.png">

<br>

---

<br>

### 장점
  
- 이미 토큰 자체가 인증된 정보이기 때문에 세션 저장소와 같은 별도의 인증 저장소가 필수적으로 필요하지 않음
- 세션과는 다르게 클라이언트의 상태를 서버가 저장해 두지 않아도 됨
- signature를 공통 키 개인키 암호화를 통해 막아두었기 때문에 데이터에 대한 보완성이 늘어남
- 다른 서비스에 이용할 수 있는 공통적인 스펙으로써 사용할 수 있음

  > stateful 해야 하는 세션의 단점을 보완하기 위해 만들어진 JWT는 별도의 세션 저장소를 강제하지 않기 때문에 stateless 하여 확장성이 뛰어나고, signature를 통한 보안성까지 갖추고 있다.
  
<br>
<br>
<br>

참고 https://github.com/gyoogle/tech-interview-for-developer/blob/master/Web/JWT(JSON%20Web%20Token).md / https://brunch.co.kr/@jinyoungchoi95/1
