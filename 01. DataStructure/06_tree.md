# Tree

* Tree의 개념
    - 데이터를 계층화한 자료구조
    - 비선형 자료구조, 계층적 자료구조
    - 노드(node)와 선분(edge)으로 이루어짐

* Tree를 이루는 구성요소
    - 노드: 트리를 구성하고 있는 각각의 요소
    - 간선: 요소와 요소를 잇는 선분
    - 루트 노드: 부모가 없는 최상위 노드
    - 단말 노드: 자식이 없는 말단 노드
    - 레벨: 루트 노드를 기준으로 특정 노드까지의 경로 길이
    - 깊이: 루트 노드에서 특정 노드에 도달하기 위한 간선의 수
    - 차수: 특정 노드에 연결된 자식 노드의 수

* Tree의 특징
    - 사이클이 없음
    - 노드가 n개면 간선은 n-1개
    - 구현할 때 인접 배열, 인접 리스트 이용
    - 임의의 두 노드간의 경로는 유일성을 지님

* Tree 순회 방식
    - 전위 순회 (pre-order)
        : 루트 먼저 방문하는 방식
        : root -> left -> right
    - 중위 순회 (in-order)
        : 왼쪽 하위 트리 방문 후 루트를 방문하는 방식
        : left -> root -> right
    - 후위 순회 (post-order)
        : 왼쪽 하위 트리부터 모두 방문 후 루트 방문하는 방식
        : left -> right -> root