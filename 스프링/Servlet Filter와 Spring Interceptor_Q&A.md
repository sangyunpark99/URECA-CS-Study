## 박상윤
<details> <summary><strong>서블릿 필터(Filter)와 스프링 인터셉터(Interceptor)의 가장 큰 차이점은 무엇인가요?</strong></summary>
필터는 서블릿 컨테이너(WAS)에 의해 관리
인터셉터는 스프링 컨테이너에 의해 관리됨
필터는 스프링 외부에서 동작하고, 인터셉터는 DispatcherServlet 이후 스프링 MVC 흐름 안에서 동작함

</details> <details> <summary><strong>스프링 인터셉터에서 preHandle, postHandle, afterCompletion은 각각 언제 호출되나요?</strong></summary>
preHandle: 컨트롤러 호출 전 실행 (핸들러 어댑터 이전)
postHandle: 컨트롤러 호출 후, View 렌더링 전 실행
afterCompletion: View 렌더링 후, 예외 발생 여부와 상관없이 항상 실행

</details> <details> <summary><strong>다음 중 필터(Filter)와 인터셉터(Interceptor)의 공통 기능이 아닌 것은?</strong></summary>
① 인증 및 인가 처리
② 요청 로깅
③ 이미지 압축 처리
④ 컨트롤러 호출 후 ModelAndView 조작

→ 4번
인터셉터의 postHandle에서만 가능하며, 필터는 ModelAndView를 알지 못한다.

