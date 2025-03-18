## 변하영

<details> 
<summary><b>DNS에서 사용하는 주요 전송 프로토콜은 무엇인가요?</b></summary>
<div markdown="1">

  DNS는 기본적으로 UDP port 53을 사용하여 빠른 질의/응답을 처리합니다. 특수한 경우, 예를 들어 대용량의 데이터나 영역 전송(Zone Transfer) 시에는 TCP port 53을 사용합니다.
  
  - 영역전송이란?
    - DNS 서버는 영역 전송(Zone Transfer)을 통해 정보를 동기화합니다.
    - 마스터(Primary) 서버에서 변경된 DNS 데이터를 슬레이브(Secondary) 서버로 전송하여 두 서버의 데이터가 동일하게 유지되도록 합니다.

</div>
</details>

<details> 
<summary><b>DNS name space 의 계층 구조에 대해 설명해주세요</b></summary>
<div markdown="1">

  DNS name space은 계층적 구조로 이루어져 있습니다. 가장 상위에는 루트 도메인이 있고 그 아래로 최상위 도메인(TLD)가 있고, 그 아래로 2단계 도메인, 3단계 도메인이 있습니다.

</div>
</details>

<details> 
<summary><b>DNS 쿼리의 종류에는 무엇이 있나요?</b></summary>
<div markdown="1">

DNS 쿼리는 리졸버가 DNS 서버로부터 결과를 모두 받아 클라이언트에게 반환하는 방식인 재귀적 질의와 리졸버가 다른 DNS 서버에게 질의를 반복하여 처리하는 반복적 질의로 나뉩니다. 

</div>
</details>

<details> 
<summary><b>DNS 레코드 타입에 대해 설명해주세요</b></summary>
<div markdown="1">

- A : 도메인 이름을 IPv4주소로 매핑
- AAAA : 도메인 이름을 IPv6주소로 매핑
- CNAME : 도메인 이름에 대한 별칭을 설정하는 레코드, 도메인 주소를 다른 도메인 주소로 매핑
- NS : 특정 도메인의 네임서버를 정의

</div>
</details>

<details> 
<summary><b>Root DNS 서버의 역할이 무엇인가요?</b></summary>
<div markdown="1">

Root DNS 서버는 최상위 DNS 서버로, 클라이언트의 DNS 질의가 들어오면 적절한 TLD DNS 서버의 IP 주소를 반환하여, 해당 도메인의 정보를 처리할 수 있도록 합니다.

</div>
</details>

<details> 
<summary><b>DNS에서 도메인 이름을 IP로 변환하는 과정은 어떻게 이루어지나요?</b></summary>
<div markdown="1">

클라이언트는 도메인 이름을 DNS 서버에 질의하고, 리졸버는 해당 도메인 이름을 IP주소로 변환하기 위해 여러 단계의 DNS 서버(루트 DNS 서버 → TLD DNS 서버 → Authoritative DNS 서버)를 거쳐 결과를 반환합니다. 

</div>
</details>

<br>

## 박상윤

<details> 
<summary><b>DNS 서버에서 권한 있는 DNS 서버와 권한이 없는 DNS 서버를 각각 이야기 하세요 </b></summary>
<div markdown="1">

권한 있 : **Root DNS 서버, TLD DNS 서버, Authoritative DNS서버**

권한 없 : **Local DNS 서버, ISP DNS 서버, Resolver 서버**

</div>
</details>

<details> 
<summary><b>DNS의 계층 구조가 어떻게 되어 있을까요?</b></summary>
<div markdown="1">

루트 DNS 서버 - TLD(Top Level Domain) DNS 서버 - Authoritative DNS 서버 - 권한 없는 DNS 서버(Local DNS, ISP DNS, Resolver)

Local DNS, ISP DNS, Resolver는 역할이 겹치지만, 완전히 동일한 개념은 아니다.

</div>
</details>

