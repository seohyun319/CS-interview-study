 # Composite Pattern
 
- 여러 개의 객체들로 구성된 복합 객체와 단일 객체를 클라이언트에서 구별 없이 다루게 해주는 패턴. 
   - 즉, 전체-부분의 관계(Ex. Directory-File)를 갖는 객체들 사이의 관계를 정의할 때 유용하다.
   - 또한 클라이언트는 전체와 부분을 구분하지 않고 동일한 인터페이스 를 사용할 수 있다.
   - ‘구조(Structural)’의 하나 (아래 참고)

<img src ="https://gmlwjd9405.github.io/images/design-pattern-composite/composite-pattern.png" height=300 /><br>

<br>

# 역할이 수행하는 작업

- Component
   - 구체적인 부분
   - 즉 Leaf 클래스와 전체에 해당하는 Composite 클래스에 공통 인터페이스를 정의
- Leaf
   - 구체적인 부분 클래스
   - Composite 객체의 부품으로 설정
- Composite
   - 전체 클래스
   - 복수 개의 Component를 갖도록 정의
   - 그러므로 복수 개의 Leaf, 심지어 복수 개의 Composite 객체를 부분으로 가질 수 있음


<br>

# 예시

- <img src ="https://gmlwjd9405.github.io/images/design-pattern-composite/composite-example.png" height=400 /><br>

   - 컴퓨터(Computer 클래스) 모델링
   - 키보드(Keyboard 클래스): 데이터를 입력받는다.
   - 본체(Body 클래스): 데이터를 처리한다.
   - 모니터(Monitor 클래스): 처리 결과를 출력한다.
   - Computer 클래스 –‘합성 관계’– 구성 장치

<br>

``` python
class Component:
  def fn(self):
    pass

class Leaf(Component):
  def fn(self):
    print('leaf')
    
class Composite(Component):
  def _init_(self):
    self.components =[]
    
  def add(self, component:Component):
    self.components.append(component)
    
  def fn(self):
    print('composite')
    for component in self.components:
      component.fn()
```

<br>

```
compost1 = Composite()
compost1.add(Leaf())
compost1.add(Leaf())

compost0 = Composite()
compost0.add(Leaf())
compost0.add(compost1)

compost0.fn()
```

<br>

실행 결과
```
composite
leaf
composite
leaf
leaf
```
<br>

> 트리 구조를 이루기 때문에 트리 구조가 아주 복잡할 때 루트에서 함수 하나만 호출하면 Composite 패턴을 따라 leaf의 함수가 점화된다는 장점을 가진다.
<br>
