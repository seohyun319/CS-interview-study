# CPU Scheduling

---

## 스케줄링

***💗 스케줄링 개념***

- CPU를 사용하려고 하는 프로세스들 사이의 우선순위를 관리하는 작업이다.
- 처리율과 CPU 이용률을 증가시키고 오버헤드, 응답시간, 반환시간, 대기시간을 최소화하는 기법이다.
- 프로세스 사이에서 CPU 교체가 일어난다.

***💗 프로세스 상태 전이***

- **승인 (Admitted)**: 프로세스 생성이 가능해서 승인된 것
- **스케줄러 디스패치 (Scheduler Dispatch)**: 준비 상태에 있는 프로세스 중 하나를 선택하여 실행시키는 것
- **인터럽트 (Interrupt)**: 예외, 입출력, 이벤트 등이 발생하여 현재 실행 중인 프로세스를 준비 상태로 바꾸고 해당 작업을 먼저 처리하는 것
- **입출력 또는 이벤트 대기 (I/O or Event wait)**: 실행 중인 프로세스가 입출력이나 이벤트를 처리해야 하는 경우, 입출력/이벤트가 모두 끝날 때까지 대기 상태로 만드는 것
- **입출력 또는 이벤트 완료 (I/O or Event Completion)**: 입출력/이벤트가 끝난 프로세스를 준비 상태로 전환하여 스케줄러에 의해 선택될 수 있도록 만드는 것

***💗 스케줄링 주요 용어***

- **서비스 시간:** 프로세스가 결과를 산출하기까지 소요되는 시간
- **응답시간:** 프로세스들이 입력되어 서비스를 요청하고, 반응할 때까지 소요되는 시간
- **반환시간:** 프로세스들이 입력되어 수행하고 결과를 산출하기까지 소요되는 시간
    - 반환시간 = 대기시간 + 수행시간
- **대기시간:** 프로세스가 프로세서에 할당 대기까지 큐에 대기하는 시간
    - 만약 도착 즉시 할당되면 대기시간은 0이 된다.
- **평균 대기시간:** 프로세스가 대기 큐에서 대기하는 평균 시간
    - 대기시간이 0인 프로세스도 평균 대기시간에 합산하여 결과를 도출한다.
- **종료시간:** 요구되는 Processing time을 모두 수행하고 종료된 시간
- 시간 할당량: 한 프로세스가 프로세서를 독점하는 것을 방지하기 위해 서비스되는 할당량
- **응답률:** HRN (Highest Response ratio Next) 스케줄링에서 사용 (응답률이 높을수록 우선순위가 높다고 판단)
    - (대기시간 + 서비스 시간) / 서비스 시간
    

***💗 스케줄링 유형***

1. **선점형 스케줄링 (Preemptive Scheduling)**
    - 개념
        
        하나의 프로세스가 CPU를 차지하고 있을 때 우선순위가 높은 다른 프로세스가 현재 프로세스를 중단시키고 CPU를 점유하는 스케줄링 방식
        
    - 장점
        - 비교적 빠른 응답
        - 대화식 시분할 시스템에 적합
    - 단점
        - 높은 우선순위 프로세스들이 들어오는 경우 오버헤드 가능성
    - 알고리즘
        
        1) 라운드 로빈 (Round Robin)
        
        2) SRT (Shortest Remaining Time First)
        
        3) 다단계 큐 (Multi-Level Queue)
        
        4) 다단계 피드백 큐 (Multi-Level Feedback)
        
2. **비선점형 스케줄링 (Non Preemptive Scheduling)**
    - 개념
        
        한 프로세스가 CPU를 할당받으면 작업 종료 후 CPU 반환 시까지 다른 프로세스는 CPU 점유가 불가능한 방식
        
    - 장점
        - 응답시간 예상이 용이
        - 모든 프로세스에 대한 요구를 공정하게 처리
    - 단점
        - 짧은 작업을 수행하는 프로세스가 긴 작업 종료 시까지 대기해야 함
    - 알고리즘
        
        1) 우선순위 (Priority)
        
        2) 기한부 (Deadline)
        
        3) FCFS
        
        4) HRN (High Response Ratio Next)
        
        5) SJF (Shortest Job First)
        

***💗 선점형 스케줄링 알고리즘*** 

1. **라운드 로빈 (Round Robin)**
    - 같은 크기의 CPU 시간을 할당
    - 프로세스가 할당된 시간 내에 처리 완료를 못하면 준비 큐 리스트의 가장 뒤로 보냄
    - CPU는 대기 중인 다음 프로세스로 넘어감
    - 균등한 CPU 점유 시간
    - 시분할 시스템 사용
