## 변하영
<details>
<summary>서블릿의 생명주기를 설명하고, init(), service(), destroy() 메서드가 각각 언제 호출되는지 설명해주세요.</summary>
<div>

서블릿은 처음 요청이 오면 init()이 한 번만 호출되며, 이후 클라이언트 요청마다 service()가 호출됩니다. service()는 HTTP 메소드에 따라 doGet(), doPost() 등을 실행합니다. 마지막으로 서블릿이 소멸될 때 destroy()가 한 번 호출되어 자원을 정리합니다.

</div>
</details>

<details>
<summary>서블릿 컨테이너(Servlet Container)의 역할은 무엇이며, 멀티스레드 지원 방식에 대해 설명해주세요.</summary>
<div>

서블릿 컨테이너는 서블릿의 생명주기를 관리하며, 요청을 적절한 서블릿으로 전달하고 응답을 반환하는 역할을 합니다. 멀티스레드 환경에서는 요청이 올 때마다 새로운 스레드를 생성하여 service() 메서드를 실행하므로, 동시에 여러 요청을 처리할 수 있습니다

</div>
</details>

<details>
<summary>WAS(Web Application Server)와 WEB Server의 차이점은 무엇인가요?</summary>
<div>

웹 서버는 정적인 리소스를 클라이언트에 제공하는 역할을 하며, 대표적으로 Nginx, Apache가 있습니다. 반면, WAS는 동적 웹 애플리케이션을 실행하는 환경을 제공하는 역할을 합니다. 대표적인 WAS로는 Tomcat이 있습니다.

</div>
</details>

<details>
<summary>Tomcat이 무엇인가요?</summary>
<div>

Tomcat은 Apache에서 개발한 오픈소스 웹 애플리케이션 서버로, 서블릿과 JSP 실행환경을 제공합니다. 클라이언트의 HTTP 요청을 받아 적절한 서블릿에 전달하고, 결과를 응답하는 역할을 합니다. 

</div>
</details>

<details>
<summary>서블릿의 동작 과정에 대해 설명해주세요.</summary>
<div>

먼저 클라이언트가 요청을 보내면 서블릿 컨테이너는 HttpServletRequest와 HttpServletResponse 객체를 생성합니다. 요청된 서블릿을 찾아 service() 메서드를 호출하고, HTTP 메소드에 따라 doGet(), doPost() 등을 실행합니다. 처리가 완료되면 결과를 HttpServletResponse에 담아 클라이언트에게 전송하며, 요청 객체는 소멸됩니다.
서블릿 객체는 싱글톤으로 유지되며, 더 이상 필요하지 않으면 destroy()가 호출됩니다.

</div>
</details>

---

## 박상윤
<details>
<summary>서블릿의 라이프 사이클은 어떻게 될까요?</summary>
<div>

1. 서블릿 인스턴스가 존재하지 않는 경우
    1. 웹 컨테이너가 서블릿 클래스를 로드합니다.
    2. 서블릿 클래스의 인스턴스를 생성합니다.
    3. init() 메서드를 호출해서 서블릿 인스턴스를 초기화 합니다.
2. 서블릿 인스턴스가 존재하는 경우
    1. 컨테이너가 서블릿 인스턴스에 요청과 응답 객체를 넘겨주면서, 서블릿의 service()메서드를 호출합니다.

</div>
</details>

<details>
<summary>컨테이너에서 서블릿 인스턴스를 정리하기 위해 사용하는 메서드가 무엇인가요?</summary>
<div>

destory()

</div>
</details>

<details>
<summary>서블릿에서 동시성 문제가 어떻게 발생할까요?</summary>
<div>

서블릿은 기본적으로 싱글턴 패턴으로 동작하기 때문에, 다수의 클라이언트 요청이 하나의 서블릿 인스턴스를 공유합니다. 따라서 인스턴스 변수(Instance Variable)를 사용하면 동시성 문제가 발생합니다.

</div>
</details>

<details>
<summary>서블릿에서 필터(Filter)의 역할은 무엇인가요?</summary>
<div>

필터(Filter)는 요청(Request)과 응답(Response)에 대한 전처리 및 후처리를 수행하는 서블릿 컴포넌트입니다.

</div>
</details>

---

## 신예지

<details>
<summary>servlet의 동작 과정에 대해 설명해주세요</summary>
<div>

1. 클라이언트 요청
2. HttpServletRequest, HttpServletResponse 객체 생성
3. 서블릿 컨테이너가 요청 URL과 매핑된 서블릿을 탐색
4. 해당하는 서블릿에서 service() 메소드 호출
5. doGet() 또는 doPost() 호출
6. 동적 페이지 생성 후 ServletResponse 객체에 응답 전송
7. HttpServletRequest, HttpServletResponse 객체 소멸

</div>
</details>

