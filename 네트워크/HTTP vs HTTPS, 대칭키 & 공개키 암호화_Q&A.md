## 신예지
<details>
  <summary><b>HTTP와 HTTPS의 차이를 설명하고 왜 HTTPS가 필요한지 설명해주세요</b></summary><br>
  HTTP는 비암호화된 기본 통신 프로토콜이고, HTTPS는 SSL/TLS를 사용해 데이터를 암호화하고, 서버 인증을 제공하는 보안 프로토콜입니다.<br><br>
  
  HTTPS는 데이터 암호화, 서버 인증, 데이터 무결성을 통해 보안 위협으로부터 사용자를 보호하므로 필요합니다.
</details>


<details>
  <summary><b>비대칭키 암호화 방식 중 개인키 암호화 방식의 실제 활용 예시를 들어주세요</b></summary><br>
  데이터 제공자의 신원이 보장되는 ‘전자서명’ 등의 공인인증체계
</details>

<details>
  <summary><b>대칭키 암호화의 단점에 대해 설명해주세요</b></summary><br>
  
  - 키 교환 과정 중 노출의 위험이 있음
  - 송/수신자가 늘어날수록 키의 수가 늘어나므로 관리하기 어려움
</details>

<details>
  <summary><b>SSL Handshake 과정을 설명해주세요</b></summary><br>
  
  1. **Client Hello** → 클라이언트가 지원하는 암호화 방식(암호 스위트)과 랜덤 값 전송
2. **Server Hello** → 서버가 선택한 암호화 방식과 랜덤 값 전송
3. **인증 & 키 교환** → 서버는 SSL 인증서(공개키 포함)를 전송하고, 클라이언트는 이를 검증
4. **세션 키 생성** → 클라이언트와 서버가 대칭키를 생성하여 이후 데이터 암호화
5. **Finished** → 보안 연결 설정 완료, 이후 데이터 암호화 통신 시작
</details>

<details>
  <summary><b>멱등성이란 무엇이고, HTTP Method의 속성 중 멱등성을 가진 메서드를 말해주세요</b></summary><br>

  멱등성이란 여러 번 동일한 요청을 보내도 서버에 미치는 의도된 영향이 동일한 성질

주요 메서드: `GET`, `PUT`, `DELETE`

기타 메서드: `HEAD`, `OPTIONS`, `TRACE`
</details>

<details>
  <summary><b>클라이언트가 서버에 DELETE /post/1 요청을 보냈고, 서버의 응답으로 200이 왔습니다. 그리고 서버에 같은 요청을 보냈더니 이번에는 응답으로 404가 왔습니다. 이는 멱등성이 지켜진 상황인가요? (O / X)</b></summary><br>
  네. 멱등성은 응답값이 동일한지에 따라 결정되는 것이 아니라 서버의 상태가 동일한지에 따라 결정됩니다. DELETE의 경우 서버의 응답은 다르지만 서버의 상태는 동일하게 post/1이 사라진 상태이므로 멱등성이 지켜진 상황입니다.
</details>

<details>
  <summary><b>캐싱이 가능한 메서드를 말해주세요</b></summary><br>
    
  `GET`, `HEAD` → HTTP 캐싱이 가능한 메서드는 **주로 읽기 전용 메서드**
    
  `POST`, `PUT` → 기본적으로 캐싱되지 않지만, 캐시 정책에 따라 일부 가능
</details>

<details>
  <summary><b>POST 메서드도 데이터의 조회가 가능합니다. 그런데 왜 데이터를 조회할 때는 GET을 이용할까요?</b></summary><br>
  GET 대신 POST를 사용하면 캐싱이 어렵고, 불필요한 부하가 발생할 수 있기 때문입니다.
</details>

<details>
  <summary><b>HTTP 상태코드 401과 403의 차이를 설명해주세요</b></summary><br>
  
  **401 Unauthorized** → 인증이 필요하지만 인증되지 않음

**403 Forbidden** → 인증은 되었지만 접근 권한 없음

401의 경우 서버가 누가 요청했는지 모르는 상태이고, 403의 경우 서버가 클라이언트의 신원을 알고 있지만 접근을 허용하지 않음
</details>

---

## 이소원
<details>
  <summary><b>HTTP와 HTTPS는 어떤 차이가 있나요?</b></summary><br>
  
  HTTP는 웹에서 데이터를 주고받는 프로토콜이며, HTTPS는 HTTP에 SSL/TLS를 적용하여 보안을 강화한 프로토콜입니다.

