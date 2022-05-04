## Garbage Collection

### Garbage Collection 이란?

다른 언어와 달리 Java나 Kotlin에서는 JVM의 가비지 컬렉터가 불필요한 메모리를 알아서 정리해주기 때문에 개발자가 메모리를 직접해자하지 않아도 된다.
대신 불필요한 데이터 표현을 위해 null을 할당한다.

``` java
Person person = new Person(); 
person.setName("Mang"); 
person = null;
```

### Minor GC와 Major GC
Java에서 객체는 대부분 일회성이고 메모리에 장기간 남아있는 경우가 드물다 따라서 객체의 생존 기간에 따라 힙 영역을 Young, Old의 두가지 영역으로 나눈다.
- Young 영역(Young Generation)
    - 새롭게 생성된 객체가 할당(Allocation)되는 영역
  - 대부분의 객체가 금방 Unreachable 상태가 되기 때문에, 많은 객체가 Young 영역에 생성되었다가 사라진다.
  - Young 영역에 대한 가비지 컬렉션(Garbage Collection)을 Minor GC라고 부른다.
- Old 영역(Old Generation)
    - Young영역에서 Reachable 상태를 유지하여 살아남은 객체가 복사되는 영역 
    - Young 영역보다 크게 할당되며, 영역의 크기가 큰 만큼 가비지는 적게 발생한다.
    - Old 영역에 대한 가비지 컬렉션(Garbage Collection)을 Major GC 또는 Full GC라고 부른다.
<br><img src="https://postfiles.pstatic.net/MjAyMDA4MjhfMTY2/MDAxNTk4NTUwNDc2MTgw.xUM3JOgHawFpFpu85ZXhh8bfqAtdljdHWtn7yjI2Ihog.WaklINa6Pu8FBiEW_qYam-gYhdYnvMwxygkh3SSvo6Mg.PNG.pcmola/JVMHeap.png?type=w773" title="px(픽셀) 크기 설정" alt="RubberDuck"/><br>

### Garbage Collection(가비지 컬렉션)의 동작 방식
기본적으로 다음과 같이 2가지 단계를 따른다.<br>
>    1. Stop The World<br>
>        - 가비지 컬렉션을 실행하기 위해 JVM이 애플리케이션의 실행을 멈추는 작업 
>    2. Mark and Sweep
>        - Mark: 사용되는 메모리와 사용되지 않는 메모리를 식별하는 작업
>        - Sweep: Mark 단계에서 사용되지 않음으로 식별된 메모리를 해제하는 작업

General GC과정은 다음과 같다.

처음 생성된 객체는 Young Generation 영역의 일부인 Eden 영역에 위치하게된다.

➡ 그리고 Minor GC가 발생하게 되면, 사용하지 않는 다시말하면 다른 곳에서 참조되지 않는 객체는 메모리에서 제거된다.

➡ Eden 영역에서 살아남은 객체는 Young Generation 영역의 또다른 일부인 Survivor 영역으로 이동함

➡ Minor GC가 발생할 때마다 Survivor1 영역에서 Survivor2 영역으로 또는 Survivor2 영역에서 Survivor1 영역으로 객체가 이동하게되며, 이 과정에서 더이상 참조되지 않는 객체는 메모리에서 제거된다.

➡ Minor GC가 발생하는 동안 Survivor1, Survivor2 영역을 오가며 살아남은 객체들은 최종적으로 Old Generation 영역(=테뉴어드, Tenured)으로 옮겨진다.

➡ Old Generation 영역에 있다가 미사용된다고 식별되는 객체들은 Full GC를 통해 메모리에서 제거된다.

> 각 객체는 Minor GC에서 살아남은 횟수를 기록하는 age bit를 가지고 있는데 이 비트는 Minor GC발생 시 마다 1씩 값이 증가하며 이 값을 통해 오래되었다는 것을 판단한다.

