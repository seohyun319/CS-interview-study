## OAuth

> Open Authentification

인터넷 사용자들이 비밀번호를 제공하지 않고, 다른 웹사이트 상의 자신들의 정보에 대해 웹사이트나 애플리케이션의 접근 권한을 부여할 수있는 개방형 표준 방법

<br>

이러한 매커니즘은 구글, 페이스북, 트위터 등이 사용하고 있으며 타사 애플리케이션 및 웹사이트의 계정에 대한 정보를 공유할 수 있도록 허용해준다.  
ex) 외부 웹 어플리케이션에 Google로 로그인하면 API를 통해 연동된 계정의 Google Calendar 정보를 가져와 사용자에게 보여줄 수 있다.  

<br>
<img width="704" alt="스크린샷 2022-05-19 오전 3 54 59" src="https://user-images.githubusercontent.com/65678579/169130452-776f4d1b-1dfb-4149-9d93-aaa0b8e95420.png">

위 사진을 예시로 살펴보자. 외부 어플리케이션(원티드)은 사용자 인증을 위해 Facebook과 Apple 및 Google의 등의 사용자 인증 방식을 사용한다.  
이 때, OAuth를 바탕으로 제 3자 서비스(원티드)는 외부 서비스(Facebook, Apple, Google)의 특정 자원을 접근 및 사용할 수 있는 권한을 인가받게 된다.  

<br>

## 사용 용어

- **사용자** : 계정을 가지고 있는 개인
- **소비자** : OAuth를 사용해 서비스 제공자에게 접근하는 웹사이트 or 애플리케이션
- **서비스 제공자** : OAuth를 통해 접근을 지원하는 웹 애플리케이션
- **소비자 비밀번호** : 서비스 제공자에서 소비자가 자신임을 인증하기 위한 키
- **요청 토큰** : 소비자가 사용자에게 접근권한을 인증받기 위해 필요한 정보가 담겨있음
- **접근 토큰** : 인증 후에 사용자가 서비스 제공자가 아닌 소비자를 통해 보호 자원에 접근하기 위한 키 값

<br>

## OAuth 참여자

OAuth 동작에 관여하는 참여자는 크게 세 가지로 구분할 수 있다.

- Resource Server : Client가 제어하고자 하는 자원을 보유하고 있는 서버 (서비스 제공자)
  - Facebook, Google, Twitter 등이 이에 속함.  
- Resource Owner : 자원의 소유자 (사용자)
  -Client가 제공하는 서비스를 통해 로그인하는 실제 유저가 이에 속함.
- Client : Resoure Server에 접속해서 정보를 가져오고자 하는 클라이언트(웹 어플리케이션)임. (소비자)

토큰 종류로는 Access Token과 Refresh Token이 있다.

Access Token은 만료시간이 있고 끝나면 다시 요청해야 한다. Refresh Token은 만료되면 아예 처음부터 진행해야 한다. 

<br>

## OAuth Flow (인증 과정)

> 소비자 <-> 서비스 제공자

1. 소비자가 서비스 제공자에게 요청토큰을 요청한다.
2. 서비스 제공자가 소비자에게 요청토큰을 발급해준다.
3. 소비자가 사용자를 서비스제공자로 이동시킨다. 여기서 사용자 인증이 수행된다.
4. 서비스 제공자가 사용자를 소비자로 이동시킨다.
5. 소비자가 접근토큰을 요청한다.
6. 서비스제공자가 접근토큰을 발급한다.
7. 발급된 접근토큰을 이용해서 소비자에서 사용자 정보에 접근한다.

<br>

예시를 통해 조금 더 자세히 살펴보자.

Github 계정을 바탕으로 웹 어플리케이션에서 로그인하고, Github에서 제공하는 여러 API 기능을 외부 웹 어플리케이션에서 사용해보자.

### 1. Client 등록
- Client(웹 어플리케이션)가 Resource Server(서비스 제공자)를 이용하기 위해서는 자신의 서비스를 등록함으로써 사전 승인을 받아야 한다.
- Github Developer Settings에서 Github에 웹 어플리케이션을 등록한다.
<img width="700" alt="스크린샷 2022-05-19 오전 4 09 16" src="https://user-images.githubusercontent.com/65678579/169137683-b6e1a2de-3fd0-4504-be06-4e9200149f65.png">
<img width="698" alt="스크린샷 2022-05-19 오전 4 09 32" src="https://user-images.githubusercontent.com/65678579/169137728-cedf5a5e-7d41-4eb9-9313-b39898d8c254.png">

등록 절차를 마치고 나면 세 가지 정보를 부여 받는다.

- Client ID : 클라이언트 웹 어플리케이션을 구별할 수 있는 식별자이며, 노출이 무방함.  
- Client Secret : Client ID에 대한 비밀키로서, 절대 노출해서는 안 됨.  
- Authorized redirect URL : Authorization Code를 전달받을 리다이렉트 주소.  

Google 등 외부 서비스를 통해 인증을 마치면 클라이언트를 명시된 주소로 리다이렉트 시키는데, 이 때 Query String으로 특별한 Code가 함께 전달된다.  
클라이언트는 해당 Code와 Client ID 및 Client Secret을 Resource Server에 보내, Resource Server의 자원을 사용할 수 있는 Access Token을 발급 받는다.   
등록되지 않은 리다이렉트 URL을 사용하는 경우, Resource Server가 인증을 거부한다.  

