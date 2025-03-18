## 변하영
<details>
  <summary>DispatcherServlet이란 무엇인가요?</summary>
  <div>
    DispatcherServlet은 모든 HTTP 요청을 가장 먼저 받아 적절한 컨트롤러에 위임하는 프론트 컨트롤러입니다.<br>
    이를 통해 공통 로직을 중앙에서 처리하고, 컨트롤러 간 코드 중복을 줄일 수 있습니다.
  </div>
</details>

<details>
  <summary>DispatcherServlet이 web.xml의 의존성을 낮추는 이유는 무엇인가요?</summary>
  <div>
    기존에는 모든 서블릿을 URL 매핑을 위해 web.xml에 모두 등록해주어야 했습니다.<br>
    DispatcherServlet은 들어오는 모든 요청을 처리하면서 개별 서블릿 등록을 생략할 수 있게 해줍니다.
  </div>
</details>

<details>
  <summary>DispatcherServlet의 주요 요청 처리 과정은 어떻게 이루어지나요?</summary>
  <div>
    1. DispatcherServlet으로 클라이언트의 웹 요청(HttpServletRequest)이 들어옴<br>
    2. 웹 요청을 HandlerMapping에 위임하여 해당 요청을 처리할 Handler(Controller)를 탐색<br>
    3. 찾은 Handler를 실행할 수 있는 HandlerAdapter를 탐색<br>
    4. 찾은 HandlerAdapter를 사용해 Handler의 메서드를 실행<br>
    5. 이때 Handler의 반환값은 Model과 View임<br>
    6. View 이름을 ViewResolver에게 전달하고, ViewResolver는 해당 View 객체를 반환<br>
    7. DispatcherServlet은 View에 Model을 전달하여 화면을 렌더링 (Model이 null이면 View를 그대로 사용)<br>
    8. 최종적으로 View 결과(HttpServletResponse)가 클라이언트에 반환됨
  </div>
</details>

<details>
  <summary>DispatcherServlet과 ViewResolver간의 관계는 무엇인가요?</summary>
  <div>
    DispatcherServlet은 컨트롤러가 반환한 View 이름을 ViewResolver에게 전달합니다.<br>
    ViewResolver는 해당 이름에 맞는 실제 View 객체를 찾아 반환하며, 최종적으로 DispatcherServlet이 View를 렌더링하여 응답합니다.
  </div>
</details>

<details>
  <summary>Spring MVC에서 HandlerMapping의 역할은 무엇인가요?</summary>
  <div>
    HandlerMapping은 들어온 요청 URL을 기반으로 어떤 컨트롤러(Handler)를 실행할지 결정하는 역할을 합니다.<br>
    예를 들어, @RequestMapping("/hello")가 선언된 컨트롤러를 찾는 역할을 합니다.
  </div>
</details>

---

## 신예지
<details>
  <summary>프론트 컨트롤러가 무엇인지 설명해주세요</summary>
  <div>
    프론트 컨트롤러는 웹 애플리케이션의 모든 요청을 단일 진입점에서 받아,
    적절한 컨트롤러나 뷰로 분기하는 패턴입니다.
  </div>
</details>

<details>
  <summary>DispatcherServlet은 수많은 @Controller 중에서 어떻게 구분할까요?</summary>
  <div>
    DispatcherServlet은 HandlerMapping을 사용하여 요청에 맞는 컨트롤러를 매핑합니다.
  </div>
</details>

<details>
  <summary>DispatcherServlet의 동작 과정에 대해 설명해주세요</summary>
  <div>
    1. 클라이언트의 웹 요청(HttpServletRequest)이 DispatcherServlet에 들어옴<br>
    2. HandlerMapping을 통해 해당 요청을 처리할 Handler(Controller)를 탐색<br>
    3. 찾은 Handler를 실행할 수 있는 HandlerAdapter를 탐색<br>
    4. HandlerAdapter를 사용해 Controller의 메서드를 실행<br>
    5. Controller의 반환값은 Model과 View임<br>
    6. View 이름을 ViewResolver에게 전달하여 실제 View 객체를 반환<br>
    7. DispatcherServlet이 View에 Model을 전달해 화면을 렌더링 (Model이 null이면 View 그대로 사용)<br>
    8. 최종적으로 View 결과(HttpServletResponse)가 클라이언트에 반환됨
  </div>
</details>

