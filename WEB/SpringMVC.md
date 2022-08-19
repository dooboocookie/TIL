# Spring MVC

> ## Servlet

### 서블릿 등록

* `스프링 부트`에서는 @ServletComponentScan 어노테이션을 추가
  * 서블릿 클래스들을 컴포넌트 스캔하여 jar파일 실행시 싱글톤으로 객체를 생성

```java
@ServletComponentScan //서블릿 컴포넌트 스캔
@SpringBootApplication
public class ServletApplication {
	public static void main(String[] args) {
		SpringApplication.run(ServletApplication.class, args);
	}
}
```

* 어노테이션을 통한 등록
  * @WebServlet
    * name속성
    * urlPattern
```java
@WebServlet(name = "exServlet", urlPatterns = "/ex")
public class ExServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    }
}
```
  * `/ex` URL패턴에 걸리는 요청을 받으면 해당 서블릿 객체 호출
  * service(HttpServletRequest req, HttpServletResponse resp)
    * 해당 메소드 실행
    * `HttpServletRequest`요청을 담는 객체
    * `HttpServletResponse` 응답에 대한 객체
 
** [JSP 정리](JSP.md)에 자세히 정리한 내용이 있음
  

### HttpRequest 객체

요청 데이터
    겟 방식
    포스트방식
    Http 메세지 바디