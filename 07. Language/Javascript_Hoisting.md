## Hoisting

### 정의

**hoist**:

- 끌어올리다
- var keyword 로 선언된 모든 변수는 범위에 따라 `선언`과 `할당`으로 분리

  - 변수가 함수 내에서 정의되었을 경우, 선언이 함수의 최상위로 변경
  - 변수가 함수 바깥에서 정의되었을 경우, 전역 컨텍스트의 최상위로 변경

- **선언(Declaration)**과 **할당(Assignment)**

  - 선언문 - 자바스크립트 엔진 구동 시 가장 최우선으로 해석 → 호이스팅됨 (끌어올려짐)
  - 할당문 - 런타임 과정에서 해석 → 호이스팅됨 X
  - 변수 선언 전 호출해도 오류 발생 X. undefined라고 하고 넘어감.

          ```js
          function getX() {
          console.log(x); // undefined
          var x = 100; // var x;를 호이스트함
          console.log(x); // 100
          }
          getX();
          ```

    - 작동 순서에 맞게 재구성한 코드

      ```js
      function getX() {
        var x;
        console.log(x);
        x = 100;
        console.log(x);
      }
      getX();
      ```

  - 함수 호이스팅: 함수 끌어올림 O, 변수 값 끌어올림 X

    - 함수 선언을 호이스팅해 global 객체에 등록시키기에 정상 출력

      ```js
      foo( );
      function foo( ){
      console.log(‘hello’);
      };
      // console> hello
      ```

    - 함수 리터럴을 할당하는 구조라 호이스팅 안 됨 → 런타임 환경에서 `Type Error` 발생

      ```js
      foo( );
      var foo = function( ) {
      console.log(‘hello’);
      };
      // console> Uncaught TypeError: foo is not a function
      ```
