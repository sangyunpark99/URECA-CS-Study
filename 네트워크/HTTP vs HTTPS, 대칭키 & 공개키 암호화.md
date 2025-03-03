# HTTP
## HTTP란?
> HTTP(Hypertext Transfer Protocol)은 **텍스트 기반의 통신 규약으로 인터넷에서 데이터를 주고받을수 있는 프로토콜**이다.

**클라이언트-서버 모델**을 기반으로 동작하며, 주로 HTML 문서, 이미지, 동영상 등 다양한 리소스를 전송하는 데 사용된다.
<img src="https://github.com/user-attachments/assets/a62cb9ee-28c1-4ab5-8298-a104075dcb6d" width = "500"/>

## HTTP의 특징
**1. 비연결성(Connectionless)**
  - 클라이언트가 요청(Request)을 보내고, 서버가 응답(Response)을 보내면 연결을 종료
  - 요청마다 새로운 연결을 생성하므로, 불필요한 자원 사용이 발생할 수 있음
  - 해결책: HTTP/1.1부터 기본적으로 지속적인 연결(Persistent Connection)을 지원하며, Connection: close를 명시해야 연결이 종료됨

**2. 무상태성(Stateless)**
  - 서버는 클라이언트의 이전 요청 정보를 저장하지 않음
  - 매 요청이 독립적으로 처리되므로 확장성이 높지만, 사용자의 상태를 유지하려면 별도의 방법이 필요함
  - 해결책: 쿠키(Cookie), 세션(Session), 토큰(JWT) 등의 기술을 사용하여 상태를 유지할 수 있음

**3. TCP/IP 기반 프로토콜(Transport & Network Layer 사용)**
  - HTTP는 애플리케이션 계층(Application Layer)에서 동작하는 프로토콜로, TCP/IP 프로토콜 스택을 기반으로 동작함
  - HTTP 자체는 데이터 전송을 담당하지 않고, 아래 계층의 프로토콜을 통해 데이터를 전달함
  - 기본적으로 TCP(Transmission Control Protocol)를 사용하여 신뢰성 있는 데이터 전송을 보장함

## HTTP의 요청/응답 메세지
### HTTP 요청
```http
GET /hello HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/html
```
**요청 라인(Request Line)**
- GET: 요청 메서드
- /hello: 요청 URL
- HTTP/1.1: HTTP 버전

**헤더(Header)**

요청에 대한 부가 정보를 전달하는 영역

- Host: 요청 대상 서버
- User-Agent: 클라이언트 정보 (브라우저, OS 등)
- Accept: 클라이언트가 받을 수 있는 응답 형식 지정

**빈 줄(CRLF, Carriage Return + Line Feed)**

헤더와 바디를 구분하는 역할 (헤더 끝을 의미)

**바디(Body)**

POST, PUT 같은 요청에서 데이터를 전송할 때 사용

서버에 대한 추가 정보 전달하는 선택적 헤더들

### HTTP 응답
```http
HTTP/1.1 200 OK
Content-Type: text/html; charset=UTF-8
Content-Length: 27

<html><body>Hello!</body></html>
```
**응답 라인(Status Line)**

HTTP 버전 + 상태 코드 + 상태 메시지 포함

- HTTP/1.1: HTTP 버전
- 200: 상태 코드 (요청 성공)
- OK: 상태 메시지

**헤더(Header)**

응답에 대한 부가 정보 포함

- Content-Type: 응답 데이터의 형식
- Content-Length: 응답 데이터 크기
- Set-Cookie: 쿠키 설정

**빈 줄(CRLF, Carriage Return + Line Feed)**

헤더와 바디를 구분하는 역할 (헤더 끝을 의미)

**바디(Body)**

클라이언트가 요청한 데이터가 포함됨

# HTTPS
> HTTPS(Hypertext Transfer Protocol Secure)는 **HTTP에 보안 기능을 추가한 프로토콜**로, **SSL/TLS 프로토콜**을 통해 데이터를 암호화하여 안전한 통신을 제공함

