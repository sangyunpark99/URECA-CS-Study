## 신예지
<details>
<summary><strong>웹서버는 정적 컨텐츠와 동적 컨텐츠를 각각 어떻게 지원하나요?</strong></summary>

정적 컨텐츠: WAS를 거치지 않고 바로 자원 제공

동적 컨텐츠: 동적컨텐츠 요청을 WAS로 넘겨주고, WAS에서 처리한 결과를 클라이언트에게 전달
</details>

<details>
<summary><strong>forward proxy와 reverse proxy의 차이점을 설명해주세요</strong></summary>

forward proxy: 서버에 방문하는 클라이언트의 주소를 감춤

reverse proxy: 클라이언트에게 서버의 주소를 감춤
</details>

<details>
<summary><strong>웹서버의 기능 4가지를 말해주세요</strong></summary>

- Reverse Proxy
    - 서버와 클라이언트 사이 프록시를 두고 프록시를 통해 데이터를 주고받음
    - 보안의 이유로 서버 내부 구조를 감추기 위해 사용
- 로드 밸런싱
    - 클라이언트의 요청에 따른 처리를 동작 중인 여러 WAS에게 적절히 분배
- 캐싱
    - Reverse Proxy의 캐시를 의미
    - 서버로 찾아오는 클라이언트들이 자주, 반복적으로 요청하는 리소스들을 프록시 서버에 저장하고 제공
- 주기적인 체크
    - 웹 서버에 존재하는 수 많은 모듈을 사용해 WAS 서비스가 정상적으로 동작하고 있는지 체크
</details>

<details>
<summary><strong>Apache Tomcat이 동작하는 과정을 설명해주세요</strong></summary>

1. `HTTP request`: HTTP요청을 Coyote에서 받아 Catalina로 전달  
2. `Catalina` : Catalina에서 전달받은 HTTP요청을 처리할 웹 어플리케이션(Context)를 찾음  
3. `Context` : WEB-INF/web.xml 파일 내용을 참조해 전달받은 요청을 서블릿에게 전달  
4. `Servlet` : JSP 파일이 요청되면 Tomcat의 Jasper(JSP 엔진)가 Validation check를 하고, 이를 서블릿으로 변환하여 컴파일한 뒤 실행합니다.
</details>

<details>
<summary><strong>Tomcat의 Catalina는 어떤 역할을 하나요?</strong></summary>

톰캣의 Servlet Container 역할로 JSP, Java Servlet을 호스팅하는 환경을 제공하고, 서블릿의 라이프사이클을 관리합니다.
</details>

---

## 이소원
<details>
<summary><strong>Apach Tomcat이 뭔가요?</strong></summary>

Apache Tomcat은 Java Servlet과 JSP(JavaServer Pages)를 실행할 수 있는 경량 웹 애플리케이션 서버(WAS)입니다.

동적인 웹 애플리케이션을 처리하며, 기본적인 웹서버 기능도 포함하고 있지만 주로 Nginx나 Apache HTTP Server와 함께 사용됩니다. 

오픈소스이며 가볍고 빠른 성능 덕분에 Spring Boot 등 Java 기반 웹 애플리케이션에서 널리 활용됩니다.
</details>

<details>
<summary><strong>Apach Tomcat의 동작 과정을 설명해주세요.</strong></summary>

1. `HTTP request`: HTTP요청을 Coyote에서 받아 Catalina로 전달  
2. `Catalina` : Catalina에서 전달받은 HTTP요청을 처리할 웹 어플리케이션(Context)를 찾음  
3. `Context` : WEB-INF/web.xml 파일 내용을 참조해 전달받은 요청을 매핑된 서블릿에게 전달  
4. `Servlet` : 요청된 Servlet Handler을 통해 생성된 jsp 파일들이 호출될 때, Jasper (JSP Engine)가 Validation Check / Compile 등을 수행
</details>

<details>
<summary><strong>Apach Tomcat의 역할이 뭔가요?</strong></summary>

Tomcat은 Java 웹 애플리케이션을 실행하고, 클라이언트 요청을 처리하여 동적인 응답을 반환하는 역할을 합니다
</details>

<details>
<summary><strong>Apache Tomcat과 Nginx/Apache HTTP Server는 어떻게 다르고, 함께 사용하는 이유는?</strong></summary>

- Apache Tomcat은 WAS이고 Nginx/Apache HTTP Server는 웹서버 입니다.  
- 함께 사용하므로써 서버 부하를 줄여 성능을 향상시키고, 웹서버는 리버스 프록시 기능이 있어 서버의 내부 ip를 숨김으로써 보안을 강화할 수 있습니다.  
- Nginx/Apache는 로드 밸런서 역할 수행 가능하기 때문에 여러 개의 Tomcat 서버에 부하 분산 가능하여 확장성이 증가합니다.  
- Tomcat은 Java 기반 웹 애플리케이션만 실행 가능하고,  
Nginx/Apache는 PHP, Python, Node.js 같은 다른 언어도 지원하기 때문에 다양한 웹서비스 지원이 가능해집니다.
</details>

