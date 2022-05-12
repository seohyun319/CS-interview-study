## LIS ****(Longest Increasing Sequence)****

> 원소가 n개인 배열의 일부 원소를 골라내서 만든 부분 수열 중, **각 원소가 이전 원소보다 크다는 조건**을 만족하고, 그 **길이가 최대인 부분 수열**을 최장 증가 부분 수열이이라고 한다.
> 

- 예를 들어, { 6, **2**, **5**, 1, **7**, 4, **8**, 3} 이라는 배열이 있을 경우, LIS는 { 2, 5, 7, 8 } 이다.
- { 2, 5 }, { 2, 7 } 등 증가하는 부분 수열은 많지만 그 중에서 가장 긴 것이 { 2, 5, 7, 8 } 이다.
- DP(동적 계획법)를 활용할 경우 시간 복잡도는 O(n^2)이다.
- 입력값이 너무 많아서 이분탐색을 활용할 경우 시간 복잡도는 O(n log n)이 된다.

```python
n = int(input())  # 수열의 길이
array = list(map(int, input().split()))  # 주어진 수열

# DP 테이블 1로 초기화
dp = [1] * n

for i in range(1, n):
    for j in range(0, i):
        if array[j] < array[i]:
            dp[i] = max(dp[i], dp[j] + 1)

# 가장 긴 증가하는 부분 수열의 길이값
result = max(dp)
print(result)
```

[참고]

[https://chanhuiseok.github.io/posts/algo-49/](https://chanhuiseok.github.io/posts/algo-49/)

[https://techblog-history-younghunjo1.tistory.com/295](https://techblog-history-younghunjo1.tistory.com/295)
