## ⏩ String vs StringBuffer / StringBuilder

String과 StringBuffer / StringBuilder 클래스의 가장 큰 차이점은 **String**은 **불변(immutable)**의 속성을 갖는다는 점이다.

```java
String str = "hello";   // String str = new String("hello");
str = str + " world";  // [ hello world ]
```

이 코드를 보자. 위의 예제에서 "hello" 값을 가지고 있던 String 클래스의 참조변수인 str이 있다. 

여기서 str이 가리키는 곳에 저장된 "hello"에 "world" 문자열을 더해 "hello world"로 변경한 것이라고 착각하기 쉽다.

하지만 변경이 아니다. 

기존에 "hello" 값이 들어가있던 String 클래스의 참조변수 str이 "hello world"라는 값을 가지고 있는 **새로운 메모리영역을 가리키게 변경**되고 **처음 선언했던 "hello"로 값이 할당되어 있던 메모리 영역은 Garbage로 남아있다가 GC(garbage collection)에 의해 사라지는 것**이다. 

왜 그럴까?

**String 클래스는 불변하기 때문에 문자열을 수정하는 시점에 새로운 String 인스턴스가 생성된 것이다.**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bbde5b24-dd75-4a09-8eba-45ff8a4aa5a6/Untitled.png)

### ⏩ **String 특징**

- new 연산을 통해 생성된 인스턴스의 메모리 공간은 변하지 않는다. (Immutable)
- Garbage Collector로 제거되어야 한다.
- 문자열 연산 시 새로 객체를 만드는 Overhead 발생한다.
- 객체가 불변하므로, Multithread에서 동기화를 신경 쓸 필요가 없다. (조회 연산에 매우 큰 장점)
- 문자열 연산이 적고, 조회가 많은 멀티쓰레드 환경에서 좋다.
- 변하지 않는 문자열일 때 사용하면 좋다.

이를 해결하기 위해 Java에서는 **가변(mutable)성**을 가지는 **StringBuffer** / **StringBuilder** 클래스를 도입했다.

String 과는 반대로 StringBuffer/StringBuilder 는 가변성을 가지기 때문에 .append() .delete() 등의 API를 이용하여 **동일 객체내에서 문자열을 변경**하는 것이 가능한 것이다. 따라서 **문자열의 추가,수정,삭제가 빈번하게 발생할 경우**라면 String 클래스가 아닌 **StringBuffer/StringBuilder를 사용**해야 한다.

```java
StringBuffer sb= new StringBuffer("hello");
sb.append(" world");
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8cbd348d-dda2-4117-a402-f596637eaae0/Untitled.png)

## ⏩ StringBuffer vs StringBuilder

StringBuffer와 StringBuilder의 공통점은 다음과 같다.

- new 연산으로 클래스를 한 번만 만듬 (Mutable)
- 문자열 연산 시 새로 객체를 만들지 않고, 크기를 변경함
- StringBuffer와 StringBuilder 클래스의 메서드가 동일함.

그렇다면 동일한 API를 가지고 있는 **StringBuffer, StringBuilder의 차이점**은 무엇일까?

가장 큰 차이점은 **동기화의 유무**로써 **StringBuffer**는 동기화 키워드를 지원하여 **멀티쓰레드 환경에서 안전하다는 점(thread-safe)**이다.

참고로 **String**도 ****불변성을 가지기때문에 마찬가지로 **멀티쓰레드 환경에서 안정성(thread-safe)**을 가지고 있다.

반대로 **StringBuilder**는 **동기화를 지원하지 않기** 때문에 멀티쓰레드 환경에서 사용하는 것은 적합하지 않지만 동기화를 고려하지 않는 만큼 **단일쓰레드에서의 성능은 StringBuffer 보다 뛰어나다.**

## ⏩ 정리

**String**               :  문자열 연산이 적고 멀티쓰레드 환경일 경우

**StringBuffer**    **** :  문자열 연산이 많고 멀티쓰레드 환경일 경우

**StringBuilder**   :  문자열 연산이 많고 단일쓰레드이거나 동기화를 고려하지 않아도 되는 경우

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a6834685-b331-4b44-b32c-856eefc5e670/Untitled.png)