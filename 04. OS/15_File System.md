<h2>파일 시스템</h2>

---

### 🍀 *개념*

컴퓨터 사용자가 응용 프로그램을 실행하면서 생성하는 정보를 ‘파일’이라는 단위로 저장 및 관리하는 운영체제의 서브 시스템

### 🍀 *특징*

- 커널 영역에서 동작한다.
- 파일의 CRUD를 원활히 수행하기 위한 목적이다.
- 계층적 디렉터리 구조를 가진다.
- 디스크 파티션마다 하나씩 가질 수 있다. (파티션 단위)
- 주기억장치와 보조기억장치 간의 파일 전송을 담당한다.
- 여러 사용자가 파일을 공유하여 사용할 수 있도록 한다.

### 🍀 *작업*

- 파일 단위 작업
    1. open: 파일을 사용할 수 있는 상태로 준비
    2. close: 파일의 변경된 내용을 저장하고 사용 권한을 종료
    3. copy: 새로운 파일 생성
    4. destroy: 파일명을 디스크에서 삭제
    5. rename: 파일명을 변경
    6. list: 디스크에 저장되어 있는 파일 목록 출력
    
- 레코드 단위 작업
    1. read: 데이터를 읽음
    2. write: 데이터를 기록
    3. update: 데이터를 갱신
    4. insert: 데이터를 추가
    5. delete: 데이터를 삭제
    6. search: 데이터를 검색

### 🍀 *접근 방법*

- **순차 접근 (Sequential Acess)**
    - 가장 간단한 접근 방법으로 대부분의 연산은 read, write로 이루어진다.
    
    <img width="720" alt="1" src="https://user-images.githubusercontent.com/61955796/161659098-1c59de34-605b-4db0-b63a-17e9ff4fd3bb.png">
    
    - 현재 위치를 가리키는 포인터에서 시스템 콜이 발생할 경우에 포인터를 앞으로 보내면서 read와 write를 진행한다.
    - 뒤로 돌아갈 땐 지정해둔 offset만큼 되감기를 한다.
    
- **직접 접근 (Direct Access)**
    - 특별한 순서 없이 빠르게 레코드를 read, wirte할 수 있다.
    
    <img width="712" alt="2" src="https://user-images.githubusercontent.com/61955796/161659119-d2f0c918-5643-4aa3-9871-d8c339fecb5d.png">
    
    - 현재 위치를 가리키는 cp 변수만 유지하면 직접 접근 파일을 가지고 순차 파일 기능을 구현할 수 있다.
    - 무작위 파일 블록에 대한 임의의 접근을 허용하기에 순서의 제약이 없다.
    - 대규모 정보에 접근할 때 유용하기 때문에 데이터베이스에 활용된다.
    
- **기타 접근**
    - 직접 접근 파일에 기반하여 색인을 구축하는 방법이다.
    
    <img width="728" alt="3" src="https://user-images.githubusercontent.com/61955796/161659144-aae9b74d-3c4c-4cb3-b783-4a29e80caf7e.png">
    
    - 크기가 큰 파일을 입출력 탐색할 수 있게 도와주는 방법이다.

### 🍀 *디렉터리와 디스크 구조*

- **디렉터리란?**
    - 파일 시스템 내부에 있으며 디스크에 존재하는 파일에 대한 정보를 가지고 있는 테이블이다.
    - 각 파일의 위치, 크기, 할당 방식, 형태, 소유자 등의 정보를 가진다.
    
- **1단계 디렉터리 (단일 디렉터리)**
    - 모든 파일이 같은 디렉터리에서 관리되는 가장 간단한 구조이다.
    - 모든 파일이 유일한 이름을 가져야 하며 다른 사용자라도 같은 이름 사용이 불가하다.
    - 다수의 사용자가 사용하거나 파일의 수가 증가할 때 관리가 어렵다.
    
    <img width="846" alt="4" src="https://user-images.githubusercontent.com/61955796/161659161-30da63f2-d97b-410c-8833-218ed6eee1f4.png">

- **2단계 디렉터리**
    - 중앙에 마스터 파일 디렉터리(MFD)가 있고 그 아래에 각 사용자에게 할당하는 디렉터리(UFD)가 있는 구조
    - 각 사용자에게 서로 다른 디렉터리를 할당한다.
    - 사용자는 각자 디렉터리를 가지므로 다른 사용자와 같은 이름의 파일을 소지할 수 있다.
    - 사용자마다 디렉터리가 독립적이기 때문에 파일을 공유할 수 없다.
    
    <img width="915" alt="5" src="https://user-images.githubusercontent.com/61955796/161659176-a8455a0f-ee35-48ae-8a81-8c828d3ad5a5.png">
    
- **트리 구조 디렉터리**
    - 2단계에서 확장된 다단계 트리 구조
    - 하나의 루트 디렉터리와 여러 개의 서브 디렉터리로 구성된다.
    - 디렉터리 생성 및 삭제가 용이하다.
    - 파일 및 디렉터리 탐색은 절대 경로와 상대 경로를 이용한다.
        - 절대 경로: 루트 디렉터리를 기준으로 함
        - 상대 경로: 현재 디렉터리를 기준으로 함
    
    <img width="774" alt="6" src="https://user-images.githubusercontent.com/61955796/161659195-1cd8a69c-d110-40c2-b408-8982bc2dcfd2.png">
    
- **그래프 구조 디렉터리**
    - 순환이 발생하지 않도록 하위 디렉터리가 아닌 파일에 대한 링크만 허용한다.
    - 가비지 컬렉션을 이용해서 전체 파일 시스템을 순회하고 접근 가능한 모든 것을 표시한다.
        - 가비지 컬렉션: 제거된 파일의 디스크 공간 확보를 위해 사용
    - 파일이나 디렉터리 공유가 가능하다.
    
    <img width="773" alt="7" src="https://user-images.githubusercontent.com/61955796/161659211-e7367f45-e324-47e6-b86a-d30807e72251.png">
