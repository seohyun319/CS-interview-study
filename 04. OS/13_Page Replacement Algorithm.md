
# **페이지 교체 알고리즘**

 페이지 부재 발생 → 새로운 페이지를 할당해야 함 → 현재 할당된 페이지 중 어떤 걸 교체할 지(기존에 있던 거 버리고 그 자리에 할당) 결정하는 방법
 
- 가상 메모리 - `요구 페이지 기법`으로 필요한 페이지만 메모리에 적재하고 사용하지 않는 부분은 그대로 둠
- 근데 필요한 페이지만 올려도 메모리는 결국 가득 차게 되고, 올라와있던 페이지가 사용이 다 된 후에도 자리만 차지하고 있을 수 있음
- 메모리가 가득 차면, 추가로 페이지를 가져오기 위해서 안쓰는 페이지는 out하고, 해당 공간에 현재 필요한 페이지를 in 시켜야 함
- 어떤 페이지를 out시킬 지 정해야... ⇒ 페이지 교체 알고리즘에 따라 상황에 맞는 페이지를 교체!
    
    > 기왕이면 수정이 되지 않는 페이지를 선택해야 좋음 (Why? : 만약 수정되면 메인 메모리에서 내보낼 때, 하드디스크에서 또 수정을 진행해야 하므로(수정 상황 반영해줘야함) 시간이 오래 걸림)
    > 

1. **FIFO 알고리즘**
    
    > First-in First-out, 메모리에 먼저 올라온 페이지를 먼저 내보내는 알고리즘
    > 
    - victim page : 가장 먼저 메모리에 올라온 페이지.
    - 가장 간단한 방법으로, 특히 초기화 코드에서 적절한 방법
        - `초기화 코드` : 처음 프로세스 실행될 때 최초 초기화를 시키는 역할만 진행하고 다른 역할은 수행하지 않으므로, 메인 메모리에서 빼도 괜찮음
        - 하지만 처음 프로세스 실행시에는 무조건 필요한 코드이므로, FIFO 알고리즘을 사용하면 초기화를 시켜준 후 가장 먼저 내보내는 것이 가능
    
            <img src="https://user-images.githubusercontent.com/76686872/161933121-4f1106a7-db5c-4631-bcd1-a34e2261a731.png" width="500"/>
    
2. **OPT 알고리즘**
    
    > Optimal Page Replacement 알고리즘, 앞으로 가장 오랫동안 사용하지 않을 페이지를 가장 우선적으로 내보냄
    > 
    - FIFO에 비해 페이지 결함의 횟수를 많이 감소시킬 수 있음
    - 하지만, 실질적으로 페이지가 앞으로 잘 사용되지 않을 것이라는 보장이 없기 때문에 (미래에 대한 정확한 지식 없음) 수행하기 어려운 알고리즘임
    
        <img src="https://user-images.githubusercontent.com/76686872/161933121-4f1106a7-db5c-4631-bcd1-a34e2261a731.png" width="500"/>
    
3. **LRU 알고리즘**
    
    > Least-Recently-Used, 최근에 사용하지 않은(현재 기준 가장 오랫동안 참조되지 않은) 페이지를 가장 먼저 내보내는 알고리즘
    > 
    - 최근에 사용하지 않았으면, 나중에도 사용되지 않을 것이다
    - OPT의 경우 미래 예측이지만, LRU의 경우는 과거를 보고 판단하므로 실질적으로 사용이 가능한 알고리즘
    - OPT보다는 페이지 결함이 더 일어날 수 있지만, **실제로 사용할 수 있는 페이지 교체 알고리즘에서는 가장 좋은 방법 중 하나임**
    
        <img src="https://user-images.githubusercontent.com/76686872/161933162-c3a5c909-f202-42a7-bfe8-63adcb976ab8.png" width="500"/>
    

---

## **교체 방식**

다중 프로그래밍의 경우, 메인 메모리에 다양한 프로세스가 동시에 올라올 수 있음 → 메모리에 다양한 프로세스의 페이지가 존재

- Global 교체: 메모리 상의 모든 프로세스 페이지에 대해 교체하는 방식
- Local 교체: 메모리 상의 자기 프로세스 페이지에서만 교체하는 방식
    
    → 실제로는 전체를 기준으로 페이지를 교체하는 것이 더 효율적이라고 함. 자기 프로세스 페이지에서만 교체를 하면, 교체를 해야할 때 각각 모두 교체를 진행해야 하므로 비효율적