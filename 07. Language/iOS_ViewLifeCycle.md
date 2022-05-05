## View Life Cycle

![image](https://user-images.githubusercontent.com/65678579/166628554-8f67c481-4871-4896-bd4a-dbb57a05034d.png)

----

<br>

### 1. viewDidLoad()
- view controller가 메모리에 로드되고 난 후 호출되는 함수
- 시스템에 의해 자동으로 호출 ➡️ 리소스를 초기화하거나, 초기화면을 구성하는 용도로 사용
- 처음 한 번 실행해야하는 코드를 이 메소드 내에 작성

### 2. viewWillAppear()
- 뷰가 나타나기 직전에 호출되는 함수(뷰가 나타날거라는 신호를 컨트롤러에게 알리는 역할). 

**✅ viewDidLoad vs viewWillAppear**
```
navigation controller에서 차이를 보인다.
navigation controller는 stack과 같이 동작한다. 

1️⃣첫 번째 뷰 ▶ 2️⃣두 번째 뷰 ▶ 3️⃣첫 번째 뷰

로 이동할 때,1️⃣과 2️⃣에서는 뷰가 처음 호출됙 때문에 stack 메모리에 적재되어 viewDidLoad가 실행된다.
하지만 3️⃣에서는 이미 적재된 두 번째 뷰가 pop된 것으로 메모리에 뷰 컨트롤러가 로드되지 않았기 때문에 viewDidLoad가 실행되지 않는다.
```

### 3. viewDidAppear()
- 뷰가 화면에 나타난 직후 호출
- 뷰가 나타났다는 것을 컨트롤러에게 알리는 역할
- 화면에 적용될 애니메이션을 그려줌

### 4. viewWillDisappear()
- 뷰가 사라지기 직전에 호출되는 함수
- 뷰가 삭제 되려고 하는 것을 뷰 컨트롤러에 통지

### 5. viewDidDisappear()
- 뷰 컨트롤럴 뷰가 제거되었음을 알려줌

---- 

### 네비게이셔 스택에서의 함수 호출 결과

<img width="331" alt="스크린샷 2022-05-04 오후 3 08 06" src="https://user-images.githubusercontent.com/65678579/166630477-68d538d6-9b92-4414-bde4-fc7588433a41.png">

#### 1️⃣ 첫 번째 뷰 로드
- 메모리 로드 후 viewDidLoad() 호출
- 뷰가 나타나기 직전 호출되는 viewWillAppear()
- 뷰가 나타나고 나서 호출되는 viewDidAppear()

#### 2️⃣ 두 번째 뷰로 이동
- 첫 번째 뷰가 사라지기 전 호출되는 viewWillDisappear()
- 두 번째 뷰 메모리에 적재 viewDidLoad()
- 두 번째 뷰가 나타나기 전 호출되는 viewWillAppear()
- 첫 번째 뷰 사라지는 viewDidDisappear()
- 그 다음 두 번째 뷰 진정으로 보여줌 viewDidAppear()
- `✅ 뷰가 두 개 이상일 때는 viewWillAppear() -> viewDidDisappear()//기존 뷰 -> viewDidAppear() 임을 기억`

#### 3️⃣ 다시 첫 번째 뷰로 이동
- 두 번째 뷰가 사라질 것이라는 viewWillDisappear()
- 첫 번째 뷰가 나타나기 전 호출되는 viewWillAppear()
- 두 번째 뷰 사라지는 viewDidDisappear()
- 첫 번째 뷰가 다시 나타나는 viewDidAppear()
- `✅ 첫 번째 뷰는 이미 메모리에 적재되었기 때문에 viewDidLoad가 실행되지 않음'


--- 

### 추가 loadView
```swift
override func loadView() {
    print("1st loadView")
}
```
위의 함수로 직접 호출을 하려면 self.loadView()가 아닌, super.loadView()를 해주어야 한다.  
애플 공식문서에서도 이 함수를 직접 호출하면 안되고 뷰의 추가 초기화를 사용하려며 viewDidLoad()를 사용하라는 말이 있다.  

그렇다면 loadView()의 역할은 무엇일까?
❗️바로 컨트롤러가 관리하는 뷰를 **만드는** 역할을 한다. 

즉 loadView()가 뷰를 만들고 메모리에 올린 후에 viewDidLoad()가 호출된다고 할 수 있다.

---

#### 참고 
[link](https://zeddios.tistory.com/43)
