# LFM_01 - JSP / Servlet Setup
## :muscle:실수에서 배우자 01 - JSP / Servlet 환경설정
* JSP / Servlet 수업이 끝난 후, 복습할 내용을 한곳에 모아두기 위해 프로젝트의 디렉토리를 이동하였다.
* 이동한 장소에서 웹 프로젝트가 작동하지 않았다.
* 자바 프로젝트의 위치를 바꾸고 싶은 경우 export와 import를 사용해야 한다!
* 또한 프로젝트를 시작할 때 설정 내용을 기록해 두는 것도 좋을 것 같다.
* 아래 내용은 복구를 시도하는 과정에서 사용했던 설정들이다.

## :mag:자바 환경설정
1. JDK 설치
   * Oracle 1.8.0-openjdk 혹은 Amazon Correto jdk11.0.8
2. 환경 변수 설정
   * This PC -> Advanced system setting -> Environment Variables -> System variables -> Path
   * JDK가 설치된 폴더 경로를 작성한다.
 
![Edit_environment_variable](https://raw.githubusercontent.com/372dev/TIL/main/LFM/img/01_01.png)

3. java / javac 테스트
   * CMD를 열어 입력창에서 java - version을 실행한다.
   * javac -version을 실행한다.

![cmd](https://raw.githubusercontent.com/372dev/TIL/main/LFM/img/01_02.png)

4. 이클립스 혹은 인텔리제이 설치
5. 인코딩 설정
   * 한글을 사용하여 개발할 경우 인코딩을 모두 UTF-8로 변경해 준다.
   * 이클립스의 경우, Window -> Preferences -> "encoding" 검색 -> "Content Types"에서 Java Class File과 Text의 Default encoding을 UTF-8로 변경.
   * 그외에 Workspace, CSS Files, HTML Files, JSP Files, XML Files의 Encoding을 모두 UTF-8로 변경.

![encoding](https://raw.githubusercontent.com/372dev/TIL/main/LFM/img/01_03.png)

## :mag:JSP / Servlet 설정
1. 웹컨테이너 설치
   * 아파치 톰캣 (ApacheTomcat 8.5 혹은 9.0) 설치
2. 이클립스에서 서버 생성
   * 서버탭(서버탭이 없다면 Window -> Show view에서 설정하여 보이도록 한다.)에서 No servers are available... 링크를 클릭한다.
   * New Server 창에서 톰캣 버전을 선택한다. -> Next
   * Tomcat installation directory를 설정해준다. -> Finish
3. 생성된 웹컨테이너 설정
   * 생성된 서버를 더블클릭하면 설정창이 열린다.
   * 8080으로 되어있는 포트번호를 다른 번호로 변경해 준다. SQL 디벨로퍼와의 충돌을 막기 위해서이다. (DBMS에서 이미 쓰고있다면 서버가 생성되지 않을 것이다.)
   * (선택적) Server Locations에서 Use Tomcat installation을 선택, Server Options에서 Publish module contexts to separate XML files를 선택.
   * 콘솔창 오른쪽에서 Publish to the server 버튼을 클릭하여 변경 내역을 동기화 한다.

## :mag:기타 설정
1. JDBC 드라이버 설정
   * Oracle 에서 JDBC 드라이버를 다운로드 한다.
   * 임의의 장소에 저장한 뒤 경로설정을 해줄 수 있다.
   * 프로젝트 안의 경로에 포함할 수도 있다.
   * Java Build Path의 Libraries에서 드라이버를 추가해준다.

![jdbc](https://raw.githubusercontent.com/372dev/TIL/main/LFM/img/01_04.png)

2. 파일업로드 라이브러리 추가
   * servlets.com/cos 에서 cos를 다운로드 받는다.
   * JDBC와 동일하게 라이브러리에 추가해준다.

## :mag:시행착오
1. 정상적으로 export되지 않은 프로젝트를 되살리고 싶을 때, 프로젝트 타입의 선택이 잘못될 경우 컴파일이 안되고 오류를 해결하려 해도 시간만 낭비될 수 있다. 이번의 경우엔 새로운 Dynamic Web Project를 새로 생성한 후에 작업 내용만 복사해오는 방식으로 해결했다.
2. 생성된 프로젝트에 지구본 모양이 없다? 자바 애플리케이션으로만 인식이 된 프로젝트를 아래 과정을 통해서 프로젝트를 다이나믹 웹 프로젝트로 바꿀 수 있다.
   * 오른쪽 클릭하여 나오는 메뉴에서 Properties 선택 -> Project Facets 선택 -> Dynamic Web Module과 Java의 버전을 설정해준다.
   * Dynamic Web Module 선택 옵션이 보이지 않을 경우엔 Configuration에서 Dynamic Web Project 선택한 뒤 버전을 설정해준다.

![facet](https://raw.githubusercontent.com/372dev/TIL/main/LFM/img/01_05.png)

3. git에서 가져온 프로젝트엔 gitignore로 인해 빠진 내용이 많을 것이다. Eclipse의 경우 Navigator에는 나타나지 않는 치명적 오류를 가진 파일이나 Libraries 내용이 Project Explorer에는 명확히 표현되니 잘 활용하도록 하자.

![explorer](https://raw.githubusercontent.com/372dev/TIL/main/LFM/img/01_06.png)

4. .settings 폴더와 .classpath 파일을 함부로 건드리지 말자!

5. build 폴더는 직접 지우기 보다는 프로젝트 Clear를 이용하자! 가끔 수정된 스타일이나 코드를 바로 적용시키지 못하는 바보 이클립스를 프로젝트 Clear를 이용해서 정신을 차리게 해줄수도 있다.
