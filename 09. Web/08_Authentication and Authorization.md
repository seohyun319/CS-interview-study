## Authentication and Authorization
> Authentication: 로그인  
> Authorization : 권한  

### Authentication / 인증
- 로그인과 같이 사용자 또는 프로세스의 신원을 확인하는 프로세스
- 인증에 사용하기 위해 제공하는 데이터(자격 증명)는 이미 저장된 데이터와 비교함
- 이 데이터는 인증 서버에 저장되며, 가장 일반적인 인증 방법은 비밀번호를 사용하는 것
- 인증에서는 비밀번호 기반 인증, SSO, API 인증, Barcode 인증, 생체 인증 등이 있음
- 줄여서 AuthN이라고도 함

#### Authentication Techniques
- 비밀번호 기반 인증
- 비밀번호없는 인증
- 2FA(Two Factor Authentication) / MFA(Multi Factor Authentication)
- Single Sign On
- Social Authentication
- API Authentication
- API Key / Token
- 생체인증

-------

### Authorization / 권한부여
- 권한부여는 누가 무엇을 할 수 있는지 결정하는 규칙
- 파일, 데이터 등과 같은 시스템 리소스에 대한 액세스 수준을 결정하는 데 사용되는 보안 메커니즘
- 예로 DBA는 데이터베이스 작성 및 삭제 권한이있는 반면 Software Engineer는 읽기 및 쓰기 권한만 주어짐
- 기본적으로 개인에게 조직의 기밀 리소스에 대한 부분 또는 전체 액세스 권한이 부여되는 프로세스
- 기술에는 역할 기반 액세스 제어, JSON 웹 토큰, SAML, OpenID 권한 부여, 0Auth 등이 있음
- 줄여서 AuthZ라고도 함

#### Authorization Techniques
- API keys
- HMAC (Hash-Based Message Authentication Code)
- JWT / JSON Web Token
- SAML / Security Assurance Markup Language
- OpenID
- OAuth

|항목|Authentication|Authorization|
|------|---|---|
|정의|사용자의 신원 확인|액세스 권한 확인|
|목적|자신이 누구인지 확인하도록 사용자를 확인|사용자에게 특정 리소스에 대한 액세스 권한이 있는지 확인|
|방법|사용자 이름, 망막 스캔, 얼굴 인식 등과 같은 요소를 통해 사용자를 식별|미리 지정된 규칙을 통해 리소스에 엑세스 할 수 있는 사용자의 권한을 확인|
|순서|AuthZ전에 수행|AuthN 후에 수행|




