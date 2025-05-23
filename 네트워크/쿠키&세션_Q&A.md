## 변하영
<details>
  <summary>쿠키와 세션의 차이는 무엇인가요?</summary>
  쿠키는 클라이언트에 저장되고, 세션은 서버에 저장됩니다. 쿠키는 클라이언트가 직접 수정이 가능하지만, 세션은 서버가 관리해 보안성이 높습니다. 대신 세션은 사용자가 많아지면 서버 메모리를 많이 차지합니다.    
</details>

<details>
  <summary>세션의 동작과정에 대해 설명해주세요</summary>

1. 웹브라우저가 서버에 요청
2. 서버가 해당 웹브라우저(클라이언트)에 유일한 ID(Session ID)를 부여함  
3. 서버가 응답할 때 HTTP 헤더(Set-Cookie)에 Session ID를 포함해서 전송  
4. 웹브라우저는 부여된 Session ID를 쿠키에 저장해두고, 다음 요청 때마다 해당 쿠키를 HTTP 헤더에 넣어서 전송  
5. 서버는 Session ID를 확인하고, 해당 세션에 관련된 정보를 확인한 후 응답  
    - 로그인을 하는 경우, 해당 Session ID의 로그인 상태를 유효한 값으로 바꿔 저장  
    - 이후 요청에서 해당 Session ID를 가진 클라이언트는 로그인 상태가 유효하므로 별도의 로그인 없이 서비스 이용 가능
</details>

<details>
  <summary>JWT가 탈취되었을 때 어떻게 대처할 수 있나요?</summary>
  Access Token은 만료 시간을 짧게 설정하여 피해를 줄일 수 있고, Refresh Token을 사용하는 경우 서버에서 저장하고 관리하여 탈취되었을 때 무효화할 수 있습니다. 필요시 블랙리스트 처리도 가능합니다. 
</details>

<details>
  <summary>JWT에 민감한 정보를 저장해도 될까요? 이유는 무엇인가요?</summary>
  저장하면 안됩니다. JWT의 Payload는 단순히 Base64로 인코딩된 것이므로 누구나 내용을 확인할 수 있습니다. 민감한 정보는 저장하지 않거나 암호화해야합니다.
</details>

<details>
  <summary>HMAC 방식과 RSA 방식의 JWT 서명 차이는 무엇일까요?</summary>
  HMAC은 대칭 키 기반으로 서명자와 검증자가 동일해야 하지만, RSA는 비대칭키 기반으로 개인키로 서명하고 공개키로 검증할 수 있습니다. 이로 인해, 공개키를 여러 서버에 배포해도 안전하게 검증이 가능해, 분산 시스템 환경에서 더욱 적합합니다. 또한, 누가 서명했는지를 검증할 수 있어 서버 간 신뢰가 필요한 환경에서도 적합합니다. 
</details>

<details>
  <summary>다중 서버 환경에서의 세션 관리에 대해 설명해주세요. 어떤 방법들이 있는지 말하고 각 방법들에 대해 설명하세요.</summary>
  
- Sticky Session은 로드밸런서가 클라이언트의 세션 ID를 기준으로 항상 같은 서버로 요청을 전달하는 방식입니다. 설정은 간단하지만, 특정 서버에 부하가 집중될 수 있습니다.
- Session Clustering은 세션 정보를 모든 서버 간에 복제하여 공유하는 방식으로, 고가용성 환경에 적합하지만 네트워크 비용이 증가할 수 있습니다.
- Session Storage는 Redis나 DB 같은 별도의 저장소에 세션을 저장하고, 모든 서버가 이를 참조하는 방식입니다. 가장 보편적이며 서버 확장성이 뛰어납니다.
</details>

## 이소원
<details>
  <summary>쿠키와 세션의 차이에 대해 설명해주세요</summary>

쿠키

- 클라이언트 로컬(브라우저 & 하드디스크)에 저장되는 Key-value가 들어있는 파일
- 보안성이 낮음
- 빠르다
- 종료 시점 : 쿠키에 지정된 유효기간까지 유지

세션

- 서버에 저장되어 관리
- 보안성 높음
- 서버에서 조회를 해야하기 때문에 상대적으로 느리다.
- 종료 시점 : 브라우저 종료 시 또는 서버 설정 정보에 따라
</details>

