## 어댑터 패턴
> 한 클래스의 인터페이스를 클라이언트에서 사용하고자하는 다른 인터페이스로 변환한다. <br>
> 어댑터를 이용하면 인터페이스 호환성 문제 때문에 같이 쓸 수 없는 클래스들을 연결해서 쓸 수 있다.

- 사용 방법 : 상속
- 호환되지 않은 인터페이스를 사용하는 클라이언트 그대로 활용 가능
- 향후 인터페이스가 바뀌더라도, 변경 내역은 어댑터에 캡슐화 되므로 클라이언트 바뀔 필요X
- ex) 맞지 않는 이어폰 잭 

클래스 다이어그램

<img width="578" alt="image" src="https://user-images.githubusercontent.com/66426083/170428036-341fdb43-6150-4335-9066-59e55c86335f.png">

<br>

<img width="529" alt="image" src="https://user-images.githubusercontent.com/66426083/170428189-c95d7032-e7e1-42a3-9dc8-7188918b4746.png">

<br>

예시 - 오리가 부족해서 칠면조를 대신 사용해야 하는 상황

Duck.java
```java
package AdapterPattern;

public interface Duck {
	public void quack();
	public void fly();
}
```

<br>

Duck.java
```java
package AdapterPattern;

public interface Duck {
	public void quack();
	public void fly();
}
```

<br>

Turkey.java
```java
package AdapterPattern;

public interface Turkey {
	public void gobble();
	public void fly();
}
```

<br>

WildTurkey.java
```java
package AdapterPattern;

public class WildTurkey implements Turkey {

	@Override
	public void gobble() {
		System.out.println("Gobble gobble");
	}

	@Override
	public void fly() {
		System.out.println("I'm flying a short distance");
	}
}
```

<br>

TurkeyAdapter.java
```java
package AdapterPattern;

public class TurkeyAdapter implements Duck {

	Turkey turkey;

	public TurkeyAdapter(Turkey turkey) {
		this.turkey = turkey;
	}

	@Override
	public void quack() {
		turkey.gobble();
	}

	@Override
	public void fly() {
		turkey.fly();
	}

}
```
<br>

DuckTest.java
```java
package AdapterPattern;

public class DuckTest {

	public static void main(String[] args) {

		MallardDuck duck = new MallardDuck();
		WildTurkey turkey = new WildTurkey();
		Duck turkeyAdapter = new TurkeyAdapter(turkey);

		System.out.println("The turkey says...");
		turkey.gobble();
		turkey.fly();

		System.out.println("The Duck says...");
		testDuck(duck);

		System.out.println("The TurkeyAdapter says...");
		testDuck(turkeyAdapter);

	}

	public static void testDuck(Duck duck) {

		duck.quack();
		duck.fly();

	}
}
```

<br>

- Target은 오리, Adapter는 칠면조

<br>
<br>
<br>

참고 https://jusungpark.tistory.com/22 / https://github.com/gyoogle/tech-interview-for-developer/blob/master/Design%20Pattern/Adapter%20Pattern.md
