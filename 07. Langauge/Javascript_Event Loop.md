## Javascript Event Loop

<br>

### Javascript Engine
> Javascript로 작성된 코드를 해석하고 실행하는 인터프리터
- 최근에는 Node.js가 등장하면서 V8 엔진이 이용됨
- 싱글 스레드 기반으로 동작함

<img width="615" alt="image" src="https://user-images.githubusercontent.com/66426083/166441969-e120cf5f-3281-44ef-8260-4e6a1836a2c6.png">

- Call Stack, Task Queue, Heap 으로 구성
- Event Loop: Task Queue에 들어가는 task들 관리

<br>

#### Call Stack
- 자바스크립트는 단 하나의 호출 스택(call stack) 사용 -> Run to Completion(하나의 함수가 실행되면 끝날 때까지 다른 task 수행 불가)
- 요청을 순차적으로 호출 스택에 담아 처리하는 방식

<br>

#### Heap
- 동적으로 생성된 객체는 힙에 할당됨
- 구조화되지 않은 더미같은 메모리 영역을 heap이라 표현

<br>

#### Task Queue(Event Queue, Callback Queue)
- 처리해야 하는 태스크들을 임시 저장하는 대기 큐
- Call Stack이 비었을 때 먼저 대기열에 들어온 순서대로 수행
- 자바스크립트에서 비동기로 호출되는 함수들은 Call Stack에 쌓이지 않고 Task Queue에 enqueue됨
  - 이벤트에 의해 실행되는 함수(Handler)들
  - 자바스크립트 엔진이 아닌 Web API 영역에 따로 정의되어 있는 함수들(ex. setTimeout 등)

<br>

#### Event Loop
- 현재 실행 중인 태스크가 있는지, 태스크 큐에 태스크가 있는지 반복적으로 확인
- 태스크 큐에 처리해야 할 이벤트가 존재하면 해당 이벤트를 꺼내 Call Stack에 넣어서 처리
- 이벤트 큐에서 대기하고 있는 이벤크들은 한 번에 하나씩 Call Stack으로 호출되어 처리됨

<br>
<br>

ex)
```javascript
function test1() {
    console.log("test1");
    test2();
}

function test2() {
    let timer = setTimeout(function() {
        console.log("test2");
    }, 0);
    test3();
}

function test3() {
    console.log("test3");
}

test1();
```

결과
```
test1
test3
test2
```

<br>
<br>
<br>

참고 https://sculove.github.io/post/javascriptflow/ / https://asfirstalways.tistory.com/362
