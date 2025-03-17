## 이소원
<details>
  <summary><b>join이 왜 필요한가요?</b></summary><br>
 두 개 이상의 테이블이나 DB를 연결하여 데이터를 검색하기 위해
</details>

<details>
  <summary><b>jjoin의 성능도 인덱스 유무의 영향을 받나요?</b></summary><br>
네 받습니다.

join 연산을 하게 되면 두 개 이상의 테이블을 결합하기 위해 매핑되는 행을 찾는 작업이 필요합니다. 이때 인덱스가 없으면 모든 데이터를 하나씩 확인해야 하므로(Full Table Scan) 속도가 느려질 수 있습니다.

따라서 인덱스가 존재하면 빠르게 매칭할 수 있어 성능이 향상됩니다.

특히 한 테이블을 기준으로 다른 테이블을 반복 조회하는 Nested Loop Join의 경우에는 인덱스의 유무에 따라 성능 차이가 크게 납니다.
</details>

<details>
  <summary><b>cross join은 모든 행이 서로 매핑되어 불필요한 정보가 많아질 가능성이 큽니다. cross join이 필요한 상황은 뭘까요?</b></summary><br>

- 가능한 모든 조합을 생성해야 할 때

    ex. 제품과 모든 색상의 조합을 만들 때
    
- 테스터를 만들 때
</details>

<details>
  <summary><b>3개 이상의 테이블을 조인할 때 고려해야 할 점은?</b></summary><br>

1. 조인 순서
    
    조인 순서가 성능에 큰 영향을 미칩니다.
    
    일반적으로 가장 작은 데이터셋을 먼저 조인하는 것이 유리합니다.
    
2. 테이블 간의 관계 이해
3. 인덱스를 활용하여 성능 최적화
</details>

## 변하영
<details>
  <summary><b>EQUI JOIN과 NON-EQUI JOIN 차이점은 무엇인가요?</b></summary><br>
EQUI JOIN은 = 연산자를 사용해 두 테이블에서 동일한 값을 가진 행을 조인하는 방식입니다. 반면, NON-EQUI JOIN은 <, >, BETWEEN 같은 비교 연산자를 사용해 범위 조건을 만족하는 데이터를 조인하는 방식입니다. 
</details>

<details>
  <summary><b>INNER JOIN과 CROSS JOIN의 차이점은 무엇인가요?</b></summary><br>
INNER JOIN은 두 테이블에서 지정된 조건을 만족하는 데이터만 반환하는 반면에 CROSS JOIN은 조건 없이 두 테이블의 모든 조합(카테시안 곱)을 생성합니다. 예를 들어, A 테이블에 3개, B 테이블에 4개가 있으면 INNER JOIN은 조건에 따라 0~3개의 결과를 반환할 수 있지만, CROSS JOIN은 무조건 3×4=12개의 조합을 생성합니다.
</details>

<details>
  <summary><b>FULL OUTER JOIN을 지원하지 않는 데이터베이스에서 구현하려면 어떻게 해야 하나요?</b></summary><br>
LEFT JOIN UNION RIGHT JOIN을 사용하여 구현할 수 있습니다.
</details>

## 박상윤
<details>
  <summary><b>문제를 읽고 어떤 JOIN을 사용해야 할지 말해주세요.</b></summary><br>
  
  https://school.programmers.co.kr/learn/courses/30/lessons/59042
</details>

<details>
  <summary><b>A집합과 B집합이 있고, 두 집합은 교집합이 존재합니다. A U B의 영역을 조회하기 위해 필요한 쿼리는 무엇일까요? (그림은 아래에 있습니다.)</b></summary><br>

  ![image.png](attachment:cb2d1514-b2c9-4476-abc6-a4e3c02af7fd:image.png)

  ![image.png](attachment:cb2d1514-b2c9-4476-abc6-a4e3c02af7fd:image.png)

  (A left join B) union (A right join B)
</details>

<details>
  <summary><b>쇼핑몰에서 회원(Member)과 주문(Order) 테이블을 만들었습니다. 각 회원은 주문을 하나 이상할 수도 있고, 한번도 주문하지 않았을 수도 있습니다. 만약 이 테이블에서 INNER JOIN으로 회원 정보와 주문 목록을 조회하는 경우, 어떤 데이터가 누락될  수 있으며, 이를 방지하기 위해 어떻게 해야할까요?</b></summary><br>

```sql
CREATE TABLE Member (
    id BIGINT PRIMARY KEY,
    name VARCHAR(100)
);

CREATE TABLE Orders (
    id BIGINT PRIMARY KEY,
    member_id BIGINT,
    order_date TIMESTAMP,
    FOREIGN KEY (member_id) REFERENCES Member(id)
);
```
</details>

<details>
  <summary><b>각 회원은 주문을 하나 이상할 수도 있고, 한번도 주문하지 않았을 수도 있습니다. 회원과 주문 목록을 조인하는 경우, 아래 두 쿼리중 처리해야하는 데이터가 더 작은 쿼리는 어떤 쿼리일까요?</b></summary><br>

정답 : INNER JOIN

**INNER JOIN**은 양쪽 테이블 모두 매칭되는 행만 조회하기 때문입니다..!

```sql
SELECT m.*, o.*
FROM Member m
INNER JOIN Orders o ON m.id = o.member_id;
```

```sql
SELECT m.*, o.*
FROM Member m
LEFT JOIN Orders o ON m.id = o.member_id;
```
</details>

## 김수훈
<details>
  <summary><b>inner join과 outer join가 각각 무엇인지 설명해주세요.</b></summary><br>

**Inner Join**은 두 테이블에서 조인 조건을 만족하는 행만 결과에 포함합니다. 즉, 양쪽 테이블에 모두 일치하는 데이터만 반환합니다.

**Outer Join**은 두 테이블 간의 교집합이 되는 데이터 뿐만 아니라 해당되지 않는 값까지 가져오는 join
</details>

<details>
  <summary><b>left join과 right join에서 테이블의 순서가 중요한 이유가 무엇인가요?</b></summary><br>

해당 조인은 앞에 나온 테이블을 기준으로 join을 하기 때문입니다.

예를 들어 left join을 하면 왼쪽 테이블을 모두 가져오면서 교집합을 추가하고, right join을 하면 오른쪽 테이블을 모두 가져오면서 교집합을 추가하기 때문에 순서가 중요합니다.
</details>

<details>
  <summary><b>exclusive join이 무엇이고, 어떤 join을 사용하여 구현하나요?</b></summary><br>

어느 특정 테이블에 있는 레코드만 가져오는 join을 말합니다.

left / right join과 where절을 함께 사용하여 구현합니다.
</details>

<details>
  <summary><b>OUTER JOIN에서 행(데이터)의 개수는 어떻게 될까요?</b></summary><br>
  
  기준 테이블(드라이빙 테이블)의 행(데이터)의 수
</details>

<details>
  <summary><b>UNION ALL은 언제 사용하나요?</b></summary><br>
  
  UNION에서 중복되는 레코드까지 모두 출력하고 싶을 때 사용
</details>

<details>
  <summary><b>FULL OUTER JOIN과 UNION ALL의 차이를 설명해주세요</b></summary><br>

  - UNION ALL은 UNION 하려는 두 테이블의 **필드의 개수**와 **타입**은 모두 같아야하며 **필드순서** 또한 같아야 하지만 FULL OUTER JOIN은 상관 없음
- **FULL OUTER JOIN**은 두 개의 테이블을 조인하여 모든 레코드를 포함하는 결과를 생성하는 반면, **UNION ALL**은 두 개의 SELECT 문의 결과를 합침
</details>
