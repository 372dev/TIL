# Oracle vs MySQL

## :muscle:Oracle vs MySQL
Oracle 그리고 MySQL. MS SQL과 더불어 3대 DBMS의 위상을 지키고 있는 두가지 데이터 베이스의 특성적 차이 그리고 문법 차이를 알아본다.

### :star:각각의 특성

#### :mag:Oracle
Oracle is a relational database management system designed to be self-driving, self-securing, self-repairing, and eliminate error-prone manual database management. It can run on various operating systems and allows for safe storage and fast retrieval of data. Oracle is the first database tool developed for business purposes to manage data using a query language, released in 1980 with basic SQL features. 

* It is scalable, portable, distributed, and programmable.
* It allows interacting with the database without knowing the physical storage of the data.
* Oracle enables the communication between applications across the different platforms with the Oracle database smoothly.
* Oracle database can run on various operating systems such as Windows, Linux, Mac, etc.
* It enables the ACID property to maintain the integrity and reliability of your data.
* It can manage a large volume of data quickly.
* It has a recovery manager tool that provides cold, hot, and incremental database backups and recoveries.
* Capable of running large ILTB and VLDBs.
* Very feature-rich.
* Reliable.
* Provides Flashback technology.

#### :mag:MySQL
MySQL is a popular database management system designed for handling relational databases. It is a scalable, open-source tool supported by Oracle Company. Compared to the Oracle database, MySQL's processing is just as fast and its interface is often cited on review sites as being more intuitive and easier to use.

The Swedish Company MySQL AB developed and supported MySQL. In January 2008, Sun Microsystems bought MySQL AB for $1 billion. In April 2009, Oracle Corporation agreed to purchase Sun Microsystems, then owners of MySQL copyright and trademark. Many small and big companies use MySQL. MySQL works with many operating systems like Windows, Linux, macOS, etc. with C, C++, and Java languages. 

* 무료이고 오픈소스다. 다만, 상용버전이 있고 Standard, Enterprise, Cluster 등 제공 기능 범위에 따른 제품군이 있다.
* MariaDB는 MySQL에서 파생되었다.
* MySQL is an easy-to-use relational database management system. 
* It follows a client /server architecture.
* It provides excellent performance, high flexibility, and increased productivity.
* It is scalable.
* Incredible security
* It enables transactions to be rolled back, commit, and crash recovery.

### :star:비교표

#### :mag:신택스와 활용도 비교
| 목차 | MySQL | Oracle |
| 출시 | 1995 | 1980 |
| 가격 | * 무료이고 오픈소스다  * GPL 라이선스 | * 유료이고 상업적인 용도를 위해 라이선스가 필요하다  * 학생들은 XE버전을 무료로 사용할 수 있다  |
| OS | * Windows  * Mac OS X  * Linux  * UNIX  * z/OS  * BSD  * Symbian  * AmigaOS | * Windows  * Mac OS X  * Linux  * UNIX  * z/OS |
| 확장성 | 소규모 비즈니스에 적합하다 | 큰 규모의 프로젝트에 적합하다 |
| 데이터 파티셔닝 | 지원되지 않는다 | 지원된다 |
| 보안 | 접근할 때 username, password 그리고 host가 요구된다 | 접근할 때 username, password 그리고 프로필 확인이 요구된다 |
| 시스템 타입 | Static 시스템 | Static 시스템, Dynamic 시스템 |
| Null 값 | 지원된다 | 지원되지 않는다 |
| 문자 자료형 | CHAR, VARCHAR | CHAR, VARCHAR2, NCHAR, NVARCHAR2 |
| 언어 | SQL | SQL, PL/SQL |

#### :mag:


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