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
        * SELF JOIN<br>
    * JOIN 이미지<br><br>

* INNER JOIN (내부 조인) <br>
    * 일종의 교집합으로, 기준 테이블과 조인 테이블의 중복된 값을 보임<br>
    * 기준 테이블과 조인 테이블 모두 데이터가 존재해야 조회 가능<br>
    <pre>
    <code>
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A
    INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
    </code>
    </pre>
    <br><br>

* LEFT OUTER JOIN (왼쪽 외부 조인)<br>
    * 왼쪽 테이블을 기준으로 기준 테이블의 값과 기준 테이블에 중복되는 값을 보임<br>
    * 즉, 기준인 왼쪽 테이블의 모든 데이터가 조회<br>
    * 오른쪽 테이블에는 왼쪽 테이블과 중복되는 데이터가 존재할 경우 해당 데이터를 참조<br>
    <pre>
    <code>
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A
    LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
    </code>
    </pre>
    <br><br>

* RIGHT OUTER JOIN (오른쪽 외부 조인)<br>
    * 오른쪽 테이블을 기준으로 기준 테이블의 값과 기준 테이블에 중복되는 값을 보임<br>
    * 즉, 기준인 오른쪽 테이블의 모든 데이터가 조회<br>
    * 왼쪽 테이블에는 오른쪽 테이블과 중복되는 데이터가 존재할 경우 해당 데이터를 참조<br>
    <pre>
    <code>
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A
    RIGHT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
    </code>
    </pre>
    <br><br>

* FULL OUTER JOIN (완전 외부 조인)<br>
    * 일종의 합집합으로, 두 테이블의 모든 데이터를 조회
    * 사실상 기준 테이블이 의미가 없음
    <pre>
    <code>
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A
    FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
    </code>
    </pre>
    <br><br>

* CROSS JOIN (교차 조인)<br>
    * 모든 테이블의 경우의 수를 전부 표현해주는 방식<br>
    * 두 테이블의 카티션 프로덕트(곱집합)를 표현<br>
        * A 테이블의 데이터 * B 테이블의 데이터<br>
    <pre>
    <code>
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A
    CROSS JOIN JOIN_TABLE B
    </code>
    </pre>
    <br><br>
    
* SELF JOIN (셀프 조인)<br>
    * 자기 자신을 조인하는 조인하는 방식<br>
    * 하나의 테이블을 여러 번 복사해서 조인하는 방식<br>
    * 하나의 컬럼을 여러 번 변형할 때 사용
    <pre>
    <code>
    SELECT
    A.NAME, B.AGE
    FROM EX_TABLE A, EX_TABLE B
    </code>
    </pre>
    <br><br>