## HTTPS의 특징
- 암호화 통신: 데이터가 암호화되어 전송되므로, 중간에 제3자가 데이터를 가로채더라도 내용을 확인할 수 없음
- 서버 인증: SSL/TLS 인증서를 통해 서버의 신원을 확인할 수 있음
- 데이터 무결성: 데이터가 전송 중에 변경되지 않았음을 보장함
- 기본 포트: TCP 포트 443번을 사용함

## HTTPS 통신
HTTPS는 비대칭 & 대칭 암호화를 혼합하여 사용하여 속도와 보안을 모두 만족함

### HTTPS 통신 과정
<img src="https://github.com/user-attachments/assets/7ce74750-4011-403d-8086-ff37038136aa" width = 500/>

**위의 그림과 밑의 설명의 번호가 다름**

#### 1) 클라이언트 → 서버: SSL/TLS 핸드셰이크 시작
1. 클라이언트가 ClientHello 메시지를 보냄
  - 지원하는 TLS 버전, 암호화 알고리즘, 랜덤 값 포함

#### 2) 서버 → 클라이언트: 공개키 전달
2. 서버가 ServerHello 메시지를 응답
  - 서버의 SSL 인증서(공개키 포함)를 클라이언트에 보냄

#### 3) 클라이언트 → 서버: 세션 키 생성 & 공유
3. 클라이언트는 비대칭 키 암호화(RSA 등) 를 사용하여 세션 키(대칭키)를 생성
4. 서버의 공개키로 세션 키를 암호화하여 서버에 전송

#### 4) 서버 → 클라이언트: 세션 키로 데이터 암호화
5. 서버는 자신의 개인키로 암호화된 세션 키를 복호화
6. 이후 클라이언트 & 서버는 세션 키(AES 등 대칭키)로 통신
7. 데이터는 대칭 암호화를 사용하여 빠르게 주고받음

## 비대칭 키 암호화 & 대칭 키 암호화
### 비대칭 키 암호화
> 공개키(Public Key)와 개인키(Private Key) 두 개의 키를 사용

공개키로 암호화하면 개인키로만 복호화 가능, 개인키로 암호화하면 공개키로만 복호화 가능

#### 비대칭 키 암호화 특징
- 안전하지만 속도가 느림 (복잡한 수학 연산)
- 키 분배가 용이함 (공개키를 여러 사람에게 배포 가능)
- 주로 데이터 교환 초기 단계(예: SSL/TLS Handshake)에서 사용

#### 활용 예시
- HTTPS(SSL/TLS에서 세션 키 교환)
- 전자서명(개인키로 서명하고, 공개키로 검증)
- SSH, PGP 등

### 대칭 키 암호화
> 하나의 공통된 키(Secret Key)를 사용하여 암호화 & 복호화

#### 대칭 키 암호화 특징
- 속도가 빠름 (비대칭 암호화보다 연산이 간단함)
- 보안 문제 (키를 안전하게 공유하는 것이 어려움)
- 주로 데이터 전송 과정에서 사용

#### 활용 예시
- HTTPS에서 세션 키(Session Key) 암호화
-	파일 암호화
- VPN, SSL/TLS 내부 통신

# HTTP Method
HTTP 메서드는 클라이언트가 서버에게 요청하는 **행동(동작)**을 정의하는 역할을 함

- 주요 메서드: GET, POST, PUT, PATCH, DELETE
- 기타 메서드: HEAD, TRACE, OPTIONS

## GET
> 데이터를 조회할 때 사용하는 메서드

### 특징
- 멱등성 보장 (같은 요청을 여러 번 보내도 결과가 동일)
- 캐싱 가능 (서버 응답을 저장하여 성능 향상)
- 데이터를 URL에 포함 (쿼리 스트링 형태) → 보안 취약 가능성 있음

### 예시
```http
GET /users/1 HTTP/1.1
Host: example.com
```

## POST
> 새로운 데이터를 서버에 생성할 때 사용

### 특징
- 멱등성 없음 (같은 요청을 여러 번 보내면 중복 데이터 생성 가능)
- 캐싱 불가능
- 데이터를 요청 본문(Body)에 포함 (GET보다 보안 측면에서 안전)

