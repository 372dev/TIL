# Servlet

## :muscle:서블릿

### :star:서블릿 매핑
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

### :star:서블릿 요청/응답

#### :mag:request 객체와 response 객체에서 문자인코딩을 변경하는 코드

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
5. destroy() 메소드 호출, 서블릿 제거

* 각각의 메소드를 오버라이드 하여 System.out을 작성하면 서블릿 실행시 메세지를 통해 콘솔에서 라이프 사이클을 확인할 수 있다.

-References :
실전 JSP (renew ver.) - 신입 프로그래머를 위한 강좌 by 인프런  
https://dololak.tistory.com/56  
