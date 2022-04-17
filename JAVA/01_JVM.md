# Java_01_JVM

## :muscle:JVM

### :star:JVM이란 무엇인가 / JVM의 구성 요소
* 자바를 실행하기 위한 가상의 기계이며 추상적이고 플랫폼에 의존적이다.
* JVM은 코드를 실행하고 해당 코드에 대해 런타임 환경을 제공하는 소프트웨어 프로그램에 대한 가이드라인이며 청사진이다.
* JVM은 가비지 컬렉션이란 프로세스를 통해 메모리를 관리한다.  

자바가 개발될 당시에는 프로그래밍 언어와 가상머신이 따로 존재하는 방식은 어불성설로 여겨졌으나 자바 이후로 다른 여러 프로그래밍 언어들(Microsoft .NET 등)도 이 방식을 채택했다.  

* JVM은 세 부분으로 구성되었다고 말 할 수 있다.  
1. The JVM specification  
JVM은 아래의 implementations 단계에 필요한 가이드라인과 청사진, 다르게 표현하자면 규칙성을 정해준다. 덕분에 다양한 플랫폼에서 동일하게 실될할 수 있다.  
2. JVM implementations  
위 과정을 실제 소프트웨어 프로그램에 구현한다. 다양한 JVM 구현이 존재하며, 라이센스가 부여된 거의 모든 JVM은 오픈JDK와 핫스팟 JDK에서 파생되었다.  
3. A JVM instance  
위 과정을 거쳐 소프트웨어 제품으로 완성이되면 다운로드 받아 실행할 수 있다. 다운로드된 프로그램이 JVM 인스턴스이다. 개발자들이 JVM 에 대해서 말할 때 대부분 이 단계의 프로그램을 말한다.  
-Sources : [https://www.infoworld.com/article/3272244/what-is-the-jvm-introducing-the-java-virtual-machine.html](https://www.infoworld.com/article/3272244/what-is-the-jvm-introducing-the-java-virtual-machine.html)  
[https://www.itworld.co.kr/news/110837](https://www.itworld.co.kr/news/110837)  
[https://simple.wikipedia.org/wiki/Program_specification](https://simple.wikipedia.org/wiki/Program_specification)  
[https://en.wikipedia.org/wiki/Java_virtual_machine](https://en.wikipedia.org/wiki/Java_virtual_machine)  

### :star:컴파일 하는 방법 / 실행하는 방법
1. 텍스트 에디터(메모장 등)를 이용해 자바 프로그램을 작성한다.
2. 확장자 를 .java로 하여 저장한다 (Hello.java로 해보자)
3. 윈도우의 경우엔 CMD(Command Prompt), 그리고 맥의 경우엔 터미널을 열어준다
4. javac Hello.java 를 입력한다. 자바 컴파일러에게 입력된 파일을 컴파일 해달라 요청하는 과정이다. 코드에 에러가 없다면 다음 라인으로 진행된다.
5. java Hello를 입력한다. 컴파일된 자바 파일이 실행된다.  
-Sources : [https://beginnersbook.com/2013/05/first-java-program/](https://beginnersbook.com/2013/05/first-java-program/)  
[https://www.studytonight.com/java/first-java-program.php](https://www.studytonight.com/java/first-java-program.php)  

### :star:바이트코드란 무엇인가
자바 가상 머신이 프로그램을 가져올 때, 자바 언어의 소스 코드를 그대로 가져 오지 않는다는 것을 알아둬야 한다. 대신에 자바 소스 코드는 자바 바이트코드 라고 하는 것으로 변환(컴파일)된다. 자바 바이트코드는 자바 가상 머신으로 전달될 때 클래스 파일의 형태로 전해저야 한다(확장자는 항상 .class를 갖는다).  
-Source : Java in a nut shell 7th edition by Benjamin J. Evans and David Flanagan  

![whiteship01_1](https://raw.githubusercontent.com/372dev/372dev.github.io/1ea8172a288c6defb62cd4fbb3b7f21ba2e99ff0/_posts/imgs/whiteship01_1.PNG)  
-Source : [https://www.javatpoint.com/java-bytecode](https://www.javatpoint.com/java-bytecode)  

### :star:JIT 컴파일러란 무엇이며 어떻게 동작하는지
모든 프로그래밍 언어는 컴파일러를 이용하여 고수준 언어를 저수준 언어로 변환해 사용한다. 시스템이 바이너리 코드만 이해할 수 있기 때문이다. 프로그래밍 언어의 종류에 따라 컴파일러도 제각각인데, 자바의 컴파일러는 JIT이라고 불린다. Just-in-Time의 준말이며 JIT는 JRE의 일부분이다. 자바 기반의 어플리케이션의 런타임이나 실행시에 성능 최적화의 역할을 주로 맡는다. 더 자세히 알고 싶으면 source를 읽어보자.  
-Source : [https://www.edureka.co/blog/just-in-time-compiler/](https://www.edureka.co/blog/just-in-time-compiler/)

### :star:JDK와 JRE의 차이
* JRE는 Java Runtime Environment의 약자로 소프트웨어 툴의 집합체이고 자바 어플리케이션을 개발하는데 이용된다. 런타임 환경을 제공하며 JVM을 활용한다. JVM과 달리 실제로 존재하며 JVM이 런타임에 이용할 수 있는 라이브러리들과 다른 파일들을 포함한다.
* JDK는 Java Development Kit의 약자로 소프트웨어 개발 환경이다. 자바 어플리케이션을 개발할 때 쓰이며 JRE와 마찬가지로 실제로 존재한다. JRE를 포함하고 있으며 그 외에 javac(컴파일러), java(인터프리터/로더) 등 개발 툴들을 갖고 있다. 오라클 사가 출시한 다음 세가지 버전 중 하나를 적용하게 되는데 이는 SE(Standard Edition), EE(Enterprise Edition), ME(Micro Edition)이다.  

![whiteship01_2](https://raw.githubusercontent.com/372dev/372dev.github.io/master/_posts/imgs/whiteship01_2.PNG)  
![whiteship01_3](https://raw.githubusercontent.com/372dev/372dev.github.io/master/_posts/imgs/whiteship01_3.PNG)  
-Source : [https://www.javatpoint.com/difference-between-jdk-jre-and-jvm](https://www.javatpoint.com/difference-between-jdk-jre-and-jvm)