## Java - Thread 활용

멀티스레딩이란 하나의 프로세스 안에 여러개의 스레드가 동시에 작업을 수행하는 것이다. 여기서 스레드는 하나의 작업단위이다.

### 1.스레드의 구현,생성, 실행


   스레드 구현 방법에는 2가지가 있다<br>
   1. Runnable 인터페이스 구현
   2. Thread 클래스 상속
<br>
      둘다 run() 메서드를 오버라이드한다.
``` java
public class MyThread implements Runnable {
    @Override
    public void run() {
        // 수행 코드
        for(int i = 0; i <= 50; i++) {
            System.out.print(i + ":" + Thread.currentThread().getName() + " ");
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
    public static void main(String[] args) {
        Runnable r = new MyThread();
        Thread t = new Thread(r, "mythread");
    }
}
```
Runnable을 임포트 한 경우 해당 클래스를 인스턴스화해서 Thread 생성자에 argument로 넘겨줘야 한다.
run()을 호출하면 Runnable 인터페이스에서 구현한 run()이 호출되므로 따로 오버라이딩하지 않아도 된다.
``` java
public class MyThread extends Thread {
    @Override
    public void run() {
        // 수행 코드
        
    }
    public static void main(String[] args) {
        // create thread objects
        Thread thread1 = new MyThread();
        thread1.setName("Thread #1");
        System.out.println(thread1.getName());
        thread1.start();
    }
}
```
Thread를 임포트 하면 위의 수행 코드부분과 같이 Thread의 getName() 메서드를 바로 호출해서 쓸 수 있지만 Runnable에서는 currentThread()를 통해 메서드를 호출해야한다.
<br>
Thread를 상속한 경우 실행 시 start() 메소드를 실행시켜야한다. 이때 run() start()는 모두 같은 작업을 하지만 run()은 main()의 콜 스택 하나만 이용하는 것과 다르게 start()는 Thread를 위한 새로운 콜스택을 생성한다는 점에서 차이가 있다.

### 스레드 실행 제어문

스레드의 상태에는 5가지가 있다.

| 상태 | 열거 상수 | 실행 |
|---|---|---|
|객체 생성|NEW|	스레드 객체가 생성 후, 아직 start() 메소드가 호출되지 않은 상태|
|실행 대기|	RUNNABLE	|실행 상태로 언제든지 갈 수 있는 상태|
|일시 정지|	WAITING|	다른 스레드가 통지할 때까지 기다리는 상태|
|일시 정지|    TIMED_WAITING|	주어진 시간 동안 기다리는 상태
|일시 정지|BLOCKED|	사용하고자 하는 객체의 락이 풀릴 때까지 기다리는 상태
|종료	|TERMINATED|	실행을 마친 상태|
또한 이런 스레드의 상태는 Thread를 상속하는 StatePrintThread 클래스를 이용해 출력할 수 있다.<br>
``` java
Thread.State state = targetThread.getState(); //스레드 상태 얻기
System.out.println("타켓 스레드 상태: " + state);
```
스레드가 객체로 생성되면 New 상태를 가지고, run() 메소드가 종료되면 TERMINATED 상태로 변한다.

<br>

### 스레드의 동기화와 스케줄링