HTTPS는 대칭키와 비대칭키 암호화를 조합하여 데이터를 보호합니다.

클라이언트와 서버 간 SSL/TLS handshake를 수행하여 세션 키(대칭키)를 안전하게 공유합니다.

이후 데이터를 대칭키로 암호화하여 성능과 보안성을 확보하는데 이를 통해 HTTPS를 사용하면 중간자 공격(MITM), 도청, 데이터 변조를 방지할 수 있으며, 웹사이트의 신뢰성을 높일 수 있습니다.
</details>

<details>
  <summary><b>비대칭키 암호화는 어떻게 보안을 보장하나요?</b></summary><br>

  비대칭키 암호화는 공개키와 개인키 한 쌍을 이용하여 데이터를 암호화하는 방식입니다.

공개키로 암호화된 데이터는 개인키로만 복호화할 수 있습니다.

예를 들어, 클라이언트가 서버의 공개키로 데이터를 암호화하면, 서버만이 자신의 개인키로 해당 데이터를 복호화할 수 있습니다.

이를 통해 보안이 중요한 환경(HTTPS, 전자서명, 인증서 기반 로그인 등)에서 안전하게 키를 공유할 수 있습니다.
</details>

<details>
  <summary><b>SSL/TLS 핸드셰이크 과정에서 어떤 암호화 방식이 사용되나요?</b></summary><br>

  SSL/TLS 핸드셰이크는 클라이언트와 서버가 안전한 통신을 위해 암호화 방식을 협상하고 대칭키를 교환하는 과정입니다.

클라이언트가 서버에 지원하는 암호화 방식(암호 스위트)을 전달합니다.

서버는 사용할 암호화 방식과 자신의 SSL 인증서를 전송합니다.

클라이언트는 서버의 인증서를 검증하고 세션 키를 생성한 뒤 서버의 공개키로 암호화하여 전달합니다.

서버는 자신의 개인키로 이를 복호화하여 세션 키를 얻습니다.

이후부터는 세션 키(대칭키)를 사용하여 빠르게 데이터 암호화가 이루어집니다.

이 과정을 통해 비대칭키 암호화의 보안성과 대칭키 암호화의 속도를 결합하여 안전한 통신이 가능합니다.
</details>

<details>
  <summary><b>HTTPS를 사용하면 완벽한 보안이 보장되나요?</b></summary><br>
  
  HTTPS는 데이터를 암호화하여 중간자 공격(MITM)과 도청을 방지할 수 있습니다.

하지만 HTTPS 자체가 완벽한 보안을 보장하지는 않습니다.

SSL 인증서가 위조되거나, 브라우저가 신뢰할 수 없는 CA에서 발급된 인증서를 받아들이면 피싱 공격이 가능합니다.

또한, 클라이언트가 악성 사이트에서 HTTPS를 사용한다고 해서 해당 사이트가 안전한 것은 아닙니다.

+) HTTPS 보안 강화 방법

- HSTS(HTTP Strict Transport Security)를 적용하여 강제 HTTPS 사용
- 정상적인 CA에서 발급된 인증서 사용
- 인증서 핀닝(Certificate Pinning) 적용
</details>

<details>
  <summary><b>HTTP 상태코드는 어떤 것들이 있고, 어떤 역할을 하나요?</b></summary><br>

  HTTP 상태 코드는 클라이언트와 서버 간 통신 결과를 나타내는 숫자 코드입니다.

- 1xx (정보): 요청이 처리 중임을 알림
- 2xx (성공): 요청이 성공적으로 처리됨
- 3xx (리다이렉션): 클라이언트가 다른 URL로 이동해야 함
- 4xx (클라이언트 오류): 잘못된 요청
- 5xx (서버 오류): 서버에서 요청을 처리하지 못함

 의미: 상태 코드는 API 통신, 디버깅, 로깅 등에서 중요한 역할을 합니다.
</details>

<details>
  <summary><b>대칭키 암호화와 비대칭키 암호화의 차이점은 무엇인가요?</b></summary><br>

  대칭키 암호화

- 하나의 키(Secret Key) 로 암호화와 복호화 진행
- 속도가 빠르지만 키를 안전하게 공유하는 문제가 발생

비대칭키 암호화

- 공개키(Public Key)와 개인키(Private Key) 한 쌍으로 암호화 및 복호화
- 공개키로 암호화하면 개인키로만 복호화 가능
- 속도가 느리지만 키를 안전하게 공유할 수 있음

HTTPS에서는 비대칭키를 이용해 대칭키를 안전하게 전달한 후, 대칭키로 데이터 암호화를 수행합니다.
</details>

