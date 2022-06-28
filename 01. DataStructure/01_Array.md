## Array 배열

<br/>

### 1. 사이즈 구하기


  ```c
  int arr[] = { 1, 2, 3, 4, 5, 6, 7 }; 
  int n = sizeof(arr) / sizeof(arr[0]); // 7
  ```
  
  <br/>
  
  java
  ```java
  int arr[] = { 1, 2, 3, 4, 5, 6, 7 }; 
  int n1 = arr.length;;
  
  List<Integer> list = new ArrayList<Integer>();
  int n2 = list.size();
  ```
  
  <br/>
  
  python 
  ```python
  food = [ "자장면", "짬뽕", "탕수육", "물만두", "팔보채" ]
  n = len(food)
  ```

  <br/>

### 2. 배열 회전 프로그램

회전이라는것이 맨 앞 요소를 맨 뒤로 한칸씩 빼서 넣어준다는것을 의미한다. 우리가 흔히 아는 temp 변수를 사용한 Swap을 이용해 구현한다.
<image src ="https://shoark7.github.io/assets/img/algorithm/rotate-right.png" />

#### 2.1 배열 슬라이싱
  > 파이썬은 배열이 기본적으로 슬라이싱 인덱스를 지원한다. 슬라이싱은 원 배열에서 0개 이상의 원소를 갖는 부분 배열을 추출해내는 것을 말하며 가령 arr 의 1번째부터 3번째 원소까지를 슬라이싱 하려면 다음과 같이 입력하면 된다.
  
  <br/>
  
  ```python
  def rotate(arr, n):
    # 1.
    if not arr:
        return arr
    n %= len(arr)
    if not n:
        return arr

    # 2.
    left = arr[:-n]
    right = arr[-n:]  

    # 3.
    return right + left

  >>> rotate([1, 2, 3, 4, 5], 2)

  [4, 5, 1, 2, 3]
  ```
  
#### 2.2 배열 값 이동
  > 새 배열을 만들어 원 배열의 i 번째 인덱스의 값을 새 배열의 i+n 인덱스에 집어넣는다. 이때 i+n 이 배열의 길이를 넘길 수 있기 때문에 배열의 길이만큼 나머지 연산을 한다.
  
  <br/>
  
  ```python
  def rotate(arr, n):
    if not arr:
        return arr
    N = len(arr)
    n %= N
    if not n:
        return arr
    new_arr = [None for _ in range(N)]

    for i in range(N):
        new_arr[(i+n) % N] = arr[i]
    return new_arr

  >>> rotate([1, 2, 3, 4, 5], 2)

  [4, 5, 1, 2, 3]
  ```
  
