## 스트레티지 패턴(Strategy Pattern)

> 어떤 동작을 하는 로직을 정의하고, 이것들을 하나로 묶어(캡슐화) 관리하는 패턴



- 행위를 클래스로 캡슐화해 동적으로 행위를 자유롭게 바꿀 수 있게 해주는 패턴
- 같은 문제를 해결하는 여러 알고리즘이 클래스별로 캡슐화되어 있고 이들이 필요할 때 교체할 수 있도록 함으로써 동일한 문제를 다른 알고리즘으로 해결할 수 있게 하는 디자인 패턴

=> 새로운 로직을 추가하거나 변경할 때, 한번에 효율적으로 변경이 가능하다.

<br>

연못에서 오리를 키우는 게임을 구현한다고 해보자. 이 게임에서 오리는 헤엄도 치고 꽥꽥거리는 다양한 오리들이 존재한다. 게임을 구현하기 위해 Duck이라는 슈퍼 클래스를 만들고 그 클래스를 상속하여 다른 청동오리 클래스, 붉은머리오리 클래스, 고무오리 클래스, 나무오리 클래스를 만든다고 해보자.

``` java
class Duck {
	swim() { "수영하기" }
	display() < 모양은 서로 다르기 때문에 추상메소드
 }
 ```

<br>

나무오리와 고무오리는 다른 오리와 다르게 날거나 꽥꽥거리지 못하고 헤엄만 칠 수 있다.

### 디자인 원칙

<br>

> 디자인 원칙 1.
> 
> 애플리케이션에서 달라지는 부분을 찾아내고, 달라지지 않는 부분으로부터 분리시킨다.

오리의 행동이 바뀌는 부분은 fly()와 quack() 이다. 따라서 청동오리 클래스를 생성할 때, fly행동을 생성자 인자에 넣거나 오리의 행동과 관련된 setter와 관련된 메소드를 추가하여 객체를 생성한 후에도 오리의 행동을 재설정할 수 있도록 하면 좋다.

<br>

> 디자인원칙 2.
> 
> 구현이 아닌 인터페이스에 맞춰서 프로그래밍 한다.

각 행동의 큰 틀은 인터페이스 FlyBehavior, QuackBehavior로 표현하고, 구체적인 설명은 각 인터페이스를 상속받아 구현한다.

``` java
interface FlyBehavior {
	fly()
 }
 
class FlyWithWings implements FlyBehavior {
	fly() { "날개로 훨훨 날다" } // 나는 모습을 구현
 }
 
class FlyNoWay implements FlyBehavior {
	fly() { "stay.." } // 날 수 없음
 }
 ```
 
 ``` java
 interface QuackBehavior {
	quack()
 }
  
class Quack implements QuackBehavior {
	quack() { "꽥꽥" } 
 }
 
class Squeak implements QuackBehavior {
	quack() { "삑삑" } 
 }

class MuteQuack implements QuackBehavior {
	quack() { "..." } // 아무 소리도 내지 않음 
 }
 ```
 
 이렇게 구현하면 다른 객체에서도 나는 행동과 꽥꽥 행동을 재사용할 수 있다. 또한, 기존의 Quack, Squeak 같은 행동 클래스를 전혀 건드리지 않고도 새로운 MuteQuack 행동을 추가할 수 있다.
 
 
 > 디자인 패턴 3.
 > 
 > 상속보다는 두가지 클래스를 합치는 구성(Composition)을 활용한다.

" 'A는 B이다'보다 'A에는 B가 있다'가 낫다 "와 같이 "오리에는 FlyBehavior와 QuackBehavior가 있다"를 사용해야한다.


<br>

참고 : https://jason-api.tistory.com/21
