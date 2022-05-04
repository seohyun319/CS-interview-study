## Optional(옵셔널)
> 직역하면 '선택적인'이라는 뜻으로 어떠한 변수에 값이 **있을 수도 - 없을 수도** 있는 경우를 표현하기 위하 문법

```swift
//Int와 String 옵셔널 형
var optionalNum : Int?
var optionalString : String?
```
optionalNum과 optionalString에는 각각 Int와 String값이 있을 수도 없을 수도 있다는 의미
   
<br>

### optional과 nil
```swift
var optionalNum : Int?
var num : Int

optionalNum = 100
optionalNum = nil

num = 100
num = nil // error
```
옵셔널과 nil은 같이 묶여 사용되는데, 일반 변수에 nil을 대입하며 에러가 발생한다.  
일반 변수에서느 데이터가 없다는 케이스가 없기 때문에 nil이 들어올 수가 없다.(에러 발생). 
반면, 옵셔널은 **값이 있을 수도 - 없을 수도 있는 형태**기 때문에 Int값을 넣을 수도 있고 nil값을 넣을 수도 있다.  

<br>

```swift
var optionalNum : Int?
var num : Int

optionalNum = 100
optionalNum = nil

num = 100

num = optionalNum // error

print(optionalNum) // Optional(100)
```
- swift는 타입에 굉장이 엄격한 언어이기 때문에 Int형 변숭 Optional Int형 변수를 대입하며 에러를 발생시킨다. 둘은 다른 데이터 형이다.  
- print문으로 옵셔널 변수 출력 시 Optional(100)이 출력되는 것으로 다르 데이터형임을 확인할 수 있다.  


### 언래핑

> Optional형 변수들은 상자가 있는 상태라고 했을 때, 상자 안에 정말 값이 들어있다는 것을 알려주려면 어떻게 해야할까? -> 언래핑

#### 강제 언래핑
```swift
var optionalNum : Int?
var num : Int

optionalNum = 100
num = optionalNum!
```
- 느낌표를 하나의 망치 개념으로 생각하면 됨
- 단, 만약 **언래핑을 했는데 nil값이 들어있는** 경우에는 에러 발생 `컴파일러에서 빌드는 성공적으로 되지만, 나중에 변수에 접근 시 nil값에 접근 하려 하므로 에러 발생`
- 느낌표를 사용하여 존재하지 않는(nil) 옵셔널 값에 접근하려 시도하면 런타임 에러가 발생함. 강제 언래핑 전에는 항상 옵셔널 값이 nil이 아님을 확실히 해야 함.

#### 옵셔널 바인딩

> nil을 체크하고 -> 안전하게 값을 추출

```swift
func printName(_ name : String){
  print(name)
}

var myName : String? = nil
printName(myName)
// 전달되는 값의 타입이 String/String? 으로 다르기 때문에 컴파일 에러 발생
```
여기서 강제 언래핑(!)을 사용하며 myName은 nil값이기 때문에 에러가 발생한다.  
이 문제는 옵셔널 바인딩으로 해결할 수 있다.  

```swift
func printName(_ name : String){
  print(name)
}

var myName : String? = nil

if let name : String = myName{
  printName(name)
}else {
  print("myName is nil... so sad.. ")
}

printName(name)
```
- 옵셔널 바인딩은 if-let(또는 if var)구문을 활용해서 옵셔널 값이 nil인지 아닌지 체크한다. `if let name : String = myName`
- nil인 경우 false로 떨어지고, String? 값이면 언래핑해서 name이라는 변수에 넘겨주게 되는 형식이다.

```swift
var myName : String? = "yunseo"
var yourName : String? = nil

if let name = myName, let friend = yourName {
  print("\(name) and \(friend)")
}
// yourName이 nil이기 때문에 안의 구문은 실행되지 않음

yourName = "apple"
if let name = myName, let friend = yourName {
  print("\(name) and \(friend)")
}
// yuseo and apple이 출력 됨!
```
- if-let 구문은 콤마(,)를 사용해 연달아 이어 붙일 수 있다.
- 나열한 모든 조건이 통과되어야 안으 구문이 실행된다. (하나라도 nil인 경우 false로 떨어짐)


### 옵셔널 체인
```swift
class Person {
   var name: String
   var job: String?
   var home: Apartment?
   
   init(name: String) {
      self.name = name
   }
}

class Apartment {
   var buildingNumber: String
   var roomNumber: String
   var `guard`: Person?
   var owner: Person?
   
   init(dong: String, ho: String) {
      buildingNumber = dong
      roomNumber = ho
   }
}
```
- \`guard\`는 키워드이므로 \`\`를 붙여줘야 함.

❓nil인지 아닌지 체크 해야 할 값이 여러개라면 어떻게 해야할까?
```swift
func guardJob(owner: Person?) {
   if let owner = owner {
      if let home = owner.home {
         if let `guard` = home.guard {
            if let guardJob = `guard`.job{
               print("체크 완료")
            }else{
               print("nil값 존재")
            }
         }
      }
   }
}
```
- 일일이 바인딩을 중첩해야 해서 굉장히 코드가 길어지게 됨

`owner?.home?.guard?.job`



#### 참고
28기 SOPT iOS 파트장님 기초 문법 강의자료

