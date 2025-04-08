# DB Lock의 Level

## 1. Global Lock
MySQL 인스턴스(서버) 전체에 영향을 주는 락
- FLUSH TABLES WITH READ LOCK 명령으로 획득할 수 있다.
- SELECT 쿼리를 제외한 대부분의 DDL(create, alter, drop, truncate)이나 DML(select를 제외한 insert, update, delete) 쿼리를 실행할 수 있다.
- 데이터베이스의 구조적 변경, 백업 수행 또는 크리티컬한 데이터 마이그레이션 작업 시에 사용된다.
- 보통 백업 시에 자주 사용되며, 모든 테이블에 대한 읽기 락을 걸어 새로운 쓰기 작업을 차단한다. 락이 걸린 동안에는 DML 작업이 차단되어 읽기만 가능하다.

<br>

### Backup Lock
- LOCK INSTANCE FOR BACKUP
- MySQL이 8.0부터 InnoDB가 기본 Storage 엔진이 되면서 조금 더 가벼운 글로벌 락의 필요성이 생겼다.
- 논리적 백업 대신 물리적 백업을 위해 사용되는 락으로, FTWRL 과 달리 InnoDB의 내부 기능과 통합되어 세분화된 백업 시점 제어가 가능하다.
- InnoDB는 트랜잭션을 지원하기 때문에 일관된 데이터 상태를 위해 모든 데이터의 변경 작업을 멈출 필요가 없어졌다.
```
LOCK INSTACE FOR BACKUP
-- // 백업 실행
UNLOCK INSTANCE
```
- 백업 락은 일반적인 테이블의 데이터 변경은 허용되고 스키마 변경 같은 DDL 명령어가 실행되면 복제를 일시중지하는 역할

<br>

## (2. Database Lock)
- MySQL에서는 명시적인 데이터베이스 단위 락은 존재하지 않지만 논리적인 분류로 이해하는 경우가 많다.
- 예를 들어, 어떤 관리 작업(DDL)이 특정 DB의 여러 테이블에 동시에 영향을 미친다면 전체 DB 수준의 영향을 줄 수는 있다.
- 하지만 실제 락 수준은 테이블 락이나 MDL로 구현된다.

<br>

## 3. Table Lock
- 전체 테이블에 대한 잠금으로 특정 테이블의 모든 행에 대한 읽기 또는 쓰기를 제한하는 락
- 주로 대량의 데이터를 추가, 업데이트 또는 삭제하는 배치 작업에서 유리하며, 이러한 작업 중에는 다른 작업의 간섭을 최소화할 필요가 있다.
- (명시적) 명령으로 특정 테이블의 락을 획득할 수 있으며 MylSAM 뿐만 아니라 InnoDB에서도 사용이 가능하며 명시적으로 획득한 잠금은 UNLOCK TABLES 명령으로 잠금을 반납할 수 있다.
- (묵시적) 묵시적인 테이블 락은 스키마를 변경하는 쿼리(DDL)을 사용하는 경우에 발생하며, 이 경우에는 쿼리가 완료된 후 자동으로 락이 해제된다.

<br>

### Intention Lock

- MySQL InnoDB 엔진에는 intention lock의 개념도 존재한다.
- row에 대해서 나중에 어떤 row-level 락을 걸 것을 알려주기 위해 미리 table-level에 걸어두는 Lock (선언적 의미)

(1) Intention Shared Lock (IS)
  - SELECT ... LOCK IN SHARED MODE 가 실행되면
    - Intention Shared Lock이 테이블에 걸림
    - row-level 에 S-lock이 걸림

(2) Intention Exclusive Lock (IX) 
  - SELECT ... FOR UPDATE, INSERT, DELETE, UPDATE 이 실행되면
    - Intention Exclusive Lock 이 테이블에 걸림
    - row-level 에 X-Lock 이 걸림

<br>

## 4. Row Level Lock
- InnoDB Storage 엔진에서 제공하는 가장 세분화된 락 수준
- 트랜잭션 처리 시 특정 행 단위에 대한 락으로 동시성이 높은 환경에서 유리
- 행 단위로 잠금을 관리함으로 여러 트랜잭션이 서로 다른 행을 동시에 처리할 수 있다.

(1) Shared Lock (S Lock, 공유 락)
  - 데이터를 읽을 때, 사용하는 락
  - SELECT ... LOCK IN SHARE MODE 등의 쿼리에서 사용
  - 하나의 트랜잭션이 테이터를 읽고 있는 경우, 다른 트랜잭션들도 해당 데이터를 읽을 수는 있지만 쓰기 작업은 금지된다.
  - 데이터의 일관성을 유지할 수 있다.
  - 트랜잭션 격리수준 중 Repeatable Read 단계와 연관

