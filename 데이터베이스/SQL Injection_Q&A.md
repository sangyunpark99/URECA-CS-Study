## 박상윤
<details>
  <summary><b>다음 코드에서 SQL Injection이 가능한 부분을 찾고 어떻게 우회가 가능할까요? 해결 방법은?</b></summary><br>

  로그인 상황

  ```java
  String query = "SELECT * FROM users WHERE username = '" + username + "' AND password = '" + password + "'";
  Statement stmt = connection.createStatement();
  ResultSet rs = stmt.executeQuery(query);
  ```
</details>

<details>
  <summary><b>검색 기능이 아래와 같다고 가정할 때, 공격자가 유저의 pk와 이름 컬럼을 탈취할 수 있는 SQL을 작성해주세요. </b></summary><br>

  ```sql
SELECT id, name FROM products WHERE name LIKE '%검색어%';
```
</details>

<details>
  <summary><b>블랙 리스트와 화이트 리스트는 보통 사람을 칭한다. (o,x)</b></summary><br>

  x

사람뿐 만이 아닌 특정 IP를 가진 PC, 실행 파일, 프로세스, 웹 사이트 등이 되기도 함

</details>

<details>
  <summary><b>DB 서버의 응답 시간을 기준으로 공격자가 데이터베이스 정보를 추출하는 기법이 뭘까요?</b></summary><br>

  Time based SQL Injection
</details>

<details>
  <summary><b>블랙 리스트와 화이트 리스트의 차이점을 말하시요.</b></summary><br>

  화이트 리스트. : **모든 접근을 막아놓고 접근 허용 대상만 따로 등록**하는 방식

블랙 리스트 : 기본적으로 **모든 접근을 허용하되 접근하지 못하는 예외**를 두는 방식
</details>

## 변하영
<details>
  <summary><b>SQL Injection 중 Classic SQL Injection과 Blind SQL Injection 차이점은 무엇인가요?</b></summary><br>

  Classic SQL Injection의 경우 공격자가 직접 쿼리 결과를 확인할 수 있는 반면에 Blind SQL Injection은 응답이 없거나 제한적이라 참/거짓 기반 또는 응답 시간을 이용해 정보를 유추합니다. 
</details>

<details>
  <summary><b>화이트리스트와 블랙리스트 기반 보안의 차이점은 무엇인가요?</b></summary><br>

  화이트리스트는 허용할 입력만 지정하여 보안성이 높지만, 관리 부담이 큽니다. 블랙리스트의 경우 금지할 입력을 지정하여 관리 부담이 크지 않지만, 모든 경우를 차단하기 어렵습니다. SQL Injection 방어에는 화이트리스트 기반 입력 검증이 효과적입니다.
</details>

<details>
  <summary><b>Error-based SQL Injection과 Union-based SQL Injection의 차이점은 무엇인가요?</b></summary><br>

  Error-based SQL Injection은 에러 메시지를 이용해 데이터베이스 정보를 유출하는 공격 방식이고, Union-based SQL Injection은 UNION 키워드를 사용해 추가 데이터를 조회하는 방식입니다 
</details>

<details>
  <summary><b>Boolean-based SQL Injection과 Time-based SQL Injection의 차이점이 무엇인가요?</b></summary><br>

  Boolean-based SQL Injection은 참/거짓 여부를 판단하여 정보를 유추하는 방식이고 Time-based SQL Injection은 특정 조건을 만족하면 sleep()을 사용해 서버 응답을 지연시켜 정보를 유추하는 방식입니다. 
</details>

## 신예지
<details>
  <summary><b>Error Based SQL Injection의 원리를 설명해주세요</b></summary><br>

  **Error Based SQL Injection은 논리적 에러**를 이용한 SQL 인젝션은 대중적인 공격 기법이다. 

SQL구문 에러를 발생 시 반환되는 정보를 통해 데이터베이스의 테이블/컬럼/데이터의 개수와
이름을 확인하는 과정을 반복하여 원하는 데이터를 추출하는 원리이다
</details>

<details>
  <summary><b>SQL Injection을 방어하기 위한 방법을 3가지만 얘기해주세요</b></summary><br>
  
  1. 화이트리스트 기반 검증
2. Prepared Statement 사용
3. 에러 메시지 최소화
4. 웹 방화벽 사용
5. 입력 값의 정규화
6. 최소 권한 원칙
7. 보안 업데이트
</details>

<details>
  <summary><b>화이트리스트 방식의 장단점을 설명해주세요</b></summary><br>

  장점

- 쉽고 빠른 보안 조치 가능
- 담당자의 노동이 적게 들어감

단점

- 새로운 입력값이 필요할 경우 **화이트리스트를 업데이트해야 함**
- 일부 인코딩된 공격(payload)은 필터링을 우회할 수 있음
</details>

<details>
  <summary><b>Union based SQL Injection을 성공하기 위한  조건을 말해주세요</b></summary><br>

  1. Union 하는 두 테이블의 `컬럼 수`가 같아야 함
