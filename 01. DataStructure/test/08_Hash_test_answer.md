CS 스터디 1주차 시험지
Data Structure - Hash


1. 해싱이란?
( 키(임의의 길이의 데이터) )를 ( 값(고정된 길이의 데이터) )(으)로 매핑하는 과정



2. 다른 데이터가 같은 해시 값으로 매핑되는 현상을 지칭하는 용어는?

- 해시 충돌 (collision)


3. 다음 해시테이블을 보고 각각을 지칭하는 명칭을 쓰시오.

        키          해싱    ( 인덱스   ) (  버킷   )
 


4. Chaining에 대해 서술하시오.(목적, 방식, 단점 포함)


- 해시충돌의 해결법
- 한 버킷에 여러 값이 들어갈 수 있도록 연결리스트로 체인처럼 노드를 추가해가는 방식
- 메모리 문제 야기 가능



5. 해시 함수로 얻은 주소가 아닌 다른 주소에 데이터를 저장할 수 있도록 허용하는 방법의 이름은?


- 오픈 어드레싱(Open Addressing)
