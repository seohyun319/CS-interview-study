## Design Pattern
> SW 재사용성, 호환성, 유지 보수성을 보장하기 위한 일종의 설계 기법

<br>

- SOLID (객체지향 설계 원칙)을 기초로 함.

1) Single Responsibility Principle
    - 하나의 클래스는 하나의 역할만 해야 함.
2. Open - Close Principle
    - 확장 (상속)에는 열려있고, 수정에는 닫혀 있어야 함.
3) Liskov Substitution Principle
    - 자식이 부모의 자리에 항상 교체될 수 있어야 함.
4) Interface Segregation Principle
    - 인터페이스가 잘 분리되어서, 클래스가 꼭 필요한 인터페이스만 구현하도록 해야함.
5) Dependency Inversion Property
    - 상위 모듈이 하위 모듈에 의존하면 안됨.

<br>

## 디자인 패턴 분류

<img width="527" alt="image" src="https://user-images.githubusercontent.com/66426083/170427160-a30eae7f-1d65-4e8d-ab30-7fd5d6b6b6df.png">


### 생성 패턴 (Creational) 
> 객체의 생성 방식 결정

- 객체의 생성과 조합을 캡슐화해 특정 객체가 생성되거나 변경되어도 프로그램 구조에 영향을 크게 받지 않도록 유연성을 제공
- 예) DBConnection을 관리하는 Instance를 하나만 만들 수 있도록 제한하여, 불필요한 연결을 막음.


<br>


### 구조 패턴 (Structural)
> 객체간의 관계를 조직

- 클래스나 객체를 조합해 더 큰 구조를 만드는 패턴
- 예) 2개의 인터페이스가 서로 호환이 되지 않을 때, 둘을 연결해주기 위해서 새로운 클래스를 만들어서 연결시킬 수 있도록 함.


<br>

### 행위 패턴 (Behavioral) 
> 객체의 행위를 조직, 관리, 연합

- 한 객체가 혼자 수행할 수 없는 작업을 여러 개의 객체로 어떻게 분배하는지, 또 그렇게 하면서도 객체 사이의 결합도를 최소화하는 것에 중점
- 예) 하위 클래스에서 구현해야 하는 함수 및 알고리즘들을 미리 선언하여, 상속시 이를 필수로 구현하도록 함.



<br>
<br>
<br>

참고 https://github.com/gyoogle/tech-interview-for-developer/blob/master/Design%20Pattern/%5BDesign%20Pattern%5D%20Overview.md / https://gmlwjd9405.github.io/2018/07/06/design-pattern.html