(2) Exclusive Lock (X Lock, 배타 락)
  - 데이터를 변경하고자 할 때, 사용하는 락
  - 트랜잭션이 완료될 때까지 유지
  - UPDATE, DELETE 등에서 자동으로 사용되며, 특정 트랜잭션이 데이터를 수정하고 있는 경우, 해당 행(데이터)에 접근하지 못하도록 다른 모든 트랜잭션의 접근이 금지된다. (Lock)
  - 트랜잭션 격리수준 중 Serializable 단계와 연관

<br>

### row-level 및 table-level에서 두 번 Lock을 하는 이유는?
- 서로 다른 트랜잭션이 데이블 구조와 행 데이터를 동시에 변경하는 것을 방지하기 위함
- 예를 들어, 행 데이터를 수정 중일때 스키마 변경을 막기 위해 Intention Lock을 통해 Table-level Lock도 함께 관리

<br>

### Escalation
- 잠금 수준을 최적화하는 과정
  - Lock Escalation은 데이터베이스 시스템이 특정 Lock Level에서 다른 Lock Level로 전환하는 과정을 의미한다.
  - 일반적으로 특정 트랜잭션에서 많은 수의 잠금을 설정하려는 경우, 시스템은 이를 관리하기 위해 Lock Level을 높일 수 있다.
- Lock level이 낮을 수록 : 동시성은 좋아지지만, 관리해야할 Lock이 많아지기 때문에 메모리 효율성은 떨어진다.
- Lock level이 높을 수록 : 관리 리소스는 낮지만, 동시성은 떨어진다.

  <br>

# Blocking (블로킹)
- Lock 간의 경합(Race Condition)이 발생하여 특정 트랜잭션이 작업을 진행하지 못하고 대기하는 상태
- 공유 락끼리는 블로킹이 발생하지 않지만, 베타 락은 블로킹을 발생시킨다.
  - 특정 데이터에 공유 락이 설정된 상태에서, 해당 데이터에 배타 락을 설정하려고 할 때
  - 특정 데이터에 베타 락이 설정된 상태에서, 해당 데이터에 공유 락을 설정하려고 할 때
- 블로킹을 해소하는 방법
  - 어떤 트랜잭션이 완료(commit/rollback) 되어야 한다.

![Image](https://github.com/user-attachments/assets/71729e95-abf1-4ab2-a40a-ebac92cf8de1)

- 위 그림에서 Coupon 데이터에 트랜잭션 A가 S-Lock을 설정한 후에 트랜잭션 B가 X-Lock을 설정하여 트랜잭션 B가 블로킹 상태에 진입한 것을 알 수 있다.
- 트랜잭션 A:
  - SELECT ... FOR SHARE 실행 → S-Lock (공유 락) 획득
  - → 읽기 전용으로 id=1인 행을 보고 있음 (변경은 안 함)
- 트랜잭션 B:
  - SELECT ... FOR UPDATE 실행 → X-Lock (배타 락)을 걸려고 시도
  - → 하지만 이미 A가 S-Lock을 걸고 있어서 X-Lock을 획득할 수 없음

<br>

### 해결방법
1. SQL문 리펙토링
2. 트랜잭션을 가능한 짧게 정의
3. 동일한 데이터를 동시에 변경하는 작업을 하지 않도록 설계
4. 대용량 작업이 불가피한 경우, 작업 단위를 쪼개거나 lock_timeout을 설정

<br>

# Dead Lock (데드락, 교착상태)

![Image](https://github.com/user-attachments/assets/be42e10a-c2d6-402a-83e8-8fbc037ae61f)

- 두 개의 트랜잭션 간의 각각의 트랜잭션이 가지고 있는 리소스의 Lock을 획득하려고 할 때 발생
- 각각의 트랜잭션에 Lock을 걸고 상대방 Lock에 접근하여 반환받지 못하는 상황에서
- 서로 상대방의 락이 풀리기를 기다리는데, 그 락을 각자 상대가 들고 있어 영원히 진행되지 않는 Dead Lock이 발생하게 된다.

<br>

### 해결방법
1. Dead Lock이 감지되면 둘 중 하나의 트랜잭션을 강제종료한다.
2. Dead Lock 방지를 위해 접근 순서 규칙을 정한다.

<br>

# Optimistic Lock과 Pessimistic Lock
## 1. Optimistic Lock
- 데이터 갱신 시 충돌이 발생하지 않을 것으로 간주하는 방식
- 데이터를 읽을 때 잠금을 설정하지 않고, 데이터를 변경하기 전에 충돌을 검출하는 방식
- 주로 데이터 충돌이 적은 상황에서 사용

<br>

## 2. Pessimistic Lock
- 데이터 갱신 시 충돌이 발생할 것으로 보고 미리 잠금을 하는 방식
- 데이터를 읽을 때나 변경할 때 바로 잠금을 설정하여 다른 트랜잭션의 접근을 막는 방식
- 무결성에 장점이 있지만 데드락의 위험성이 존재