<details>
    <summary>토큰 인증 과정을 설명하세요</summary>

1. 클라이언트가 서버에 로그인 요청을 보낸다.
2. 서버는 검증 후 클라이언트의 고유 id 등의 정보를 Payload에 담고, 암호화할 비밀키를 사용해 Access Token (JWT) 발급
3. 클라이언트는 전달받은 토큰을 저장해두고, 서버에 요청을 할 때마다 토큰을 요청 헤더 Authorization에 포함시켜 전달
4. 서버는 토큰의 전자서명을 비밀키로 복호화한 다음, 위변조 여부 및 유효 기간 등을 확인 후 유효한 토큰이라면 요청에 응답
</details>

<details>
    <summary>HTTP의 특성인 Stateless에 대해 설명해 주세요.</summary>
    HTTP 는 비상태성 프로토콜로 상태 정보를 유지하지 않는 것을 의미합니다.

연결을 유지하지 않기 때문에 리소스 낭비가 줄어드는 것은 큰 장점이지만
통신을 할 때마다 매번 연결을 설정해야 하며, 이전 요청과 현재 요청이 같은 사용자의 요청인지 알 수 없다는 단점이 있습니다.

이러한 문제를 쿠키와 세션을 통해 해결할 수 있습니다.
</details>

<details>
    <summary>JWT의 장점과 단점은 무엇인가요?</summary>
    
- 장점:
    - 서버가 상태를 저장하지 않기 때문에 수평적 확장에 유리
    - 사용자 정보를 포함할 수 있어 빠른 인증 가능

- 단점:
    - 토큰 탈취 시 정보 노출 가능성
    - 토큰 폐기 어렵다 (만료 전까지 유효)
    - 토큰이 커질 수 있어 네트워크 부담 증가
</details>

<details>
    <summary>규모가 커져 서버가 여러 개가 된다면, 세션을 어떻게 관리할 수 있을까요?</summary>
    
1. Sticky Seesion

    클라이언트의 요청이 항상 해당 클라이언트의 세션이 저장된 서버로만 전달

2. Session Clustering

   세션을 서버에 각각 복사해서 모든 서버가 모든 세션을 보유

   병렬 처리를 통해 여러 서버가 하나의 서버처럼 운영

3. Session Storage

   세션만 관리하는 별도의 db 서버를 두고, 모든 서버가 해당 서버를 참조하도록
</details>

## 박상윤
<details>
    <summary>쿠키의 동작 방식 순서를 말하세요.</summary>

1. 웹브라우저가 서버에 요청
2. 상태를 유지하고 싶은 값을 쿠키(cookie)로 생성
3. 서버가 응답할 때 HTTP 헤더(Set-Cookie)에 쿠키를 포함해서 전송
4. 전달받은 쿠키는 웹 브라우저가 관리, 다음 요청 때 쿠키를 HTTP 헤더에 자동으로 넣어서 전송
5. 서버에서 쿠키 정보를 읽어 이전 상태 정보를 확인 후 응답
</details>

<details>
    <summary>세션의 동작 방식 순서를 말하세요.</summary>

1. 웹브라우저가 서버에 요청
2. 서버가 해당 웹브라우저(클라이언트)에 유일한 ID(Session ID)를 부여함
3. 서버가 응답할 때 HTTP 헤더(Set-Cookie)에 Session ID를 포함해서 전송
4. 웹브라우저는 부여된 Session ID를 쿠키에 저장해두고, 다음 요청 때마다 해당 쿠키를 HTTP 헤더에 넣어서 전송
5. 서버는 Session ID를 확인하고, 해당 세션에 관련된 정보를 확인한 후 응답
    - 로그인을 하는 경우, 해당 Session ID의 로그인 상태를 유효한 값으로 바꿔 저장
    - 이후 요청에서 해당 Session ID를 가진 클라이언트는 로그인 상태가 유효하므로 별도의 로그인 없이 서비스 이용 가능
</details>

<details>
    <summary>다중 서버 환경에서 세션을 관리하는 방법 3가지를 말하세요.</summary>

1.Sticky Session (스티키 세션)

- 클라이언트의 요청이 항상 해당 클라이언트의 세션이 저장된 서버로만 전달됨
    - 로드밸런서에서 요청 쿠키(Session ID)를 읽고 지정된 서버(세션이 있는)로만 요청을 전달함
    - 세션 정보가 없을 경우, 로드밸런서의 기본 알고리즘대로 요청 전달