<details> 
<summary><b>클라이언트에서 www.naver.com을 검색한 경우, DNS서버에서 발생하는 순서를 설명하세요.</b></summary>
<div markdown="1">

- **첫 번째 단계:**
    - 클라이언트(사용자 컴퓨터)는 먼저 로컬에 저장된 hosts 파일이나 DNS 캐시에서 naver.com의 IP 주소를 찾으려고 시도합니다.
    - 만약 찾지 못하면, **로컬 DNS 서버에 naver.com에 대한 질의**를 보냅니다.
- **두 번째 단계:**
    - **로컬 DNS 서버가 캐시**에도 없으면, **루트 DNS 서버에 질의**를 보내 naver.com의 최상위 도메인(**.com**)에 해당하는 **TLD DNS 서버들의 IP 주소**를 받아옵니다.
- **세 번째 단계:**
    - **로컬 DNS 서버는 받은 TLD DNS 서버 목록 중 하나를 선택해 다시 질의**를 보냅니다.
    - **TLD DNS 서버는 naver.com에 대한 정보를 알고 있는 Authoritative DNS 서버의 IP 주소**를 알려줍니다.
- **네 번째 단계:**
    - **로컬 DNS 서버가 Authoritative DNS 서버에 질의를 보내 최종적으로 www.naver.com의 정확한 IP 주소**를 받아옵니다.
    - 이 IP 주소는 로컬 DNS 서버에 캐시되고, 클라이언트에게 전달되어 브라우저가 해당 웹사이트에 연결할 수 있게 됩니다.

