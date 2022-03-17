## Normalization의 목적
- 데이터의 중복을 없애면서 불필요한 데이터 최소화
- 무결성을 지키고 이상 현상을 방지
- 논리적이고 직관적인 테이블 구성
- 데이터베이스 구조의 확장에 용이

## 정규화의 단계
정규화에는 여러가지 단계가 있지만, 대체적으로 1~3단계 정규화까지의 과정을 거친다.

### 제 1 정규화 (1NF)

테이블(Relation)이 1정규형을 만족했다는 것은 아래 세 가지 조건을 만족했다는 것을 의미한다.

    1. 어떤 relation에 속한 모든 domain이 원자값(atomic value, 즉 1개의 값)만으로 되어 있다.
    2. 모든 attribute에 반복되는 그룹(repeating group)이 나타나지 않는다.
    3. 기본 키를 사용하여 관련 데이터의 각 집합을 고유하게 식별할 수 있어야 한다.

예제)

![](http://dl.dropbox.com/s/9s8vowdzs3t66uw/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202018-12-02%2017.50.02.png)
- 위의 조건 중 1번 조건을 충족하지 못 함. (전화번호를 여러개 가지고 있기 때문에 atomic하지 않음)

![](http://dl.dropbox.com/s/rk4jovticy5y3fw/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202018-12-02%2017.54.10.png)
- 위의 조건 중 2번 조건을 충족하지 못 함. (전화번호 그룹이 반복)

이를 제 1정규화를 만족할 수 있게 재디자인하면
![](http://dl.dropbox.com/s/1rr8ofxuy46i61b/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202018-12-02%2018.00.52.png)
- 그래도 위의 조건 중 3번 조건을 충족하지 못 함. (ID가 더 이상 고유하게 식별할 수 있는 키가 아님)

이를 다시 재디자인하면 제 1정규화를 만족한다.
![](http://dl.dropbox.com/s/dpuppv89n42ubre/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202018-12-02%2022.55.29.png)
- Customer Name과 Customer Telephone Number는 One-to-Many 관계 형성

### 제 2정규화(2NF)

테이블이 제 2정규형을 만족하면, 모든 컬럼이 완전 함수적 종속을 만족한다. (부분 함수적 종속 모두 제거됨)

**함수적 종속**
-  X의 값에 따라 Y값이 결정될 때 X -> Y로 표현하는데, 이를 Y는 X에 대해 함수적 종속
-  X가 바뀌었을 경우 Y가 바뀌어야만 함
  
함수적 종속에서 X의 값이 여러 요소일 경우, 즉, {X1, X2} -> Y일 경우, 
- **완전 함수적 종속** : X1와 X2가 Y의 값을 결정할 때
- **부분 함수적 종속** : X1, X2 중 하나만 Y의 값을 결정할 때

예시)
![](http://dl.dropbox.com/s/c2xfxdanbuiaw1l/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202018-12-03%2006.58.17.png)
- {Model, Manufacturer} -> Model Full Name은 **완전 함수적 종속**
- {Model, Manufacturer} -> Manufacturer Country은 Manufacturer Country는 Manufacturer와만 종속관계에 있기 때문에 **부분 함수적 종속**. 

이 테이블을 **부분 함수 종속을 제거**해 재디자인하면 제 2정규화를 만족한다.
![](http://dl.dropbox.com/s/x8481598dhnpzeg/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202018-12-03%2010.58.15.png)

### 제 3정규화 (Third Normal Form, 3NF)
테이블이 제 3정규형을 만족한다는 것은 아래 두 가지 조건을 만족하는 것을 의미한다.
1. 테이블(relation)이 제 2정규화 되었다.
2. 기본 키(primary key)가 아닌 속성(attribute)들은 기본 키에만 의존해야 한다.

예시)
![](http://dl.dropbox.com/s/xtfoetv8hg6jn3f/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202018-12-03%2012.59.46.png)
- 위의 조건 중 두번째 조건을 충족하지 못 함.({Tournament, Year}가 후보키가 되는데, Winner Date of Birth은 기본키가 아닌 속성인 Winner를 거쳐 {Tournament, Year}에 의존)

이를 재디자인하면 제 3정규화를 만족한다.
![](http://dl.dropbox.com/s/ks03nkc26nsffin/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202018-12-04%2014.51.39.png)


### 출처
- https://wkdtjsgur100.github.io/database-normalization/