<details>
  <summary><b>사용자가 직접 HTTP 응답 코드를 정의할 수 있을까요?</b></summary><br>

  아니요, HTTP 상태 코드는 공식적으로 정해진 코드만 사용할 수 있습니다.

그러나 비표준 코드를 사용할 방법은 있습니다.

비표준 상태 코드가 필요할 경우 표준 HTTP 상태 코드 + 응답 바디(body) 방식을 활용하는 것이 일반적입니다.

```bash
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
  "code": 285,
  "message": "Custom error: Specific business logic validation failed."
}
```

그러나 비표준 코드 대신 기존 표준 코드(200, 400, 500 등)와 JSON 응답을 활용하는 것이 가장 좋은 방법입니다.
</details>

<details>
  <summary><b>멱등성과 관련하여 get과 post 방식의 차이에 대해 설명해주세요</b></summary><br>

  GET은 데이터를 조회하기 위해 사용되며, 같은 데이터를 여러 번 보내도 결과가 변하지 않아 멱등성이 보장됩니다.

반면 POST는 데이터를 생성할 때 사용되며, 같은 요청을 여러 번 보내면 중복 데이터가 생성될 수 있어 비멱등성을 가집니다.
</details>

---

## 변하영
<details>
  <summary><b>HTTP와 HTTPS의 차이점은 무엇인가요?</b></summary><br>

  HTTP는 데이터를 암호화하지 않고 전송하지만, HTTPS는 SSL/TLS를 사용해 데이터를 암호화하여 보안성을 높입니다. HTTPS는 데이터 도청 및 위변조를 방지하며, 신뢰할 수 있는 인증서를 통해 서버의 신원을 검증할 수 있습니다. 
</details>

<details>
  <summary><b>HTTP가 기본적으로 Connectionless한 프로토콜이라는 것은 어떤 의미인가요?</b></summary><br>

  HTTP는 클라이언트가 요청을 보내고 서버가 응답을 반환한 후 연결을 종료하는 방식입니다. 즉, 요청마다 새로운 연결을 맺고 끊는 구조로 동작합니다. 그러나 HTTP/1.1부터는 keep-alive를 통해 일정 시간 동안 연결을 유지할 수 있도록 개선되었습니다. 
</details>

<details>
  <summary><b>HTTP에서 GET과 POST 메소드의 주요 차이점은 무엇인가요?</b></summary><br>

  GET은 주로 데이터를 조회하는데 사용되며, 요청 데이터를 URL에 포함시킵니다. 반면, POST는 데이터를 서버에 저장하거나 변경할 때 사용되며, 요청 body에 데이터를 포함합니다. GET은 멱등성을 가지지만, POST는 멱등성이 없습니다.
</details>

<details>
  <summary><b>HTTP 메소드 중 멱등성을 가지는 메소드는 무엇이고, 멱등성이 필요한 이유는 무엇인가요?</b></summary><br>

  GET, HEAD, PUT, DELETE, OPTIONS 메소드는 멱등성을 가집니다. 멱등성이란 동일한 요청을 여러 번 보내도 서버의 상태가 변하지 않는 성질을 의미합니다. 이는 네트워크 장애로 재요청이 발생한 경우, 중복 실행으로 인한 부작용을 방지하는데 유용합니다. 
</details>

<details>
  <summary><b>HTTP 상태 코드 301과 302의 차이점은 무엇인가요?</b></summary><br>

  301은 영구 이동을 의미하며, 리소스의 위치가 영구적으로 변경된 경우 사용됩니다. 302는 임시 이동을 의미하며, 리소스의 위치가 일시적으로 변경된 경우 사용됩니다. 브라우저는 301을 받으면 캐시하여 다음 요청부터 새로운 URL을 사용합니다. 
</details>

<details>
  <summary><b>SSL/TLS에서 대칭키 암호화와 비대칭키 암호화는 각각 어떤 역할을 하나요?</b></summary><br>
  
  비대칭키 암호화는 클라이언트와 서버 간의 안전한 키 교환을 위해 사용되며, 공기캐로 데이터를 암호화하고 개인키로 복호화합니다. 이후 실제 데이터 전송에는 속도가 빠른 대칭키 암호화를 사용하여 데이터를 보호합니다 
</details>

<details>
  <summary><b>SSL handshake 과정에서 클라이언트는 서버의 인증서를 어떻게 검증하나요?</b></summary><br>

  클라이언트는 서버가 제공한 SSL 인증서를 검증하기 위해 CA의 공개키를 사용하여 전자 서명을 확인합니다. CA가 신뢰할 수 있는 기관이라면, 해당 서버가 인증된 서버임을 보장할 수 있습니다.
