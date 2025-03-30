## 신예지 

<details>
<summary><strong>DB의 서버 확장성에서 Scale-up과 Scale-out의 차이를 설명해주세요</strong></summary>

- **수직적 확장(Scale-up)**: 컴퓨터의 성능을 업그레이드하는 방법  
  - 단순히 데이터베이스의 성능을 향상시키는 것  
  - 데이터가 분산되지 않기 때문에 동기화가 필요 없어 데이터 일관성이 유지됨  
  - RAM의 공간에 한계가 있어 결국 하드웨어에서 데이터를 가져옴 → I/O 발생으로 인해 성능 저하 가능  

- **수평적 확장(Scale-out)**: 컴퓨터를 여러 대 사용하여 분산시키는 방법  
  - 더 많은 서버가 추가되며, DB가 전체적으로 분산됨  
  - 하나의 데이터베이스에서 작동하지만 여러 호스트에서 작동  
  - 데이터 복제가 이루어짐  
</details>

<details>
<summary><strong>데이터 읽기(read)를 자주 하지만, 변경(update)은 자주 이루어지지 않는 경우에는 어떤 종류의 데이터베이스를 사용하는 것이 적절한가요?</strong></summary>

- **NoSQL**이 적절함
</details>

<details>
<summary><strong>RDB의 단점을 얘기해주세요.</strong></summary>

- 작성된 스키마를 수정하기 어려움  
- 테이블 간의 관계가 복잡해질 경우, JOIN문이 많아져 복잡한 쿼리가 생성될 수 있음  
- 성능 향상을 위해서는 `Scale-up`만을 지원하여 비용이 증가할 가능성이 있음  
- 다른 DB에 비해 많은 자원이 활용되어 시스템 부하가 높음  
</details>

<details>
<summary><strong>RDB에서 튜플과 속성은 각각 무엇을 의미하나요?</strong></summary>

- **튜플(Tuple)**: 관계된 데이터의 묶음으로, 테이블의 행(Row)을 의미  
- **속성(Attribute)**: 데이터의 항목/필드로, 테이블의 열(Column)을 의미  
</details>

<details>
<summary><strong>NoSQL에서 고속 읽기와 쓰기에 최적화된 모델은 무엇인가요?</strong></summary>

- **Key-Value 모델**  
</details>

---

## 이소원 

<details>
<summary><strong>수평적 확장과 수직적 확장의 차이를 설명해주세요</strong></summary>

- **수직적 확장(Scale-up)**  
  - 컴퓨터의 성능을 업그레이드하는 방법  
  - 데이터가 분산되지 않기 때문에 동기화가 필요 없어 데이터 일관성이 유지됨  
  - RAM의 공간에 한계가 있어 결국 하드웨어에서 데이터를 가져옴 → I/O 발생으로 인해 성능 저하 가능  

- **수평적 확장(Scale-out)**  
  - 컴퓨터를 여러 대 사용하여 분산시키는 방법  
  - 더 많은 서버가 추가되며, DB가 전체적으로 분산됨  
  - 하나의 데이터베이스에서 작동하지만 여러 호스트에서 작동  
  - 데이터 복제가 이루어짐  
</details>

<details>
<summary><strong>RDB와 NoSQL의 차이에 대해 설명해 주세요.</strong></summary>

- **RDB**는 테이블 기반의 구조화된 데이터를 저장하며, 고정된 스키마와 ACID 트랜잭션을 보장함  
- **NoSQL**은 키-값, 문서, 컬럼 패밀리, 그래프 등 다양한 방식으로 데이터를 저장함  
- RDB는 데이터 일관성을 중시하는 반면, NoSQL은 확장성과 속도를 우선시함  
</details>

<details>
<summary><strong>NoSQL의 강점과, 약점이 무엇인가요?</strong></summary>

- **강점**  
  - 수평적 확장 용이  
  - 유연한 데이터 모델  
  - 빠른 읽기/쓰기 성능  

- **약점**  
  - 트랜잭션(ACID) 지원 부족  
  - 복잡한 쿼리 처리 어려움  
  - 일관성 유지 어려움  
</details>

<details>
<summary><strong>은행 시스템에서는 어떤 SQL을 사용하는 게 좋은가요?</strong></summary>

- **RDB**가 적절함  
  - 데이터 정합성이 중요함  
  - JOIN을 활용한 복잡한 관계형 데이터 모델 필요  
  - 트랜잭션(ACID) 지원이 필수적임  
</details>

<details>
<summary><strong>페이스북, 인스타그램, 트위터 등의 사용자 피드를 관리하는 SNS 서비스에서는 어떤 SQL을 사용하는 게 좋을까요?</strong></summary>

- **NoSQL**이 적절함  
  - 방대한 데이터를 빠르게 저장 & 조회해야 함  
  - 수평 확장이 필요함  
  - JOIN이 거의 필요 없음  
  - 데이터 구조가 자주 변경될 가능성이 있음  
</details>

---

