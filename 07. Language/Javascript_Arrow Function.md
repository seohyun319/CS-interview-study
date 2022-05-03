## Arrow Function
> 기존 function 표현 방식보다 간결한 함수 표현

<br>

### 짧은 함수

```javascript
var materials = [
  'Hydrogen',
  'Helium',
  'Lithium',
  'Beryllium'
];

materials.map(function(material) { 
  return material.length; 
}); // [8, 6, 7, 9]

materials.map((material) => {
  return material.length;
}); // [8, 6, 7, 9]

materials.map(({length}) => length); // [8, 6, 7, 9]
```
<br>

### 상위 스코프 this

```javascript
function Person(){
  this.age = 0;

  setInterval(() => {
    this.age++; // |this|는 person 객체를 참조
  }, 1000);
}

var p = new Person();
```
<br>

- 일반 함수에서 this는 자기 자신
- 화살표 함수에서 this는 Person의 this와 동일한 값을 가짐 
- setInterval의 this는 Person의 this를 가리키며, Person 객체의 age에 접근

<br>

---

<br>

### 화살표 함수 정리
- 짧은 함수로 사용 가능
- 상위 스코프의 this를 그대로 물려받아 사용 가능

<br>

---

<br>

### 화살표 함수에서 지원되지 않는 것

1. 자신의 this, super

<br>

2. arguments
    - arguments 객체: 함수에 전달된 인수에 해당하는 Array 형태의 객체
      ```javascript
      function func1() {
      console.log(arguments[0]);
      // expected output: 1

      console.log(arguments[1]);
      // expected output: 2

      console.log(arguments[2]);
      // expected output: 3
      }
      func1(1, 2, 3);
      ```
    
    - 화살표 함수에서는 arguments가 정의되지 않았기 때문에 사용 불가 -> es6 문법에서 ... 키워드 추가
      ```javascript
      const func1 = (...args)=>{
        console.log(args[0])
      }

      func1(1, 2, 3);
      ```

<br>

3. 생성자
    - 생성자 함수는 prototype property를 가지며 그게 가리키는 prototype 객체의 constructor를 사용
    - 화살표 함수는 prototype property가 없음 -> new와 함께 호출 불가
      ```javascript
      const Foo = () => {};

      // 화살표 함수는 prototype 프로퍼티가 없다
      console.log(Foo.hasOwnProperty('prototype')); // false

      const foo = new Foo(); // TypeError: Foo is not a constructor
      ```


<br>
<br>
<br>

참고 https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/JavaScript#closure/
https://ko.javascript.info/arrow-functions / https://webclub.tistory.com/649 / https://bubobubo003.tistory.com/55 / https://doozi316.github.io/javascript/2019/10/23/JS15/
