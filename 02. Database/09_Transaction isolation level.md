# Isolation level

> 트랜잭션에서 일관성 없는 데이터를 허용하도록 하는ㄴ 수준

<br>

## Isolation level의 필요성
데이터 베이스는 ACID 특징과 같이 트랜잭션이 독립적인 수행을 하도록 한다.  
따라서 Locking을 통해, 트랜잭션이 DB를 다루는 동안 다른 트랜잭션이 관여하지 못하도록 규제하는 것이 필요하다.  
그러나 무조건 Locking으로 동시에 수행되는 많은 트랜잭션들을 순서대로 처리하도록 하면, 성능이 매우 떨어지게 된다.  
반면, 성능을 위해 Locking의 범위를 줄인다면, 잘못된 데이터베이스 처리로 인해 문제가 발생하게 될 가능성이 높아진다.  
➡ 최대한 효율적인 Locking 방법이 필요

--------------------------  

## Isolation level 종류
1. Read Uncommited (레벨 0)
> SELECT 문장이 수행되는 동안 해당 데이터에 Shared Lock이 걸리지 않는 계층  

* 트랜잭션에서 처리 중이거나, 아직 Commit 되지 않은 데이터를 다른 트랜잭션이 읽는 것을 허용 -> **DIRTY READ** 현상 

* 데이터베이스의 일관성 유지가 불가능함 -> 정합성에 문제가 많음

![image](https://user-images.githubusercontent.com/65678579/158745098-3418c463-6bb5-4cb1-bc60-bf36175e3ab7.png)

<br>
<br>

2. Read Commited (레벨 1)
> SELECT 문장이 수행되는 동안 해당 데이터에 Shared Lock이 걸리는 계층  

* 트랜잭션이 수행되는 동안 다른 트랜잭션이 접근할 수 없고 대기하게 됨.  
* Commit된 트랜잭션만 조회 가능   
* SQL 서버의 Default Isolation level

![image](https://user-images.githubusercontent.com/65678579/158745219-5a42d8c9-3150-41cd-beba-ab6156ce9c5b.png)


<br>
<br>


3. Repeatable Read (레벨 2)
> 트랜잭션이 완료될 때 까지 SELECT 문장이 사용하는 모든 데이터에 Shared Lock이 걸리는 계층 

* 트랜잭션이 범위 내에서 조회한 데이터 내용이 항상 동일함을 보장함.  
다른 사용자는 트랜잭션 영역에 해당하는 데이터에 대해 수정이 불가능 

![image](https://user-images.githubusercontent.com/65678579/158745261-2d1cb918-67d8-430e-9861-eab6966854c4.png)


* PHANTOM READ
다른 트랜잭션에서 수행한 변경 작업에 의해 레코드가 보였다가 안 보였다가 하는 현상으로 이를 방지하기 위해서는 쓰기 잠금을 걸어야 한다.

<br>
<br>

4. Serializable (레벨 3)
> 트랜잭션이 완료될 때 까지 SELECT 문장이 사용하는 모든 데이터에 Shared Lock이 걸리는 계층  

완벽한 읽기 일관성 모드를 제공하지만 잘 사용되지 않는다.  
다른 사용자는 트랜잭션 영역에 해당되는 데이터에 대해 수정 및 입력이 불가능함.  

<br> 
<br>

### 🔗참고링크  
[Link](https://nesoy.github.io/articles/2019-05/Database-Transaction-isolation)

