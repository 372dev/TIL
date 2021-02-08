# JSP & Servlet

## :muscle:JSP
JSP(Java Server Pages)는 웹 페이지를 개발하기 위한 다양한 기술들의 집합체이다. JSP 태그를 통해 자바 코드를 HTML안에서 사용 할 수 있다. 이 과정에서 HTML, XML, JSP 액션과 커맨드가 사용된다.

JSP는 정적인 데이터, 동적인 데이터 모두 가질 수 있으며, JSP 요소는 동적으로, HTML, XML, SVG, WYML 요소는 정적으로 사용된다. 

### :star:주요 스크립트

#### :mag:표기법
* 주석(Comments tag) : <%-- Comments --%>
* 지시자(Directive tag) : <%@ Directive %>
* 선언문(Declaration tag) : <%! Declaration %>
* 스크립틀릿(Scriptlet tag) : <% Scriptlet %>
* 표현식(Expression tag) : <%= Expression %>

### :star:JSP/Servlet 내장 객체
* application
* session
* request
* page
* response
* out
* pageContext
* config
* exception

#### :mag: 스코프
page < request < session < application 순서로 포함하는 영역이 커진다.

* page : 한번의 클라이언트 요청으로 하나의 JSP 페이지를 처리할 때 사용되는 영역.
따로 내장된 객체가 없기 때문에 pageContext 객체를 이용해야 하고 하나의 page 안에서 입/출력이 모두 이뤄진다.
다른 페이지에서는 스코프를 넘어가기 때문에 pageContext 객체를 이용할 수 없다.
지역변수처럼 사용된다.

* request : 한번의 웹 브라우저 요청을 처리할 때 사용되는 영역.
브라우저 주소창에 url을 입력하거나 링크를 클릭하여 페이지를 이동할 때, 브라우저가 웹 서버에 전송하는 요청이
하나의 request 영역이다. 새로운 요청이 보내질 때 마다 새로운 request 영역이 생성된다.
page 영역은 하나의 jsp 페이지만 포함하는데 반해 request 영역은 하나의 요청을 처리하는데 사용되는
모든 jsp 페이지를 포함한다는 차이점이 있다.

* session : 하나의 웹 브라우저와 관련된 영역.
세션이 생성되면 하나의 웹 브라우저와 관련된 모든 요청은 하나의 세션 영역에 포함된다.
각 세션을 구분하기 위해 고유 ID가 할당된다.
한번 생성된 세션은 지정한 유효기간 동안 유지된다. 웹 애플리케이션을 실행하는 동안 지속적으로 사용해야 하는
데이터의 저장할 장소로 세션 영역이 적당하다.
request 기본 객체가 하나의 요청을 처리하는데 사용되는 jsp 페이지 사이에서 공유된다면
session 기본 객체는 웹 브라우저의 여러 요청을 처리하는 jsp 페이지 사이에서 공유된다.
로그인한 회원 정보 등 웹 브라우저와 일대일로 관련된 값을 저장할 때는 쿠키 대신 세션을 사용할 수 있다.

* application : 하나의 웹 애플리케이션과 관련된 영역
어느 하나의 웹 애플리케이션 서비스를 실행하면 하나의 애플리케이션 영역이 생성된다. 내가 웹 서버에 접속한
시점부터 서비스를 종료하는 시점까지 유효하며, 모든 클라이언트가 공통으로 사용할 값 들이 있을 때 주로 사용한다.

* jsp 페이지에서 표현식 지시자 태그를 이용해 스코프를 테스트 해볼 수 있다.

<%= request.getAttribute("요소") %>
request 영역은 요청을 주고받은 페이지에서는 접근이 가능하겠으나 그 이후 새로운 요청이 생기면 사라지게 된다.

<%= session.getAttribute("요소") %>
세션이 유지되는 동안 유지되며, 다른 jsp 에서도 접근할 수 있다.

<%= application.getAttribute("요소") %>
웹 애플리케이션이 작동하는 동안 유지된다. 가장 넓은 스코프이다.


#### :mag:JSP request 주요 메서드

#### :mag:JSP response 주요 메서드


### :star:JSP의 장단점
* 장점
  * JSP can be used to write Servlets.
  * JSP is very easy to modify, and therefore, it makes it very convenient.
  * Developers can easily show and process information in JSP.
  * JSP can use the multithreading feature of Java.
  * JSP can be easily connected to the MYSQL databases. 
  * JSP can use the exceptional handling feature of Java.
  * JSP has better performance and scalability, as developers can embed dynamic elements into the HTML code.
  * JSP is based in Java and is platform-independent.