<details>
<summary>대표적인 servlet 컨테이너에는 무엇이 있나요?</summary>
<div>

Tomcat

</div>
</details>

<details>
<summary>service() 메서드는 언제 호출되나요?</summary>
<div>

매 요청마다 내부적으로 HTTP 요청 방식을 확인한 후 doGet() 또는 doPost() 같은 메서드를 호출함

</div>
</details>

<details>
<summary>서블릿이 싱글톤 패턴으로 동작하는 이유는 무엇이며, 이에 따른 문제점과 해결 방법에 대해 설명해주세요 </summary>
<div>

**이유**: 요청이 들어올 때마다 서블릿 객체를 생성하면 성능이 저하되기 때문에

**문제점**: 여러 요청이 동시에 하나의 서블릿 인스턴스를 공유하면서 **멤버 변수(인스턴스 변수)** 가 변경될 경우 **레이스 컨디션** 발생 가능

**해결 방법:**

- **지역 변수 사용 (가장 좋은 방법)**
    - 지역 변수는 **각 요청마다 새로 생성**되므로 동시성 문제가 없음.
- **동기화 (synchronized)**

</div>
</details>

<details>
<summary>서블릿 컨테이너의 역할을 설명해주세요</summary>
<div>

- 웹 서버와 통신지원
- 서블릿 생명주기 관리
- 멀티스레드 지원 및 관리
- 선언적인 보안 관리

</div>
</details>

---

## 이소원
<details>
<summary>왜 동적 웹페이지를 만들 때 서블릿이 필요한가요?</summary>
<div>

클라이언트(브라우저)의 요청을 처리하고 서버에서 동적으로 데이터를 생성하여 응답을 제공하기 위해서입니다.

</div>
</details>

<details>
<summary>서블릿이 뭔가요?</summary>
<div>

서블릿은 클라이언트의 HTTP 요청을 처리하고, 그 요청에 맞는 동적인 응답을 생성하는 서버 측 컴포넌트 입니다.

</div>
</details>

<details>
<summary>서블릿 컨테이너의 역할 4가지에 대해 설명해보세요.</summary>
<div>

1. 웹 서버와 통신 지원
    
    일반적으로 소켓을 만들고 listen, accept 등을 하고 웹 서버와 통신하지만
    
    서블릿 컨테이너는 이러한 기능을 API로 제공하여 생략할 수 있게 해줍니다.
    
    개발자가 서블릿에 구현해야할 비즈니스 로직에만 초점을 둘 수 있게 지원합니다.
    
2. 서블릿 생명 주기 관리
    
    서블릿 컨테이너는 서블릿 클래스를 로딩하여 인스턴스화하고 init( ) 메소드를 호출, 적절한 서블릿 메소드 등을 호출하게 도와줍니다.
    
    수명이 다 된 서블릿을 적절하게 가비지 collector를 호출하여 필요 없는 자원 낭비를 막아줍니다.
    
3. 멀티 스레드 지원 및 관리
    
    서블릿 컨테이너는 request가 올 때마다 새로운 자바 스레드를 하나씩 생성합니다. 이후 http 서비스 메소드를 실행하고 난 후 자동으로 소멸합니다.
    
    따라서 동시에 여러 요청이 들어와도 멀티 스레딩 환경에서 동시 다발적인 작업을 관리할 수 있습니다.
    
4. 선언적인 보안 관리
    
    서블릿 컨테이너는 보안 관련 기능을 제공해주므로 보안 관련 메소드를 구현하지 않아도 됩니다.
    
    일반적으로 보안 관리는 xml 배포 서술자에다 기록하므로 보안에 대해 수정할 일이 생겨도 자바 소스 코드를 수정하여 다시 컴파일 하지 않아도 보안 관리가 가능합니다.

</div>
</details>

<details>
<summary>서블릿의 생명주기는 무엇인가요? 서블릿의 생명주기에서 중요한 메서드는 무엇인가요?</summary>
<div>

서블릿의 생명주기는 서블릿 컨테이너가 서블릿을 로드, 서비스, 종료하는 과정을 말합니다.

- init( ) : 서블릿이 처음 요청을 받기 전에 호출. 서블릿 초기화 작업(초기 설정)을 수행하는 메소드 입니다.
- service( ) : 클라이언트 요청이 올 때마다 호출되며, 요청을 처리하고 응답을 반환하는 메소드 입니다. doGet( ), doPost( ) 등의 http 요청 처리 메소드를 호출합니다.
- destroy( ) : 서블릿이 종료되기 전에 호출되어 리소스를 해제하는 등의 작업을 수행합니다.

</div>
</details>

<details>
<summary>서블릿에서 HttpServletRequest와 HttpServletRespose 객체는 각각 어떤 역할을 하나요?</summary>
<div>

