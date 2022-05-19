## REST API

> 자원(RESOURCE) - URI / 행위(Verb) - HTTP METHOD / 표현(Representations) 으로 이루어진 웹 (HTTP) 의 장점을 활용한 아키텍쳐
<p align="center"><img src="https://image.toast.com/aaaadh/alpha/2016/techblog/uADF8uB9BC1.png" width="400" /></p>

<br>

### REST의 개념
HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.
<br>
- CRUD Operation
  - Create : 생성(POST)
  - Read : 조회(GET)
  - Update : 수정(PUT)
  - Delete : 삭제(DELETE)
  - HEAD: header 정보 조회(HEAD)

<br>

### REST의 요소
  * 자원(RESOURCE) - URI
  
    http://myweb/users와 같은 URI
    모든 것을 Resource (명사)로 표현하고, 세부 Resource에는 id를 붙임

  * 행위(Verb) - HTTP METHOD

    | Method | 의미   | 역할 |
    | ------ | ------ |  ---------- | 
    | POST   | Create | POST를 통해 해당 URI를 요청하면 리소스를 생성한다.|
    | GET    | Select | GET를 통해 해당 리소스를 조회한다. 리소스를 조회하고 해당 도큐먼트에 대한 자세한 정보를 가져온다.|
    | PUT    | Update | PUT를 통해 해당 리소스를 수정한다.|
    | DELETE | Delete | DELETE를 통해 리소스를 삭제한다.|
    
  * 표현(Representations)
  
    - 메시지 포맷이 존재

      : JSON, XML 과 같은 형태가 있음 (최근에는 JSON 을 씀)
      ```text
      HTTP POST, http://myweb/users/
      {
      	"users" : {
      		"name" : "terry"
      	}
      }
      ```


<br>

### REST의 특징

  1. Server-Client(서버-클라이언트 구조)
    
     자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 된다.
      - REST Server: API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.
      - Client: 사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임진다.
     서로 간 의존성이 줄어든다.

  2. Stateless(무상태)
     
     서버는 클라이언트에 대한 사전 정보나 클라이언트의 상태를 저장하지 않는다. 다르게 말하면, 서비스의 클라이언트가 동작하는 과정에서 생기는 상태 변화에 대해 서버는 관여하지 않고 오로지 클라이언트단에서 감당하게 된다. 그렇기 때문에 요청은 반드시 서버가 해당 요청을 처리하기 위해 필요로 하는 모든 정보를 함께 전송해야 한다.
     
     Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.
      - 각 API 서버는 Client의 요청만을 단순 처리한다.
      - 즉, 이전 요청이 다음 요청의 처리에 연관되어서는 안된다.
      - 물론 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용한다.
      - Server의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아진다.

  3. Cacheable(캐시 처리 가능)
     
     응답과 요청이 모두 캐싱 처리가 가능한지 아닌지 명시가 필요하다. 캐싱이 가능한 데이터라면 클라이언트 차원에서 캐시에 저장해두고 이후에 같은 요청에 대해선 해당 데이터를 꺼내올 수 있게 된다.
     
     대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.
     
     캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있다.

  4. Layered System(계층화)
  
     서버도 응답을 주기 다른 서버와 통신할 수도 있지만 클라이언트 입장에선 철저하게 분리되어 있기 때문에 직접적으로 바로 연결된 쪽(REST Server)과의 연결만 신경 써주면 된다.
     
     REST Server는 다중 계층으로 구성될 수 있다.
      - API Server는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있다.
      - 또한 로드밸런싱, 공유 캐시 등을 통해 확장성과 보안성을 향상시킬 수 있다.

   
   5. Code-On-Demand(optional)
    
      서버는 applet이나 스크립트 등을 전송하여 클라이언트의 기능을 확장하거나 변화(커스터마이즈)를 줄 수 있다.
      Server로부터 스크립트를 받아서 Client에서 실행한다.
      반드시 충족할 필요는 없다.

  6. Uniform Interface(인터페이스 일관성)
    
     URI로 지정한 Resource에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다.
     HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
      - 특정 언어나 기술에 종속되지 않는다.
   
<br>

### REST API 디자인 가이드
REST API 설계 시 가장 중요한 항목은 다음의 2가지로 요약할 수 있다.

첫 번째, URI는 정보의 자원을 표현해야 한다.
두 번째, 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.

  1. URI는 정보의 자원을 표현해야 한다.
     1. resource는 동사보다는 명사를, 대문자보다는 소문자를 사용한다.
     2. resource의 도큐먼트 이름으로는 단수 명사를 사용해야 한다.
     3. resource의 컬렉션 이름으로는 복수 명사를 사용해야 한다.
     4. resource의 스토어 이름으로는 복수 명사를 사용해야 한다.
        > Ex) GET /Membering/1 -> GET /members/1
     
  2. 자원에 대한 행위는 HTTP Method(GET, PUT, POST, DELETE 등)로 표현한다.
     1. URI에 HTTP Method가 들어가면 안된다.
       > Ex) GET /members/delete/1 -> DELETE /members/1
     2. URI에 행위에 대한 동사 표현이 들어가면 안된다.(즉, CRUD 기능을 나타내는 것은 URI에 사용하지 않는다.)
       > Ex) GET /members/show/1 -> GET /members/1
       > 
       > Ex) GET /members/insert/2 -> POST /members/2

     3. 경로 부분 중 변하는 부분은 유일한 값으로 대체한다.(즉, :id는 하나의 특정 resource를 나타내는 고유값이다.)
       > Ex) student를 생성하는 route: POST /students
       > 
       > Ex) id=12인 student를 삭제하는 route: DELETE /students/12
