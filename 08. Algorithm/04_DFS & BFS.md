### ⏩ 트리의 순회

그래프 알고리즘으로, 문제를 풀 때 상당히 많이 사용한다. <br>

경로를 찾는 문제 시, 상황에 맞게 DFS와 BFS를 활용하게 된다. <br>

### ⏩ 트리 너비 우선 검색 구현 (Breadth-first Search)

- 루트 노드 또는 임의 노드에서 인접한 노드부터 먼저 탐색하는 방법이다.
- 큐를 통해 구현한다. (해당 노드의 주변부터 탐색해야하기 때문)
- 최소 비용(즉, 모든 곳을 탐색하는 것보다 최소 비용이 우선일 때)에 적합하다.


```python
class BinarySearchTree(object):
    def breadthfirst(self, node):
        q = []
        q.append(node)
        while q:
            cur_node = q.pop(0)

            print(cur_node.data, end=' ') # Processing for data
            
            if cur_node.left != None:
                q.append(cur_node.left)
            if cur_node.right != None:
                q.append(cur_node.right)

array = [11, 5, 4, 7, 1, 6, 9, 15, 13, 18, 12, 14]

bst = BinarySearchTree()
for x in array:
    # bst.insert(x)
    bst.insert(x)
    
bst.breadthfirst(bst.root)
```

- 자식 넣고 루트를 지우는 방식
- 트리는 중복을 생각할 필요가 없다
<br>

### ⏩ 트리 깊이 우선 검색 (Depth-first Search

<img width="671" alt="Untitled (6)" src="https://user-images.githubusercontent.com/61955796/167764732-728ff489-a4aa-4f4a-885f-be36fd17bf0c.png">

- 루트 노드 혹은 임의 노드에서 다음 브랜치로 넘어가기 전에, 해당 브랜치를 모두 탐색하는 방법이다.
- 스택 or 재귀함수를 통해 구현한다.
- 모든 경로를 방문해야 할 경우 사용에 적합하다.

```python
class BinarySearchTree(object):
    def everyorder(self, node):
        if node != None:
            print(node.data, end = ' ') #node를 지날 때마다 출력하는 코드

            if node.left:
                self.everyorder(node.left) 

            print(node.data, end = ' ') #node를 지날 때마다 출력하는 코드

            if node.right:
                self.everyorder(node.right)

            print(node.data, end = ' ') #node를 지날 때마다 출력하는 코드

array = [11, 5, 4, 7, 1, 6, 9, 15, 13, 18, 12, 14]

bst = BinarySearchTree()
for x in array:
    # bst.insert(x)
    bst.insert(x)

bst.everyorder(bst.root)
```

- 3번 패스 (자식이 2) - 떨어져서 3번
- 2번 패스 (자식이 1) - 연속 2번, 떨어져서 1번
- 1번 패스 (말단노드) - 연속 3번

가장 먼저 나온 숫자만 고르면 → 전위 순회

두 번째 나온 숫자만 고르면 → 중위 순회

마지막으로 나온 숫자만 고르면 → 후위 순회
<br>

### ⏩ 전위, 중위, 후위

<img width="677" alt="Untitled (7)" src="https://user-images.githubusercontent.com/61955796/167764767-f0e75204-ba5f-41f1-8087-deb394ab0354.png">

- 전위 순회 (pre-order) : 루트 먼저 방문하는 방식 : root -> left -> right
- 중위 순회 (in-order) : 왼쪽 하위 트리 방문 후 루트를 방문하는 방식 : left -> root -> right
- 후위 순회 (post-order) : 왼쪽 하위 트리부터 모두 방문 후 루트 방문하는 방식 : left -> right -> root

<img width="689" alt="Untitled (8)" src="https://user-images.githubusercontent.com/61955796/167764775-6dca9831-0c5f-4134-98b7-2554fb4735a5.png">

```python
class BinarySearchTree(object):
    # 전위 순회
    def preorder(self, node):
        if node != None:
            print(node.data, end = ' ')

            if node.left:
                self.preorder(node.left)
            if node.right:
                self.preorder(node.right)
    
    # 중위 순회
    def inorder(self, node):
        if node != None:
            if node.left:
                self.inorder(node.left)
            
            print(node.data, end = ' ')

            if node.right:
                self.inorder(node.right)
    
    #후위 순회
    def postorder(self, node):
        if node != None:
            if node.left:
                self.postorder(node.left)
            if node.right:
                self.postorder(node.right)
            
            print(node.data, end = ' ')
```
