# **Array vs ArrayList vs LinkedList**

- **Array**는 index로 빠르게 값을 찾는 것이 가능함
- **ArrayList**는 데이터를 찾는데 빠르지만, 삽입 및 삭제가 느림
- **LinkedList**는 데이터의 삽입 및 삭제가 빠름

---

## Array(배열)

- 원소의 주소 연속적으로 할당 (index)
    - 메모리 공간에 할당할 사이즈를 미리 정해놓고 사용 → 크기 제한 O
        - 선언 시 크기와 데이터 타입 지정
            - `int arr[10];
            String arr[5];`
- **index**로 위치 검색에 편함. `O(1)` → random access 가능
- 데이터 삽입, 삭제가 비효율적 `O(N)`
    - 4번째 index 값에 새로운 값을 넣어야 한다면? 원래값을 뒤로 밀어내고 해당 index에 덮어씌워야 → 사이즈를 정해놓은 배열에서 해결하기엔 부적합한 점이 많음
    - 해당 원소에 접근한 후, shift하는 비용 발생
    - 계속 데이터가 늘어날 때, 최대 사이즈를 알 수 없을 때는 사용에 부적합

---

## **List**

- 노드들의 연결로 이뤄짐. 원소들을 일렬로 정렬해 놓은 것.
- 크기 제한 X
- 다음 노드에 대한 참조를 통해 접근 `O(N)`

---

## Array List

- Array 형태로 만든 리스트
- 동적으로 크기 조절되는 배열
- 배열이 가득 차면 알아서 크기를 2배로 할당하고 복사 수행 (재할당 `O(N)`)
- 접근시간 `O(1)`
    - index로 원하는 위치에 직접 접근 가능
- 삽입/삭제 시 연속성 보장 위해 나머지 값을 전부 shift해줘야
- 데이터가 예측 가능할 때 사용, 보편적으로 사용.
    
      

---

## **Linked List(연결 리스트)**

- 연결리스트: 각 노드가 연결돼있는 방식으로 데이터가 저장돼있는 추상적 자료형
- 한 노드는 해당 노드의 실제값(value)과 다음 노드의 주소값이 담긴 포인터(pointer)로 구성
    - 단일연결리스트(singly linked list)는 뒤의 노드만 가리킴
    - 이중연결리스트(doubly linked list)는 앞뒤 노드를 모두 가리킴
    - 원형 연결 리스트 (circular linked list)는 마지막 노드의 링크가 다시 첫 번째 노드를 가리킴
- 포인터 덕분에 리스트 길이를 미리 정할 필요 x
    - 삽입, 삭제 시 포인터만 바꾸면 돼서 빠르게 가능
- List의 k번째 값을 찾을 때는 비효율적
    - 검색/삽입/삭제 시 원하는 위치를 첫 번째 원소부터 따라가며 탐색해야 함 `O(N)`
- array나 arrayList에서 index를 갖고 있기 때문에 검색이 빠르지만, LinkedList는 처음부터 살펴봐야하므로(순차) 검색에 있어서는 시간이 더 걸린다는 단점이 존재
- 차례대로 읽을 때, 불규칙적으로 추가하거나 끊을 일이 많을 때 ^^

---

|  | Array List | Linked List |
| --- | --- | --- |
| 형태 | array 형식 → index 가짐 | 각 노드가 연결됨 |
| 크기 | 동적으로 조절 (배열 가득 차면 2배 → 공간 낭비 존재) | 리스트 길이 미리 정할 필요 x, 필요할 때 포인터 바꿔주며 해당 원소 크기만큼만 할당 |
| 접근 시간 | O(1) | O(N) |
| 탐색 | index 사용, 쉽게 접근 가능😀 | 첫 번째 원소부터 순차 탐색 필요😢 |
| 삽입/삭제 | 나머지 값을 shift 해줘야 함😢 | 포인터만 바꿔주면 됨😀 |

---

참고 링크

- [ratsgo’s blog](https://ratsgo.github.io/data%20structure&algorithm/2017/09/30/list/)
- [interview_Question_for_Beginner](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure#array-vs-linked-list)
- [tech-interview-for-developer](https://github.com/gyoogle/tech-interview-for-developer/tree/master/Computer%20Science/Data%20Structure)
- <자료구조와 C>, 이석호