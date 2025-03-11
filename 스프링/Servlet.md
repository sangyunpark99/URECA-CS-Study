## 서블릿이란?

: 클라이언트의 요청을 처리하고 그 결과를 반환하는 Servlet클래스의 구현 규칙을 지킨 자바 웹 프로그래밍 기술

서블릿이 요구하는 구현 규칙을 지켜주며 서블릿을 정의해주면 HTTP 요청 정보를 쉽게 사용할 수 있고, 처리 결과를 쉽게 응답으로 변환할 수 있음.

![](https://velog.velcdn.com/images%2Ffalling_star3%2Fpost%2Fea1d422a-c7d1-476f-b6b6-cf308320f4ce%2F%EC%BA%A1%EC%B2%98.png)


### 1) 서블릿의 특징

- 클라이언트의 요청에 대해 동적으로 작동하는 웹 애플리케이션 컴포넌트
- 주로 HTML 사용하여 응답함 (XML, JSON, 일반 텍스트 모두 가능)
- JAVA의 스레드를 활용하여 동작
- HTTP 프로토콜 서비스를 지원하는 javax.servlet.http.HttpServlet 클래스를 상속받음
- Spring MVC에서 컨트롤러로 사용될 수 있음 (DispatcherServlet)
- 보안 기능 적용하기 쉬움

<br>

### 2) 서블릿의 동작 과정

![](https://velog.velcdn.com/images%2Ffalling_star3%2Fpost%2F4fabf50a-d3d7-4391-8eb5-0cb436379d71%2Fimage.png)

1. 클라이언트 요청
2. HttpServletRequest, HttpServletResponse 객체 생성
3. Web.xml이 어느 서블릿에 대해 요청한 것인지 탐색
4. 해당하는 서블릿에서 service() 메소드 호출
5. doGet() 또는 doPost() 호출
6. 동적 페이지 생성 후 ServletResponse 객체에 응답 전송
7. HttpServletRequest, HttpServletResponse 객체 소멸

<br>

**정적 웹 페이지와 서블릿 요청의 비교**

정적 웹 페이지 :
- 브라우저가 요청하면 WEB에서는 저장된 페이지를 제공함

동적 웹 페이지 : 
- 과거 정적 웹페이지에서 업그레이드되면서 연산기능을 가지게됨
- 과거에 서버라 불리던 것은 **WEB**과 **WAS(Web Application Server)**로 나뉘게됨
- WEB 서버에서는 사용자 요청에 따라 정적 페이지를 제공하고, WAS는 사용자 요청 중에 '연산'이 필요한 부분만 맟아 결과를 제공함
- WAS는 연산 결과를 WEB서버에 제공, WEB서버는 정적 페이지를 만들어 사용자에게 전달함 
<br>이때 WAS에 연산을 담당하는 것이 **'Servlet'**
<br>(서블릿은 WAS안에 있는 서블릿 컨테이너 혹은 웹 컨테이너 공간에서 활동함)

<br>

### 3) 서블릿의 생명주기

: 서블릿 로딩부터 소멸될 때까지의 수명

![](https://velog.velcdn.com/images/hayong39/post/28ede403-a49a-4534-81dc-8edd8c333571/image.png)


1. 서블릿 로딩
2. 서브릿 인스턴스 생성
3. init() 메소드 호출
4. 각 클라이언트 요청에 대해 반복적으로 service() 메소드 호출
5. 소멸하기 위해 destroy() 메소드 호출

<br>

### 4) 주요 메소드

1. `init()`
- 서블릿의 일생동안 오직 한 번 호출됨
- 디폴트 생성자를 이용하여 서블릿 객체를 생성하고 init() 메소드를 사용하여 서블릿 객체를 초기화할 때 사용함

```java
public void init(ServletConfig config) throws ServletException
```

2. `service()`
- 요청이 있을 때마다 호출됨
- Http 메소드를 보고 doGet() 혹은 doPost() 호출할지 결정한다. 
- 서비스 메서드만 재정의해서 처리 방법 지정하면 됨.

```java
public void service(ServletRequest request, ServletResponse response) throws ServletException
```


3. `destroy()`
- 서블릿의 일생동안 단 한 번 호출됨
- 서블릿이 소멸할 때 호출하며, 자원 해제와 관련된 작업을 함

```java
public void destroy()
```

<br>

### 5) 서블릿 컨테이너

: 구현되어 있는 서블릿 클래스의 규칙에 맞게 서블릿을 담고 관리해주는 컨테이너
즉, 서블릿 생명 주기를 관리하는 객체

- 클라이언트의 요청을 받고 응답할 수 있도록 웹 서버와 소켓으로 통신하며 대표적으로 톰캣(Tomcat)이 있음
- 클라이언트에서 요청을 하면 컨테이너는 HttpServletRequest와 HttpServletResponse 두 객체를 생성하여 get/post 여부에 따라 동적인 페이지를 생성하여 응답을 보냄
- 톰캣은 웹 서버와 통신하며 JSP(Java Server Page)와 Servlet이 작동하는 환경을 제공해준다. 

![](https://velog.velcdn.com/images/hayong39/post/0db3775b-6b72-458a-a43f-bec76c2bc86a/image.png)

1. Servlet Request/Servlet Response 객체 생성
2. 설정 파일을 참고하여 매핑할 Servlet 확인
3. 해당 서블릿 인스턴스 존재 유무를 확인하여 없으면 생성 (init()을 통해)
4. Servlet Container에 스레드를 생성하고 res, req를 인자로 service 실행
5. 응답을 처리

<br>

> ❓ **서블릿은 생성만 하고 소멸시키는 동작 하지 않는 이유**
<br> 서블릿이 싱글톤으로 관리되기 때문이다. 서블릿 객체는 소멸되지 않고 있다가 다음번 같은 요청이 왔을 때 서블릿 컨테이너에 의해서 또 호출되서 사용된다.

<br>

**역할**

**1. 웹 서버와 통신 지원**
- 일반적으로 소켓 만들고 listen/accept 등을 하고 웹 서버와 통신하지만, 서블릿 컨테이너는 이러한 기능을 API로 제공하여 생략할 수 있게 해줌. 
- 개발자가 서블릿에 구현해야할 비즈니스 로직에만 초점을 둘 수 있도록 지원

**2. 서블릿 생명주기 관리** 
- 서블릿 컨테이너는 서블릿 클래스 로딩하여 인스턴스화하고 init() 메소드를 호출, 적절한 서블릿 메소드를 호출하게 도와줌. 
- 수명이 다 된 서블릿을 적절하게 가비지 콜렉터를 호출하여 필요없는 자원 낭비를 막아줌

**3. 멀티스레드 지원 및 관리** 
- 서블릿 컨테이너는 Request가 올 때마다 새로운 자바 스레드를 하나씩 생성함. 이후 HTTP 서비스 메소드를 실행하고 난 후 자동으로 소멸함. 따라서 동시에 여러 요청이 들어와도 멀티스레딩 환경에서 동시다발적인 작업을 관리할 수 있음. 
- 하지만 조심해서 사용해야함. 스레드를 생성한다는 것 자체가 비용이 많이 들고 다른 스레드로 전환하는 Context Switch가 많은 오버헤드를 일으키기 때문.

**4. 선언적인 보안 관리** 
- 서블릿 컨테이너는 보안 관련 기능을 제공해주므로 보안관련 메소드를 구현하지 않아도됨. 
- 일반적으로 보안관리는 XML 배포 서술자에다가 기록하므로, 보안에 대해 수정할 일이 생겨도 자바 소스 코드를 수정하여 다시 컴파일하지 않아도 보안 관리가 가능하다. 
        

<br>



**Reference**
[[Servlet] 서블릿(Servlet)이란?](https://velog.io/@falling_star3/Tomcat-%EC%84%9C%EB%B8%94%EB%A6%BFServlet%EC%9D%B4%EB%9E%80)