2. **SRT (Shortest Remaining Time First)**
    - 가장 짧은 시간이 소요되는 프로세스를 먼저 수행
    - 남은 처리 시간이 더 짧다고 판단되는 프로세스가 준비 큐에 생기면 프로세스 선점
    - 짧은 수행시간 프로세스 우선 수행
3. **다단계 큐 (Multi Level Queue)**
    
    ![Untitled (1)](https://user-images.githubusercontent.com/61955796/160862180-ffb59044-619a-4111-895d-940ebc4f6698.png)
    
    - 작업들을 여러 종류 그룹으로 분할
    - 여러 개의 큐를 이용하여 상위단계 작업에 의한 하위단계 작업이 선점 당함
    - 각 큐는 자신만의 독자적인 스케줄링을 가짐
    - 독립된 스케줄링 큐
4. **다단계 피드백 큐 (Multi Level Feedback Queue)**
    
    ![Untitled (2)](https://user-images.githubusercontent.com/61955796/160861935-3d277685-0571-4bba-bc5a-b7fd8a0c847d.png)
    
    - 입출력 위주와 CPU 위주인 프로세스의 특성에 따라 큐마다 서로 다른 CPU 할당량 부여
    - FIFO와 라운드 로빈 스케줄링 기법을 혼합한 것
    - 새로운 프로세스는 높은 우선순위, 프로세스의 실행시간이 길어질수록 점점 낮은 우선순위 큐로 이동하고 마지막 단계에는 라운드 로빈 적용
    - 큐마다 다른 시간 할당량
    - 마지막 단계는 라운드로빈 방식 처리

***💗 비선점형 스케줄링 알고리즘***

1. **우선순위 **(Priority)**
    - 프로세스별로 우선순위가 주어지고, 우선순위에 따라 CPU 할당
    - 동일 순위는 FCFS 방식
    - 주요/긴급 프로세스에 대한 우선 처리
    - 설정, 자원 상황 등에 따른 우선순위 선정
2. **기한부 (Deadline)**
    - 작업들이 명시된 기간이나 기한 내에 완료되도록 계획
    - 요청에 명시된 시간 내 처리를 보장
3. **FCFS (First Come First Service)**
    - 프로세스가 대기 큐에 도착한 순서에 따라 CPU를 할당
    - FIFO 알고리즘이라고도 함
    - 도착한 순서대로 처리
4. **SJF (Shortest Job First)**
    - 프로세스가 도착하는 시점에 따라 그 때 가장 작은 서비스 시간을 갖는 프로세스가 종료 시까지 자원 점유
    - 준비 큐 작업 중 가장 짧은 작업부터 수행
    - 평균 대기 시간 최소
    - CPU 요구 시간이 긴 작업과 짧은 작업 간의 불평등이 심해서 CPU 요구 시간이 긴 프로세스는 기아 현생 발생
5. **HRN (Highest Response Ratio Next)**
    - 대기 중인 프로세스 중 현재 응답률이 가장 높은 것을 선택
    - SJF의 약점인 기아 현상을 보완한 기법으로 긴 작업과 짧은 작업 간의 불평등 완화
    - HRN의 우선순위 = (대기시간 + 서비스 시간) / 서비스 시간
    - 기아 현상 최소화 기법

***💗 스케줄링 알고리즘 계산 예시***

1. **Round Robin**
    
    <img width="599" alt="Untitled (3)" src="https://user-images.githubusercontent.com/61955796/160861977-09ef69e0-c0cd-4571-9744-b9bca6bf0ab2.png">
    
    <img width="598" alt="Untitled (4)" src="https://user-images.githubusercontent.com/61955796/160862032-5e95ff67-96ea-496b-baf1-71dcbcf89617.png">
    
2. **SRT (Shortest Remaining Time First)**
    
    <img width="599" alt="Untitled (5)" src="https://user-images.githubusercontent.com/61955796/160862074-79f6d62a-5b3e-4871-a0ef-93ff1fd8fc1a.png">
    
    <img width="606" alt="Untitled (6)" src="https://user-images.githubusercontent.com/61955796/160862108-8161de9d-7a53-4174-a213-7c8d8c980585.png">

참조

1) [https://github.com/gyoogle/tech-interview-for-developer](https://github.com/gyoogle/tech-interview-for-developer)

2) [https://geol2.tistory.com/208](https://geol2.tistory.com/208)
