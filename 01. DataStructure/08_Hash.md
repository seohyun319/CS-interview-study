## 해시 (Hash)

<br>

- 데이터의 효율적 관리를 목적으로 임의의 길이의 데이터를 고정된 길이의 데이터로 매핑하는 함수
- 키(key, 매핑 전 데이터)를 값(hash value, 매핑 후 데이터)으로 매핑하는 과정 자체를 해싱(hashing)이라고 함
- 해시함수는 many-to-one 으로 대응 -> 다른 데이터가 같은 해시 값으로 매핑되어 충돌이 되는 해시충돌(collision) 발생
  <br>
  <image width=400 src="https://user-images.githubusercontent.com/66426083/157606315-c3e34f45-e326-4450-afe2-cfaadd5dafc4.png" />
  <br>

---

<br>

### 해시의 장점

- 적은 자원으로 많은 데이터를 효율적으로 관리 가능
- ex) 하드디스크나 클라우드에 존재하는 데이터들을 해시값으로 매핑해 작은 크기의 캐쉬 메모리로 프로세스 관리 가능
- index에 해시값을 사용함으로써 모든 데이터를 살피지 않고 검색, 삽입, 삭제를 빠르게 수행 가능
- 계산복잡성 O(1) 지향
- 키와 해시값 사이에 직접적인 연관이 없기 때문에 보안에 좋음
- 길이가 서로 다른 입력 데이터에 대해 일정한 길이의 출력을 만들어 '데이터 축약' 기능 수행 가능
  <br>

---

<br>

### 해시테이블

- 해시함수를 사용한 키와 해시값을 매핑하고, 해시값을 index 또는 주소 삼아 데이터의 값을 키와 함께 저장하는 자료구조
- 데이터가 저장되는 곳을 버킷(bucket) 또는 슬롯(slot)이라고 함
  <br>
  <img width=400 background-color="white" src="https://user-images.githubusercontent.com/66426083/157603076-d056057e-1751-4ea6-8cd1-ea02480117f4.png" />
  <br>
  <img width="610" alt="image" src="https://user-images.githubusercontent.com/66426083/157603488-2fac0046-4dbb-43fb-a94b-cc5fd4775bf7.png">
  <br>

---

<br>

### 충돌문제 해결법

- Chaining
  - 한 버킷당 들어갈 수 있는 엔트리의 수에 제한을 두지 않고 연결리스트로 체인처럼 노드를 추가해나가는 방식
  - 장점) 유연함
  - 단점) 메모리 문제 야기 가능
  - 시간복잡도: 삽입 - O(1) / 검색, 삭제 - O(1) (최악의 경우 O(n))
    <br>
    <img width=400 src ="https://user-images.githubusercontent.com/66426083/157603993-dee1326c-ba34-40a8-b66d-1ccacd8aed66.png" />
    <br>
    <br>
- Open Addressing
  - 해시 함수로 얻은 주소가 아닌 다른 주소에 데이터를 저장할 수 있도록 허용(이미 다른 데이터가 저장되어 있으면 다음 버킷에 저장)
  - 장점) 메모리 문제가 발생하지 않음(비어있는 테이블의 공간을 활용하기 때문)
  - 단점) 해시 충돌 발생 가능 -> 해시테이블 내 새로운 주소를 찾는 탐사(probing)로 해결
    - 선형 탐사: 정해진 고정 폭으로 옯겨 해시값의 중복을 피함
    - 제곱 탐사: 정해진 고정 폭을 제곱수로 옮겨 해시값의 중복을 피함
  - 시간복잡도: 탐사 횟수에 비례
- 해시함수
  - 특정 값에 치우치지 않고 해시값을 고르게 만들어내는 좋은 해시함수를 이용
  - division method: 숫자로 된 키를 해시테이블의 크기로 나눈 나머지를 해시값으로 반환
  - universal hasing: 다수의 해심함수를 만들고, 해시함수의 집합에서 무작위로 해시함수를 선택해 해시값을 만드는 기법

<br>
참고 https://ratsgo.github.io/data%20structure&algorithm/2017/10/25/hash/ / https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Hash.md
