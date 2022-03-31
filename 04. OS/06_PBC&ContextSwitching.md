- **Process Management** : Process가 여러개일 때 CPU 스케쥴링을 통해 관리하는 것
  - 이 때 CPU는 각  process들이 누군지 알아야 관리가 가능

- **Process Metadata** : Process들의 특징을 갖고 있는 것 (process 구분)
  - Process ID
  - Process State
  - Process Priority
  - CPU Registers
  - Owner
  - CPU Usage
  - Memeory Usage

- **PCB (Process Control Block)** : Process가 생성될 때, process metadata가 저장되는 곳

단계 : 프로그램 실행 → 프로세스 생성 → 프로세스 주소 공간에 (코드, 데이터, 스택) 생성 → 이 프로세스의 메타데이터들이 **PCB에 저장**

## PCB
하나의 PCB 안에는 하나의 process 정보가 담긴다.

### PCB가 필요한 이유
CPU에서는 프로세스의 상태(waiting/running)에 따라 교체작업이 이루어진다. 
이때, 앞으로 다시 수행할 대기 중인 프로세스에 관한 저장 값을 PCB에 저장해두기 때문에 PCB가 필요하다.
### PCB 관리 방법
**Linked List** 으로 관리한다.
PCB List Head에 PCB들이 생성될 때마다 붙게 된다. 주소값으로 연결이 이루어져 있는 연결리스트이기 때문에 삽입/삭제가 용이하다.
즉, 프로세스가 생성되면 해당 PCB가 생성되고 프로세스 완료시 제거된다.

**Context Switching** : 수행 중인 프로세스를 변경할 때, CPU의 레지스터 정보가 변경되는 것

## Context Switching
- CPU가 이전의 프로세스 상태를 PCB에 보관하고, 다른 프로세스의 정보를 PCB에 읽어 레지스터에 적재하는 과정
- 보통 인터럽트가 발생하거나, 실행 중인 CPU 사용 허가시간을 모두 소모하거나, 입출력을 위해 대기해야 하는 경우에 Context Switching이 발생 (ready/running/waiting)


### Context Switching의 OverHead
프로세스 작업 중에는 OverHead를 감수해야 하는 상황이 있다.
- CPU에 계속 프로세스를 수행시키도록 하기 위해서 다른 프로세스를 실행시키고 Context Switching 하는 것으로, CPU가 대기 상태로 놀지 않고, **다른 프로세스를 수행시켜** 사용자에게 빠르게 일처리를 제공해주기 위한 것이다.
