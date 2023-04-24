# 서블릿
> 클라이언트 요청에 따라 동적으로 컨텐츠를 생성하는 자바 클래스

- web.xml을 기반으로 사용자가 요청한 url 이 어느 서블릿에 대한 요청인지 찾는다.
- 클라이언트가 요청하면 서버에서 실행되며 DB 처리를 하고 서버 리소스를 이용해서 결과를 클라이언트에 응답한다.
- doGet() 방식과 doPost() 방식으로 동적 페이지를 생성한다.
- 서블릿 저장위치 :  \Context\WEB-INF\classes\
- 서버에 의해 호출되므로 반드시 public 클래스로 작성해야한다.
- web.xml에 적는 것 대신 간단하게 아래와 같이 어노테이션으로 표현할 수 있다.  
@WebServlet(name = "boardlist", urlPatterns = {"/board/list.do"})  
-> name은 유일한 값이어야 하며, urlParrterns 은 서버가 인식하는 페이지 내부에 있어야 함.   


## 서블릿이 요청을 처리하는 과정
> 서블릿은 생명주기(LifeCycle)를 관리하기 위해 콜백 메소드(init(), service(), destroy())가 실행된다.  


1. 클라이언트가 HTTP 요청(웹은 대부분 GET or POST) 
2. 서블릿 컨테니어에 요청이 도착하면 컨테이너에서 서블릿 객체 생성
3. init() 메소드가 딱 한 번 호출되며 서블릿 객체를 초기화한다.
4. service() 메소드를 호출해 doPost() 혹은 doGet()메소드로 전달된다.
5. doPost()혹은 doGet() 메소드는 클라이언트 요청을 처리하여, HTTP 응답을 생성한다.
6. 응답 전송 후에는 객체가 소멸되며 소멸 전 destroy() 메소드를 호출한다.


## 요청재지정
> 클라이언트가 최초 요청한 서블릿을 응답하지 않고 다른 웹 어플리케이션(HTML, JSP, 다른 서블릿)이 응답하도록 재요청하는 것을 의미

1. 데이터 공유
- page(현재 페이지 공유)
- request(한 번 실행하여 응답되는 모든 페이지 공유. jsp에서는 include)
- session(인터넷 창을 닫기 전까지 혹은 세션 시간이 만료될때 까지 공유)
- application(웹 애플리케이션이 시작될때 생성되어 전체에 공유)

2. 메서드  
scope객체.setAttribute("공유할이름",객체명);

3. 요청 재지정    
   1. response.sendRedirect
   2. RequestDispatcher의 forward(서블릿에서 주로 사용)
   3. RequestDispatcher의 include(JSP에서 주로 사용)

