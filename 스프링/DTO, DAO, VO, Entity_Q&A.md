## 박상윤
<details>
  <summary><b>DTO, DAO, VO, Entity가 각각 무엇인지 설명하시오.</b></summary>
  <div>
    DTO(Data Transfer Object) - 계층간 데이터 교환을 위해 사용하는 객체, 요청과 응답을 처리하기 위한 객체<br>
    DAO(Data Access Object) - DB에 접근하는 역할을 하는 객체<br>
    VO(Value Object) - 값 그 자체를 표현하는 객체<br>
    Entity -  JPA와 같은 ORM 프레임워크에서 사용되는 개념으로 @Entity 어노테이션을 붙여 엔티티를 나타낸다, 실제 DB의 테이블과 정확하게 매칭되는 속성들을 갖도록 디자인 된 클래스
  </div>
</details><br>

<details>
  <summary><b>DTO는 가변 또는 불변 객체로 사용할 수 있다. 불변객체로 만들려면 어떻게 해야할까요?</b></summary>
  <div>
    setter 메서드를 삭제후, 생성자를 통해 값을 초기화하해서 불변객체로 만듭니다.<br><br>
    <pre><code>
// 불변 객체 예시
public DtoEx(String name, int age) {
    this.name = name;
    this.age = age;
}

public String getName() {
    return name;
}

public int getAge() {
    return age;
}
</code></pre>
  </div>
</details><br>

<details>
  <summary><b>이놈!은 VO(Value Object)라고 볼 수 있을까요? 그 이유를 포함하여 설명해보세요.</b></summary>
  <div>
    enum은 VO가 X<br><br>
    enum은 미리 정의된 상수들의 열거형 타입으로, VO처럼 불변성을 갖긴하지만<br>
    상태보다는 식별 가능한 고정된 이름에 가깝고, 값 객체로서의 풍부한 의미나 조합을 표현하지 않는다.
  </div>
</details><br>

<details>
  <summary><b>VO가 가지는 특징 5가지 말해주세요.</b></summary>
  <div>
    1. 동등성<br>
    2. 불변성<br>
    3. 자가 유효성 검사<br>
    4. getter 이외의 로직 포함 가능<br>
    5. 값 타입을 여러 엔티티에 공유시 Side Effect 발생
  </div>
</details><br>

<details>
  <summary><b>VO를 왜 사용할까요?</b></summary>
  <div>
    원시 타입이 도메인 객체를 모델링하기에 충분하지 않기 때문이다.
  </div>
</details><br>

---

## 신예지
<details>
  <summary><b>DTO와 VO의 차이를 말해주세요</b></summary>
  <div>
    - DTO는 데이터 전송을 위한 객체로 가변적일 수 있음<br>
    - VO는 불변객체로 값 자체를 표현
  </div>
</details><br>

<details>
  <summary><b>DTO 중에서 setter 메서드가 없는 DTO를 뭐라고 하나요?</summary>
  <div>
    불변객체 DTO
  </div>
</details><br>

<details>
  <summary><b>VO의 특징을 설명해주세요</b></summary>
  <div>
    - <strong>동등성</strong><br>
    &nbsp;&nbsp;&nbsp;&nbsp;- 값 객체의 모든 속성이 같은 값을 가질 시 동일한 객체로 판단<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- 이때, equals(), hashCode() 오버라이딩을 했다는 전제 조건 필요<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- 해당 속성들은 primitive 타입<br><br>
    - <strong>불변성</strong><br>
    &nbsp;&nbsp;&nbsp;&nbsp;- 수정자(setter)를 포함하지 않고, 생성자를 통해서 값 초기화<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- 새로운 값 사용을 위해선 새로운 객체 생성<br>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- 중간에 데이터를 조작할 수 없음<br>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- Read Only<br><br>
    - <strong>자가 유효성 검사(Self-Validation)</strong><br>
    &nbsp;&nbsp;&nbsp;&nbsp;- 유효성 검사 진행 후 VO 생성<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- VO 사용 시 유효성 검사가 보장되어있으므로 안전하게 사용 가능<br><br>
    - getter 이외의 로직 포함 가능<br>
    - 값 타입을 여러 엔티티에서 공유 시 Side effect 발생가능
  </div>
</details><br>

<details>
  <summary><b>왜 Entity로 요청을 주고받으면 안될까요?</b></summary>
  <div>
    - Entity는 DB 테이블과 직접 매핑되는 핵심 도메인 객체<br>
    - 요청/응답으로 사용 시, 프론트의 요구에 따라 Entity가 자주 변경되어야 할 수 있음<br>
    - 이는 DB 스키마에 직접 영향을 줄 수 있고, 유지보수성이 떨어짐<br>
    - 따라서 API 요청/응답은 DTO를 사용하고, Entity는 비즈니스 로직과 DB 매핑에만 집중
  </div>
</details><br>

<details>
  <summary><b>Java Beans에 대해 설명해주세요</b></summary>
  <div>
    - JavaBeans는 재사용 가능한 소프트웨어 컴포넌트<br>
    - 기본 생성자와 private 필드, 그리고 getter/setter를 가진 클래스<br>
    - 주로 DTO처럼 데이터를 담고 전달하는 데 사용됨<br>
    - 직렬화 가능하고, setter/getter로 속성 제어
  </div>
</details><br>

