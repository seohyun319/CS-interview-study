# JOIN

* JOIN의 정의<br>
    * 두 개 이상의 테이블이나 데이터베이스를 연결하여 데이터를 검색하는 방법<br>
    * 컬럼을 기준으로 행을 합쳐주는 연산<br>
    * 적어도 하나 이상의 컬럼을 공유하고 있어야 함<br>
    * Join의 종류<br>
        * INNER JOIN<br>
        * LEFT OUTER JOIN<br>
        * RIGHT OUTER JOIN<br>
        * FULL OUTER JOIN<br>
        * CROSS JOIN<br>
        * SELF JOIN<br><br>
    <img width="543" alt="화면 캡처 2022-03-17 012917" src="https://user-images.githubusercontent.com/61955796/158659607-a374222b-2491-4fca-9d5e-7bc00bdcdb31.png">
    <br><br>

* INNER JOIN (내부 조인) <br>
    * 일종의 교집합으로, 기준 테이블과 조인 테이블의 중복된 값을 보임<br>
    * 기준 테이블과 조인 테이블 모두 데이터가 존재해야 조회 가능<br><br>
    <pre>
    <code>
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A
    INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
    </code>
    </pre><br>
    <img width="343" alt="image" src="https://user-images.githubusercontent.com/61955796/158660088-ee813c70-c542-4734-a376-7e53b0a849e1.png"><br>
    <br><br>

* LEFT OUTER JOIN (왼쪽 외부 조인)<br>
    * 왼쪽 테이블을 기준으로 기준 테이블의 값과 기준 테이블에 중복되는 값을 보임<br>
    * 즉, 기준인 왼쪽 테이블의 모든 데이터가 조회<br>
    * 오른쪽 테이블에는 왼쪽 테이블과 중복되는 데이터가 존재할 경우 해당 데이터를 참조<br><br>
    <pre>
    <code>
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A
    LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
    </code>
    </pre><br>
    <img width="333" alt="image" src="https://user-images.githubusercontent.com/61955796/158660280-9c9a09fc-255d-4a79-a1c4-ef19dfde95c1.png">
    <br><br>

* RIGHT OUTER JOIN (오른쪽 외부 조인)<br>
    * 오른쪽 테이블을 기준으로 기준 테이블의 값과 기준 테이블에 중복되는 값을 보임<br>
    * 즉, 기준인 오른쪽 테이블의 모든 데이터가 조회<br>
    * 왼쪽 테이블에는 오른쪽 테이블과 중복되는 데이터가 존재할 경우 해당 데이터를 참조<br><br>
    <pre>
    <code>
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A
    RIGHT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
    </code>
    </pre><br>
    <img width="304" alt="image" src="https://user-images.githubusercontent.com/61955796/158660382-343489ac-f757-4d1c-94f4-c3bc4305bb09.png">
    <br><br>

* FULL OUTER JOIN (완전 외부 조인)<br>
    * 일종의 합집합으로, 두 테이블의 모든 데이터를 조회
    * 사실상 기준 테이블이 의미가 없음<br><br>
    <pre>
    <code>
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A
    FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
    </code>
    </pre><br>
    <img width="320" alt="image" src="https://user-images.githubusercontent.com/61955796/158660494-ade36b02-60ec-4043-8f25-26f2a9782f9d.png">
    <br><br>

* CROSS JOIN (교차 조인)<br>
    * 모든 테이블의 경우의 수를 전부 표현해주는 방식<br>
    * 두 테이블의 카티션 프로덕트(곱집합)를 표현<br>
        * A 테이블의 데이터 * B 테이블의 데이터<br><br>
    <pre>
    <code>
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A
    CROSS JOIN JOIN_TABLE B
    </code>
    </pre><br>
    <img width="308" alt="image" src="https://user-images.githubusercontent.com/61955796/158660590-eaedb25a-91ee-4de4-9201-b5a5c0b1bfb5.png">
    <br><br>
    
* SELF JOIN (셀프 조인)<br>
    * 자기 자신을 조인하는 조인하는 방식<br>
    * 하나의 테이블을 여러 번 복사해서 조인하는 방식<br>
    * 하나의 컬럼을 여러 번 변형할 때 사용<br><br>
    <pre>
    <code>
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A, EX_TABLE B
    </code>
    </pre><br>
    <img width="302" alt="image" src="https://user-images.githubusercontent.com/61955796/158660674-615b3986-c174-436c-acc3-60eb899b5692.png">
    <br><br>

