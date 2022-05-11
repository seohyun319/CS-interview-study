## 이분탐색
 
> 정렬되어있는 배열에서 탐색 범위를 절반씩 줄여나가며 찾는 Search 방법이다.
 
<br>

배열 정렬 후 진행 순서
1. 가운데 인덱스값인 mid 값을 구함
2. 구하는 값이 mid보다 높으면 : left = mid +1  /  구할 값이 mid보다 낮으면 : right = mid -1
3. left >right가 될 때까지 반복
<br><img width="600" alt="image" src="https://images.velog.io/images/ming/post/ab848f15-3998-4e61-b061-01458ad6f18d/%EC%9D%B4%EB%B6%84%ED%83%90%EC%83%89.png" ><br>
<br>

```java
public static int binarySearch(int[] array, int target){ 
 
    int start= 0; 
    int end= array.length-1; 
    int mid= (end+start)/2; 
 
    while(end-start>= 0){ 
        if(array[mid]== target){
            // target 값을 찾았을 때
            return mid; 
        }
        else if(array[mid]<= target){ 
            // target이 배열의 오른쪽에 존재할 때
            start= mid+1; 
        }
        else{ 
            // target이 배열의 왼쪽에 존재할 때
            end= mid-1; 
        } 
        mid= (end+start)/2; 
    } 
    // target 값을 찾을 수 없을 때
    return -1; 
}
```