2.Session Clustering (세션 클러스터링)

- 클러스터링: 병렬 처리해서 여러 대의 서버를 하나의 서버처럼 운영
- 세션을 서버 각각에 복사해서 모든 서버가 모든 세션을 보유하고 있음
- 특정 서버에서 세션이 생성될 때 다른 서버로 세션을 전파하여 복제

3.Session Storage (세션 스토리지)

- 세션만 관리하는 별도의 DB 서버를 두고, 모든 서버가 해당 서버를 참조함
</details>

<details>
    <summary>토큰의 동작 방식을 말하세요.</summary>

1. 클라이언트가 서버에 접속 시, 서버는 클라이언트에게 인증되었다는 의미로 토큰 부여 (해당 토큰은 유일함)
    - 클라이언트는 전달받은 토큰을 쿠키나 스토리지에 저장함
2. 토큰을 발급받은 클라이언트는 다시 서버에 요청을 보낼 때 헤더에 토큰을 심어보냄
3. 서버의 토큰 일치여부 체크로 인증과정 처리
    - 클라이언트로부터 받은 토큰과 서버에서 제공한 토큰의 일치여부 체크
</details>

<details>
    <summary>JWT 토큰의 인증 과정을 말하세요.</summary>

1. 클라이언트가 서버로 로그인 **요청**을 보냄
2. 서버는 **검증** 후 클라이언트 고유 ID등의 정보를 Payload에 담고, 암호화할 비밀키를 사용해 **Access Token(JWT) 발급**
3. 클라이언트는 전달받은 **토큰을 저장**해두고, 서버에 요청할 때마다 토큰을 **요청 헤더 Authorization**에 포함시켜 함께 전달
4. 서버는 토큰의 Signature 을 비밀키로 **복호화**한 다음, 위변조 여부 및 유효 기간 등을 확인 후 **유효한 토큰이라면 요청에 응답**
</details>

## 신예지

<details>
    <summary>HTTP 프로토콜의 특징을 말해주세요 </summary>
    
- 클라이언트 서버 구조
- 비연결 지향(Connectionless)
- 무상태(Stateless)
</details>

<details>
    <summary>쿠키의 구성 요소를 말해주세요</summary>

- 쿠키의 이름(name)
- 쿠키의 값(value)
- 쿠키의 유효시간(Expires)
- 쿠키를 전송할 도메인 이름(Domain)
- 쿠키를 전송할 요청 경로(Path)
</details>

<details>
    <summary>세션의 동작 방식을 설명해주세요</summary>

1. 웹브라우저가 서버에 요청
2. 서버가 해당 웹브라우저(클라이언트)에 유일한 ID(Session ID)를 부여함
3. 서버가 응답할 때 HTTP 헤더(Set-Cookie)에 Session ID를 포함해서 전송
4. 웹브라우저는 부여된 Session ID를 쿠키에 저장해두고, 다음 요청 때마다 해당 쿠키를 HTTP 헤더에 넣어서 전송
5. 서버는 Session ID를 확인하고, 해당 세션에 관련된 정보를 확인한 후 응답
    - 로그인을 하는 경우, 해당 Session ID의 로그인 상태를 유효한 값으로 바꿔 저장
    - 이후 요청에서 해당 Session ID를 가진 클라이언트는 로그인 상태가 유효하므로 별도의 로그인 없이 서비스 이용 가능
</details>

<details>
    <summary>다중 서버 환경에서 세션을 관리하는 방법 중 세션 클러스터링은 어떤 방식인지 설명해주세요</summary>

- 세션을 서버 각각에 복사해서 모든 서버가 모든 세션을 보유하고 있음
- 특정 서버에서 세션이 생성될 때 다른 서버로 세션을 전파하여 복제
</details>

<details>
    <summary>토큰의 한계점을 설명해주세요</summary>

- 한 번 발행한 토큰은 유효기간 만료시 까지 통제 불가
- 여러 기기에서 로그인 제한 불가
- 세션에 비해 토큰 정보 탈취 당할 가능성 높음
    - 해결 방법으로 `만료 시간` 이용
