## 신예지
<details>
<summary><b>MySQL과 Oracle에서 사용하는 트랜잭션 격리 수준에 대해 얘기하고, 나머지 두 격리 수준을 잘 사용하지 않는 이유를 설명해주세요</b></summary>
<div markdown="1">
  <br>
  MySQL은 Repeatable Read, Oracle은 Read Commited의 격리 수준을 사용합니다.
  Read Uncommitted는 Dirty Read 문제로 인해 데이터 정합성이 깨질 수 있어 사용하지 않습니다.
  Serializable은 트랜잭션을 직렬화하여 실행하기 때문에 동시성을 크게 저하시켜 성능 문제가 발생하므로 잘 사용하지 않습니다. 하지만 은행 거래 등 강한 정합성이 필요한 경우에는 사용되기도 합니다.
</div>
</details>

<details>
  <summary><b>MVCC에서 순차적으로 증가하는 고유한 트랜잭션 번호가 존재합니다. 왜 순차적으로 증가할까요?</b></summary>
  <div markdown="1">
    <br>
    MVCC(Multi-Version Concurrency Control)는 동시성 제어 기법으로, 각 트랜잭션이 실행될 때마다 순차적으로 증가하는 트랜잭션 ID를 할당받습니다.
    트랜잭션 번호가 순차적으로 증가하는 이유는 트랜잭션 실행 순서를 명확히 정하고, 오래된 데이터를 참조할 수 있도록 하기 위함입니다.
    이는 Repetable Read뿐만 아니라 Read Committed에서도 MVCC가 활용됩니다.

   ![MVCC 동작방식](https://file.notion.so/f/f/46ca05aa-38a8-4cd2-8035-e9090549d1dd/fc2c4abe-2d8f-4b89-8d7b-366639bbb696/Screenshot_2025-02-20_at_7.23.17_PM.png?table=block&id=1a0e787f-36ef-8018-a517-f22e0c1c3a7f&spaceId=46ca05aa-38a8-4cd2-8035-e9090549d1dd&expirationTimestamp=1740441600000&signature=_AtxpWMiWZ6sXDHZbG1GXyqocjOi2gAXZ1PD_mQr5Xg&downloadName=Screenshot+2025-02-20+at+7.23.17%E2%80%AFPM.png)
  </div>
</details>

<details>
  <summary><b>조회만 하는 건 트랜잭션을 안 걸어도 될까요?</b></summary>
  <div markdown="1">
    <br>
    만약 격리 수준이 Read Uncommitted일 경우 Commit 되지 않은 데이터를 조회하여 Ditry Read가 발생할 수 있기 때문에 조회만 하더라도 일관된 데이터를 보장하기 위해 트랜잭션을 걸어야 합니다.
    Read Committed 이상 격리 수준에서는 Dirty Read가 방지되므로, 조회만 하는 경우 트랜잭션을 걸지 않아도 됩니다.
  </div>
</details>

<details>
  <summary><b>Non-Repeatable Read와 Phantom Read의 차이점에 대해 설명하고, 각각의 해결 방법을 트랜잭션 격리수준을 이용하여 설명해주세요</b></summary>
  <div markdown="1">
    <br>
    
1. Non-Repeatable Read
 - 같은 행을 여러 번 조회했지만 그 값이 바뀜(UPDATE)
 - 해결 방법: Repeatable Read 이상의 격리 수준을 사용
2. Phantom Read
 - 같은 조건으로 조회했는데, 행 개수가 달라짐(INSERT, DELETE)
 - 해결 방법: Serializable Read 격리 수준을 사용
  </div>
</details>

<details>
  <summary><b>MySQL의 InnoDB는 어떻게 MVCC를 구현하나요?</b></summary>
  <div markdown="1">
    <br>

  MySQL의 InnoDB는 MVCC를 UNDO 로그와 트랜잭션 ID를 활용하여 구현합니다.
  트랜잭션이 실행될 때 현재 활성화된 트랜잭션보다 오래된 데이터를 UNDO 로그에서 조회하여 일관성을 유지합니다.
  이를 통해 동시성을 보장하면서도 별도의 잠금 없이 과거 데이터를 읽을 수 있도록 함으로써 성능을 최적화합니다.
  </div>
</details>

---

## 변하영
<details>
  <summary><b>트랜잭션에서 발생할 수 있는 문제점에는 어떤 것들이 있나요?</b></summary>
  <div markdown="1">
    <br>

첫번째로, Dirty Read가 발생할 수 있습니다. 한 트랜잭션이 커밋되지 않은 데이터를 다른 트랜잭션이 읽어버리는 문제입니다. 

두번째로, Non-Repeatable Read가 발생할 수 있습니다. 한 트랜잭션이 같은 데이터를 두 번 읽었는데, 그 사이 다른 트랜잭션이 해당 데이터를 수정 또는 삭제하여 결과가 달라지는 현상입니다. 

마지막으로 Phantom Read가 발생할 수 있습니다. 한 트랜잭션 내에서 동일한 조건으로 데이터를 조회했을 때, 중간에 다른 트랜잭션이 새로운 데이터를 삽입하거나 삭제하여 조회 결과가 달라지는 현상입니다.

  </div>
</details>

<details>
  <summary><b>트랜잭션 격리 수준에 대해 설명해주세요.</b></summary>
  <div markdown="1">
    <br>

ANSI SQL 표준에서는 4가지 트랜잭션 격리 수준을 정의하고 있습니다.

첫번째는 Read Uncommitted입니다. 커밋되지 않은 데이터도 읽을 수 있으며 Dirty Read, Non-Repeatable Read, Phantom Read 모두 발생할 수 있습니다. 가장 낮은 수준의 격리성으로 일반적으로 잘 사용하지 않습니다. 

두번째는 Read Committed입니다. 트랜잭션이 커밋된 데이터만 읽을 수 있으며, Dirty Read는 방지되지만 Non-Repeatable Read와 Phantom Read는 발생할 수 있습니다. 이는 오라클의 기본 트랜잭션 격리 수준입니다.

세번째는 Repeatable Read입니다. 트랜잭션이 읽은 데이터를 다른 트랜잭션이 갱신하거나 삭제할 수 없으며, Non-Repeatable Read는 방지되지만, Phantom Read는 발생할 수 있습니다. MySQL InnoDB 엔진의 기본 격리 수준입니다. 

마지막으로 Serializable은 가장 높은 수준의 격리성으로, 트랜잭션을 순차적으로 실행하여 모든 문제를 방지합니다. 하지만 성능이 매우 낮아지므로, 특별한 경우가 아니면 사용하지 않습니다.

  </div>
</details>

<details>
  <summary><b>MySQL과 Oracle의 기본 트랜잭션 격리 수준은 무엇인가요?</b></summary>
  <div markdown="1">
    <br>

MySQL의 InnoDB 엔진은 기본적으로 Repeatable Read를 사용하며, Oracle은 기본적으로 Read Committed를 사용합니다.

MySQL이 Repeatable Read를 사용하는 이유는 MVCC(Multi-Version Concurrency Control, 다중 버전 동시성 제어) 덕분에 일반적인 조회에서는 Phantom Read를 방지할 수 있기 때문입니다.

  </div>
</details>

<details>
  <summary><b>트랜잭션 격리 수준을 언제 높이고, 언제 낮춰야 하나요?</b></summary>
  <div markdown="1">
    <br>
격리 수준을 높여야 하는 경우는 금융 시스템이나 결제 처리와 같이 데이터 오류가 치명적인 상황입니다. 이 경우 Repeatable Read 또는 Serializable 수준이 필요할 수 있으며, 이를 통해 데이터의 정확성과 일관성을 유지할 수 있습니다.

반면, 격리 수준을 낮춰야 하는 경우는 로그 수집이나 통계 분석처럼 대량의 데이터를 빠르게 처리해야 하는 상황입니다. 이때는 성능이 더 중요하므로 Read Committed 수준이 적절하며, 경우에 따라 Read Uncommitted도 고려할 수 있습니다.

  </div>
</details>

<details>
  <summary><b>Serializable 격리 수준이 가장 안전하지만 거의 사용되지 않는 이유는 무엇인가요?</b></summary>
  <div markdown="1">
    <br>
    
이는 한 트랜잭션이 끝날 때까지 다른 트랜잭션이 블로킹되기 때문입니다. 
이로 인해 온라인 서비스에서는 처리 속도가 느려지고 대기 시간이 길어져 성능이 크게 저하됩니다. 
따라서 일반적인 애플리케이션에서는 Read Committed나 Repeatable Read를 사용하며, 절대적인 일관성이 필요한 일부 금융 시스템에서만 제한적으로 활용됩니다.
  </div>
</details>

---

## 박상윤
<details>
  <summary><b>트랜잭션 격리 수준이 필요한 이유</b></summary>
  <div markdown="1">
    <br>

트랜잭션 격리 수준이 필요한 이유는 동시 실행시 데이터 무결성을 보장하기 위함입니다.
  </div>
</details>

<details>
  <summary><b>트랜잭션 간의 동시 실행에서 발생할 수 있는 문제를 3가지 설명해주세요</b></summary>
  <div markdown="1">

- Dirty Read : 커밋되지 않은 데이터를 다른 트랜잭션이 읽는 문제

- Non-Repeatable Read : 같은 트랜잭션 내에서 반복 조회시 결과가 다르게 나오는 문제 

- Phantom Read  : 같은 조건으로 데이터를 조회했는데 데이터가 새로 생기거나 삭제되는 문제
  </div>
</details>

<details>
  <summary><b>READ UNCOMMITED 격리 수준에서 Dirty Read가 발생할 수 있는 시나리오를 말해주세요</b></summary>
  <div markdown="1">
    <br>

트랜잭션 A가 커밋하기 전의 데이터를 트랜잭션 B가 읽고, 이후 트랜잭션 A가 롤백되는 경우
  </div>
</details>

<details>
  <summary><b>REPEATABLE READ에서도 Phantom Read문제가 발생할 수 있는 이유를 설명하세요</b></summary>
  <div markdown="1">
    <br>

REPEATABLE READ는 UPDATE/DELETE로 인한 변경은 방지하지만, INSERT에 대한 동기화는 보장하지 않습니다.
  </div>
</details>

<details>
  <summary><b>SERIALIZABLE에서 성능이 저하되는 이유를 말해주세요.</b></summary>
  <div markdown="1">
    <br>

SERIALIZABLE 격리 수준에서는 트랜잭션 간 충돌을 방지하기 위해, 데이터에 대한 동시 접근을 제어하기 때문입니다.(모든 트랜잭션의 직렬화 = 순차실행)
  </div>
</details>

<details>
  <summary><b>MySQL에서 Repeatable Read 격리 수준을 기본으로 사용함에도 불구하고 Phantom Read가 거의 발생하지 않는 이유가 뭘까요?</b></summary>
  <div markdown="1">
    <br>

Gap Lock을 통해서 PhantomRead가 거의 발생하지 않습니다.
  </div>
</details>

<details>
  <summary><b>MySql InnoDB 에서 MVCC는 어떻게 Non-Repeatable Read 문제를 방지할까요?</b></summary>
  <div markdown="1">
    <br>

MVCC는 트랜잭션이 시작될 때 생성된 스냅샷을 기준으로 데이터를 조회합니다.

트랜잭션이 실행되는 동안, 자신의 트랜잭션보다 이후에 커밋된 데이터는 무시되고,필요할 경우 Undo Log를 참고하여 변경 전 데이터를 조회함으로써 Non-Repeatable Read를 방지합니다.
  </div>
</details>

<details>
  <summary><b>MVCC는 트랜잭션이 시작될 때, 무엇을 할까요?</b></summary>
  <div markdown="1">
    <br>

트랜잭션이 시작될 때 스냅샷을 생성합니다.
  </div>
</details>

---

## 이소원
<details>
  <summary><b>트랜잭션 격리 수준이 무엇인지 설명해주세요</b></summary>
  <div markdown="1">
    <br>

트랜잭션 격리 수준이란 동시에 실행되는 여러 트랜잭션이 서로 간섭하지 않도록 정해진 규칙입니다.

실행 중인 트랜잭션의 중간 결과(DB를 수정하기 위해 쿼리가 실행되는 동안)에 다른 트랜잭션이 해당 데이터에 접근/변경/조회/수정할 수 있는 정도를 조정하는 격리 레벨(수준)을 설정하는 것을 의미합니다.
  </div>
</details>

<details>
  <summary><b>트랜잭션 격리 수준이 높아야 좋은 건가요?</b></summary>
  <div markdown="1">
    <br>

아닙니다. 

격리 수준이 높으면 트랜잭션이 완전히 독립적으로 실행되도록하여 데이터 정합성이 보장되지만, 동시 처리 성능이 저하되어 데이터 처리 성능이 낮아질 수 있습니다.
  </div>
</details>


<details>
  <summary><b>Phantom Read 문제는 왜 발생하며, 해결하기 위한 격리 수준이 뭔가요?</b></summary>
  <div markdown="1">
    <br>

Phantom Read는 트랜잭션이 특정 조건을 만족하는 데이터를 조회할 때 다른 트랜잭션이 새로운 데이터를 추가하거나 삭재해서 결과가 바뀌는 문제입니다.

이를 해결하기 위해 모든 트랜잭션을 순차적으로 실행하는 Serializable 격리 수준을 적용해야 합니다.
  </div>
</details>

<details>
  <summary><b>트랜잭션 격리 수준을 높이지 않고 데이터 정합성을 유지하는 방법이 있나요?</b></summary>
  <div markdown="1">
    <br>

있습니다. 필요한 부분에만 Lock을 사용하여 격리 수준을 변경하지 않으면서 데이터 정합성을 유지할 수 있습니다.

++ 이런것도 있다~

- 애플리케이션 레벨에서 동시성 제어 (Optimistic Locking)
Optimistic Locking은 **Lock을 사용하지 않고도 데이터 정합성을 유지하는 방법**으로, 보통 **버전 번호(version) 또는 타임스탬프(timestamp)를 활용한다.**
- 논리적 일관성을 유지하는 추가적인 트랜잭션 설계
- 데이터 변경 시 트리거(Trigger) 활용
- 데드락을 방지하는 적절한 트랜잭션 처리 순서
  </div>
</details>


<details>
  <summary><b>온라인 쇼핑몰 환경에서는 어떻게 트랜잭션 격리 수준을 어떻게 설정하는 것이 좋을까요?</b></summary>
  <div markdown="1">
    <br>

주문 처리 : Serializable

일반 상품 조회 : Read Committed
  </div>
</details>

---

## 김수훈

<details>
  <summary><b>Read Committed에서 사용하는 Undo로그에 대해서 간단히 설명해주세요</b></summary>
  <div markdown="1">
    <br>

트랜잭션이 변경하기 전의 데이터를 저장하는 로그입니다.
  </div>
</details>


<details>
  <summary><b>Read Committed에서 Undo 로그의 사용 방식에 대해서 간단히 설명해보세요</b></summary>
  <div markdown="1">
    <br>

트랜잭션이 변경한 데이터가 아직 커밋되지 않은 상태라면, 다른 트랜잭션이 그 데이터를 읽으려 할 때 Undo 로그에 저장된 이전 값을 반환합니다.

이를 통해 Dirty Read를 방지하고, 다른 트랜잭션이 커밋되지 않은 변경 내용을 읽지 못하도록 합니다.
  </div>
</details>


<details>
  <summary><b>MVCC가 무엇인지 간단하게 설명하고, 특징을 설명해주세요.</b></summary>
  <div markdown="1">
    <br>

동시 접근을 허용하는 DB에서 동시성을 제어하기 위해 사용하는 방법 중 하나로 동일한 레코드에 대해 여러 버전의 데이터가 존재하는 것을 말합니다.

- 특징
    1. 트랜잭션이 롤백된 경우 데이터 복원 가능
    2. 서로 다른 트랜잭션간 접근할 수 있는 데이터 세밀하게 제어
    3. 트랜잭션 번호가 있음
        
        각각의 트랜잭션은 순차 증가하는 고유한 트랜잭션 번호 존재
        
        백업 레코드에 어느 트랜잭션에 의해 백업되었는지 트랜잭션 번호를 함께 저장
  </div>
</details>


<details>
  <summary><b>트랜잭션 격리 수준을 낮은 단계부터 차례로 말하고, 각 단계별 발생할 수 있는 데이터 부정합 문제를 말해보세요.</b></summary>
  <div markdown="1">
    <br>

1. **Read Uncommitted**
    - Dirty Read
    - Non-Repeatable Read
    - Phanton Read
2. **Read Committed**
    - Non-Repeatable Read
    - Phanton Read
3. **Repeatable Read**
    - Phanton Read
4. **Serializable Read**
    - 데이터 부정합 문제 x, but 매우 낮은 동시 처리 성능
  </div>
</details>


<details>
  <summary><b>트랜잭션 격리 수준은 왜 필요한가요?</b></summary>
  <div markdown="1">
    <br>

데이터베이스는 ACID 같이 원자적이면서도 독립적인 수행을 하도록 합니다.

그래서 Locking 이라는 개념이 있긴 하지만 무조건적인 Locking으로 동시에 수행되는 많은 트랜잭션들을 순서대로 처리하는 방식은 성능이 떨어집니다. 

그래서 최대한 효율적인 Locking 방법이 필요하기 때문에 이 방법을 결정짓는 트랜잭션 격리 수준이 필요합니다.
  </div>
</details>
