1. python으로 이분탐색 알고리즘을 구현한 다음 코드를 완성하시오.

```python
def binary_search(target, data):
    data.sort()
    start = 0
    end = len(data) - 1
    count = 0

    while _____________:
        mid = (start + end) // 2

        if data[mid] == target:
            return mid # 함수를 끝내버린다.
        elif data[mid] < target:
            start = ________
        else:
            end = _______
        count++

    return None
```

2. 위에 작성한 코드의 target은 34, data 배열로 아래와 같은 배열을 넣었을 때 함수 종료 후 count의 값을 구하시오

<br><img src="https://velog.velcdn.com/images%2Fcrystalhwang16%2Fpost%2F47c58f74-1448-4575-a687-445f56647078%2F%EC%9D%B4%EC%A7%84%ED%83%90%EC%83%891.png" />
