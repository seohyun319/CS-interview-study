# CSRF

> 사이트 간 요청 위조
(CSRF; Cross-Site Request Forgery)
> 

![img](https://user-images.githubusercontent.com/61955796/169044026-590b1a1a-39ff-4961-8a1a-b8037996dce1.png)

<br>

**⏩ 개념**

- 웹 어플리케이션 취약점 중 하나
- 인터넷 사용자가 자신의 의지와는 무관하게 공격자가 의도한 행위 (modify, delete, register 등)를 특정한 웹사이트에 request하도록 만드는 공격
- 주로 해커들이 많이 이용하는 것으로, 유저의 권한을 도용해 중요한 기능을 실행하도록 함
- 예시) 해커가 사용자의 SNS 계정으로 광고성 글을 올리는 것
- 공격이 실행되는 조건
    1. 사용자가 해커가 만든 피싱 사이트에 접속한 경우
    2. 위조 요청을 전송하는 서비스에 사용자가 로그인을 한 상황
- 자동 로그인을 해둔 경우에 이런 피싱 사이트에 접속하게 되면서 피해를 입는 경우가 많고 해커가 XSS 공격을 성공시킨 사이트라면, 피싱 사이트가 아니더라도 CSRF 공격이 이루어질 가능성 O

<br>

**⏩ 공격 방식**

1. 공격자는 CSRF 스크립트가 포함된 게시물을 등록한다.
2. 사용자는 CSRF 스크립트가 포함된 페이지의 게시물 열람을 요청한다.
3. 게시물을 읽은 사용자의 권한으로 공격자가 원하는 요청이 발생한다.
4. 공격자가 원하는 CSRF 스크립트 결과가 발생한다.

<br>

**⏩ 대응 방식**

- **리퍼러(Refferer) 검증**
    
    백엔드 단에서 Refferer 검증을 통해 승인된 도메인으로 요청 시에만 처리하도록 한다.
    
- **Security Token 사용**
    
    사용자의 세션에 임의의 난수 값을 저장하고, 사용자의 요청시 해당 값을 포함하여 전송시킨다. 
    
    백엔드에서는 요청을 받을 때 세션에 저장된 토큰값과 요청 파라미터로 전달받는 토큰 값이 일치하는지 검증한다. 
    
    즉, 세션별로 CSRF 토큰을 사용하여 점검하는 것이다.
    
- **POST 방식 사용**
    
    입력화면 폼 작성 시에 GET 방식보다 POST 방식을 사용한다.
    

---

# XSS

> Cross Site Scription
> 

