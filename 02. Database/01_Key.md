# KEY

* 키의 정의<br>
    * 데이터베이스에서 조건에 만족하는 튜플을 찾거나 순서대로 정렬할 때 사용<br>
    * 다른 튜플들과 구별할 수 있는 유일한 기준이 되는 Attribute(속성)<br>
    * 즉, 데이터를 구별할 수 있는 기준<br><br>

* 후보키 (Candidate Key)<br>
    * Tuple을 유일하게 식별하기 위해 사용하는 속성들의 부분 집합<br>
    * 모든 릴레이션은 반드시 하나 이상의 후보키를 가져야 함<br>
    * 릴레이션에 있는 모든 Tuple에 대해서 유일성과 최소성을 만족시켜야 함<br>
        * 유일성 : 하나의 Tuple을 유일하게 식별할 수 있음<br>
        * 최소성 : 꼭 필요한 속성으로만 구성해야 함<br>
    * 기본키가 될 수 있는 후보들이라고 생각하면 됨<br><br>

* 기본키 (Primary Key)<br>
    * 후보키 중에서 선택한 Main Key<br>
    * 한 릴레이션에서 특정 Tuple을 유일하게 구별할 수 있는 속성<br>
    * Null 값을 가질 수 없음<br>
    * 동일한 값이 중복될 수 없음<br>
       * ex) 주민등록번호<br>
    * 테이블에 기본키는 하나만 만들 수 있음<br><br>

* 대체키 (Alternate Key)<br>
    * 후보키가 둘 이상일 때 기본키를 제외한 나머지 키<br>
    * 보조키라고도 불림<br><br>

* 슈퍼키 (Super Key)<br>
    * 한 릴레이션 내에 있는 속성들의 집합으로 구성된 키<br>
    * 유일성 O, 최소성 X<br><br>

* 외래키 (Foreign Key)<br>
    * 관계(Relation)를 맺고 있는 릴레이션 R1, R2가 있을 때 R2의 기본키를 참조하는 R1의 속성<br>
    * 다른 릴레이션의 기본키를 그대로 참조하는 속성의 집합<br><br>

<img width="625" alt="화면 캡처 2022-03-16 214554" src="https://user-images.githubusercontent.com/61955796/158595755-2e39cd98-1472-4abc-a05e-c52f86c5e443.png"><br>

참고: https://limkydev.tistory.com/108