![Image](https://github.com/user-attachments/assets/9752f586-b8c2-4727-9b43-69bfdb7c5919)

![Image](https://github.com/user-attachments/assets/daa0d40a-ca0f-4084-8132-c49b3704c4aa)

</div>
</details>

<details> 
<summary><b>사용자가 도메인을 입력하고 IP 주소를 얻기 위해 DNS 서버에 보내는 요청을 뭐라 할까요?</b></summary>
<div markdown="1">

DNS Query

</div>
</details>

<details> 
<summary><b>DNS Query의 종류는 뭐가 있을까요?</b></summary>
<div markdown="1">

- **Recursive Query (재귀적 질의)**
    - **결과물(IP) 주소를 돌려주는 작업**
    - Recursive 서버는 Recursive 쿼리를 클라이언트에게 돌려주는 역할
        - Recursive 쿼리를 받은 Recursive 서버(Resolver)는 권한 있는 네임 서버로 Iterative 쿼리를 보내서 IP 주소를 찾고 결과를 반환함
- **Iterative Query (반복적 질의)**
    - Recursive DNS 서버가 다른 DNS 서버에게 쿼리를 보내어 응답을 요청하는 작업
    - Recursive 서버가 권한 있는 네임 서버들에게 반복적으로 쿼리를 보내서 IP 주소를 찾음
    - 만약 Recursive 서버에 이미 IP 주소가 캐시 되어있다면 해당 과정은 건너뜀

</div>
</details>

<br>

## 신예지

<details> 
<summary><b>DNS의 동작 과정을 설명해주세요</b></summary>
<div markdown="1">

1. 사용자가 **웹 브라우저에서 도메인 주소를 입력함**
2. 먼저 **내 컴퓨터(로컬)에서 DNS 정보를 찾아봄** (hosts 파일, 브라우저 캐시 확인)
3. 정보가 없으면 **내 인터넷 서비스 제공업체(ISP)의 DNS 서버**에 요청을 보냄
4. 그래도 정보가 없으면, DNS 서버는 **계층적으로 상위 DNS 서버에 물어봄**
5. 최종적으로 **권한 있는 DNS 서버(Authoritative DNS)** 가 도메인 주소의 정확한 IP 주소를 알려줌
6. 내 컴퓨터는 이 정보를 받아서 해당 IP 주소로 웹사이트에 접속함

</div>
</details>

<details> 
<summary><b>네임 서버와 리졸버의 차이점을 설명해주세요</b></summary>
<div markdown="1">

네임 서버는 권한이 있는 DNS 서버로 IP 주소와 도메인 이름을 매핑한다.

리졸버는 권한이 없는 DNS 서버로 질의를 통해 IP 주소를 알아내거나 캐시한다.

</div>
</details>

<details> 
<summary><b>DNS 레코드에서 A 레코드와 CNAME 레코드의 차이를 설명해주세요</b></summary>
<div markdown="1">

A 레코드는 도메인 주소와 IPv4 주소를 매핑하고, CNAME 레코드는 도메인 주소를 다른 도메인 주소로 매핑한다.

</div>
</details>

<details> 
<summary><b>재귀적 질의(Recursive Query)와 반복적 질의(Iterative Query)의 차이점을 설명해주세요</b></summary>
<div markdown="1">

**Recursive Query (재귀적 질의)**: 결과물(IP) 주소를 돌려주는 작업

**Iterative Query(반복적 질의)**: Recursive DNS 서버가 다른 DNS 서버에게 쿼리를 보내어 응답을 요청하는 작업

</div>
</details>

<details> 
<summary><b>도메인 네임 스페이스 각 단계에 어떤 것들이 있는지 설명해주세요</b></summary>
<div markdown="1">

1단계: TLD(Top Level Domain, 국가코드 최상위 도메인, 일반 최상위 도메인

2단계: SLD(Second Level Domain, 영리기업, 정부기관)

3단계: Authoritative DNS(도메인 이름)

</div>
</details>

<details> 
<summary><b>Local DNS server에서 DNS 질의를 하지 않고 바로 반환하는 경우는 어떨 때 인가요?</b></summary>
<div markdown="1">

이때 로컬 DNS 서버에 도메인에 대한 IP 주소가 캐시되어있다면 바로 클라이언트에세 요청한 도메인에 대한 IP 주소를 반환한다.

</div>
</details>

<br>

## 김수훈

<details> 
<summary><b>DNS의 전송 프로토콜 중 TCP 전송 시 사용되는 영역 전송이 무엇인가요?</b></summary>
<div markdown="1">

안정성을 위해 두 개 이상의 DNS 서버를 사용할 경우, Master(기본 서버)와 Slave(보조 서버)간의 동기화가 필요합니다.

이때 기본 서버의 정보를 이용해 보조 서버의 데이터를 최신 상태로 업데이트 하는 작업을 영역 전송이라고 합니다.

</div>
</details>

<details> 
<summary><b>DNS의 구성요소 중 도메인 네임 스페이스, 네임 서버, 리졸버의 역할에 대해 간단히 설명 해주세요.</b></summary>
<div markdown="1">

- 도메인 네임 스페이스는 분산시스템으로 도메인 이름을 분산하여 저장하는데 계층적 구조로 저장하고 관리합니다.
- 네임 서버(Name Server)는 해당 도메인의 IP 주소를 찾는 역할을 담당합니다.
- 리졸버(DNS Recursive Resolver)는 클라이언트의 요청을 네임 서버로 전달하고, 찾은 정보를 클라이언트에게 제공하는 기능을 담당합니다.

</div>
</details>

<details> 
<summary><b>DNS에서 TLD가 무엇인지 설명하고 TLD의 종류에는 무엇이 있나요?</b></summary>
<div markdown="1">

도메인 네임 스페이스에서 도메인의 역트리 구조 중 1단계 도메인인 최상위 도메인을 나타내는 Top Level Domain의 약자입니다.

TLD에는 국가 최상위 도메인(ccTLD)과 일반 최상위 도메인(gTLD)이 있습니다.

</div>
</details>

<details> 
<summary><b>실제로 우리가 원하는 도메인에 대한 IP 주소를 매핑하는 서버로, 개인 도메인과 IP 주소의 관계가 저장되며 일반적으로 도메인/호스팅 업체의 네임 서버를 말하는 이것은 어떤 종류의 네임서버일까요?</b></summary>
<div markdown="1">

Authoritative DNS 서버

</div>
</details>

<details> 
<summary><b>DNS 캐싱은 왜 사용하나요?</b></summary>
<div markdown="1">

DNS 캐싱은 요청하는 클라이언트와 가까운 곳에 데이터를 저장함으로써 DNS 쿼리를 조기에 확인할 수 있고 DNS 조회 체인의 추가 쿼리를 줄이기 위해 사용합니다.

</div>
</details>

<br>

## 이소원

<details> 
<summary><b>DNS 는 어느 계층에서 동작하는 프로토콜 인가요?</b></summary>
<div markdown="1">

OSI 7계층 중에서 애플리케이션 계층에서 동작하는 프로토콜

</div>
</details>

<details> 
<summary><b>DNS는 tcp / udp 어떤 전송 프로토콜을 더 많이 사용하나요?</b></summary>
<div markdown="1">

udp

- 빠른 속도 (연결의 시작과 끝이 없음)
    - DNS 질의는 신뢰성보다는 속도(빠른 응답)가 더 중요한 서비스
    - DNS가 전송하는 데이터 패킷 사이즈는 매우 작다.
    - UDP는 512 bytes를 넘어가지 않는 패킷만 전송이 가능하고, 오버헤드가 없어서 속도가 빠르다.

- 연결 상태 유지 불필요
    - DNS 서버는 도메인 네임을 IP로 변경해주는 서비스를 제공하기 때문에 항상 많은 클라이언트를 수용해야 한다.
    - UDP는 어떤 정보도 기록하지 않고, 유지할 필요가 없어서 TCP보다 UDP에서 동작할 때 더 많은 클라이언트를 수용할 수 있다.

</div>
</details>

<details> 
<summary><b>DNS iterative query와 DNS recursive query의 차이점에 대해서 설명해주세요.</b></summary>
<div markdown="1">

1. **반복(Iterative) 질의**
    - 리졸버가 **한 번 질의하면**, 네임 서버는 직접 IP를 주지 않고 "다음 서버로 가서 물어봐"라고 알려줌.
    - 그러면 리졸버는 다시 그 서버에 직접 질의하는 방식.
    - **즉, 리졸버가 최상위 루트부터 단계별로 직접 질의하는 것**
2. **재귀(Recursive) 질의**
    - 리졸버가 **한 번 질의하면**, **스스로 다른 DNS 서버를 거쳐 최종 IP를 찾아서 응답**함.
    - 즉, 사용자는 **한 번만 질문하면 리졸버가 알아서 끝까지 해결해줌.**
    - **즉, 리졸버가 모든 과정(루트 → TLD → 권한 네임 서버)을 대신 처리하는 것**
    - 그렇기 때문에 처리 시간이 길어지는 단점이 있다.

</div>
</details>

<details> 
<summary><b>도메인과 url의 차이점을 설명해주세요</b></summary>
<div markdown="1">

웹 주소인 url에 도메인 이름과 전송 프로토콜 및 경로 등의 정보가 포함되어 있습니다.

도메인 : ```google.com``` ( 도메인 이름 +  최상위 도메인(TLD))

url : ```https://www.google.com/search?1=dns``` (프로토콜 + 도메인 + 경로 + 파라미터 등)

</div>
</details>

<details> 
<summary><b>리졸버는 TLD 서버에 바로 직접 질의를 할 수 있습니다. (o, x)</b></summary>
<div markdown="1">

x

리졸버는 항상 루트 네임 서버부터 시작해서 단계별로 내려가는 방식을 따르기 때문에 루트 네임 서버부터 시작하여 질의를 할 수 있습니다.

</div>
</details>
