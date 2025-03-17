# SQL - JOIN
![SQL JOINS](image.png)

## 1. JOIN이란?
### JOIN의 개념
- 두 개 이상의 테이블을 결합하여 **관련된 데이터를 하나의 결과 집합으로 반환하는 연산**
- 릴레이션 간의 관계를 처리하는 데 사용
- 데이터 중복을 줄이고 정규화된 데이터 구조를 유지하는 역할
- 관계형 데이터베이스에서 가장 많이 사용되는 연산 중 하나

### JOIN의 목적
- **테이블 간 관계를 맺어 데이터를 활용**
- 중복 데이터를 줄이고 데이터 일관성 유지
- 데이터 검색과 분석을 효율적으로 수행

## 2. JOIN의 종류
JOIN은 크게 **INNER JOIN**과 **OUTER JOIN**으로 나뉘며, 세부적으로 다양한 방식이 존재한다.

### INNER JOIN(내부 조인)
> **두 테이블 간 공통된 데이터(교집합)만 반환**
- 조인 조건을 만족하는 행만 결과로 출력됨
- NULL 값이 포함된 행은 제외됨
- 어떤 테이블을 기준으로 하든 결과는 동일

```sql
SELECT A.ID, A.ENAME, B.DEPARTMENT
FROM A INNER JOIN B
ON A.ID = B.ID;
```

### OUTER JOIN (외부 조인)
> 조인 조건을 만족하지 않는 행도 포함하여 결과 반환
- `드라이빙 테이블`이 필요하다
    - 기준 테이블(드라이빙 테이블)의 모든 정보는 가져옴
    - 대상 테이블은 기준 테이블과 연결되는 행을 포함하는 정보 가져옴
- 데이터의 개수: 기준이 되는 테이블의 데이터 수

#### LEFT OUTER JOIN
> 오른쪽 테이블(B)의 모든 행을 반환, 왼쪽 테이블(A)에서 일치하는 행이 없으면 NULL 채움
- 왼쪽 테이블이 기준이며, 모든 데이터를 포함
- 오른쪽 테이블에 일치하는 데이터가 없으면 NULL

```sql
SELECT A.ID, A.ENAME, B.DEPARTMENT
FROM A LEFT OUTER JOIN B
ON A.ID = B.ID;
```

#### RIGHT OUTER JOIN
> 오른쪽 테이블(B)의 모든 행을 반환, 왼쪽 테이블(A)에서 일치하는 행이 없으면 NULL 채움
- 오른쪽 테이블이 기준이며, 모든 데이터를 포함
- 왼쪽 테이블에 일치하는 데이터가 없으면 NULL

```sql
SELECT A.ID, A.ENAME, B.DEPARTMENT
FROM A RIGHT OUTER JOIN B
ON A.ID = B.ID;
```

#### FULL OUTER JOIN
> 두 테이블의 모든 데이터를 포함하며, 일치하지 않는 경우 NULL로 채움
- 일치하는 데이터가 없으면 NULL

```sql
SELECT A.ID, A.ENAME, B.DEPARTMENT
FROM A FULL OUTER JOIN B
ON A.ID = B.ID;
```

- MySQL에서는 FULL OUTER JOIN을 지원하지 않음
&rarr; LEFT JOIN + RIGHT JOIN을 UNION을 사용해 구현 가능

```sql
SELECT A.ID, A.ENAME, B.DEPARTMENT
FROM A LEFT JOIN B ON A.ID = B.ID
UNION
SELECT A.ID, A.ENAME, B.DEPARTMENT
FROM A RIGHT JOIN B ON A.ID = B.ID;
```

#### UNION JOIN
> 여러 개의 SELECT문의 결과를 하나의 결과 집합으로 합치는 연산
- 각 SELECT문의 필드 개수와 데이터 타입이 동일해야 하며, 필드의 순서도 같아야 한다.
- 기본적으로 중복된 행은 제거(DISTINCT 포함) 되어 유일한 결과만 반환된다.
- 중복된 데이터도 포함하고 싶다면 **UNION ALL**을 사용해야 한다.

```sql
SELECT 필드이름 from 테이블A
UNION
SELECT 필드이름 from 테이블B
```

**UNION JOIN과 FULL OUTER JOIN의 차이점**
> FULL OUTER JOIN은 두 테이블을 조인하여 모든 레코드를 포함하는 결과를 생성하지만 UNION JOIN은 두 개의 SELECT문의 결과를 단순히 합치는 것을 의미함

#### EXCLUSIVE JOIN
> 두 테이블을 조인할 때 특정 테이블에만 존재하는 데이터만 가져오는 JOIN 방식
- LEFT JOIN 또는 RIGHT JOIN을 사용하고, WHERE 절을 추가하여 특정 테이블에만 존재하는 데이터를 필터링함
- 즉, LEFT JOIN을 수행한 후 오른쪽 테이블에 일치하는 데이터가 없는 경우만 추출하는 방식

```sql
SELECT A.ID, A.ENAME, A.KNAME
FROM A LEFT OUTER JOIN B
ON A.ID = B.ID;
WHERE B.ID IS NULL  // 조인한 B 테이블의 값이 null만 출력 >> 조인이 안된 A 레코드 나머지값만 출력
```

**LEFT, RIGHT JOIN시 주의점**
> INNER JOIN과는 달리 조인하는 테이블의 순서가 상당히 중요하다.
조인 순서의 일관성을 위해 LEFT, RIGHT JOIN을 쓰다가 갑자기 INNER JOIN 이나 다른 조인을 사용하지 않는다.

#### SELF JOIN (자기 자신과 JOIN)
> 같은 테이블을 두 번 참조하여 JOIN 수행
- 계층적 데이터(트리 구조, 조직도)에서 많이 사용됨
```sql
SELECT A.ID, A.ENAME, B.MANAGER_NAME
FROM EMPLOYEES A JOIN EMPLOYEES B
ON A.MANAGER_ID = B.ID;
```

#### CROSS JOIN (카테시안 곱)
> 모든 행을 조합하여 반환 (곱집합, Cartesian Product)
- 테이블 간 모든 가능한 조합을 생성
- 테이블 A가 10개 행, 테이블 B가 5개 행이면 → 10 × 5 = 50개 행 반환
- 특정한 조건 없이 모든 데이터 조합이 필요할 때 사용

```sql
SELECT A.ID, B.DEPARTMENT
FROM A CROSS JOIN B;
```

## 3. JOIN 사용 시 주의할 점
### 테이블 크기 고려
- 대용량 테이블 조인 시 성능 문제 발생 가능
- 필요한 컬럼만 SELECT하여 불필요한 데이터 조회 방지

### 인덱스 활용
- JOIN 키에 인덱스가 있으면 성능이 향상됨
- WHERE 조건절에도 인덱스 적용 고려

### JOIN 순서 최적화
- 작은 테이블을 드라이빙 테이블로 사용하면 성능 향상
- 테이블 조인 순서를 최적화하여 성능 개선 가능
