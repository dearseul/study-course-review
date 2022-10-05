## 스프링 MVC 기본구조 이해
### 인터페이스 살펴보기
- 스프링 MVC의 큰 강점은 DispatcherServlet 코드의 변경 없이, 원하는 기능을 변경하거나 확장할 수 있다는 점이다. 
- 지금까지 설명한 대부분을 확장 가능할 수 있게 인터페이스로 제공한다. 
- 이 인터페이스들만 구현해서 DispatcherServlet 에 등록하면 여러분만의 컨트롤러를 만들 수도 있다.
### 주요 인터페이스 목록
- 핸들러 매핑: org.springframework.web.servlet.HandlerMapping 
- 핸들러 어댑터: org.springframework.web.servlet.HandlerAdapter 
- 뷰 리졸버: org.springframework.web.servlet.ViewResolver
- 뷰: org.springframework.web.servlet.View


    Tip: 대부분의 기능은 다 구현되어 있으니 만드려고 하기전에 스프링을 다 찾아보자


