# 싱글톤 패턴(Singleton pattern)

### ▶️ 개념

<br>

애플리케이션이 시작될 때, 어떤 클래스가 **최초 한 번만 메모리를 할당(static)**하고 해당 **메모리에 인스턴스를 만들어 사용**하는 패턴

즉, **하나의 인스턴스만 생성**하여 사용하는 디자인 패턴이라고 볼 수 있다.

인스턴스가 필요할 때마다 생성하는 것이 아니라 **기존의 것을 활용**하는 개념이다.

예로, java에서는 생성자를 private으로 선언해 다른 곳에서 생성하지 못하도록 만들고, getInstance() 메소드를 통해 받아서 사용하도록 구현한다.

하나의 인스턴스를 메모리에 등록해서 여러 스레드가 동시에 해당 인스턴스를 공유하여 사용할 수 있게 할 수 있기 때문에 요청이 많은 곳에서 사용하면 효율을 높일 수 있다. 

![Untitled](https://user-images.githubusercontent.com/61955796/170219294-d6910e15-d8f1-4119-aa64-c8c9424af523.png)

하지만 동시성 문제가 발생할 수 있다는 점을 주의해야 한다.

<br>

### ▶️ 사용 이유

<br>

1. 메모리 낭비 방지
    
    객체를 생성할 때마다 메모리 영역을 할당 받아야 한다. 이때 한번의 new를 통해 객체를 생성한다면 메모리 낭비를 방지할 수 있다.
    
2. 전역 인스턴스
    
    싱글톤으로 구현한 인스턴스는 '전역'이므로, 다른 클래스의 인스턴스들이 데이터를 공유할 수 있다.
    
<br>

### ▶️ 주로 사용하는 곳

<br>

- 공통된 객체를 여러 개 생성해서 사용해야 하는 상황
    
    ex) 커넥션풀, 스레드풀, 캐시, 로그 기록 객체 등
    
- 안드로이드 어플리케이션
    
    각 액티비티들이나 클래스에게 주요 클래스를 하나하나 전달하는 게 번거롭기 때문에 싱글톤 클래스를 만들어 어디서든 접근하도록 설계한다. 
    
- 인스턴스가 절대적으로 한 개만 존재하는 것을 보증해야 하는 상황

### ▶️ 단점

<br>

- 개방-폐쇄 원칙 위배
    
    만약 싱글톤 인스턴스가 혼자 너무 많은 일을 하거나, 많은 데이터를 공유하면 다른 클래스들 간의 결합도가 높아지게 되는데, 이때 개방-폐쇄 원칙이 위배된다.
    
    결합도가 높아지게 되면 유지보수가 힘들고 테스트도 원활하게 진행하기 힘들다.
    
- 동기화 문제
    
    멀티 스레드 환경에서 동기화 처리를 하지 않았을 때, 인스턴스가 2개가 생성되는 문제가 발생할 수 있다.
    

따라서 반드시 싱글톤 패턴으로 구현해야 하는 경우가 아니면 지양하는 것이 좋다고 한다. 

### ▶️ 예시

<br>

‘자동차’ 객체가 있다.

```java
public class CarClass
```

과연 어떻게 해야 자동차 객체의 인스턴스가 하나만 존재하도록 할 수 있을까?

```java

private CarClass() {

}
```

→ 이 방식으로는 아무도 객체를 생성할 수 없다.

```java
private static CarClass car = new CarClass();
```

→ 자신을 멤버로 선언해서 메모리에 올렸지만, 외부에서 멤버로 선언된 CarClass 역시 private이다.

그럼 외부에서 멤버로 선언된 car를 가져오는 method를 만들면 되지 않을까?!

**** 정답 ****

```java
public static CarClass getInstance() {
	return car;
}
```

** 구현 예시 **

```java
public class CarClass {

	private static CarClass car = new CarClass();

	private CarClass() {}

	public static CarClass getInstance() {
		return car;
	}

	private static boolean isUse = false;

	//차 사용 시작
	public static void drive() {
		isUse = true;
		System.out.println("start driving");
	}

//차 사용 종료
	public static void parking() {
		isUse = false;
		System.out.println("parking");
	}

	public static boolean isEnableUseCar() {
		return isUse;
	}
}
```

- getInstance 메소드 외에는 CarClass 객체를 생성 및 사용할 수 없다.
- private static CarClass = car = new CarClass();를 통해 최초 한 번만 객체를 생성하고 이후에 getInstance 메소드를 활용해서 return 받아서 사용하는 형식이다.
- 이때 차 객체를 누군가 이용하고 있으면 이용을 못하게 구현하여 동시성 문제를 제어했다.

**![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ee1a0ebd-fde2-4ef2-a651-da7c4ad1bd5b/Untitled.png)**

<br>

### ▶️ 멀티스레드 환경에서 안전한 싱글톤 만드는 방법

<br>

1. ***Lazy Initialization (초기화 지연)***
    
    ```java
    public class ThreadSafe_Lazy_Initialization{
     
        private static ThreadSafe_Lazy_Initialization instance;
     
        private ThreadSafe_Lazy_Initialization(){}
         
        public static synchronized ThreadSafe_Lazy_Initialization getInstance(){
            if(instance == null){
                instance = new ThreadSafe_Lazy_Initialization();
            }
            return instance;
        }
     
    }
    ```
    
    - private static으로 인스턴스 변수를 만든다.
    - private으로 생성자를 만들어서 외부에서의 생성을 막는다.
    - synchronized 동기화를 활용해 스레드를 안전하게 만든다.
    - 하지만 이 방식은 큰 성능 저하가 발생하므로 권장하지 않는다.

<br>

2. ***Lazy Initialization + Double-checked Locking***
    
    > 1번의 성능 저하를 완화하는 방법
    > 
    
    ```java
    public class ThreadSafe_Lazy_Initialization{
        private volatile static ThreadSafe_Lazy_Initialization instance;
    
        private ThreadSafe_Lazy_Initialization(){}
    
        public static ThreadSafe_Lazy_Initialization getInstance(){
        	if(instance == null) {
            	synchronized (ThreadSafe_Lazy_Initialization.class){
                    if(instance == null){
                        instance = new ThreadSafe_Lazy_Initialization();
                    }
                }
            }
            return instance;
        }
    }
    ```
    
    - 1번과 달리 조건문으로 인스턴스의 존재 여부를 확인한 다음에 두 번째 조건문에서 synchronized를 통해 동기화를 시키는 것
    - 스레드를 안전하게 만들면서 처음 생성 이후에는 synchronized를 실행하지 않기 때문에 성능 저하를 완화할 수 있다.

<br>

3. ***Initialization on demand holder idiom (holder에 의한 초기화)***
    
    > 클래스 안에 클래스를 두어서 JVM의 클래스 로더 매커니즘과 클래스가 로드되는 시점을 이용한 방법
    > 
    
    ```java
    public class Something {
        private Something() {
        }
     
        private static class LazyHolder {
            public static final Something INSTANCE = new Something();
        }
     
        public static Something getInstance() {
            return LazyHolder.INSTANCE;
        }
    }
    ```
    
    - JVM의 클래스 초기화 과정에서 보장되는 원자적 특성을 이용해서 싱글톤의 초기화 문제에 대한 책임을 JVM에게 떠넘기는 것 !!
    - 클래스 안에 선언한 클래스인 holder에서 선언된 인스턴스는 static이기 때문에 클래스 로딩 시점에서 한 번만 호출된다.
    - final을 사용해서 다시 값이 할당되지 않도록 만든다.
    - 실제로 가장 많이 사용되는 방식이다 !