---

## 이소원
<details>
  <summary><b>Entity와 DTO를 분리함으로써의 E(2)점</b></summary>
  <div>
    1. 보안 및 데이터 노출 최소화<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- Entity를 그대로 노출하면 민감한 정보(예: 비밀번호, 내부 식별자 등)가 API 응답에 포함될 수 있다.<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- DTO는 필요한 데이터만 선택해서 보내므로 불필요한 노출을 막을 수 있다.<br><br>
    2. 계층 간 역할 분리 (관심사 분리, Separation of Concerns)<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- Entity는 DB와의 매핑/비즈니스 중심<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- DTO는 요청/응답 중심<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- 각자의 역할을 명확히 분리하면 코드 유지보수가 쉽다.
  </div>
</details><br>

<details>
  <summary><b>VO vs Entity</b></summary>
  <div>
    - <strong>Entity</strong><br>
    &nbsp;&nbsp;&nbsp;&nbsp;- 실제 DB 테이블과 매핑되는 독립적인 데이터<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- 별도 테이블로 생성 (pk 포함)<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- 식별자(pk) 반드시 포함<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- 독립적으로 존재하여 create, read, update, delete 가능<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- 대부분 가변적<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- id 기준으로 동일성 비교 (equals/hashCode)<br><br>
    - <strong>VO</strong><br>
    &nbsp;&nbsp;&nbsp;&nbsp;- 의미있는 값을 묶은 객체, Entity의 일부<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- Entity의 속성으로 포함되어 저장, 테이블 없음<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- 식별자 없음<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- Entity에 종속되어 있음<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- 보통 불변으로 설계 (final)<br>
    &nbsp;&nbsp;&nbsp;&nbsp;- 모든 필드가 같으면 동일하다고 간주
  </div>
</details><br>

<details>
  <summary><b>VO를 사용하는 이유는 무엇인가요?</b></summary>
  <div>
    - VO(Value Object)는 의미 있는 값들을 하나의 객체로 묶어 표현할 수 있어 코드의 가독성과 재사용성을 높입니다.<br>
    - VO는 불변 객체로 설계되어 사이드 이펙트가 줄어들고, Entity의 내부 속성을 논리적으로 묶는 데에 적합합니다.
  </div>
</details><br>

<details>
  <summary><b>DTO에 어떤 기능을 넣으면 안 되나요?</b></summary>
  <div>
    DTO는 계층 간 데이터 전달만을 목적으로 하므로, 비즈니스 로직을 포함해서는 안 됩니다.<br><br>
    예외적으로 Getter/Setter, 유효성 검사(@Valid) 정도는 들어갈 수 있지만, DB 연산이나 도메인 관련 로직이 들어가면 DTO의 목적을 벗어나게 됩니다.<br><br>
    책임이 명확히 분리되어야 유지보수성이 높아집니다.
  </div>
</details><br>

<details>
  <summary><b>DTO의 위치는?</b></summary>
  <div>
    DTO는 "API 요청/응답"과 "컨트롤러 내부 로직"을 연결하는 중간 역할을 합니다.
  </div>
</details><br>

---

## 변하영
<details>
  <summary><b>DTO와 Entity를 분리하지 않고 사용하면 어떤 문제가 발생할 수 있을까요?</b></summary>
  <div>
    DTO와 Entity를 혼용하면 뷰나 API 요청에 맞춰 Entity구조를 자주 바꾸게 됩니다. 이는 DB 스키마 변경으로 이어져 안정성이 떨어집니다. 또한 이는 여러 레이어에 영향을 주면서 유지보수가 어려워집니다.
  </div>
</details><br>

<details>
  <summary><b>DAO와 Repository는 어떤 차이가 있을 까요?</b></summary>
  <div>
    DAO는 DB 접근 자체에 집중한 방식이고, Repository는 도메인 관점에서 데이터 접근을 추상화한 객체입니다. Repository는 객체 중심 설계에 더 적합해 JPA에서 주로 사용됩니다.
  </div>
</details><br>

<details>
  <summary><b>DTO를 불변 객체로 만들면 어떤 장점이 있으며, 불변 객체 DTO는 어떻게 만들까요?</b></summary>
  <div>
    데이터 전달 중간에 상태가 바뀌는 것을 방지할 수 있습니다. setter 메서드를 삭제하고, 생성자를 통해 속성값을 초기화하여 불변 객체 DTO를 만들 수 있습니다.
  </div>
</details><br>

<details>
  <summary><b>VO에서 equals, hashCode를 오버라이딩 해야하는 이유는 무엇일까요?</summary>
  <div>
    VO는 값이 같으면 같은 객체로 간주하기 때문에 동등성 비교를 위해 equals와 hashCode를 오버라이딩해야 합니다.
  </div>
</details><br>

<details>
  <summary><b>VO를 사용하는 것이 원시 타입(int, String 등)보다 어떤 점에서 유리한가요?</summary>
  <div>
    VO는 관련된 값을 하나의 객체로 묶어 의미를 명확히할 수 있고 유효성 검사와 불변성보장을 통해 안정성을 높일 수 있습니다. 원시 타입은 단순하지만 중복 코드가 발생하고 도메인의 의미를 표현하기 어렵기 때문에 VO가 유지보수성과 재사용성 측면에서 더 유리합니다.
  </div>
</details><br>