### 2. Resource Owner의 승인
Github Docs에서는 Github 소셜 로그인을 하기 위해 다음과 같은 주소로 GET 요청과 필요한 파라미터들을 보내도록 명시한다.

`GET https://github.com/login/oauth/authorize?client_id={client_id}&redirect_uri={redirect_uri}?scope={scope}  `
- scope는 Client가 Resource Server로부터 인가받을 권한의 범위이며, 파라미터의 세부 옵션에 대한 내용은 문서를 참고하기 바란다.  

Resource Owner(사용자)는 Client의 웹 어플리케이션을 이용하다가, 해당 주소로 연결되는 소셜 로그인 버튼을 클릭한다.
<img width="509" alt="스크린샷 2022-05-19 오전 4 13 48" src="https://user-images.githubusercontent.com/65678579/169138405-e503643e-0551-4832-b5a9-f757467fba49.png">

Resource Owner(사용자)는 Resource Server(서비스 제공자)에 접속하여 로그인을 수행한다.  
로그인이 완료되면 Resource Server(서비스 제공자)는 Query String으로 넘어온 파라미터들을 통해 Client를 검사함.

- 파라미터로 전달된 Client ID와 동일한 ID 값이 존재하는지 확인.
- 해당 Client ID에 해당하는 Redirect URL이 파라미터로 전달된 Redirect URL과 같은지 확인.
<img width="650" alt="스크린샷 2022-05-19 오전 4 20 41" src="https://user-images.githubusercontent.com/65678579/169139566-ed84ecdf-fd3e-4a47-bb57-4b846e6d099e.png">

검증이 마무리 되면 Resource Server는 Resource Owner에게 다음과 같은 질의를 보낸다.

- 명시한 scope에 해당하는 권한을 Client에게 정말로 부여할 것인가?
- 허용한다면 최종적으로 Resource Owner가 Resource Server에게 Client의 접근을 승인하게 된다.  

### 3.  Resource Server의 승인

Resource Owner(사용자)의 승인이 마무리 되면 명시된 Redirect URL로 클라이언트를 리다이렉트 시킨다.  
이 때 Resource Server(서비스 제공자)는 Client(웹 애플리케이션)가 자신의 자원을 사용할 수 있는 Access Token을 발급하기 전에, 임시 암호인 Authorization Code를 함께 발급한다.  
<img width="713" alt="스크린샷 2022-05-19 오전 4 24 41" src="https://user-images.githubusercontent.com/65678579/169140160-a9384cd5-a9ac-47a3-8eac-d94596588337.png">

- Query String으로 들어온 코드가 바로 Authorization Code이다.

> OAuthController.java
```java
@GetMapping("/afterlogin")
public ResponseEntity<String> afterlogin(@RequestParam String code) {
    if (Objects.isNull(code)) {
        throw new IllegalStateException("Github 로그인이 실패했습니다.");
    }
    RestTemplate restTemplate = new RestTemplate();
    OauthDto oauthDto = new OauthDto();
    oauthDto.setCode(code);
    oauthDto.setClient_ID("7e930566ecaa306c71b5");
    oauthDto.setClient_secret("client secret 입력");
    String accessToken = restTemplate.postForObject("https://github.com/login/oauth/access_token", oauthDto, String.class);
    return ResponseEntity.ok(accessToken);
}
```
- Client(웹 애플리케이션)는 ID와 비밀키 및 code를 Resource Owner(사용자)를 거치지 않고 Resource Server(서비스 제공자)에 직접 전달한다. 
- Resource Server(서비스 제공자)는 정보를 검사한 다음, 유효한 요청이라면 Access Token을 발급하게 된다.
- Client는 해당 토큰을 서버에 저장해두고, Resource Server의 자원을 사용하기 위한 API 호출시 해당 토큰을 헤더에 담아 보낸다.

### 4. API 호출
<img width="697" alt="스크린샷 2022-05-19 오전 4 31 22" src="https://user-images.githubusercontent.com/65678579/169141168-20078d7d-bee0-4358-929b-31d3575d815f.png">

이후 Access Token을 헤더에 담아 Github API를 호출하면, 해당 계정과 연동된 Resource Server의 풍부한 자원 및 기능들을 내가 만든 웹 어플리케이션에서 사용할 수 있다.

### 5. Refresh Token
> Refresh Token의 발급 여부와 방법 및 갱신 주기 등은 OAuth를 제공하는 Resource Server마다 상이함.
> Access Token은 만료 기간이 있으며, 만료된 Access Token으로 API를 요청하면 401 에러가 발생. 
> Access Token이 만료되어 재발급받을 때마다 서비스 이용자가 재 로그인하는 것은 다소 번거롭다.

- 보통 Resource Server는 Access Token을 발급할 때 Refresh Token을 함께 발급한다. 
- Client는 두 Token을 모두 저장해두고, Resource Server의 API를 호출할 때는 Access Token을 사용한다. 
- Access Token이 만료되어 401 에러가 발생하면, Client는 보관 중이던 Refresh Token을 보내 새로운 Access Token을 발급받게 된다.





### 참고
----
[📎](https://tecoble.techcourse.co.kr/post/2021-07-10-understanding-oauth/)
