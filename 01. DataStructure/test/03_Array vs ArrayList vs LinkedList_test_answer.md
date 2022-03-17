# **Data Structure - Array vs ArrayList vs LinkedList**
1. 원소 삽입 및 삭제가 비교적 빠른 자료구조는?
    
    LinkedList
    
2. arrayList와 linkedList의 차이점을 서술하세요. (형태, 접근 시간, 탐색 등)    
    
    |  | Array List | Linked List |
    | --- | --- | --- |
    | 형태 | array 형식 → index 가짐 | 각 노드가 연결됨 |
    | 크기 | 동적으로 조절 (배열 가득 차면 2배 → 공간 낭비 존재) | 리스트 길이 미리 정할 필요 x, 필요할 때 포인터 바꿔주며 해당 원소 크기만큼만 할당 |
    | 접근 시간 | ⁍ | ⁍ |
    | 탐색 | index 사용, 쉽게 접근 가능😀 | 첫 번째 원소부터 순차 탐색 필요😢 |
    | 삽입/삭제 | 나머지 값을 shift 해줘야 함😢 | 포인터만 바꿔주면 됨😀 |