* 단점
  * It is very difficult for developers to perform database connectivity in JSP.
  * As the JSP is compiled on the server, it is not memory and time-efficient.
  * It is hard to track errors in JSP files because they are an extension to Servlets. The JSP codes are processed into Servlet codes for compilation.
  * As JSP is an HTML file, it doesn’t provide many features. 

## :muscle:서블릿
Servlets generate dynamic content, interact with the client, and are maintained by Servlet engine containers. Servlets are used to extend the functions provided by the servers.

### :star:서블릿 매핑, 인코딩
* full path
  * http://도메인/contextPath/servlet/com.servlet.ServletEx
  * 보안 취약, 복잡한 URL

* mapping path
  * http://도메인/contextPath/SE
  * 간결한 URL

#### :mag:매핑하는 방법
* web.xml을 통한 방법
아래와 같은 코드를 WebContent/WEB-INF/web.xml에 추가해준다. 서블릿 태그로 서블릿 별칭과 경로의 서블릿을 연결하고, 서블릿 매핑 태그로 서블릿 별칭과 연결할 주소(url 패턴)를 연결한다.

```xml
<servlet>
  <servlet-name>서블릿별칭</servlet-name>
  <servlet-class>경로.서블릿이름</servlet-class>
</servlet>
<servlet-mapping>
  <servlet-name>서블릿별칭</servlet-name>
  <url-pattern>/연결할주소</url-pattern>
</servlet-mapping>
```

* 어노테이션을 통한 방법
아래와 같이 서블릿 위에 WebServlet 이라는 어노테이션을 붙이고 주소를 지정해 준다.
```java
@WebServlet("/연결할주소")
private class 서블릿이름 extends HttpServlet {
  // 서블릿 내용...
}
```

물론 대부분 상황에서 어노테이션을 이용하겠지만 간혹 web.xml을 이용하게 될 상황이 있을 수 있다.

#### :mag:request 객체와 response 객체에의 문자 인코딩 설정

* 요청이 GET 방식인 경우
  * server.xml 파일에서 Connector의 useBodyEncodingForURI 속성을 true로 지정
  * server.xml 파일에서 Connector의 URIEncoding 속성의 값으로 원하는 캐릭터 셋 지정.

```xml
<Connector useBodyEncdoingForURI="true" />
```

```xml
<Connector URIEncoding="UTF-8" />
```

* 요청이 POST 방식의 경우
해당 서블릿에 인코딩 옵션 추가
```java
request.setCharacterEncoding("UTF-8");
response.setContentType("txt/html; charset=UTF-8");
```

필터를 이용할 경우엔 모든 url 패턴에 필터를 적용한 상태에서 인코딩 옵션을 작성하고 chain.doFilter(request, response); 하여 적용시킬 수 있다.

### :star:서블릿 라이프 사이클
1. 서블릿 객체 생성
2. 서버가 init() 메소드 호출하여 서블릿 초기화
3. service() 메소드 호출, 요청 방식이 GET이면 doGet() 실행, POST이면 doPost() 메소드 실행
4. doGet() 혹은 doPost() 실행
5. destroy() 메소드 호출, 서블릿 종료

* 각각의 메소드를 오버라이드 하여 System.out을 작성하면 서블릿 실행시 메세지를 통해 콘솔에서 라이프 사이클을 확인할 수 있다.

### :star:form 데이터 처리
* GET 방식 : 사용자 정보가 URL에 노출되며 보안에 취약
* POST 방식 : URL에는 매핑 정보만 노출되며 

### :star:서블릿의 장단점
* 장점
  * Servlets load only one copy into the Java Virtual Machine. This makes their memory efficient and faster.
  * The response time is significantly less, as it saves time to respond to the first request. 
  * Servlets are easily accessible, as they use standard API that is used by a large number of web servers.
  * It is easy for development and is platform-independent.
  * Servlet’s usage doesn’t constrain the web servers. 
  * Servlets help developers access a large number of APIs, which are available for Java. 
  * It is very easy to maintain multiple Servlets for a single web application.
  * Servlet containers provide developers with the facility of support to several other features like resource management, sessions, security, persistent, etc. 
  * If servlets have multiple requests, the web containers provide threads to handle more than one request.

* 단점
  * Servlets create threads and not a process when a request arrives.
  * It is harder to code and perform exception handling, as Servlet codes are not thread-safe by default.
  * Java Runtime Environment is necessary to run Servlets on the server.
  * Developing Servlets requires experience and a lot of knowledge of Java Servlets for development.
  * Only one Servlet is loaded into the JVM.
  * HTML code and Java code are interdependent and can cause errors if changes are not taken into consideration. 

### :star:서블릿과 JSP의 비교


-References :
실전 JSP (renew ver.) - 신입 프로그래머를 위한 강좌 by 인프런  
https://dololak.tistory.com/56  
https://www.upgrad.com/blog/jsp-vs-servlet/