### 예시
```http
POST /users HTTP/1.1
Host: example.com
Content-Type: application/json

{
    "name": "Alice",
    "email": "alice@example.com"
}
```

## PUT
> 리소스를 전체 수정(덮어쓰기)할 때 사용

> 리소스가 존재하지 않으면 새로 생성

### 특징
- 멱등성 보장 (같은 요청을 여러 번 보내도 결과가 동일)
- 캐싱 불가능
- 전체 데이터를 갱신하므로 부분 업데이트에 부적절

### 예시
```http
PUT /users/1 HTTP/1.1
Host: example.com
Content-Type: application/json

{
    "name": "Alice",
    "email": "alice@example.com"
}
```

## PATCH
> 리소스의 일부만 수정할 때 사용

PUT과 달리 부분 업데이터가 가능

### 특징
- 멱등성 보장 X (서버 구현에 따라 다름)
- 캐싱 불가능
- 일부 필드만 변경 가능하므로 PUT보다 효율적

### 예시
```http
PATCH /users/1 HTTP/1.1
Host: example.com
Content-Type: application/json

{
    "email": "newemail@example.com"
}
```

## DELETE
> 리소스를 삭제할 때 사용

### 특징
- 멱등성 보장 (같은 요청을 여러 번 보내도 결과 동일)
- 캐싱 불가능

### 예시
```http
DELETE /users/1 HTTP/1.1
Host: example.com
```

## HEAD
> GET 요청과 동일하지만, 응답 본문(Body)을 반환하지 않음

응답의 메타데이터(헤더 정보)만 확인

### 특징
- 멱등성 보장
- 캐싱 가능
- 데이터를 실제로 가져오지 않고, 리소스 존재 여부만 확인

### 예시
```http
HEAD /users/1 HTTP/1.1
Host: example.com
```

## OPTIONS
> 특정 리소스에서 사용할 수 있는 HTTP 메서드를 확인할 때 사용

### 특징
- 멱등성 보장
- 캐싱 불가능
- CORS(교차 출처 리소스 공유) 요청에서 주로 사용됨

### 예시
```http
OPTIONS /users HTTP/1.1
Host: example.com
```

## TRACE
> 서버가 요청을 어떻게 처리하는지 확인할 때 사용

요청을 서버가 그대로 반환하여 네트워크 문제 디버깅 가능

### 특징
- 멱등성 보장
- 캐싱 불가능
- 보안 문제로 인해 대부분의 서버에서 비활성화됨

### 예시
```http
TRACE /users HTTP/1.1
Host: example.com
```

## 정리
- 안전한 메서드: GET, HEAD, OPTIONS, TRACE
- 멱등성 보장: GET, PUT, DELETE, HEAD, OPTIONS, TRACE
- 캐싱 가능: GET, HEAD

# HTTP 상태코드
> HTTP 상태 코드는 클라이언트의 요청에 대한 **서버의 응답 상태**를 나타내는 숫자 코드

1xx (정보):	요청을 받았으며, 처리 중

2xx (성공):	요청을 성공적으로 처리

3xx (리다이렉션):	요청한 리소스의 위치 변경

4xx (클라이언트 오류):	클라이언트 요청이 잘못됨

5xx (서버 오류):	서버에서 요청을 처리할 수 없음

## 1xx (정보 응답)
> 요청을 정상적으로 받았으며, 처리 중임을 의미

| 상태 코드 |	의미	| 설명 |
|--|--|--|
| 100 Continue | 계속 | 요청의 일부를 받고 문제없으니 계속 요청하라는 의미 |
| 101 Switching Protocols	| 프로토콜 변경 | 클라이언트 요청에 따라 서버가 프로토콜 변경을 승인 |
| 103 Early Hints	| 사전 정보 제공 | 본 응답 전에 일부 헤더를 미리 보낼 때 사용 |

## 2xx (성공)
> 클라이언트의 요청을 성공적으로 처리했음을 의미