<details>
<summary><strong>로드 밸런싱이 무엇이며, Tomcat 환경에서 어떻게 적용할 수 있나요?</strong></summary>

로드 밸런싱은 여러 서버에 트래픽을 나누어 서버 과부하를 막고 성능을 높이는 기술입니다. 

Tomcat 환경에서는 주로 Nginx나 Apache HTTP Server를 사용해 여러 대의 Tomcat 서버로 요청을 분산합니다.

요청을 순차적으로 보내는 방식(라운드로빈), 접속 수가 적은 서버를 우선 선택하는 방식 등 다양한 방법이 있습니다. 

이를 적용하면 서버가 안정적으로 운영되고, 필요할 때 쉽게 서버를 추가할 수 있습니다.
</details>

---

## 김수훈
<details>
<summary><strong>프록시가 무엇인지 간단하게 설명해주세요</strong></summary>

프록시는 클라이언트와 서버 사이에서 중개자 역할을 하는 서버 또는 소프트웨어입니다. 사용자가 웹사이트에 접속할 때, 직접 서버에 연결하지 않고 프록시 서버를 거쳐 연결됩니다.
</details>

<details>
<summary><strong>web server와 web application server를 분리한 이유가 무엇인가요?</strong></summary>

- 기능 분리로 서버 부하 방지  
- 물리적 분리로 보안강화  
- 여러대의 WAS 연결이 가능하므로 로드밸런싱, fail over, fail back 처리에 유리  
- 여러 웹 어플리케이션 서비스 가능
</details>

<details>
<summary><strong>was의 기능에는 무엇이 있나요?</strong></summary>

- 프로그램 실행 환경과 데이터베이스 접속 기능 제공  
- 여러개의 트랜잭션 관리  
- 업무를 처리하는 비즈니스 로직 수행  
- Web Service 플랫폼으로서의 역할
</details>

<details>
<summary><strong>tomcat의 구성요소 중 Coyote , Catalina , Jasper 에 대해서 간단히 설명해주세요</strong></summary>

- <strong>Coyote(HTTP Connector)</strong>: 클라이언트와 서버 간의 통신을 처리하며, HTTP 프로토콜을 지원합니다.  
- <strong>Catalina(Servlet Container)</strong>: 톰캣의 핵심 컴포넌트로, 서블릿의 라이프사이클을 관리하고 JSP, 서블릿을 호스팅하는 환경을 제공합니다.  
- <strong>Jasper(JSP Engine)</strong>: JSP 페이지를 서블릿 코드로 변환하고 컴파일한 후 실행하는 역할을 담당합니다.
</details>

<details>
<summary><strong>WAS가 단독으로도 웹 서비스가 가능한데, 왜 웹 서버와 함께 사용하나요?</strong></summary>

- 역할 분담으로 성능 최적화  
- 로드 밸런싱으로 부하 분산  
- 보안 강화 및 직접 접근 차단
- 장애 대응 및 무중단 서비스  
- 캐싱 기능으로 응답 속도 향상  
- 모니터링 및 관리 용이
</details>

---

## 변하영
<details>
<summary><strong>Tomcat의 주요 구성 요소에 대해 설명해 주세요.</strong></summary>

Tomcat은 세 가지 핵심 컴포넌트로 구성됩니다.  
Coyote는 HTTP 요청을 받고, Catalina는 서블릿 컨테이너로서 서블릿을 실행하고 비즈니스 로직을 처리하며, Jasper는 JSP를 서블릿으로 변환해 실행합니다.
</details>

<details>
<summary><strong>Web Server와 WAS의 차이점은 무엇이며, 왜 분리해서 사용하는 경우가 많을까요?</strong></summary>

Web Server는 정적 리소스를 처리하고, WAS는 동적 로직을 처리하는 서버입니다.  

분리해서 사용하면 서버 부하를 효율적으로 분산할 수 있고, 보안 측면에서도 유리합니다. 또한 여러 대의 WAS 연결이 가능하여 로드밸런싱, fail over, fail back 처리에 유리합니다.
</details>

<details>
<summary><strong>내장 톰캣과 외장 톰캣의 차이점을 설명해 주세요.</strong></summary>

외장 톰캣은 별도로 설치된 톰캣 서버에 WAR 파일을 배포해 사용하는 방식이고, 내장 톰캣은 Spring Boot에 포함된 톰캣으로 JAR 파일을 실행하는 구조입니다. 내장 톰캣은 설정이 간단하고 배포가 편리하지만, 여러 호스트 설정 등은 복잡할 수 있습니다.
</details>

<details>
<summary><strong>Tomcat은 Web server인지 WAS인지 말하고, 이유를 Tomcat의 기능과 연결지어 설명해 주세요.</strong></summary>

WAS입니다.  

Tomcat은 JSP와 Servlet을 실행할 수 있는 서블릿 컨테이너 기능을 갖추고 있어 WAS 역할을 수행합니다. HTTP 요청을 받아 비즈니스 로직을 처리하고, 동적인 응답을 생성하기 때문에 Web Application Server로 분류됩니다.
</details>

