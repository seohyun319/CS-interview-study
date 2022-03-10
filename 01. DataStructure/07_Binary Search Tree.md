## 이진탐색트리 (Binary Search Tree)

<br>

- 탐색과 삽입, 삭제가 모두 가능하게끔 하기 위해 만든 자료구조
- 이진탐색(탐색 O(logN)) + 연결리스트(삽입, 삭제 O(1))

<br>

---

<br>

### **특징**

- 각 노드의 자식이 2개 이하
- 각 노드의 왼쪽 자식은 부모보다 작고, 오른쪽 자식은 부모보다 큼
- 중복된 노드가 없어야 함 (중복의 경우 노드에 count 값을 가지게 해 처리하는 게 호율적)
- 왼쪽, 오른쪽 서브 트리 모두 또한 이진탐색트리임
  <br><br>
  <img width=300 src="https://user-images.githubusercontent.com/66426083/157191153-87da9fc5-f816-44de-afd9-419071aee5f3.png"/>

<br>

---

<br>

### **순회방식**

중위순회 inorder (왼쪽-루트-오른쪽)

<br>

---

<br>

### **이진탐색트리 핵심연산**

- 검색
  - 트리의 높이가 h일 때 O(h)
- 삽입
  - 삽입 위치까지 찾아가는 연산 O(h)+ 삽입 연산 O(1) -> O(h)
- 삭제
  - 자식이 없는 노드인 경우 그냥 삭제
  - 자식이 1개인 노드인 경우 자식 노드의 값으로 대체
  - 자식이 2개인 노드인 경우 왼쪽 서브 트리의 최대값 or 오른쪽 서브 트리의 최소값 중 하나로 대체
    <br><br>
    <img width=600 src="https://user-images.githubusercontent.com/66426083/157184530-fa123c22-73bb-47c1-8fd6-56741f1053c8.png" />

<br>

---

<br>

### **시간 복잡도**

- 균등 트리: O(logN)
- 편향 트리: O(N)

_이진탐색트리의 시간복잡도는 최악의 경우 O(depth)인데, 시간복잡도는 원소의 개수(N)으로 표기해주는 것이 더 좋기 때문에 바꾸어 말하면 O(logN)이 됨._ <br><br>
_한 쪽으로만 편향된 트리의 경우 높이가 높아져 선형 연산에 가까워지기 때문에 비효율적임 -> 강제적으로 균형 이진 트리로 만들어줄 필요가 있음.
<br>
ex) AVL Tree, RedBlack Tree_

<br>
<br>
<br>
참고 https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Binary%20Search%20Tree.md#%EC%8B%9C%EA%B0%84-%EB%B3%B5%EC%9E%A1%EB%8F%84 / https://mommoo.tistory.com/101 / https://ratsgo.github.io/data%20structure&algorithm/2017/10/22/bst/
