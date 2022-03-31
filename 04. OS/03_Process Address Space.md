## **프로세스의 주소 공간**

> 프로그램이 CPU에 의해 실행됨 → 프로세스가 생성되고 메모리에 '**프로세스 주소 공간**'이 할당됨

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/39ce2158-1e96-455a-b99b-6904a8df8b29/Untitled.png)

- **코드(text) Segment** : 프로그램 소스 코드 저장.
- **데이터Data Segment** : 초기값 있는 전역 변수, 배열, 정적 변수 저장 (항상 접근 가능한 변수들 저장)
- **BSS**(Block Stated Symbol): 초기값 없는 전역변수(초기화 안 된 데이터), 배열, 정적 변수 저장
  > 변수 많아져도 초기값 저장 안 해도 돼서 프로그램의 실행코드 사이즈 안 늘어남
- **스택 Segment** : 함수, 지역 변수 저장.
  > 함수 안에서 공통으로 사용하는 변수/함수는 전역으로 따로 지정해주면 지역 변수로 일일이 하지 않아도 돼서 메모리 아낄 수 있음.
- **힙 Heap**: 클래스 등. 메모리 동적 할당.

<br />

- 구역 나눈 이유:
  - 최대한 데이터를 공유해 메모리 사용량 줄이기 위해
  - Code는 같은 프로그램 자체에서는 모두 같은 내용이기 때문에 따로 관리해 공유함
  - Stack과 데이터를 나눈 이유는, 스택 구조의 특성과 전역 변수의 활용성을 위한 것

<br />

---

참고 링크

- [https://dar0m.tistory.com/258[](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/Process%20Address%20Space.md)](https://dar0m.tistory.com/258)
- [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer Science/Operating System/Process Address Space.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/Process%20Address%20Space.md)