1. 동기화

   쓰레드 동기화란 여러 쓰레드가 동일한 리소스를 공유하여 사용하게 되면 서로의 결과에 영향을 주기 때문에 방지하는 기법<br>
   > *임계영역*(critical section) : 임계영역으로 설정한 구역은 동시에 리소스를 사용할 수 없는 구역<br>
   > *락*(lock) : 락을 획득한 쓰레드에 대해서만 리소스를 사용하도록 하는 방식입니다.
   
   임계영역을 지정하고 임계영역이 가지고 있는 lock을 하나의 스레드에게만 빌려준다. 따라서 임계구역 안에서 수행할 코드가 완료되면, lock을 반납해줘야 한다.<br>
   <br>
   
      #### 1.1 synchronized를 이용한 동기화
      자바에서는 synchronized 키워드를 사용하여 임계영역을 지정하여 동시에 공유자원을 차지하지 않도록 강제한다. synchronized를 사용하는 방법을 메소드 자체에 적용하거나, 코드 블록에 적용할 수 있습니다.
      ``` java
      public class Student {

            int bookCount = 5;      // 공유 자원

            public int getBookCount() {
                  return bookCount;
            }

            public void setBookCount(int bookCount) {
                  this.bookCount = bookCount;
            }

            public void borrowBook() throws InterruptedException {
                  int m = bookCount;
                  Thread.sleep(2000);
                  bookCount = m+1;
                  System.out.println("대출완료");
            }

            public void returnBook() throws InterruptedException {
                  int m = bookCount;
                  Thread.sleep(3000);
                  bookCount = m-1;
                  System.out.println("반납완료");
            }
      }
      ``` 
   
      ``` java
      public class Library {
            public  static Student student = new Student();
      }
      ```
      
      ``` java
      public class BorrowThread extends Thread{
            @Override
            public void run() {
                  try {
                        Library.student.borrowBook();
                  } catch (InterruptedException e) {
                        e.printStackTrace();
                  }
                  System.out.println("학생이 빌린 총 책의 갯수 : "+Library.student.getBookCount());
            }
      }
   
      public class ReturnThread extends Thread{
            @Override
            public void run() {
                  try {
                        Library.student.returnBook();
                  } catch (InterruptedException e) {
                        e.printStackTrace();
                  }
                  System.out.println("학생이 빌린 총 책의 갯수 : "+Library.student.getBookCount());
            }
      }
      ```
      ```java
      public class Main {
            public static void main(String[] args) {
                  System.out.println("현재 대출한 책의 갯수 : "+Library.student.getBookCount());

                  BorrowThread bt = new BorrowThread();
                  ReturnThread rt = new ReturnThread();

                  bt.setPriority(10);
                  bt.start();
                  rt.start();

                  try{
                        bt.join();
                        rt.join();
                  } catch (InterruptedException e) {
                        e.printStackTrace();
                  }
            }
      }
   ```
   <br><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbyYWfO%2FbtqV2a71EgF%2FOdL9uMK8nGIxo2s4ElMElk%2Fimg.png" width="450px" height="300px" title="px(픽셀) 크기 설정" alt="RubberDuck"/><br>
   synchronized 키워드로 임계영역을 지정하면
   
   ```java
    public synchronized void borrowBook() throws InterruptedException {
        int m = bookCount;
        Thread.sleep(2000);
        bookCount = m+1;
        System.out.println("대출완료");
    }

    public synchronized void returnBook() throws InterruptedException {
        int m = bookCount;
        Thread.sleep(3000);
        bookCount = m-1;
        System.out.println("반납완료");
    }
   ```
   <br><img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmZHoZ%2FbtqV35yhAEJ%2FO9SE4POPsBUeO8G61BcyWK%2Fimg.png" title="px(픽셀) 크기 설정" alt="RubberDuck"/><br>

      #### 1.2 wait(), notify() 동기화
      - wait() : 스레드가 lock을 가지고 있으면, lock 권한을 반납하고 대기하게 만듬
      - notify() : 대기 상태인 스레드에게 다시 lock 권한을 부여하고 수행하게 만듬

      두 메소드는 동기화 된 영역(임계 영역)내에서 사용되어야 하며 조건 만족 안할 시 wait(), 만족 시 notify()를 받아 수행한다.
      ```java
   public synchronized void borrowBook() throws InterruptedException {
        if(bookCount>=10){ //빌린 책의 수가 10권이 되면 락을 반납하여 ReturnThread가 실행
            try{
                System.out.println("10권 초과로 대출할 수 없습니다");
                wait();
            }catch (Exception e){

            }
        }
        int m = bookCount;
        bookCount = m+1;
        System.out.println("책 대출 성공. 대출한 책의 갯수 : "+bookCount);
        notify();
    }

    public synchronized void returnBook() throws InterruptedException {
        if(bookCount<=0){ //반납할 책의 수가 없다면 대출이 가능하도록 BorrowThread에게 락
            try{
                System.out.println("반납할 책이 없습니다");
                wait();
            }catch (Exception e){

            }
        }
        int m = bookCount;
        bookCount = m-1;
        System.out.println("책 반납 성공. 대출한 책의 갯수 : "+bookCount);
        notify();
    }
      ```
<br>


참고: https://scshim.tistory.com/243#:~:text=%ED%94%8C%EB%9E%98%EA%B7%B8%2C%20interrupt()-,%EC%8A%A4%EB%A0%88%EB%93%9C%EC%9D%98%20%EC%83%81%ED%83%9C,%EC%8B%A4%ED%96%89%20%EB%8C%80%EA%B8%B0%20%EC%83%81%ED%83%9C%EA%B0%80%20%EB%90%9C%EB%8B%A4.&text=%EC%8B%A4%ED%96%89%20%EB%8C%80%EA%B8%B0%20%EC%83%81%ED%83%9C%EC%97%90%20%EC%9E%88%EB%8A%94,(Running)%20%EC%83%81%ED%83%9C%EB%9D%BC%EA%B3%A0%20%ED%95%9C%EB%8B%A4.
