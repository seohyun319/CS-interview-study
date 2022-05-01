## TDD(Test Driven Development)
> 테스트 주도 개발

<br>

- 일반적인 개발 과정

<image src="https://user-images.githubusercontent.com/66426083/166142024-071efc32-da3c-4b3b-a8d2-5f8a2540daa6.png">

<br>

- TDD 개발 과정
 
  
<image src="https://user-images.githubusercontent.com/66426083/166142025-101322a7-b25e-4716-b50d-530371365424.png">
  
<br>
  
<image src="https://user-images.githubusercontent.com/66426083/166142365-2bbd3a5c-d976-43f3-abfd-4cfaf74a707a.png">

<br>

### 장점
- 작업과 동시에 테스트를 진행하면서 실시간으로 오류 파악이 가능함 (시스템 결함 방지)
- 짧은 개발 주기를 통해 고객의 요구사항 빠르게 수용 가능. 피드백이 가능하고 진행 상황 파악이 쉬움
- 자동화 도구를 이용한 TDD 테스트케이스를 단위 테스트로 사용이 가능함(자바는 JUnit, C와 C++은 CppUnit, Javascript는 Jest 등)

  
### 단점
- 기존 개발 프로세스에 테스트케이스 설계가 추가되므로 생산 비용 증가
- 테스트의 방향성, 프로젝트 성격에 따른 테스트 프레임워크 선택 등 추가로 고려할 부분의 증가
  

  <br>
  
- TDD를 활용하면, 처음 시작하는 단계에서 테스트케이스를 설계하기 위한 초기 비용이 확실히 더 들게 됨
  하지만 개발 과정에 있어서 '초기 비용'보다 '유지보수 비용'이 더 클 수 있음

- 안전성이 필요한 소프트웨어 프로젝트에서는 개발 초기 단계부터 확실하게 다져놓고 가는 것이 중요

-> 유지보수 비용이 더 크거나 비행기, 기차에 필요한 소프트웨어 등 안전성이 중요한 프로젝트의 경우 TDD를 활용한 개발 필요
  
  
  
<br>
  <br>
  <br>
  
참고 https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Software%20Engineering/TDD(Test%20Driven%20Development).md / https://velog.io/@ruthetum/node-tdd