#### 2.3 저글링(Juggling)

  <br/>
  
  > 배열을 arr 이라고 할 때 arr[0] 을 T 라는 변수에 저장한다. 그리고 인덱스를 0에서 회전 횟수 n(여기서는 3) 만큼씩 키워가면서, 3번째는 0번째로, 6번째는 3번째로, 9번째는 6번째로 값을 옮긴다. 9에 3을 더한 12는 배열의 마지막 인덱스 11을 초과하기 때문에 멈춘 후 9번째 인덱스에 아까 저장한 T 값을 옮긴다. 그러면 한 사이클이 끝났다. 
  > 
  > 사이클은 총 n 번만큼 진행하게 되며 사이클을 모두 마치면 최종적으로 n 만큼 왼쪽으로 회전하게 된다.

  <br/>
  
  <image src="https://camo.githubusercontent.com/67cbcc777f2456f8dccc00cdd2d2ecc274ce942f32751df5c71aaa000a33c8e7/68747470733a2f2f63646e636f6e747269627574652e6765656b73666f726765656b732e6f72672f77702d636f6e74656e742f75706c6f6164732f617272612e6a7067" />
    
  <br/>
  
  ```python
    def rotate(arr, n):
      # 1. Base case 검사 - 배열이 비었거나, 길이로 모듈로한 회전횟수가 0이면 그대로 반환한다. 연산할 이유가 없다.
      if not arr:
          return arr
      N = len(arr)
      n %= N
      if n == 0:
          return arr

      # 2. 길이가 회전 횟수의 배수일 때 - n 번의 사이클이 생기기 때문에 그만큼 반복문을 돌린다. 앞의 원소들을 차례로 앞으로 옮기면 마지막으로 last 원소에 아까 저장한 T 를 집어넣는다.
      elif N % n == 0:
          for last in range(n):
              start = N - n + last
              T = arr[start]
              s = start
    
              while s - n >= 0:
                  arr[s] = arr[s-n]
                  s -= n
              arr[last] = T
      # 3. 배수가 아닐 때 - 첫 원소의 인덱스를 0으로 잡은 뒤, 그때부터 n 씩 왼쪽 원소를 오른쪽으로 옮긴다. 이때 길이 N 만큼 모듈로를 쓴다.
      else:
          s = 0
          T = arr[s]
          for _ in range(N-1): # 아까 저장한 T 를 갖다 쓸 것이기 때문에 N에서 1을 빼준다
              arr[s] = arr[(s-n) % N]
              s = (s-n) % N
          arr[s] = T
      return arr

    
    >>> rotate([1, 2, 3, 4, 5, 6, 7, 8, 9], 3)
    >>> rotate([1, 2, 3, 4, 5], 2)
  ```
    
  <br/>
  
#### 2.3 역전 알고리즘 = 반전에 반전(Reverse the reversed)
  > 회전시키는 수에 대해 구간을 나누어 reverse로 구현하는 방법
  
  <br/>
  
  > ** 과정 **
  >   
  > 
  >   1. 배열을 뒤집는 reverse 함수를 만든다.
  >   
  >     리턴값이 리스트인 reverse 함수 생성
  >       
  >   2. 원 배열을 좌우 부분으로 나눈다.
  >   
  >     슬라이싱을 사용하지 않았다. 어려울 것은 없지만 왼쪽을 만드는 for 의 범위가 ‘N-n’이고, 오른쪽을 만드는 범위가 ‘N-n, N’인 것만 확인하면 된다.
  >     
  >   3. 반전된 좌우를 합친 반전 배열 전체를 다시 한 번 반전해서 원하는 결과를 만든다.
  >   
  >     이는 앞서 확인한 알고리즘을 그대로 구현했다. 그렇기 때문에 값은 옳게 나온다.
  
  <br/>
  
  ```python
  # 1.리턴값이 리스트인 reverse 함수 생성
  def reverse(arr):
    new_arr = []
    n = len(arr)
    for i in range(n):
        new_arr.append(arr[n-1-i])
    return new_arr


  def rotate(arr, n):
    if not arr:
        return arr
    N = len(arr)
    n %= N
    if not n:
        return arr
    right, left = [], []

    # 2.
    for i in range(N-n):
        left.append(arr[i])
    for i in range(N-n, N):
        right.append(arr[i])

    left_rev = reverse(left)
    right_rev = reverse(right)

    # 3.
    return reverse(left_rev + right_rev)


  >>> rotate([1, 2, 3, 4, 5], 2)

  [4, 5, 1, 2, 3]
  ```
  
  <br/>