</details> <details> <summary><strong>필터랑 인터셉터 중 요청을 더 정밀하게 제어할 수 있는 것은 어떤거냐?</strong></summary>
필터(Filter)는 서블릿 컨테이너 수준에서 동작하며, /* 같은 서블릿 URL 패턴만 사용할 수 있어 상대적으로 제어가 단순합니다.
반면 인터셉터(Interceptor)는 스프링 컨텍스트에서 동작하며, addPathPatterns("/").excludePathPatterns("/login", "/css/")처럼 패턴 기반의 정밀한 URL 제어 및 제외 경로 지정이 가능합니다.

</details> <details> <summary><strong>세부적인 인증/인가와 같은 공통 로직을 필터 대신 인터셉터로 구현하는 것이 더 적절한 이유를 설명해보세요.</strong></summary>
인터셉터는 스프링 MVC의 흐름 안에서 컨트롤러와 긴밀히 연결되기 때문에, 세션/모델 등의 스프링 컨텍스트를 활용한 인증/인가 로직 구현이 수월함
또한 preHandle()에서 요청을 막거나, postHandle()에서 응답 데이터를 조작하는 등 단계별로 세분화된 작업이 가능하여 확장성과 유지보수가 뛰어남
반면 필터는 request, response 수준의 낮은 추상화만 제공하여 로직 작성이 더 복잡하고 제한적임

</details>

---

## 신예지
<details> <summary><strong>Servlet Filter에서 로그인 사용자와 비로그인 사용자에 대해 필터 제한을 할 때의 로직을 설명해주세요</strong></summary>
로그인 사용자: HTTP 요청 ➙ WAS ➙ 필터 ➙ 서블릿 ➙ 컨트롤러
비로그인 사용자: HTTP 요청 ➙ WAS ➙ 필터(적절하지 않은 요청이라 판단, 서블릿 호출 X)

</details> <details> <summary><strong>Servlet Filter 인터페이스에는 어떤 메서드가 있나요? 그리고 각 메서드는 어떤 역할을 하나요?</strong></summary>
init(): 필터 초기화 메소드로, 서블릿 컨테이너가 생성될 때 호출

doFilter(): 고객의 요청이 올 때 마다 해당 메서드가 호출됨

url-pattern에 맞는 모든 HTTP 요청이 디스패처 서블릿으로 전달되기 전에 웹 컨테이너에 의해 실행되는 메소드로, 필터의 로직을 구현함

FilterChain은 doFilter()를 통해 다음 필터 대상으로 요청을 전달해줌

destroy(): 필터 종료 메소드로, 서블릿 컨테이너가 종료될 때 호출

</details> <details> <summary><strong>Servlet Filter와 Spring Interceptor는 왜 사용할까요?</strong></summary>
웹 애플리케이션에서 공통 관심사(cross-cutting concern)를 처리하기 위해 사용됩니다.
이러한 공통 관심사에는 인증, 로깅, 데이터 압축 등이 포함되며, 이를 통해 코드 중복을 줄이고 유지보수성을 향상시킬 수 있습니다.

</details> <details> <summary><strong>Servlet Filter와 Spring Interceptor의 차이를 동작 위치의 관점에서 말해주세요</strong></summary>
Servlet Filter는 웹컨테이너에서, Spring Interceptor는 스프링 컨텍스트에서 동작한다.

</details> <details> <summary><strong>Servlet Filter와 Spring Interceptor를 각각 언제 사용하면 좋은지 설명해주세요</strong></summary>
필터를 꼭 사용해야 하면 Servlet Filter를 사용하고,
스프링 MVC를 사용하면서 특별히 필터를 꼭 사용해야 하는 상황이 아닐 경우에는 인터셉터를 사용한다.

</details> <details> <summary><strong>Servlet Interceptor에서 postHandle()이 실행되는 시점은 언제인가요? (oo후 oo전)</strong></summary>
Controller가 호출된 후 View 렌더링 전에 실행된다.

</details>

---

## 김수훈
<details> <summary><strong>서블릿 필터는 웹 컨테이너에 의해 관리된다(o/x)</strong></summary>
o

</details> <details> <summary><strong>서블릿 필터 함수 중 init() 함수와 destroy() 함수는 언제 호출되나요?</strong></summary>
서블릿 컨테이너가 생성될 때 / 종료될 때 호출됩니다.

</details> <details> <summary><strong>스프링 인터셉터 호출 흐름을 설명하시오</strong></summary>
![image](https://github.com/user-attachments/assets/f7c800ad-2dde-478c-a0e1-0ddcabd761c0)


클라이언트 - HTTP 요청

Dispatcher Servlet

preHandle 호출

컨트롤러 호출 전에 호출(정확히는 핸들러 어댑터 호출 전에 호출)

preHandle의 응답값이 true이면 다음으로 진행, false이면 더 진행 X

false인 경우, 나머지 인터셉터는 물론이고 핸들러 어댑터도 호출되지 않음

핸들러 매핑 정보에서 핸들러 조회

핸들러 어댑터 목록에서 핸들러를 처리할 수 있는 핸들러 어댑터 조회

핸들러 어댑터의 handle(handler) 호출

Handler Adapter

handler(실제 컨트롤러) 호출

ModelAndView 반환

Dispatcher Servlet

postHandle 호출

ViewResolver - View 반환

Dispatcher Servlet

render(model) 호출

afterCompletion 호출

View - 클라이언트에 HTML 응답

</details> <details> <summary><strong>항상 호출되기 때문에 예외와 무관하게 공통 처리를 할 때 사용하는 스프링 인터셉터 함수는 무엇이며, 언제 실행되나요?</strong></summary>
afterCompletion()
모든 뷰에서 최종 결과를 생성하는 일을 포함해 모든 작업이 완료된 후에 실행됩니다.

</details> <details> <summary><strong>스프링 인터셉터의 용도는 무엇인가요?</strong></summary>
세부적인 보안 및 인증/인가 공통 작업

API 호출에 대한 로깅 또는 검사

Controller로 넘겨주는 정보(데이터)의 가공

</details>

---

## 이소원
<details> <summary><strong>Servlet Filter와 Spring Interceptor는 왜 필요한가요?</strong></summary>
애플리케이션에서 공통으로 관심있는 것에 대해 모든 로직에 작성을 하면 수정 시 모든 로직을 수정해야 하는 문제점이 발생합니다.
공통 업무에 관련된 코드를 로직마다 작성하면 코드 중복이 많아지고, 프로젝트 단위가 커질수록 서버에 부하를 줄 수 있어 Servlet Filter와 Spring Interceptor을 통해 중복된 코드를 제거할 수 있는 기능을 사용하는 것이 좋습니다.

</details> <details> <summary><strong>서블릿 필터와 스프링 인터셉터의 차이점을 설명해주세요.</strong></summary>
  
### 실행 시점
- **Servlet Filter**: DispatcherServlet **이전**에 실행됨
- **Spring Interceptor**: DispatcherServlet **이후**에 실행됨

---

### 적용 대상
- **Servlet Filter**: 모든 요청 (정적 리소스 포함)
- **Spring Interceptor**: Spring MVC 컨트롤러 요청 (RequestMapping 대상)

---

### 주요 기능
- **Servlet Filter**: 보안, 로깅, 인코딩 처리
- **Spring Interceptor**: 인증, 권한 체크, 요청/응답 가공

---

### 적용 범위
- **Servlet Filter**: 서블릿 전역 (Web Filter)
- **Spring Interceptor**: Spring MVC 요청 처리 흐름 내부

---

### 반환 방식
- **Servlet Filter**: `chain.doFilter(request, response)` 호출 **필수**
- **Spring Interceptor**: `boolean` 반환  
  → false 반환 시 요청 **중단**, 이후 컨트롤러 실행되지 않음


</details> <details> <summary><strong>Filter와 Interceptor 중 로그인 인증 기능을 구현할 때 어떤 것을 사용할 건가요?</strong></summary>
Servlet Filter
Interceptor는 Spring MVC의 컨트롤러(@RestController)를 거치는 요청만 처리할 수 있지만,
Filter는 모든 요청(Servlet 레벨)에서 동작하므로 로그인 인증에 적합합니다.

</details> <details> <summary><strong>Filter에서 chain.doFilter(request, response); 를 호출하지 않으면 어떤 문제가 발생하나요?</strong></summary>
다음 필터 또는 서블릿(컨트롤러)로 요청이 전달되지 않기 때문에, 요청이 중단됩니다.
현재 필터에서 응답을 직접 처리하지 않는다면, 클라이언트는 응답을 받지 못하고 요청이 무한 대기 상태에 빠질 수 있습니다.

</details> <details> <summary><strong>Interceptor에서 preHandle에서 false를 반환하면 어떻게 되나요?</strong></summary>
preHandle() 메서드는 컨트롤러(@Controller, @RestController)가 실행되기 전에 호출됨

true를 반환하면 요청이 계속 진행되어 컨트롤러로 전달됨

false를 반환하면 요청이 중단되며, 컨트롤러가 실행되지 않음

</details>