- HttpServletRequest : 클라이언트가 보내는 요청에 대한 정보를 담고 있는 객체이며, 
요청된 URL, 쿼리 파라미터, HTTP 헤더, 쿠키 등을 이 객체에서 확인할 수 있습니다. 
클라이언트의 요청을 서블릿이 처리하기 위해 필요한 정보를 제공합니다.
- HttpServletRespose : 서블릿이 클라이언트에 보낼 응답에 대한 정보를 담고 있는 객체이며, 
서블릿은 이 객체를 통해 응답 데이터를 작성하고 클라이언트에게 응답을 전달할 수 있습니다. 
응답 상태 코드, 응답 헤더, 응답 본문 등을 설정할 수 있습니다.

</div>
</details>

<details>
<summary>서블릿이 어떻게 다수의 클라이언트 요청을 동시에 처리하나요?</summary>
<div>

서블릿은 다수의 클라이언트 요청을 동시에 처리하기 위해 멀티 스레딩을 활용합니다.

톰캣과 같은 서블릿 컨테이너는 각 클라이언트 요청에 대해 별도의 스레드를 생성하여 요청을 처리하고, 서블릿 컨테이너가 이를 관리합니다.

1. **요청이 들어오면**: 서블릿 컨테이너는 요청을 처리하기 위해 새로운 스레드를 생성하거나, 스레드 풀에서 기존의 유휴 스레드를 할당합니다.
2. **서비스 메서드 호출**: 각 스레드는 `service()` 메서드를 호출하여 요청을 처리합니다. `service()` 메서드는 HTTP 요청에 따라 `doGet()`, `doPost()`와 같은 메서드를 호출하여 클라이언트 요청을 처리합니다.
3. **스레드 풀 활용**: 서블릿 컨테이너는 보통 스레드 풀(Thread Pool)을 사용하여 요청을 처리합니다. 
    
    일정 수의 스레드를 미리 생성해두고, 클라이언트 요청이 들어오면 이들 중 하나를 할당하여 요청을 처리합니다. 요청이 많으면 스레드가 부족할 수 있으므로, 컨테이너는 일정 수의 스레드만 동시에 실행되도록 제한할 수 있습니다.
    
4. **동시성 처리**: 각 스레드는 독립적으로 동작하므로, 여러 요청을 동시에 처리할 수 있습니다. 스레드는 서로 간섭하지 않도록 격리되어 요청을 처리합니다.

</div>
</details>

--- 

## 김수훈
<details>
<summary>서블릿의 특징에 대해서 아는대로 설명해보세요.</summary>
<div>

- 클라이언트의 Request에 대해 동적으로 작동하는 웹 애플리케이션 컴포넌트이다
- 주로 HTML을 사용하여 Response 한다 (XML, JSON, 일반 텍스트 모두 가능)
- HTML 변경 시 Servlet을 재 컴파일해야 하는 단점이 있다
- JAVA의 스레드를 활용하여 동작한다
- HTTP 프로토콜 서비스를 지원하는 javax.servlet.http.HttpServlet 클래스를 상속받는다
- Spring MVC에서 컨트롤러로 사용될 수 있다(DispatcherServlet)
- 보안기능을 적용하기 쉽다

</div>
</details>

<details>
<summary>서블릿의 생명주기(Servlet Life Cycle) 단계 3가지를 순서대로 설명하세요.</summary>
<div>

**init()** : 서블릿이 최초 실행될 때 한 번 호출되어 초기화 작업을 수행한다.

**service()** : 클라이언트의 요청이 들어오면 호출되며, doGet(), doPost()등의 메서드를 통해 요청을 처리한다.

**destroy()** : 서블릿이 종료될 때 한 번 호출되며, 자원 해제 등의 작업을 수행한다.

</div>
</details>

<details>
<summary>서블릿 컨테이너(Servlet Container)의 역할은 무엇인가요?</summary>
<div>

서블릿 컨테이너는 서블릿을 실행하고 관리하는 환경으로, 요청을 서블릿으로 전달, 세션 관리, 멀티스레딩 처리, 보안 관리 등의 기능을 제공한다.

</div>
</details>

<details>
<summary>서블릿과 JSP의 차이점은 무엇인가요?</summary>
<div>

서블릿은 자바 코드 중심으로 웹 요청을 처리하고, JSP는 HTML 중심으로 웹 페이지를 생성하는 데 초점을 맞춘다.
JSP는 내부적으로 서블릿으로 변환되므로, 서블릿이 보다 세밀한 제어가 가능하다.

</div>
</details>

<details>
<summary>서블릿이 싱글톤처럼 동작하는 이유는 무엇인가요?</summary>
<div>

서블릿 컨테이너는 하나의 서블릿 인스턴스를 생성한 후, 모든 요청을 해당 인스턴스의 service()메서드를 통해 처리하기 때문입니다.

</div>
</details>