<details>
  <summary>DispatcherServlet과 HandlerAdapter의 역할 차이를 설명해주세요</summary>
  <div>
    DispatcherServlet: 클라이언트의 요청을 받아 적절한 컨트롤러로 전달하는 역할<br>
    HandlerAdapter: DispatcherServlet이 찾은 컨트롤러를 실행하는 역할
  </div>
</details>

<details>
  <summary>Spring Boot에서 DispatcherServlet을 설정하는 기본적인 방법은 무엇일까요?</summary>
  <div>
    Spring Boot에서는 @SpringBootApplication 어노테이션을 통해 자동으로 설정되므로,
    별도의 web.xml 설정이 필요하지 않습니다.
  </div>
</details>

---

## 박상윤
<details>
  <summary>Dispatcher Servlet의 역할은?</summary>
  <div>
    DispatcherServlet은 Spring MVC의 프론트 컨트롤러로서,
    클라이언트의 모든 HTTP 요청을 받아 적절한 컨트롤러(Handler)로 위임하고,
    핸들러 매핑, 핸들러 어댑터, 뷰 리졸버 등의 공통 작업을 수행하여 응답을 생성합니다.
  </div>
</details>

<details>
  <summary>Front-Controller Pattern이 도입된 이유가 무엇일까?</summary>
  <div>
    프론트 컨트롤러 패턴은 각 컨트롤러마다 중복되는 URL 매핑 및 공통 로직을 하나의 중앙 서블릿이 처리하여,
    코드 중복을 줄이고 유지보수성을 높이기 위해 도입되었습니다.
  </div>
</details>

<details>
  <summary>HandlerAdapter의 역할은 무엇이고, 왜 필요할까?</summary>
  <div>
    HandlerAdapter는 DispatcherServlet이 다양한 형태의 컨트롤러 인터페이스를 일관되게 호출할 수 있도록 도와줍니다.<br>
    즉, 특정 컨트롤러의 세부 구현에 구애받지 않고 통일된 방식으로 요청을 처리할 수 있도록 해줍니다.
  </div>
</details>

<details>
  <summary>@RestController와 @Controller의 요청 처리 과정에는 어떤 차이가 있을까요?</summary>
  <div>
    @Controller: 반환값이 ModelAndView로, ViewResolver를 통해 뷰를 렌더링하여 HTML 페이지를 반환합니다.<br>
    @RestController: 반환값을 바로 HTTP 응답의 body에 작성하기 때문에,
    ViewResolver 과정을 생략하고 HttpMessageConverter를 통해 JSON, XML 등의 데이터로 직렬화되어 응답됩니다.
  </div>
</details>

<details>
  <summary>DispatcherServlet의 상속 구조는 어떻게 구성되어 있는가?</summary>
  <div>
    DispatcherServlet은 FrameworkServlet을 상속하고,
    FrameworkServlet은 HttpServletBean을 상속하며,
    HttpServletBean은 HttpServlet을 상속합니다.<br>
    최종적으로 HttpServlet은 GenericServlet을 상속하여 Servlet 인터페이스를 구현하는 구조입니다.
  </div>
</details>

---

## 김수훈
<details>
  <summary>DispatcherServlet이 생기고 난 이후, 기존과 비교하여 어떤 점이 편리해졌나요?</summary>
  <div>
    과거에는 모든 서블릿에 대해 URL 매핑을 직접 해주어야 했지만,
    DispatcherServlet 등장 이후 모든 요청을 단일 진입점에서 처리하여
    개별 서블릿 등록이 필요 없어졌습니다.
  </div>
</details>

<details>
  <summary>DispatcherServlet에서 사용하는 스페셜 빈 중 handlerMapping과 handlerAdapter의 역할을 간단하게 설명해주세요.</summary>
  <div>
    handlerMapping: 클라이언트의 요청을 처리할 컨트롤러를 찾습니다.<br>
    handlerAdapter: handlerMapping에서 찾은 컨트롤러에 요청을 전달해 실행합니다.
  </div>
</details>

<details>
  <summary>프론트 컨트롤러가 무엇인지 설명하고, Spring MVC 구조의 어떤 부분에서 사용되나요?</summary>
  <div>
    프론트 컨트롤러는 모든 클라이언트 요청을 받아 한 곳에서 처리한 후,
    적절한 컨트롤러로 분기하는 역할을 합니다.<br>
    Spring MVC에서는 DispatcherServlet이 이 역할을 수행합니다.
  </div>
