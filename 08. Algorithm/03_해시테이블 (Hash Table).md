##  해시테이블 (Hash Table)
> (Key, Value)로 데이터를 저장하는 자료구조 중 하나로 빠르게 데이터를 검색할 수 있는 자료구조이다.

### 정의
해시테이블은 각각의 Key값에 해시함수를 적용해 배열의 고유한 index를 생성하고, 이 index를 활용해 값을 저장하거나 검색한다.
<br><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb1zOw1%2FbtqL6HAW7jy%2FjpBA5pPkQFnfiZcPLakg00%2Fimg.png" /><br>

Key값으로 데이터를 찾을 때 해시 함수를 1번만 수행하면 되므로 매우 빠르게 데이터를 저장/삭제/조회할 수 있다. 해시테이블의 ***평균 시간복잡도는 O(1)*** 이다.

### 해시 함수의 종류
1. Division Method: 나눗셈을 이용하는 방법으로 입력값을 테이블의 크기로 나누어 계산한다.( 주소 = 입력값 % 테이블의 크기) 테이블의 크기를 소수로 정하고 2의 제곱수와 먼 값을 사용해야 효과가 좋다고 알려져 있다.
2. Digit Folding: 각 Key의 문자열을 ASCII 코드로 바꾸고 값을 합한 데이터를 테이블 내의 주소로 사용하는 방법이다.
3. Multiplication Method: 숫자로 된 Key값 K와 0과 1사이의 실수 A, 보통 2의 제곱수인 m을 사용하여 다음과 같은 계산을 해준다. h(k)=(kAmod1) × m
4. Univeral Hashing: 다수의 해시함수를 만들어 집합 H에 넣어두고, 무작위로 해시함수를 선택해 해시값을 만드는 기법이다.



### 예제 문제


<br><img src="https://kjhov195.github.io/post_img/200312/image2.png" /> <br>

<해결 방법>
python의 Dictionary를 활용하여 해결할 수 있다.
이때 key에 들어가는 값은 참가자의 이름이고 value에는 참가자의 등장횟수를 설정한 후 완주한 선수들의 목록을 차례로 돌며 value값을 -1 하면 된다. 

```python
def solution(participant, completion):
    dictionary = {}
    for key in participant:
        dictionary[key] = dictionary.get(key, 0) + 1
    for k in completion:
        dictionary[k] -= 1
    answer = [i for i in dictionary if dictionary[i] > 0]
    return answer[0]
```
위의 코드에서 시간 복잡도를 구해보면 
1. 처음 participant를 돌 때 O(n),
2. completion을 돌 때 O(n),
3. dictionary를 돌 때 O(n) 

이기 때문에 총 O(n)의 시간복잡도를 가지게 된다.

이렇게 해시 테이블을 사용하면 배열을 정렬하고나서 값을 찾아야하는 방법보다 훨씬 적은 시간이 든다.

### 자료 구조 선택 시 주의사항
> 숫자로 key 값이 주어졌다면 배열을 상요하는 것이 좋다. 왜냐하면 key 값이 겹칠 수 있기 때문이다
> <br> 위 문제에서는 key 값이 문자열이기 때문에 해시 테이블을 사용할 수 있었다.