### 3. 활용 문제
  3.1 #### 배열의 특정 최대 합 구하기



  **예시)** arr[i]가 있을 때, i*arr[i]의 Sum이 가장 클 때 그 값을 출력하기 
  
  (회전하면서 최대값을 찾아야한다.)

  ```
  Input: arr[] = {1, 20, 2, 10}
  Output: 72
  
  2번 회전했을 때 아래와 같이 최대값이 나오게 된다.
  {2, 10, 1, 20}
  20*3 + 1*2 + 10*1 + 2*0 = 72
  
  Input: arr[] = {10, 1, 2, 3, 4, 5, 6, 7, 8, 9};
  Output: 330
  
  9번 회전했을 때 아래와 같이 최대값이 나오게 된다.
  {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
  0*1 + 1*2 + 2*3 ... 9*10 = 330
  ```
  
  <br/>
  
  ##### 접근 방법
  
  arr[i]의 전체 합과 i*arr[i]의 전체 합을 저장할 변수 선언

  최종 가장 큰 sum 값을 저장할 변수 선언

  배열을 회전시키면서 i*arr[i]의 합의 값을 저장하고, 가장 큰 값을 저장해서 출력하면 된다.

  <br/>

  ##### 해결법

  ```
  회전 없이 i*arr[i]의 sum을 저장한 값
  R0 = 0*arr[0] + 1*arr[1] +...+ (n-1)*arr[n-1]
  

  1번 회전하고 i*arr[i]의 sum을 저장한 값
  R1 = 0*arr[n-1] + 1*arr[0] +...+ (n-1)*arr[n-2]

  이 두개를 빼면?
  R1 - R0 = arr[0] + arr[1] + ... + arr[n-2] - (n-1)*arr[n-1]
  
  2번 회전하고 i*arr[i]의 sum을 저장한 값
  R2 = 0*arr[n-2] + 1*arr[n-1] +...+ (n?1)*arr[n-3]
  
  1번 회전한 값과 빼면?
  R2 - R1 = arr[0] + arr[1] + ... + arr[n-3] - (n-1)*arr[n-2] + arr[n-1]
  
  
  여기서 규칙을 찾을 수 있음.
  
  Rj - Rj-1 = arrSum - n * arr[n-j]
  
  이를 활용해서 몇번 회전했을 때 최대값이 나오는 지 구할 수 있다.
  ```
  
  [구현 소스 코드 링크](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/code/maxvalue_array.cpp)

  <br/>
  
  <br/>
  
  3.2. #### 특정 배열을 arr[i] = i로 재배열 하기
  
  **예시)** 주어진 배열에서 arr[i] = i이 가능한 것만 재배열 시키기
  
  ```
  Input : arr = {-1, -1, 6, 1, 9, 3, 2, -1, 4, -1}
  Output : [-1, 1, 2, 3, 4, -1, 6, -1, -1, 9]
  
  Input : arr = {19, 7, 0, 3, 18, 15, 12, 6, 1, 8,
                11, 10, 9, 5, 13, 16, 2, 14, 17, 4}
  Output : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 
           11, 12, 13, 14, 15, 16, 17, 18, 19]
  ```
  
  arr[i] = i가 없으면 -1로 채운다.
  
  
  
  ##### 접근 방법
  
  arr[i]가 -1이 아니고, arr[i]이 i가 아닐 때가 우선 조건
  
  해당 arr[i] 값을 저장(x)해두고, 이 값이 x일 때 arr[x]를 탐색
  
  arr[x] 값을 저장(y)해두고, arr[x]가 -1이 아니면서 arr[x]가 x가 아닌 동안을 탐색
  
  arr[x]를 x값으로 저장해주고, 기존의 x를 y로 수정
  
  ```
  int fix(int A[], int len){
      
      for(int i = 0; i < len; i++) {
          
          
          if (A[i] != -1 && A[i] != i){ // A[i]가 -1이 아니고, i도 아닐 때
            
              int x = A[i]; // 해당 값을 x에 저장
              
              while(A[x] != -1 && A[x] != x){ // A[x]가 -1이 아니고, x도 아닐 때
                  
                  int y = A[x]; // 해당 값을 y에 저장
                  A[x] = x; 
                  
                  x = y;
              }
              
              A[x] = x;
              
              if (A[i] != i){
                  A[i] = -1;
              } 
          }
      }
      
  }
  ```

  [구현 소스 코드 링크](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/code/rearrange_array.cpp)
  
  <br/>
  
  <br/>
