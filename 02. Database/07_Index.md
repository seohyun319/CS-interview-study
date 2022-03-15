## 인덱스 (Index)

<br>

- 추가적인 쓰기 작업과 저장 공간을 활용하여 데이터베이스 테이블의 검색 속도를 향상시키기 위한 자료구조
- 책의 목차처럼 테이블의 칼럼을 색인화
  <br>
  <img width="600" alt="image" src="https://user-images.githubusercontent.com/66426083/158321143-20e62c90-ffa6-40ce-bbca-6f803d87e73f.png">

<br>

---

<br>

### **DB 파일 구성**

- 테이블 생성 시 3가지 파일 생성
- FRM: 테이블 구조 저장 파일 (Format(schema) file)
- MYD: 실제 데이터 파일 (Data file)
- MYI: Index 정보 파일(Index file)
  -> 사용자가 쿼리를 통해 Index를 사용하는 칼럼 검색 시 MYI 파일 활용
  <br><br>

<br>

---

<br>

### **장점**

- 검색과 정렬 속도 향상
- 테이블 행의 고유성 강화

### **단점**

- 추가적인 공간 필요
- 데이터 변경(추가, 삭제, 업데이트 등) 시 index를 재작성해야 하므로 성능에 영향을 미침
- 한 페이지를 동시에 수정할 수 있는 병행성이 줄어듦 (record lock 문제)

<br><br>

**-> Index는 데이터의 저장 성능을 희생하고 읽기 속도를 높이는 기능이라고 할 수 있음**

<br>

---

<br>

### **Index를 사용하면 좋은 경우 & 나쁜 경우**

- 🙂

  - Where절에서 자주 사용되는 컬럼
  - 외래키가 사용되는 컬럼
  - Join에 자주 사용되는 컬럼

- ☹️
  - 데이터 중복도가 높은 컬럼(나타내는 데이터의 종류가 적은 경우)
  - DML(Data Manipulation Language)이 자주 사용되는 컬럼

<br>

---

<br>

### **Index가 DML에 취약한 이유**

- INSERT

  - idex split 현상이 발생할 수 있음
  - 기존 블록에 여유 공간이 없는데 INSERT가 발생하면 기존 블록의 내용 중 일부를 새 블록에 기록한 후 기존 블록의 빈 공간에 새 데이터를 추가하는 작업 수행
  - 작업 수행 시간 동안 해당 블록의 키 값이 변경되면 안되므로 DML이 블로킹 됨 -> 대기 이벤트 발생

- DELETE
  - 삭제된 데이터에 해당되는 index는 삭제되지 않고 '사용 안 함'으로 표시됨
  - 데이터를 삭제하는 게 아니기 때문에 인덱스의 메모리는 줄지 않고 유효한 데이터보다 많은 데이터들이 인덱스에 존재할 수 있음
  - ex. 처음에 10만 개의 데이터에 해당되는 10만 개의 인덱스가 있었는데 5만 개의 데이터를 삭제하고 다시 5만 개의 새 데이터를 추가한 경우 인덱스는 총 15만 개(원래의 10만 개+추가된 5만 개)로 늘어나게 됨
  - 인덱스를 사용해도 수행 속도의 향상을 기대하기 어려움
- UPDATE
  - Index에는 UPDATE 기능이 없음 -> DELETE + INSERT 로 수행
  - 2개의 작업이 전부 일어나기 때문에 큰 부하를 주게 됨

<br>

---

<br>
  
  ### **Index 자료구조**
  
  - B+-Tree : 칼럼의 값을 변형하지 않고 원래의 값을 이용해 인덱싱하는 알고리즘
  - Hash : 칼럼의 값으로 해시 값을 계산해서(값을 변형) 인덱싱하는 알고리즘
  - 속도는 Hash 인덱스 알고리즘이 더 빠르지만 등호(=)연산이 아닌 부등호(<>) 연산의 경우 문제 발생
<br>

---

<Br>
  
  ### **Primary Index vs Secondary Index**
  
  - Primary Index (≒ Clustered Index)
    - 테이블 당 한 개만 생성 가능(primary key에 대해서만 적용되기 때문)
    - 저장할때 물리적으로 정렬하여 저장 
    - leaf level의 인덱스가 필요하지 않음
    - primary key 값이 변경되면 저장 위치 또한 변경되어야 하기 때문에 신중한 결정 필요
    - 용량을 적게 차지
    <br>
    <img width="600" alt="image" src="https://user-images.githubusercontent.com/66426083/158330846-6e514ba3-1529-422b-875c-7e705f8ef82c.png">
      <br>
      - Dense Index
      <br><br>
      <image width=400 src="https://user-images.githubusercontent.com/66426083/158326388-95cbbbdc-b8f5-4f2c-8726-a42262f061bc.png" />
      <br><br>
      - Sparse Index
      <br><br>
      <image widht=400 src="https://user-images.githubusercontent.com/66426083/158326481-63de04f7-6597-4dfe-b80e-91cb3c3b6762.png" />
      <br><Br>

- Secondary Index (≒ Non-Clustered Index)

  - primary key 이외의 값으로 만든 인덱스
  - 테이블당 여러 개 생성 가능
  - 기존 데이터를 재정렬하지 않고 별도의 공간에 테이블을 생성해 데이터를 정렬
  - 클러스터드 인덱스에 비해 용량 차지
  - root, leaf, data page로 구성
    <br><br>
    <img width="600" alt="image" src="https://user-images.githubusercontent.com/66426083/158332208-ca71e093-f670-4736-9cf6-fb664ad9265a.png">

    <br><br>
    <image width=400 src="https://user-images.githubusercontent.com/66426083/158326699-3c90f76b-e0ad-47b6-a5dd-f57bc443c0ec.png" />

<br>
  <br>
  <br>
  참고  https://sorjfkrh5078.tistory.com/71 / https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/%5BDB%5D%20Index.md / https://www.guru99.com/indexing-in-database.html#2 / https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Database#index / https://dbknowledge.tistory.com/46
