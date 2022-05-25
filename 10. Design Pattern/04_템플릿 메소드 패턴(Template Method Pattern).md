# 템플릿 메소드 패턴 (****Template Method Pattern)****

<br>

### ▶️ 개념

<br>

특정 작업을 처리하는 일부분을 서브 클래스로 캡슐화하여 전체적인 구조는 바꾸지 않으면서 특정 단계에서 수행하는 내용을 바꾸는 패턴

두 개 이상의 프로그램이 기본적으로 동일한 구조에서 동작할 때, 기본 구조는 일괄적으로 관리하면서 각 프로그램마다 달라지는 부분들에 대해서 따로 만들고 싶을 때 사용하면 좋다.

즉, 기본 구조를 특정 환경이나 상황에 맞게 확장하고 변경할 때 유용하다. 

<br>

### ▶️ 방법

<br>

1. 알고리즘의 구조를 메소드에 정의한다.
2. 하위 클래스에서 알고리즘 구조의 변경 없이 알고리즘을 재정의 한다.
3. 변하지 않는 기능은 슈퍼 클래스에 만들어 두고 자주 변경하며 확장할 기능은 서브 클래스에서 만들도록 한다.

- **Abstract Class (추상 클래스)**
    
    메인이 되는 로직 부분은 일반 메소드로 선언
    
    (구현부가 없는 클래스)
    
- **Concrete Class (구현 클래스)**
    
    메소드를 선언 후 호출하는 방식
    
    (일반적인 클래스)
    

<br>

### ▶️ 장점

<br>

1. 중복 코드를 줄일 수 있다.
2. 자식 클래스의 역할을 줄여서 핵심 로직의 관리가 용이하다.
3. 코드를 객체지향적으로 구성할 수 있다. 

<br>

### ▶️ 단점

<br>

1. 추상 메소드가 많아지면서 클래스 관리가 복잡해진다.
2. 클래스 간의 관계와 코드가 꼬여버릴 염려가 있다.

<br>

### ▶️ 사용 예제

<br>

```java
//추상 클래스 선생님 (**Abstract Class)**
abstract class Teacher{
	
    public void start_class() {
        inside();
        attendance();
        teach();
        outside();
    }
	
    // 공통 메서드 
    public void inside() {
        System.out.println("선생님이 강의실로 들어옵니다.");
    }
    
    public void attendance() {
        System.out.println("선생님이 출석을 부릅니다.");
    }
    
    public void outside() {
        System.out.println("선생님이 강의실을 나갑니다.");
    }
    
    // 추상 메서드
    abstract void teach();
}
 
// 국어 선생님 (**Concrete Class)**
class Korean_Teacher extends Teacher{
    
    @Override
    public void teach() {
        System.out.println("선생님이 국어를 수업합니다.");
    }
}
 
//수학 선생님 (**Concrete Class)**
class Math_Teacher extends Teacher{

    @Override
    public void teach() {
        System.out.println("선생님이 수학을 수업합니다.");
    }
}

//영어 선생님 (**Concrete Class)**
class English_Teacher extends Teacher{

    @Override
    public void teach() {
        System.out.println("선생님이 영어를 수업합니다.");
    }
}

public class Main {
    public static void main(String[] args) {
        Korean_Teacher kr = new Korean_Teacher(); //국어
        Math_Teacher mt = new Math_Teacher(); //수학
        English_Teacher en = new English_Teacher(); //영어
        
        kr.start_class();
        System.out.println("----------------------------");
        mt.start_class();
        System.out.println("----------------------------");
        en.start_class();
    }
}
```

<br>

![Untitled (2)](https://user-images.githubusercontent.com/61955796/170221100-0a0244b5-8c31-4698-8358-de7bc4970ae9.png)


<br>

[참고] [https://coding-factory.tistory.com/712](https://coding-factory.tistory.com/712)
https://cmelcmel.tistory.com/m/14