</details>

<details>
  <summary><b>HTTPS를 사용하면 웹사이트의 성능이 떨어지나요?</b></summary><br>

  초기에는 SSL handshake 과정으로 인해 약간의 성능 저하가 발생할 수 있습니다. 하지만 HTTP/2와 TLS1.3에서는 성능 최적화가 이루어져 오히려 HTTP/1.1보다 빠른 경우도 많습니다. 특히 Multiplexing과 0-RTT handshake는 성능을 크게 개선합니다. 
</details>

<details>
  <summary><b>SSL 인증서는 어떻게 얻을 수 있나요?</b></summary><br>

  CA에서 발급받을 수 있습니다. 대표적인 CA로는 Let’s Encrypt, DigiCert, GlobalSign 등이 있습니다. 서버가 HTTPS를 지원하려면 인증서를 서버에 설치하고 올바르게 설정해야 합니다. 
</details>

<details>
  <summary><b>브라우저에 “이 사이트는 안전하지 않음”이라고 경고가 뜨는 이유는 무엇일까요?</b></summary><br>

  HTTPS가 아닌 HTTP로 접속할 때, SSL 인증서가 만료되었거나 신뢰할 수 없는 CA에서 발급되었을 때, 인증서의 도메인과 실제 도메인이 일치하지 않을 때 경고가 뜹니다. 이를 해결하려면 인증서를 갱신하거나 올바른 인증서를 설치해야 합니다. 
</details>

---

## 박상윤

<details>
  <summary><b>HTTP 요청 메시지 구성 요소를 말해라요</b></summary><br>
  Method, Path, Version of protocal, Headers
</details>

<details>
  <summary><b>HTTP 응답 메시지 구성 요소를 말해라요</b></summary><br>
  HTTP 프로토콜 버전

상태 코드

상태코드의 짧을 설명을 나타내는 상태 메시지

Headears
</details>

<details>
  <summary><b>HTTPS에서 SSL/TLS 프로토콜은 어디에 위치할까?</b></summary><br>
  HTTP(응용 계층 프로토콜)과 TCP(전송 계층 프로토콜) 사이
</details>

<details>
  <summary><b>HTTPS 통신 방식은 뭐가 있을까?</b></summary><br>
  대칭키 방식, 공개키 방식
</details>

<details>
  <summary><b>TLS가 나온 배경은</b></summary><br>
  SSL의 취약점들을 개선하기 위해서
</details>

<details>
  <summary><b>대칭키 암호화 방식에 대해서 설명하라</b></summary><br>
  똑같은 개인 키를 송-수신자가 공유하여 정보를 암호화 하는것
</details>

<details>
  <summary><b>비대칭키 암호화 방식에 대해서 설명하라</b></summary><br>
  공개키와 개인키가 한 쌍으로 이루어진 암호화 방식
</details>

<details>
  <summary><b>개인키 암호화 방식은 어떻게 되는가?</b></summary><br>
  개인키로 암호화하고, 공개키로 복호화합니다.
</details>

<details>
  <summary><b>공개키 암호화 방식은 어떻게 되는가?</b></summary><br>
  공개키로 암호화하고, 개인키로 복호화합니다.
</details>

<details>
  <summary><b>HTTP 상태 코드에서 1xx, 2xx, 3xx, 4xx, 5xx가 의미하는 건 무엇일까?</b></summary><br>
  - `1xx (조건부 응답)`
- `2xx (성공)`
- `3xx (리다이렉션)`
- `4xx (클라이언트 오류)`
- `5xx (서버 오류)`
</details>

<details>
  <summary><b>HTTP 주요 메서드와 각 메서드가 어떤 의미를 담고 있는지도 말하시</b></summary><br>
  - `GET` : 리소스 조회
- `POST` : 요청 데이터 처리, 등록
- `PUT` : 리소스 대체(덮어쓰기), 해당 리소스가 없을 시 생성
- `PATCH` : 리소스 부분 변경
- `DELETE` : 리소스 삭제
</details>

<details>
  <summary><b>GET 메서드의 특징 2가지는?</b></summary><br>
  멱등성을  가지고, 캐싱 이용으로 조회 속도가 빠르다.
</details>

<details>
  <summary><b>멱등성을 지니는 메서드와 멱등성을 지니지 않는 메서드를 말하시오</b></summary><br>
  멱 : GET, PUT,DELETE  멱x : POST,  PATCH
</details>

