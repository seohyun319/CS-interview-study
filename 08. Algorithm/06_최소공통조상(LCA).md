# **LCA(Lowest Common Ancestor)**

## LCA(Lowest Common Ancestor) 알고리즘

> 최소 공통 조상 찾는 알고리즘
>
> → 두 정점이 만나는 최초 부모 정점을 찾는 것!

트리 형식이 아래와 같이 주어졌다고 하자

<img src="https://user-images.githubusercontent.com/76686872/167837005-a9e00134-9713-4f55-9648-7eec92bb6f0a.png" width=400>

4와 5의 LCA는? → 첫 부모 정점은 '2'

4와 6의 LCA는? → 첫 부모 정점은 root인 '1'

<img src="https://user-images.githubusercontent.com/76686872/167837204-3587ad30-418d-4237-b72e-220a292dc131.png" width=450>

- 최소 공통 조상 알고리즘
  1. 모든 노드에 대한 깊이(depth)를 구함
  2. 최소 공통 조상을 찾을 두 노드 확인
     1. 두 노드의 깊이(depth)가 동일하도록 거슬러 올라감
     2. 부모가 같아질 때까지 반복적으로 두 노드의 부모 방향으로 거슬러 올라감.
  3. 모든 LCA(a, b) 연산에 대하여 2번의 과정을 반복
- 시간 복잡도 O(NM)
  - : 부모 방향으로 거슬러가는 최악의 경우 O(N) \* 모든 쿼리(M)
- 사용하는 상황:

  - 트리 문제에서 공통 조상을 찾아야하는 문제
  - 정점과 정점 사이의 이동거리 또는 방문경로를 저장해야 할 경우

  ```python
  import sys
  sys.setrecursionlimit(int(1e5)) # 런타임 오류를 피하기 위한 재귀 깊이 제한 설정

  n = int(input()) # 정점 개수

  parent = [0] * (n + 1) # 부모 노드 정보
  d = [0] * (n + 1) # 각 노드까지의 깊이
  c = [0] * (n + 1) # 각 노드의 깊이가 계산되었는지 여부
  graph = [[] for _ in range(n + 1)] # 그래프(graph) 정보

  for _ in range(n - 1):
      a, b = map(int, input().split())
      graph[a].append(b)
      graph[b].append(a)

  # 루트 노드부터 시작하여 깊이(depth)를 구하는 함수
  def dfs(x, depth):
      c[x] = True
      d[x] = depth # 노드에 대해 깊이값 기록
      for y in graph[x]: # 위의 노드와 인접한 노드값 하나씩 깊이 구함
          if c[y]: # 이미 깊이를 구했다면 넘기기
              continue
          parent[y] = x
          dfs(y, depth + 1) # 인접한 노드에 대해 현재깊이+1만큼을 구함

  # A와 B의 최소 공통 조상을 찾는 함수
  def lca(a, b):
      # 먼저 깊이(depth)가 동일하도록
      while d[a] != d[b]:
          if d[a] > d[b]:
              a = parent[a]
          else:
              b = parent[b]
      # 노드가 같아지도록
      while a != b:
          a = parent[a]
          b = parent[b]
      return a

  dfs(1, 0) # 루트 노드는 1번 노드

  m = int(input())

  for i in range(m):
      a, b = map(int, input().split())
      print(lca(a, b))
  ```

- 개선된 최소 공통 조상 알고리즘

  1. 모든 노드에 대한 깊이(depth)를 구함
  2. 모든 노드에 대한 $2^i$번째 부모 노드를 구함

     > 2의 제곱 형태로 점프하도록 해서 (거슬러올라가는 속도를 빠르게 만듦) 시간 복잡도를 O(logN)으로 만들어줌.

     > 메모리를 조금 더 사용함

  3. 최소 공통 조상을 찾을 두 노드 설정
     1. 두 노드의 깊이(depth)가 동일하도록 거슬러 올라감
     2. 최상단 노드부터 내려오는 방식으로 두 노드의 공통 부모를 찾아냄.
  4. 모든 LCA(a, b) 연산에 대하여 2번의 과정을 반복

- 시간복잡도 O(MlogN)
  - : 부모 방향으로 거슬러가는 최악의 경우 O(logN) \* 모든 쿼리(M)

<br />

---

<br />

참고 링크

- [이코테 강의](https://www.youtube.com/watch?v=O895NbxirM8)
- [깃허브](<https://github.com/gyoogle/tech-interview-for-developer/blob/master/Algorithm/LCA(Lowest%20Common%20Ancestor).md>)
