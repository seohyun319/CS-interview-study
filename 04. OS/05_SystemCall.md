Process 생성과 제어를 위한 System call
- fork(), exec() : 새로운 Process 생성
- wait() : Process(parent)가 만든 다른 Process(child)가 끝날 때까지 기다리는 명령어

## fork
새로운 proess를 생성할 때 사용, 동일한 process의 내용을 여러 번 동작할 때 사용
- PID : process 식별자로, UNIX 시스템에서 PID는 process에게 명령할 때 사용

**fork()** 가 실행되면 process(child)가 하나 더 생긴다. 이 때 process(child)는 fork를 만든 process(parent)와 **거의** 동일한 복사본을 갖게 된다.
이 때 OS는 똑같은 2개의 프로그램이 동작한다고 생각하고, fork()가 return될 차례라고 생각한다. 
따라서 **새로 생성된 process(child)는 main에서 시작하지 않고 if문부터 시작하게 된다.**
그렇게 때문에 Child process와 parent process의 fork()값은 다르기 때문에, **완전히 동일한 복사본이라고 할 수 없다.**
    -  parent의 fork()값 : child의 pid
    -  child의 fork()값 : 0
하지만 scheduler가 parent와 child 중 어느것을 먼저 수행할지 알 수 없다. (parent와 child의 순서는 non-deterministic)


## wait
Process(child)가 종료될 때까지 기다리는 작업
Parent process가 먼저 실행되더라도, wait()은 child process가 끝나기 전에는 return하지 않으므로 **반드시 child가 먼저 실행됨**
- int wc = **wait(NULL)** 을 추가


## exec
Child process에서 parent process와 다른 동작을 하고 싶을 때 사용

**execvp(실행파일, 전달 인자)** : code segment 영역에 실행 파일의 코드를 읽어와서 덮어 씌운다. 
이후 heap, stack, 다른 메모리 영역이 초기화, OS는 그냥 실행
-> 새로운 process를 생성하지 않고 현재 프로그램에 wc 파일을 실행 
따라서 execvp() 이후 부분은 실행되지 않는다.