- 토큰 자체 데이터 길이가 긺
    - 인증 요청이 많아질 수록 네트워크 부하가 심해짐
</details>

<details>
    <summary>JWT의 Signature에는 어떤 정보가 들어가있나요?</summary>

인코딩된 Header와 Payload를 더한 뒤 비밀키로 해싱하여 생성
</details>

## 김수훈

<details>
    <summary>토큰 기반 인증 방식이 가진 단점과 단점을 개선할 수 있는 방법을 이야기해주세요.</summary>

토큰 인증 방식은 쿠키처럼 탈취에 대한 위협을 대응할 수 없다는 단점을 가지고 있습니다. 클라이언트에서 저장되기 때문에, 토큰을 가지고 있으면 누구나 웹페이지에 접근할 수 있습니다.

이러한 단점을 개선하기 위해 리프래쉬 토큰을 이용합니다. 엑세스 토큰의 유효 시간을 짧게 설정하고, 유효 시간이 끝나기 전에 로그인 연장 등의 기능으로 리프래쉬 토큰을 확인해 엑세스 토큰을 새로 발급해줍니다. 리프래쉬 토큰은 데이터베이스에 저장되어 올바른 토큰인지를 확인할 수 있으며, 엑세스 토큰이 탈취되면 리프래쉬 토큰을 삭제하여 추가적인 로그인 연장을 막을 수 있습니다.
</details>

<details>
    <summary>http 프로토콜 특징 중 무상태(stateless)에 대해 설명해주세요 </summary>
무상태란, 서버가 클라이언트의 이전 요청이나 상태 정보를 저장하지 않는다는 것을 의미합니다.

즉, 요청과 응답이 완전히 독립적이며 서버는 요청이 끝나면 클라이언트를 기억하지 않는다는 특징이 있습니다.

그렇기 때문에 클라이언트가 요청할 때 필요한 데이터를 추가적으로 담아서 전송해야 합니다.
</details>

<details>
    <summary>세션 방식에서 세션id가 탈취당하면 어떤 문제가 발생할까요?</summary>
세션 ID 자체는 유의미한 개인정보를 담고 있지 않기 때문에 그 자체로 정보가 탈취될 위험은 없지만, 해커가 세션 ID 자체를 탈취하여 클라이언트인척 위장할 수 있다는 문제점이 존재합니다.
</details>

<details>
    <summary>Sticky Session (스티키 세션), Session Clustering (세션 클러스터링), Session Storage (세션 스토리지)에 대해서 간단히 설명해주세요.</summary>

- **Sticky Session**은 클라이언트의 요청을 항상 동일한 서버로 보내는 방식입니다. 세션 ID를 기반으로 로드밸런서가 요청을 특정 서버로 고정시켜 전달합니다. 구현이 간단하지만 서버 간 부하 분산이 어려울 수 있습니다.
- **Session Clustering**은 각 서버가 모든 세션 정보를 공유하도록 세션을 복제하는 방식입니다. 어느 서버에서든 요청 처리가 가능하지만, 복제 과정에서 네트워크 비용이 발생할 수 있습니다.
- **Session Storage**는 세션만을 저장하는 별도의 저장소(Redis나 DB 등)를 두고, 모든 서버가 해당 저장소를 참조하는 방식입니다. 확장성과 유지보수가 용이하지만, 저장소가 단일 장애 지점이 될 수 있습니다.
</details>

<details>
    <summary>세션의 동작 방식에 대해서 설명해주세요 </summary>

1. 웹브라우저가 서버에 요청
2. 서버가 해당 웹브라우저(클라이언트)에 유일한 ID(Session ID)를 부여함
3. 서버가 응답할 때 HTTP 헤더(Set-Cookie)에 Session ID를 포함해서 전송
4. 웹브라우저는 부여된 Session ID를 쿠키에 저장해두고, 다음 요청 때마다 해당 쿠키를 HTTP 헤더에 넣어서 전송
5. 서버는 Session ID를 확인하고, 해당 세션에 관련된 정보를 확인한 후 응답
    - 로그인을 하는 경우, 해당 Session ID의 로그인 상태를 유효한 값으로 바꿔 저장
    - 이후 요청에서 해당 Session ID를 가진 클라이언트는 로그인 상태가 유효하므로 별도의 로그인 없이 서비스 이용 가능
</details>