| 상태 코드 |	의미	| 설명 |
|--|--|--|
| 200 OK | 성공 | 요청이 성공적으로 수행됨 |
| 201 Created	| 생성됨 | 요청이 성공하여 새로운 리소스가 생성됨 (ex: POST) |
| 202 Accepted	| 승인됨 | 요청이 서버에서 받아들여졌지만, 실제 처리는 비동기적으로 진행됨. 즉, 요청이 즉시 완료되지 않고 이후에 처리됨 |
| 204 No Content | 콘텐츠 없음 | 요청이 성공했지만 반환할 데이터가 없음 |

**200 vs 201 차이점?**
- 200 OK → 기존 리소스를 반환하는 경우
- 201 Created → 새로운 리소스를 생성하는 경우

## 3xx (리다이렉션)
> 클라이언트가 요청한 리소스의 위치가 변경되었음을 의미

| 상태 코드 |	의미	| 설명 |
|--|--|--|
| 301 Moved Permanently | 영구 이동 | 요청한 리소스가 영구적으로 새로운 URL로 이동 |
| 302 Found (Moved Temporarily) | 임시 이동 | 요청한 리소스가 임시적으로 다른 URL에 위치 |
| 303 See Other | 다른 리소스 참조 | 클라이언트가 GET 요청으로 리소스를 요청하도록 유도 |
| 304 Not Modified | 변경 없음 | 클라이언트 캐시된 리소스가 최신 상태임을 의미 |
| 307 Temporary Redirect | 임시 리디렉션 | 302와 유사하지만, 요청 메서드가 변경되지 않음 |
| 308 Permanent Redirect | 영구 리디렉션 | 301과 유사하지만, 요청 메서드가 변경되지 않음 |

**301 vs 302 vs 307 차이점?**
- 301: 영구적 이동, GET 요청으로 강제 변경될 수 있음
- 302: 임시 이동, 하지만 일부 브라우저에서는 요청 메서드를 GET으로 변경할 수 있음
- 307: 302와 유사하지만, 요청 메서드가 변경되지 않음

## 4xx (클라이언트 오류)
> 클라이언트의 요청이 잘못되었거나 권한이 없는 경우

| 상태 코드 |	의미	| 설명 |
|--|--|--|
| 400 Bad Request | 잘못된 요청 | 요청이 잘못됨 (ex: 잘못된 파라미터) |
| 401 Unauthorized | 인증 필요 | 인증되지 않은 사용자 (로그인 필요) |
| 403 Forbidden | 접근 금지 | 인증은 되었지만 권한이 없음 |
| 404 Not Found | 찾을 수 없음 | 요청한 리소스를 찾을 수 없음 |
| 405 Method Not Allowed | 허용되지 않는 메서드 | 해당 리소스에서 요청한 HTTP 메서드를 허용하지 않음 |
| 409 Conflict | 충돌 | 요청이 현재 상태와 충돌함 (ex: 중복 데이터 요청) |
| 429 Too Many Requests | 요청 한도 초과 | 너무 많은 요청을 보냄 (Rate Limit 초과) |

**401 vs 403 차이점?**
- 401 Unauthorized: 로그인이 필요한 상태 (인증 실패)
- 403 Forbidden: 로그인은 했지만 해당 리소스에 접근할 권한이 없음

## 5xx (서버 오류)
> 서버가 요청을 처리하는 과정에서 문제가 발생한 경우

| 상태 코드 |	의미	| 설명 |
|--|--|--|
| 500 Internal Server Error | 서버 오류 | 서버에서 처리 중 예기치 못한 오류 발생 |
| 502 Bad Gateway | 게이트웨이 오류 | 서버가 다른 서버로부터 잘못된 응답을 받음 |
| 503 Service Unavailable | 서비스 불가 | 서버 과부하 또는 유지보수 중 |
| 504 Gateway Timeout | 게이트웨이 타임아웃 | 서버가 응답을 기다리다 시간 초과됨 |

**502 vs 503 vs 504 차이점?**
- 502: 서버가 다른 서버로부터 잘못된 응답을 받음
- 503: 서버가 현재 요청을 처리할 수 없음 (과부하, 유지보수 등)
- 504: 서버가 응답을 기다리다가 시간 초과됨
