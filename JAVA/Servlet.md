# 서블릿
> 클라이언트 요청에 따라 동적으로 컨텐츠를 생성하는 자바 클래스

## 주요 특징
   - URL Mapping: 클라이언트 요청을 처리하기 위해 web.xml 파일이나 어노테이션을 사용하여 URL과 서블릿 클래스를 연결
   - HTTP 요청 처리: 클라이언트의 HTTP 요청(GET, POST 등)에 따라 doGet() 또는 doPost()와 같은 메서드를 오버라이딩하여 동적 페이지 생성
   - 서버 사이드 로직: 클라이언트 요청에 따라 서버에서 DB 처리, 비즈니스 로직 실행 등의 작업을 수행
   - 웹 애플리케이션 내부에 위치: 서블릿 클래스는 일반적으로 WEB-INF/classes/ 디렉토리에 위치하며, 웹 애플리케이션 컨텍스트에서 실행
   - 서블릿 컨테이너: 서블릿은 서블릿 컨테이너라는 웹 애플리케이션 서버 환경에서 실행되며, 클라이언트의 요청을 받아 처리


## 어노테이션을 통한 설정

@WebServlet(name = "boardlist", urlPatterns = {"/board/list.do"})  
-> name은 유일한 값이어야 하고, urlParrterns 은 서버가 인식하는 페이지 내부

예시 코드
~~~java
import javax.servlet.annotation.WebServlet;

@WebServlet(name = "boardlist", urlPatterns = {"/board/list.do"})
public class BoardListServlet extends HttpServlet {
    // 서블릿 코드
}
~~~

## 상속 관계 
Servlet: 인터페이스
   
GenericServlet: 'Servlet'인터페이스를 구현한 클래스로, 일반적인 서블릿 기능 제공

HttpServlet : 'GenericServlet'을 확장한 클래스로, HTTP 프로토콜에 특화된 기능 제공

CustomServlet(사용자가 만든 서블릿)

      HttpServlet 상속하여, 필요한 메소드를 오버라이딩하여 구현
      서버가 객체의 lifecycle을 관리하므로 관련 메소드를 오버라이딩 해야함

## 서블릿이 요청을 처리하는 과정
> 서블릿은 생명주기(LifeCycle)를 관리하기위해 자동으로 콜백 메소드(init(), service(), destroy())가 실행된다.  

1. 클라이언트가 HTTP 요청(웹은 대부분 GET or POST) 
2. 서블릿 컨테이너에 요청이 도착하면 컨테이너에서 서블릿 객체 생성
3. init() 메소드가 딱 한 번 호출되며 서블릿 객체를 초기화
4. service() 메소드를 호출해 doPost() 혹은 doGet()메소드로 전달
5. doPost()혹은 doGet() 메소드는 클라이언트 요청을 처리하여, HTTP 응답을 생성
6. 응답 전송 후에는 객체가 소멸되며 소멸 전 destroy() 메소드를 호출한


## 요청재지정
> 클라이언트가 최초 요청을 다른 페이지나 서블릿으로 전환하거나, 데이터를 공유하는데 사용 

      데이터 공유 Scope
      
      page(현재 페이지 공유)
      equest(한 번 실행하여 응답되는 모든 페이지 공유. jsp에서는 include)
      session(인터넷 창을 닫기 전까지 혹은 세션 시간이 만료될때 까지 공유)
      pplication(웹 애플리케이션이 시작될때 생성되어 전체에 공유)

      [메소드]
      데이터 저장 : scope객체.setAttribute("공유할이름",객체명);
      데이터 가져오기 : 객체타입 변수 = scope객체.getAttribute("공유된이름");


### 요청 재지정 메소드

1. response.sendRedirect("요청할 path")
   - 클라이언트의 요청을 다른 경로로 재지정하여 이동, 브라우저에서 새로운 요청을 보냄
   - 데이터 공유되지 않음
   - 로그인 실패 등에 사용

2. RequestDispatcher의 forward
   - RequestDispatcher rd = request.getRequestDispatcher("요청할 path");
   - 현재 서블릿의 실행을 멈추고 다른 서블릿이나 JSP로 제어를 넘김
   - 데이터 공유, 주소표시줄은 최초 요청한 서블릿 주소 유지
   - rd.forward(request, response);를 사용하여 호출
 
3. RequestDispatcher의 include
   - RequestDispatcher rd = request.getRequestDispatcher("요청할 path")
   - 다른 서블릿이나 JSP의 실행 결과를 현재 페이지에 포함
   - 데이터 공유, 주소표시줄은 최초 요청한 서블릿 주소 유지
   - rd.include(request, response);를 사용하여 호출

