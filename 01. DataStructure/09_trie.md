# Trie

> 검색(retrieval)의 줄임말로 **각각의 노드가 배열로 이루어진** 트리

문자열 탐색 시 O(1)의 시간복잡도를 가져 효율적이며, 이름이나 단어를 찾는 데 일정한 실행 시간을 가진다.  

C언어에서는 boolean 연산식으로 끝이 나는 배열을 표시할 수 있다.    
<br>

--------------------------  

## Trie 사용 예시
![image](https://user-images.githubusercontent.com/65678579/157280827-e05a1ae4-4683-4077-a6d4-c5d11301adf8.png)
> Hagrid, Harry, Hermionie의 이름을 trie에 저장한 예시 그림



* Hagrid, Haryy, Hermionie는 H를 공유하여 최소 하나의 노드를 나누어 가진다.

* 이 자료구조에서 n명의 사람이 있을 때 특정한 사람을 찾기 위해 걸리는 시간은? -> n

* 특정 문자열을 찾을 때는 해당 문자열만 보기 때문에 시간 복잡도는 상수가 된다.   

<br> 

예를 들어 Harry를 찾는 경우, H A R R Y 를 탐색하기 때문에 O(5)라고 할 수 있다.

따라서 문자열의 고정된 상한 값 만큼의 실행 시간을 가진다. -> 시간복잡도는 O(1)이 됨.

<br>


단점은 빠른 실행 즉, 상수 시간의 실행 시간을 제공하기 위해 과도한 메모리를 사용해야 한다.  

위 예시에서는 하나의 글자를 저장하기 위해 26배의 메모리를 사용함.

<br>
<br>


### 📝 관련 문제   
[14425](https://www.acmicpc.net/problem/14425) 
[5052](https://www.acmicpc.net/problem/5052)

<br> 

### 🔗참고링크  
[Link](https://www.boostcourse.org/cs112/lecture/119043?isDesc=false)

