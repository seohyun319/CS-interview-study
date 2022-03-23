# ****Blocking/Non-blocking & Synchronous/Asynchronous****

![image](https://user-images.githubusercontent.com/76686872/159624680-cfa21dac-8bcd-42da-ab3b-92128c781dbc.png)

# **Blocking/Non-blocking**

`호출된 함수`가 `호출한 함수`에게 제어권을 건네주는지(바로 리턴하는지)

함수 A, B가 있고, A 안에서 B를 호출했다고 가정 → 호출한 함수 A, 호출된 함수 B. B는 호출되었기에 일을 해야 함. (제어권이 B에게 주어짐)

- **Blocking** : 함수 B는 할 일을 다 마칠 때까지 제어권을 가지고 있음. A는 B가 다 마칠 때까지 기다려야. == 할 일 마치고 제어권 리턴
- **Non-blocking** : 함수 B는 할 일을 마치지 않았어도 A에게 제어권을 바로 넘겨줌(return). A은 B를 기다리면서도 다른 일을 진행 가능 == 일 시작할 때 바로 제어권 리턴

# **Synchronous/Asynchronous**

I/O 작업 상황(결과) 반환 방식

B의 수행 결과나 종료 상태를 A가 신경쓰고 있는지

- **Synchronous** : 함수 A는 함수 B가 일을 하는 걸 기다리면서, 현재 상태가 어떤지 계속 체크 
== 호출된 함수(B)를 호출한 함수(A)가 신경씀
- **Asynchronous** : 함수 B의 수행 상태를 B 혼자 직접 신경쓰면서 처리. (Callback)
== 호출된 함수(B)를 자기 스스로 신경씀
    
    호출한 함수 A는 호출된 함수 B에게 관심 없음. 다른 일 하다가 완료됐다는 알림인 Callback이 오면 그제서야 봄.
    
<br /><br />

## **Case Study : 대표님, 개발자 좀 더 뽑아주세요..**

### **1) Blocking & Synchronous**

- **Blocking** : 함수 B는 할 일을 다 마칠 때까지 제어권을 가지고 있음. A는 B가 다 마칠 때까지 기다려야. == 할 일 마치고 제어권 리턴
- **Synchronous** : 함수 A는 함수 B가 일을 하는 중에 기다리면서, 현재 상태가 어떤지 계속 체크 
== 호출된 함수(B)를 호출한 함수(A)가 신경씀

> 나 : 대표님, 개발자 좀 더 뽑아주세요..<br />
대표님 : 오케이, 잠깐만 거기 계세요!<br />
나 : …?!!<br />
대표님 : (채용 공고 등록.. 지원자 연락.. 면접 진행.. 연봉 협상..)<br />
나 : (과정 지켜봄.. 궁금함.. 어차피 내 일 하러는 못 가고 계속 서 있음)
> 

### **2) Blocking & Asynchronous**

- **Blocking** : 함수 B는 할 일을 다 마칠 때까지 제어권을 가지고 있음. A는 B가 다 마칠 때까지 기다려야. == 할 일 마치고 제어권 리턴
- **Asynchronous** : 함수 B의 수행 상태를 B 혼자 직접 신경쓰면서 처리. (Callback)
== 호출된 함수(B)를 자기 스스로 신경씀

> 나 : 대표님, 개발자 좀 더 뽑아주세요..<br />
대표님 : 오케이, 잠깐만 거기 계세요!<br />
나 : …?!!<br />
대표님 : (채용 공고 등록.. 지원자 연락.. 면접 진행.. 연봉 협상..)<br />
나 : (안 궁금함.. 지나가는 말로 여쭈었는데 붙잡혀버림.. 딴 생각.. 못 가고 계속 서 있음)
> 

### **3) Non-blocking & Synchronous**

- **Non-blocking** : 함수 B는 할 일을 마치지 않았어도 A에게 제어권을 바로 넘겨줌(return). A은 B를 기다리면서도 다른 일을 진행 가능 == 일 시작할 때 바로 제어권 리턴
- **Synchronous** : 함수 A는 함수 B가 일을 하는 중에 기다리면서, 현재 상태가 어떤지 계속 체크 
== 호출된 함수(B)를 호출한 함수(A)가 신경씀

> 나 : 대표님, 개발자 좀 더 뽑아주세요..<br />
대표님 : 알겠습니다. 가서 볼 일 보세요.<br />
나 : 넵!<br />
대표님 : (채용 공고 등록.. 지원자 연락.. 면접 진행.. 연봉 협상..)<br />
나 : 채용하셨나요?<br />
대표님 : 아직요.<br />
나 : 채용하셨나요?<br />
대표님 : 아직요.<br />
나 : 채용하셨나요?<br />
대표님 : 아직요~!!!!!!
> 

### **4) Non-blocking & Asynchronous**

- **Non-blocking** : 함수 B는 할 일을 마치지 않았어도 A에게 제어권을 바로 넘겨줌(return). A은 B를 기다리면서도 다른 일을 진행 가능 == 일 시작할 때 바로 제어권 리턴
- **Asynchronous** : 함수 B의 수행 상태를 B 혼자 직접 신경쓰면서 처리. (Callback)
== 호출된 함수(B)를 자기 스스로 신경씀

> 나 : 대표님, 개발자 좀 더 뽑아주세요..<br />
대표님 : 알겠습니다. 가서 볼 일 보세요.<br />
나 : 넵!<br />
대표님 : (채용 공고 등록.. 지원자 연락.. 면접 진행.. 연봉 협상..)<br />
나 : (열일중..)<br />
대표님 : 한 분 모시기로 했습니다~!<br />
나 : 😍
> 

<br /><br />

참고링크

- [https://musma.github.io/2019/04/17/blocking-and-synchronous.html](https://musma.github.io/2019/04/17/blocking-and-synchronous.html)
- [https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer Science/Network/[Network] Blocking%2CNon-blocking %26 Synchronous%2CAsynchronous.md](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/%5BNetwork%5D%20Blocking%2CNon-blocking%20%26%20Synchronous%2CAsynchronous.md)