</details>

<details>
  <summary>DispatcherServlet의 동작과정에 대해 간략히 설명해주세요.</summary>
  <div>
    1. 클라이언트가 URL을 통해 요청을 전송한다.<br>
    2. DispatcherServlet은 HandlerMapping을 통해 요청에 해당하는 컨트롤러를 찾는다.<br>
    3. DispatcherServlet은 HandlerAdapter에게 요청 전달을 맡긴다.<br>
    4. HandlerAdapter는 해당 컨트롤러에 요청을 전달하여 실행한다.<br>
    5. 컨트롤러는 비즈니스 로직을 수행한 후 뷰 이름을 반환한다.<br>
    6. DispatcherServlet은 ViewResolver를 통해 반환할 뷰를 찾는다.<br>
    7. DispatcherServlet은 컨트롤러에서 전달받은 데이터를 뷰에 추가한다.<br>
    8. 최종적으로 데이터가 추가된 뷰를 클라이언트에 반환한다.
  </div>
</details>

<details>
  <summary>@Controller와 @RestController의 차이에 대해 설명하고, @RestController를 사용했을 때 위 과정에서 어떤 부분이 생략되는지 그 이유와 함께 설명해주세요.</summary>
  <div>
    @Controller: 뷰를 반환하여 ViewResolver를 통한 HTML 렌더링 과정을 거칩니다.<br>
    @RestController: @Controller와 @ResponseBody가 결합된 형태로,<br>
    컨트롤러의 반환값이 바로 HTTP 응답 본문의 데이터로 직렬화되어 전달되므로,<br>
    ViewResolver를 통한 뷰 찾기와 렌더링 과정이 생략됩니다.
  </div>
</details>

---

## 이소원
<details>
  <summary>Dispatcher Servlet 동작원리를 설명해주세요.</summary>
  <div>
    모든 요청을 먼저 받는 프론트 컨트롤러인 DispatcherServlet은
    클라이언트의 요청을 받아 HandlerMapping을 통해 적절한 컨트롤러에 전달하고,
    처리된 결과를 클라이언트에 반환하는 역할을 수행합니다.
  </div>
</details>

<details>
  <summary>DispatcherServlet의 동작 과정(요청 처리 과정)에 대해 설명해주세요.</summary>
  <div>
   1. 클라이언트가 요청을 보냄<br>
   2. DispatcherServlet이 요청을 가로챔<br>
   3. HandlerMapping을 사용해 적절한 컨트롤러를 찾음<br>
   4. DispatcherServlet이 어떤 HandlerAdapter가 컨트롤러를 실행할 수 있는지 찾음<br>
   5. HandlerAdapter가 컨트롤러를 실행<br>
   6. 컨트롤러가 비즈니스 로직을 수행하고 결과를 반환<br>
   7. ViewResolver를 통해 적절한 뷰를 찾아 렌더링 (HTML, JSON 등)<br>
   8. 최종적으로 클라이언트에게 응답이 반환됨<br>
   핵심 컴포넌트:<br>
       HandlerMapping → 컨트롤러 찾기<br>
       HandlerAdapter → 컨트롤러 실행<br>
       ViewResolver → 뷰 렌더링
  </div>
</details>

<details>
  <summary>DispatcherServlet에서 어댑터 패턴이 적용된 부분은 어디인가요?</summary>
  <div>
    어댑터 패턴은 주로 HandlerAdapter에 적용됩니다.<br>
    DispatcherServlet은 직접 컨트롤러를 실행하지 않고,
    적절한 HandlerAdapter를 찾아 컨트롤러를 실행하도록 위임합니다.
  </div>
</details>

<details>
  <summary>DispatcherServlet이 여러 개일 수도 있나요?</summary>
  <div>
    일반적으로 하나의 DispatcherServlet을 사용하지만,
    서로 다른 역할을 하는 여러 DispatcherServlet을 설정하여,
    다른 URL 패턴으로 트래픽을 분산할 수도 있습니다.
  </div>
</details>

<details>
  <summary>DispatcherServlet 없이 Spring MVC를 사용할 수 있나요?</summary>
  <div>
    기술적으로는 가능하지만,
    프론트 컨트롤러의 역할을 직접 구현해야 하므로 비효율적입니다.<br>
    DispatcherServlet은 Spring MVC의 핵심 구성 요소로 대부분의 경우 필요합니다.
  </div>
</details>
