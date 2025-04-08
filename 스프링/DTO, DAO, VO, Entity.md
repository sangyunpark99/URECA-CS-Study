# DTO, DAO, VO, Entity
## DTO
> Data Transfer Object, 데이터 전송 객체

### 개념
- 계층 간 데이터 전송을 위한 객체
- Controller ↔ Service ↔ View 간 데이터 전달에 사용
- 요청(Request) 또는 응답(Response) 데이터를 담는 용도

### 특징
- getter, setter를 가진 Java Bean 형식의 클래스
- 일반적으로 비즈니스 로직 없이 데이터만 담음
- 필요한 데이터만 담기 때문에 가볍고 명확

### 사용 목적
- Entity와 분리하여 API 명세를 안정적으로 유지
- 뷰의 변화에 유연하게 대응
- 요청/응답에 필요한 데이터만 노출하여 보안 강화

### 예시 코드
#### 
```java
// 가변 DTO 예시 (setter 포함)
public class UserRequestDto {
    private String name;
    private int age;

    public String getName() { return name; }
    public int getAge() { return age; }

    public void setName(String name) { this.name = name; }
    public void setAge(int age) { this.age = age; }
}
```
```java
// 불변 DTO 예시 (생성자만 사용)
public class UserResponseDto {
    private final String name;
    private final int age;

    public UserResponseDto(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() { return name; }
    public int getAge() { return age; }
}
```
### 주의사항
⚠️ 주의사항
- Entity를 그대로 반환하거나 받는 방식은 지양
&rarr; API 요청/응답 스펙이 DB 구조에 종속되기 때문

---
## DAO
> Data Access Object

### 개념
- 데이터베이스와 직접 통신하여 CRUD를 수행하는 객체
- DB 접근 로직을 비즈니스 로직과 분리하여 캡슐화

### 특징
- DB 연결/쿼리 실행/결과 반환 역할
- SQL과 밀접하게 연관, Mapper(XML) 또는 Annotation 기반
- Persistence 계층을 구성하는 핵심 컴포넌트

### 사용 목적
- DB 연동 코드의 재사용성과 유지보수성 향상
- 데이터 접근 책임을 한 곳으로 모아 관심사 분리 (SoC) 실현

### 예시 코드 (MyBatis)
```java
@Mapper
public interface UserDao {
    UserEntity findById(Long id);
    void insertUser(UserEntity user);
    void deleteUser(Long id);
}
````
```java
@Repository
public interface UserRepository extends JpaRepository<UserEntity, Long> {
    Optional<UserEntity> findByEmail(String email);
}
````

### 주의사항
- DAO는 SQL 직접 제어가 가능하지만, 복잡한 비즈니스 로직은 포함하지 않아야 함

---

## VO
> Value Object, 값 객체

### 개념
- 값 그 자체를 의미하는 객체
- 도메인 모델 내부에서 의미 있는 값을 표현할 때 사용

### 특징
- 불변성 (Immutable): 값 변경 불가, setter 없음
- 동등성 (Equality): 필드 값이 같으면 같은 객체로 취급 (equals, hashCode 오버라이딩 필요)
- 자가 유효성 검사(Self-validation): 객체 생성 시 유효성 검사 포함
- getter 외의 비즈니스 로직 포함 가능

### 사용 목적
- 원시 타입(primitive type)의 중복 제거
- 의미 있는 값 표현과 유효성 검사를 한 곳에서 처리
- 재사용성과 가독성 향상

### 예시 코드
```java
public class ShapeProperty {
    private final int width;
    private final int height;

    public ShapeProperty(int width, int height) {
        validate(width, height);
        this.width = width;
        this.height = height;
    }

    private void validate(int width, int height) {
        if (width < 0 || height < 0) throw new IllegalArgumentException("Invalid dimension");
    }

    public int getWidth() { return width; }
    public int getHeight() { return height; }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof ShapeProperty)) return false;
        ShapeProperty that = (ShapeProperty) o;
        return width == that.width && height == that.height;
    }

    @Override
    public int hashCode() {
        return Objects.hash(width, height);
    }
}
````

### 주의사항
- 여러 Entity가 VO를 공유할 경우 Side effect 발생 가능
&rarr; Entity마다 별도의 VO 인스턴스를 갖도록 주의

---

## Entity
### 개념
- 데이터베이스 테이블과 매핑되는 객체
- @Entity 어노테이션을 통해 JPA에서 관리

### 특징
- **식별자(Primary Key)**를 갖고 있음
- 비즈니스 로직 포함 가능 (응집력 있는 도메인 모델)
- DB 컬럼과 매핑되는 필드로 구성됨
- **변경 가능(mutable)**하며, 영속 상태 관리

### 사용 목적
- 데이터베이스 테이블과의 매핑을 통해 ORM 처리
- 트랜잭션, Lazy Loading 등 JPA 기능 활용

### 예시 코드
```java
@Entity
public class UserEntity {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private int age;

    public void updateName(String newName) {
        this.name = newName;
    }

    // Getter, Setter 생략 가능 (Lombok 사용 가능)
}
````

### 주의사항
- Entity를 API 요청/응답에 직접 사용하지 말 것
&rarr; 뷰 변경에 따른 Entity 수정 &rarr; DB 구조에도 영향
&rarr; 항상 DTO로 변환 후 전달