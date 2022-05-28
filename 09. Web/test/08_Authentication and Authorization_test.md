5. Refresh Token 과 Access Token의 차이를 서술하시오.  

- 보통 Resource Server는 Access Token을 발급할 때 Refresh Token을 함께 발급한다.
- Client는 두 Token을 모두 저장해두고, Resource Server의 API를 호출할 때는 Access Token을 사용한다.
- Access Token이 만료되어 401 에러가 발생하면, Client는 보관 중이던 Refresh Token을 보내 새로운 Access Token을 발급받게 된다.
