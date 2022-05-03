## Closure
> 자바스크립트에 없는 private 및 public 속성/메소드를 구현할 수 있는 방법

<br>

### 클로서 생성하기

1) 내부 함수가 익명 함수로 되어 외부 함수의 반환값으로 사용된다.
2) 내부 함수는 외부 함수의 실행 환경(execution environment)에서 실행된다.
3) 내부 함수에서 사용되는 변수 x 는 외부 함수의 변수 스코프에 있다.

<br>

ex1)
```javascript
var name = `Warning`;
function outer() {
  var name = `closure`;
  return function inner() {
    console.log(name);
  };
}

var callFunc = outer();
callFunc();
```

결과
```
closure
```

- callFunc가 클로저
- outer 함수의 지역변수로 존재하는 name 변수를 자유변수(free variable)라고 함


<br>
<br>

ex2)
```javascript
function makeAdder(x) {
  var y = 1;
  return function(z) {
    y = 100;
    return x + y + z;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);
//클로저에 x와 y의 환경이 저장됨

console.log(add5(2));  // 107 (x:5 + y:100 + z:2)
console.log(add10(2)); // 112 (x:10 + y:100 + z:2)
//함수 실행 시 클로저에 저장된 x, y값에 접근하여 값을 계산
```

- add5와 add10은 둘 다 클로저
- 같은 함수 본문 정의를 공유하지만 서로 다른 맥락적 환경(context)을 저장함
  > 함수 실행 시 add5의 맥락적 환경에서 클로저 내부의 x는 5 이지만 add10의 맥락적 환경에서 x는 10 

<br>

### Closure란?
- 외부 함수 호출이 종료되더라도 외부 함수의 지역 변수 및 변수 스코프 객체의 체인 관계를 유지할 수 있는 구조
- 외부 함수에 의해 반환되는 내부 함수


<br>
<br>
<br>

참고 https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/JavaScript#closure
