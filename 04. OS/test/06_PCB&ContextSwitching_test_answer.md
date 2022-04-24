### 문제
다음 코드를 보고 답하시오.
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
int main(int argc, char *argv[]) {
    printf("pid : %d", (int) getpid()); // pid : 29146
    
    int rc = fork();					// 주목
    
    if (rc < 0) {
        exit(1);
    }									// (1) fork 실패
    else if (rc == 0) {					// (2) child 인 경우 (fork 값이 0)
        printf("child (pid : %d)", (int) getpid());
    }
    else {								// (3) parent case
        printf("parent of %d (pid : %d)", rc, (int)getpid());
    }
}
```

4. 이 코드에서 Parent 프로세스의 fork()값과 Child 프로세스의 fork()값을 각각 쓰시오.
5. 다음 코드를 실행하면 출력될 수 있는 것을 모두 쓰시오. 