<details>
<summary><strong>Reverse Proxy가 필요한 이유는 무엇인가요?</strong></summary>

Reverse Proxy는 클라이언트와 서버 사이에서 서버의 주소를 감추고, 로드밸런싱이나 캐싱 같은 기능도 수행할 수 있습니다. 특히 Web Server가 WAS 앞단에서 프록시 역할을 하며 서버 내부 구조를 보호하고 트래픽을 분산하는 데 유용합니다.
</details>

---

## 박상윤
<details>
<summary><strong>Web Server란 무엇인가요?</strong></summary>

Web Server는 HTTP 프로토콜을 이용해 클라이언트의 요청에 따라 정적 웹 페이지(HTML, CSS, 이미지 등)를 제공하는 서버입니다.

역할

- 클라이언트로부터 HTTP 요청을 받아 정적 컨텐츠를 반환
- WAS(웹 어플리케이션 서버)로 동적 컨텐츠 요청 전달
- Reverse Proxy, 로드 밸런싱, 캐싱, 주기적 상태 체크 등을 통해 보안 강화와 서버 부하 분산을 지원
</details>

<details>
<summary><strong>WAS란 무엇이며, 주로 어떤 역할을 수행하나요?</strong></summary>

WAS는 동적 컨텐츠 제공을 위해 만들어진 미들웨어로, DB 조회나 복잡한 비즈니스 로직을 처리하는 애플리케이션 서버입니다.

- JSP, Servlet 등 동적 웹 컨텐츠 실행 및 관리
- 트랜잭션 관리 및 프로그램 실행 환경 제공
- 데이터베이스 접속 기능을 통해 필요한 데이터를 조회하여 클라이언트에 전달
</details>

<details>
<summary><strong>Apache Tomcat의 주요 구성 요소인 Coyote, Catalina, Jasper의 역할을 각각 설명하라.</strong></summary>

<strong>Coyote (HTTP Connector):</strong>

- 클라이언트와의 HTTP 통신을 담당
- 요청을 받아서 Tomcat 내부로 전달하며, 정적 컨텐츠의 서비스도 지원

<strong>Catalina (Servlet Container):</strong>

- Catalina에서 전달받은 HTTP요청을 처리할 웹 어플리케이션(Context)를 찾음

<strong>Jasper (JSP Engine):</strong>

- <strong>JSP 페이지를 서블릿 코드로 변환 및 컴파일하여 실행하는 역할</strong>을 수행
- 클<strong>라이언트의 JSP 요청이 들어오면 해당 JSP를 서블릿으로 변환해 실행 결과를 생성</strong>
</details>

<details>
<summary><strong>Embedded Tomcat과 외장(Standalone) Tomcat의 차이점과 각 방식의 특징을 설명하라.</strong></summary>

<strong>외장 Tomcat:</strong>

- 별도로 설치된 Tomcat 서버에 <strong>WAR 파일을 배포하여 애플리케이션을 실행</strong>
- 톰캣 설정 파일을 구성하고, Virtual Host 설정 등을 통해 여러 애플리케이션을 동시에 서비스할 수 있음
- Tomcat 서버를 별도로 설치한 후, Spring 프로젝트를 WAR 파일로 패키징하여 그 Tomcat 서버에 배포(Deploy)해서 애플리케이션을 실행한다는 것입니다.

<strong>Embedded Tomcat:</strong>

- Spring Boot 등에서 내장되어 있는 형태로, <strong>별도 설치 없이 애플리케이션 실행 시 함께 동작</strong>
- 단일 애플리케이션으로 실행되며, 설정이 간편해 개발자가 코드에 집중할 수 있으나, 여러 호스트 분기를 처리하는 데는 한계가 있음
</details>

<details>
<summary><strong>Tomcat이 클라이언트로부터 받은 HTTP 요청을 처리하는 전체 과정을 단계별로 설명하라.</strong></summary>

1. <strong>HTTP Request 수신</strong>
    - 클라이언트가 HTTP 요청을 보내면, Tomcat의 <strong>Coyote</strong>가 이를 받아들임
2. <strong>요청 전달</strong>
    - Coyote는 수신한 요청을 내부의 Catalina (Servlet Container)로 전달
3. <strong>웹 어플리케이션 선택</strong>
    - Catalina는 요청 URL과 설정 파일(web.xml 등)을 참조해 해당 요청을 처리할 웹 어플리케이션(Context)을 찾음
4. <strong>서블릿 또는 JSP 실행</strong>
    - 요청에 해당하는 서블릿에게 전달하고, 만약 JSP 페이지 요청이면 <strong>Jasper</strong>가 JSP를 서블릿으로 변환, 컴파일하여 실행
5. <strong>응답 반환</strong>
    - 처리 결과를 생성한 후, Catalina를 통해 Coyote가 최종 HTTP 응답으로 변환하여 클라이언트에 전송
</details>