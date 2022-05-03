## this에 대하여

### 1. 객체의 메서드를 호출할 때

- 객체의 property가 함수일 때 메드라고 부름
- this는 함수를 실행할 때 함수를 소유하고 있는 객체(메서드를 포함하고 있는 인스턴스)를 참조 -> 해당 메서드를 호출한 객체로 바인딩
- ex) A.B -> B 함수 내부에서의 this는 A를 가리킴

```javascript
var myObject = {
  name: "foo",
  sayName: function() {
    console.log(this);
  }
};
myObject.sayName();
// console> Object {name: "foo", sayName: sayName()}
```

<br>

### 2. 함수를 호출할 때
 - 객체의 메소드가 아니라 함수를 호출하면 해당 함수 내부 코드에서 사용된 this는 전역객체에 바인딩됨
 
 ```javascript
var value = 100;
var myObj = {
  value: 1,
  func1: function() {
    console.log(`func1's this.value: ${this.value}`);

    var func2 = function() {
      console.log(`func2's this.value ${this.value}`);
    };
    func2();
  }
};

myObj.func1();
// console> func1's this.value: 1
// console> func2's this.value: 100
```
- func1에서의 this는 myObj
- func2에서의 this는 전역 객체로 바인딩됨 (A.B 구조에서 A가 없기 때문)

<br>

### 3. 생성자 함수를 통해 객체를 생성할 때
 - new 키워드를 통해 생성자 함수를 호출할 때 함수 내부에서의 this는 객체 자신이 됨
 
 ```javascript
var Person = function(name) {
  console.log(this);
  this.name = name;
};

var foo = new Person("foo"); // Person
console.log(foo.name); // foo
```


<br>

### 4. bind, call, apply 를 통한 호출
 - 앞의 3가지 경우에 의존하지 않고 this를 자바스크립트 코드로 주입 또는 설정할 수 있는 방법

<br>
 
 - bind 메소드 사용
 ```javascript
var value = 100;
var myObj = {
  value: 1,
  func1: function() {
    console.log(`func1's this.value: ${this.value}`);

    var func2 = function(val1, val2) {
      console.log(`func2's this.value ${this.value} and ${val1} and ${val2}`);
    }.bind(this, `param1`, `param2`);
    func2();
  }
};

myObj.func1();
// console> func1's this.value: 1
// console> func2's this.value: 1 and param1 and param2
```

<br>

- call 메소도 사용

 ```javascript
var value = 100;
var myObj = {
  value: 1,
  func1: function() {
    console.log(`func1's this.value: ${this.value}`);

    var func2 = function(val1, val2) {
      console.log(`func2's this.value ${this.value} and ${val1} and ${val2}`);
    };
    func2.call(this, `param1`, `param2`);
  }
};

myObj.func1();
// console> func1's this.value: 1
// console> func2's this.value: 1 and param1 and param2
```
<br>

- apply 메소도 사용

 ```javascript
var value = 100;
var myObj = {
  value: 1,
  func1: function() {
    console.log(`func1's this.value: ${this.value}`);

    var func2 = function(val1, val2) {
      console.log(`func2's this.value ${this.value} and ${val1} and ${val2}`);
    };
    func2.apply(this, [`param1`, `param2`]);
  }
};

myObj.func1();
// console> func1's this.value: 1
// console> func2's this.value: 1 and param1 and param2
```
<br>

- bind vs apply, call 
  - bind는 함수를 선언할 때 this와 파라미터 지정
  - call과 apply는 함수를 호출할 때 this와 파라미터 지정

- apply vs bind, call 
  - apply는 첫 번째 인자로 this를 넘겨주고 두 번째 인자로 넘겨줘야 하는 파라미터를 배열 형태로 전달
  - bind와 call은 각각의 파라미터를 하나씩 넘겨주는 형태


<br>
<br>
<br>

참고 https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/JavaScript#closure


