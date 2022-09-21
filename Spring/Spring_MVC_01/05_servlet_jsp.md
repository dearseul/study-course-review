### JSP 사용법
1. <%@ page contentType="text/html;charset=UTF-8" language="java" %>
2. 첫 줄은 JSP문서라는 뜻이다. JSP 문서는 이렇게 시작해야 한다. 
3. 회원 등록 폼 JSP를 보면 첫 줄을 제외하고는 완전히 HTML와 똑같다. JSP는 서버 내부에서 서블릿으로 변환되는데, 우리가 만들었던 MemberFormServlet과 거의 비슷한 모습으로 변환된다.

4. 실행 http://localhost:8080/jsp/members/new-form.jsp
5. 실행시 .jsp 까지 함께 적어주어야 한다.

- JSP는 자바 코드를 그대로 다 사용할 수 있다.
- <%@ page import="hello.servlet.domain.member.MemberRepository" %>
- 자바의 import 문과 같다. 
- <% ~~ %> 이 부분에는 자바 코드를 입력할 수 있다. 
  - <%= ~~ %> 이 부분에는 자바 코드를 출력할 수 있다.


    JSP를 보면, 회원 저장 서블릿 코드와 같다. 다른 점이 있다면, HTML을 중심으로 하고, 자바
    코드를 부분부분 입력해주었다. <% ~ %> 를 사용해서 HTML 중간에 자바 코드를 출력하고 있다.