2. Union 하는 두 테이블의 `데이터 형`이 같아야 함
</details>

<details>
  <summary><b>다음은 SQL Injection 종류 중 무엇을 이용한것일까요? (열어보세요)</b></summary><br>

  ```sql
SELECT * FROM users WHERE id = 1 AND IF( (SELECT COUNT(*) FROM users WHERE username='admin') > 0, SLEEP(5), 0);
```

  <details>
    <summary><b>정답 (열어보지마세요!!)</b></summary><br>
    Boolean-Based SQL Injection, Time-Based SQL Injection

  </details>
</details>

<details>
  <summary><b>블랙리스트나 화이트리스트가 될 수 있는 대상을 말해주세요</b></summary><br>
    
    사람, 특정 IP를 가진 PC, 실행 파일, 프로세스, 웹 사이트 등
</details>

## 이소원
<details>
  <summary><b>SQL Injection이 뭔가요?</b></summary><br>

  SQL Injection은 사용자가 입력한 데이터를 검증 없이 SQL 쿼리에 직접 삽입할 때 발생하는 보안 취약점 입니다.
</details>

<details>
  <summary><b>SQL Injection 대응 방안 중 화이트 리스트와 블랙 리스트의 차이를 설명해주세요.</b></summary><br>

  - 화이트 리스트
    - 기본적으로 모든 접근을 막고, 접근 허용 대상을 등록하는 방식
    - 엄격한 보안 체계를 구축할 수 있다는 장점이 있지만, 허용 대상 요청 등 업무량이 많아진다는 문제가 있다.
- 블랙 리스트
    - 기본적으로 모든 접근을 허용하고, 접근하지 못하는 예외를 두는 방식
    - 방화벽이나 백신 등에 사용하는 방식
    - 쉽고 빠른 보안 조치가 가능하다는 장점이 있지만, 예상치 못한 엑세스는 막지 못한다.
</details>

<details>
  <summary><b>사용자가 입력한 username과 password 일치 여부를 확인 후 로그인을 하는 쿼리문을 작성할 때 sql injection에 대응하려면 어떻게 할 수 있을까요?</b></summary><br>

  - Prepared Statement 사용
    - 입력 값을 직접 SQL 문자열에 삽입하지 않고, 바인딩 변수(place holder)를 사용하여 안전하게 처리할 수 있습니다.
    - Prepared Statement 사용하면 사용자의 입력값이 자동으로 이스케이프되어 공격을 방어할 수 있습니다.
</details>

<details>
  <summary><b>UNION SQL Injection과 Blind SQL Injection의 차이점은?</b></summary><br>

  - UNION SQL Injection
    - UNION SELECT를 사용하여 DB 테이블을 직접 조회하는 방식
- Blind SQL Injection
    - 결과가 직접 출력되지 않고 참/거짓으로 확인하는 방식
</details>

## 김수훈
<details>
  <summary><b>SQL Injection에 대해서 설명해주세요.</b></summary><br>

  SQL Injection은 공격자가 웹 애플리케이션의 입력 필드에 악의적인 SQL 구문을 삽입하여 데이터베이스를 조작하는 공격 기법입니다. 이를 통해 공격자는 데이터베이스의 데이터를 탈취하거나, 수정, 삭제할 수 있으며, 인증을 우회할 수도 있습니다.
</details>

<details>
  <summary><b>SQL Injection을 방어하기 위한 방법을 말해주세요.</b></summary><br>

  1. 입력값을 검증하여 사용자의 입력이 쿼리에 동적으로 영향을 주는 경우 입력된 값이 개발자가 의도한 값(유효값)인지 검증합니다.
2. 저장 프로시저를 사용합니다.

> 저장 프로시저 : 사용하고자 하는 Query에 미리 형식을 지정하는 것을 말한다. 
지정된 형식의 데이터가 아니면 Query가 실행되지 않기 때문에 보안성이 크게 향상한다.
</details>

<details>
  <summary><b>Union based SQL Injection에서 Union 인젝션을 성공하기 위한 조건이 무엇인지 설명하고, 해당 조건이 붙는 이유를 설명해보세요.</b></summary><br>

  ### 조건

1. Union 하는 두 테이블의 컬럼 수가 같아야 한다.
2. Union 하는 두 테이블의 데이터 형이 같아야 한다.

### 이유

데이터베이스에서 Union(합집합) 연산을 수행하기 위해서는 위 조건을 만족해야 하기 때문입니다.
</details>

<details>
  <summary><b>SQL Injection의 대응방안 중 입력값의 정규화에 대해 설명해주세요</b></summary><br>

  - 입력 값이 예상과 다른 형식이면 거부하도록 정규화를 수행합니다.
- 예를 들어, 숫자를 기대하는 필드에 문자열이 입력되는 경우를 방지할 수 있습니다.
</details>