![img](https://user-images.githubusercontent.com/61955796/169044066-83921578-a9e1-47bb-b49c-b6d135f97043.gif)

**⏩ 개념**

- CSRF와 같은 웹 어플리케이션 취약점 중 하나
- 관리자가 아닌 권한이 없는 사용자가 웹 사이트에 스크립트를 삽입하는 공격 기법
- 악의적으로 스크립트를 삽입하여 이를 열람한 사용자의 쿠키가 해커에게 전송되며 탈취된 쿠키를 통해 세션 하이재킹 공격이 이루어짐
    
    *세션 하이재킹: 공격자의 인증 작업이 완료되어 정상 통신을 하고 있는 다른 사용자의 세션을 가로채서 별도의 인증 작업 없이 가로챈 세션으로 통신을 계속하는 행위
    
- 해커는 세션ID를 가진 쿠키로 사용자의 계정에 로그인 가능

<br>

**⏩ 공격 종류**

- **Stored XSS**
    
    말 그대로 **지속적으로 피해를 입히는 유형**이다.
    
    XSS 취약점이 존재하는 웹 어플리케이션에 악성 스크립트를 삽입하여, 열람한 사용자의 쿠키를 탈취하거나 리다이렉션 시키는 공격을 한다. 
    
    즉, 사용자가 **페이지를 열람함과 동시에 악성 스크립트가 브라우저에서 실행되면서 감염**된다. 
    
- **Reflected XSS**
    
    사용자에게 **입력 받은 값을 서버에서 되돌려 주는 곳**에서 발생한다. 
    
    공격자는 악의적인 스크립트와 함께 URL을 사용자에게 누르도록 유도하고, 누른 사용자는 이 스크립트가 실행되어 공격을 당하게 되는 유형이다.
    
    예를 들어, 공격용 악성 URL을 생성한 후 이메일로 사용자에게 전송하면 사용자가 URL 클릭시 즉시 **공격 스크립트가 피해자로 반사**되어 민감 정보를 공격자에게 전송하는 기법이라고 할 수 있다. 
    
- **DOM 기반 (Document Object Model XSS)**
    
    악성 스크립트가 포함된 URL을 사용자가 요청할 때 브라우저를 해석하는 단계에서 발생하는 공격이다. 
    
    이 스크립트로 인해 클라이언트 측 코드가 원래 의도와 다르게 실행된다. 이는 다른 XSS 공격과는 달리 서버 측에서 탐지가 어렵다.
    
    즉, 조작된 URL을 피해자가 클릭하면 공격을 당한다고 말할 수 있다.
    
<br>

**⏩ 공격 방식**

1. 임의의 XSS 취약점이 존재하는 서버에 XSS 코드를 작성하여 삽입 저장
2. 해당 웹 서비스 사용자가 공격자가 작성해 놓은 XSS 코드에 접근
3. 사용자가 XSS 코드가 저장된 페이지에 정보를 요청
4. 사용자의 시스템에서 XSS 코드 실행
5. XSS 코드가 실행된 결과가 공격자에게 전달되고 공격자는 결과를 가지고 웹 서버에서 2차 해킹 시도

<br>

**⏩ 대응 방식**

- **입출력 값 검증**
    
    XSS Cheat Sheet에 대한 필터 목록을 만들어 모든 Cheat Sheet에 대한 대응을 가능하도록 사전에 대비한다. 
    
    XSS 필터링을 적용 후 스크립트가 실행되는지 직접 테스트 해볼 수도 있다.
    
- **XSS 방어 라이브러리, 확장앱 사용**
    
    Anti XSS 라이브러리를 제공해주는 회사들이 많다. 
    
    사용자들은 각자의 브라우저에서 악성 스크립트가 실행되지 않도록 확장앱을 설치하여 방어할 수 있다.
    
- **웹 방화벽**
    
    웹 방화벽은 웹 공격에 특화된 것으로, 다양한 Injection을 한꺼번에 방어할 수 있는 장점이 있다.
    
- **CORS, SOP 설정**
    
    CORS(Cross-Origin Resource Sharing), SOP(Same-Origin-Policy)를 통해 리소스의 Source를 제한하는 것이 효과적인 방어 방법이 될 수 있다. 
    
    > **CORS: 교차 출처 리소스 공유 정책; 자원을 공유해야 하는 브라우저와 서버 간의 안전한 교차 출처 요청 및 데이터 전송을 지원하는 정책
    
    *SOP: 동일 출처 정책; 하나의 출처(Origin)에서 로드된 자원(문서나 스크립트)이 호스트나 프로토콜, 포트번호가 일치하지 않는 자원과 상호작용 하지 못하도록 요청 발생을 제한하는 정책*
    > 
    
    웹 서비스상 취약한 벡터에 공격 스크립트를 삽입할 경우, 치명적인 공격을 하기 위해 스크립트를 작성하면 입력값 제한이나 기타 요인 때문에 공격 성공이 어렵다. 
    
    그러나 공격자의 서버에 위치한 스크립트를 불러 올 수 있다면 이는 상대적으로 쉬워진다. 
    
    따라서 CORS, SOP를 활용 하여 사전에 지정된 도메인이나 범위가 아니라면 리소스를 가져올 수 없게 제한해야 한다.
    
<br>

**⏩ CSRF와 XSS의 차이점**

|  |  CSRF | XSS |
| --- | --- | --- |
| 공격 대상 | Server | Client |
| 공격 기법 | 요청을 위조하여 사용자 권한 이용 | 사이트 위조, 백도어 |

<br>

**⏩ 참고**

[https://velog.io/@jesop/SOP와-CORS](https://velog.io/@jesop/SOP%EC%99%80-CORS)

[https://program-developer.tistory.com/99](https://program-developer.tistory.com/99)
