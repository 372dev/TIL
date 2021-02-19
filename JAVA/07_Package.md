# Java_07_Package

## :muscle:패키지
패키지는 클래스들, 인터페이스들과 참조 변수들의 모음에 이름을 붙여놓은 것이다. 비슷하거나 연관되어 있는 클래스, 인터페이스들을 그룹지어주고 분류된 그룹별 명칭을 붙여주는 역할을 한다.
자바의 핵심 클래스들은 다음과 같이 java 라는 이름의 패키지 안에 들어 있다.

* 자바 언어의 기반역할을 하는 클래스들은 java.lang. 패키지 안에 있다.
* 다양한 유틸리티 클래스들은 java.util. 패키지 안에 있다.
* 입출력을 위한 클래스들은 java.io 패키지에 있다
* 네트워킹을 위한 클래스들은 java.net. 패키지 안에 있다.

이들 패키지들은 서브패키지를 갖고 있기도 한다. 예를 들자면 java.lang 안에는 java.lang.reflect 이 있고 java.util 안에는 java.util.regex 가 있다.

Oracle(과거에는 Sun)에 의해서 규정된 추가기능(extension)들의 패키지는 javax로 시작한다. 이들 추가기능의 일부는 시간이 지나며 자바 기본 기능으로 편입되기도 했다.

마지막으로, "보증된 표준"이 몇가지 있다. 이들 패키지들은 해당 보증을 작성한 기관을 따라 이름지어졌다. 예를들어 org.w3c 이나 org.omg가 있다.

모든 클래스는 정식명칭과 별칭을 갖고 있다. 정식 명칭은 FQCN(fully qualified class name) 이라고 하며 패키지 경로를 모두 포함한 이름이고, 별칭은 클래스가 작성될때 지어진 클래스명이다.
예를 들어 String 클래스의 경우 "String"은 클래스명이고, 위치는 java.lang 패키지 안에 있으므로 FQCN은 java.lang.String 이다.

#### :mag:빌트인 패키지(built-in packages)
자바의 패키지는 두가지 종류로 나눌 수 있는데, 빌트인 패키지(built-in package)와 사용자설정 패키지(user-defined package)이다. 우리가 코딩하며 작성하는 것이 사용자설정 패키지이고, jdk/jre에 이미 포함되어 있는 패키지들이 빌트인 패키지이다. 
이 빌트인 패키지들은 jar 파일 형태로 존재한다. 예를들어 JRE lib 폴더에 위치한 rt.jar 파일을 열어보면 lang, io, util 등의 패키지를 발견할 수 있다.

주요 빌트인 패키지들
* java.awt : UI의 생성이나 그래픽, 이미지를 처리하기 위한 패키지. Button, Color, Event, Font, Graphics, Image 와 같은 클래스가 포함되어 있다.
* java.io : 시스템 인풋/아웃풋 기능을 위한 패키지. BufferedReader, BufferedWriter, File, InputStream, OutputStream, PrintStream, Serializable 과 같은 클래스가 포함되어 있다.
* <b>java.lang : 자바 프로그래밍 언어의 기반이 되는 클래스와 인터페이스들을 갖고있는 패키지. String, StringBuffer, System, Math, Integer 와 같은 클래스가 포함되어 있다. 아래에서 import 키워드를 알아볼 때 다시 확인하겠지만, java.lang은 패키지 경로를 명시하거나 import 없이 클래스명만으로 어디서든 사용이 가능하다.</b>
* java.net : 네트워크 애플리케이션을 제공하는 패키지. Authenticator, HttpCookie, Socket, URL, URLConnection, URLEncoder, URLDecoder 와 같은 클래스가 포함되어 있다.
* java.sql : 데이터베이스에 접근에 대한 기능을 담는 패키지. Connection, DriverManager, PreparedStatement, ResultSet, Statement 와 같은 클래스가 포함되어 있다.
* java.util : 프레임워크, 국가설정, 난수생성 등의 유틸리티를 가진 패키지. ArrayList, LinkedList, HashMap, Calendar, Date, TimeZone 과 같은 클래스가 포함되어 있다. 

#### :mag:네임스페이스
자바의 패키지와 같은 기능을 C++ 이나 C#에서는 네임스페이스라는 이름으로 활용한다.
프로그래밍의 더 넓은 관점으로 보자면 네임스페이스는 각각의 고유한 이름을 가진 요소들의 집합이다. 위에서 내린 패키지에 대한 정의와 비슷하게 들린다면 제대로 읽었다. 네임스페이스의 범주 안에는 다양한 종류가 있고 그중에 하나로 자바에서는 패키지가 있다고 할 수 있다. 네임스페이스의 예는 다음과 같다.

* 도메인명(Domain Names), 파일경로(File Paths), XML 문서(XML Documents).

이 외에도 소스코드에서 사용하는 다양한 네임스페이스의 예가 있을 수 있는데, 네임스페이스가 공통적으로 갖는 목적은 <b>"관계가 있는 요소들의 논리적인 집합의 분류"</b>이다.

### :star:package 키워드
클래스가 위치한 패키지를 기술하기 위해 package 키워드를 통해 선언한다. package 선언은 자바 파일의 페이지 최상단에 작성하며 다른 코멘트나 빈 공간을 두지 않아야 한다. package 키워드를 쓰고 그 뒤에 패키지 경로를 기술한뒤 세미콜론으로 닫는다.

>package org.apache.commons.net;

위와 같은 패키지가 선언되었다고 했을 때, 해당 파일에서 선언된 클래스들은 org.apache.commons.net 패키지에 포함되게 된다.

아무런 패키지가 선언되지 않았다면, 모든 클래스는 이름이 정해지지 않은 기본 패키지에 포함되게 된다. 이 경우에는 패키지 경로가 없기 때문에 클래스의 클래스명과 FQCN이 같다.
중복된 이름으로 충돌이 일어나는 것을 방지하기 위해서 기본 패키지는 사용하지 않아야 한다. 프로젝트가 더 복잡해질 수록 충돌을 피하기 힘들어진다. 때문에 프로젝트를 시작할 때 부터 패키지를 설정해 주는 것이 좋다.

### :star:import 키워드
자바 코드를 작성하며 클래스나 인터페이스를 불러올 때, 기본적으로 FQCN을 사용해야 한다. 패키지 경로를 포함한 클래스와 인터페이스 이름을 적어야 한다는 것인데 예를들어 파일을 조작하는 File 클래스를 사용하고 싶다면 java.io.File이라고 작성해야 한다.

이 규칙에는 세가지 예외가 있는데,

1. java.lang 패키지의 경우 자바 언어의 기반이며 매우 중요하다. 때문에 패키지 경로나 import 없이 타입 이름만으로 어디서든 사용이 가능하도록 되어있다.
2. 패키지.타입(p.T) 의 위치에서 해당 패키지(p)의 다른 타입(T)들을 FQCN이나 import 없이 별칭(simple name)으로만 지칭하는 것이 가능하다.
3. 해당 네이스페이스(namespace) 구역 안에서 import문으로 불러와진 타입의 경우 클래스명만으로도 사용할 수 있다.

1번과 2번 예외는 "자동 임포트(automatic imports)"라고 알려져 있다.

* 2번 예외가 잘 이해가 되지 않아 실험을 해보았다.

```java
package test;

public class Test1 {
  public static String test = "Testing";
}
```

```java
package test;

public class Test2 {
  String test2 = Test1.test;
}
```

```java
package testDifferentPackage;

import test.Test1;

public class Test3 {
  String test2 = Test1.test;
}
```

동일 경로의 패키지 안에서 다른 타입을 참조한 경우 import나 FQCN 없이 클래스명으로만 참조 되었다. 반면 testDifferentPackage 패키지에서 참조한 경우 import를 해줘야 했다.

java.lang의 타입들이나 현재 위치한 동일 경로 패키지의 타입들은 해당 네임스페이스에 임포트된(imported) 상태이므로 패키지 경로 없이 사용 가능하다. java.lang의 타입들과 동일 경로 패키지를 궂이 경로를 적어가며 FQCN으로 사용하자면 그럴수는 있겠으나 의미없는 일이다.

마찬가지로 현재 네임스페이스에서 다른 패키지의 타입을 명시적으로 임포트할 수 있다. 이는 임포트문을 통해서 가능하다. 임포트 문은 타입 선언부보다 앞에 있어야 하므로 자바 파일의 최상단에 위치한 패키지 선언에 뒤따라 위치해야 한다. 패키지 선언이 없다면 가장 위에 위치하면 된다. 임포트문은 얼마든지 많이 사용해도 괜찮다. 임포트의 선언은 해당 파일 안의 모든 타입의 작성에 적용된다.

#### :mag:import 선언
임포트 선언은 두가지 형태로 가능하다.

```java
import java.io.File;
```

1. 싱글 타입 임포트(single type import)
  * 임포트 선언이 되었으니 java.io.File의 FQCN 대신에 File 이라는 클래스명으로 사용할 수 있다. 이 방식은 싱글 타입 임포트(single type import)라고 불리우는 선언 방식이다.

```java
import java.io.*;
```

2. 온 디맨드 타입 임포트(on-demand type import)
  * 다른 한가지 임포트 방식은 온 디맨드 타입 임포트(on-demand type import) 이며, 패키지 경로 뒤에 ".\*" 을 붙여준다. 해당 패키지의 모든 타입은 이제 패키지 경로 없이 사용 가능하다. 그러므로, File 클래스 하나만이 아니라 io 패키지 안의 여러 클래스를 사용하고 싶다면 이렇게 패키지 전체를 임포트 하면 된다.
  * 다만 온 디맨드 타입 임포트는 해당 패키지에만 적용되며 서브패키지에는 적용되지 않는다. java.util 패키지를 임포트 한 경우, ZipInputStream 클래스를 사용하고 싶다면 FQCN으로 전체 경로(java.util.zip.ZipInputStream)를 임포트 해줘야 한다.
  * 온 디맨드 타입 임포트를 한다고 해서 해당 패키지 안의 모든 타입이 빠짐없이 임포트 되는 것은 아니다. 코드를 작성하며 실제로 사용하는 타입에 대해서만 임포트가 자동으로 이뤄진다. 그렇기 때문에 "on demand"라는 이름이 붙었다. 사용여부에 따라 임포트가 이뤄진다.

#### :mag:Java Static Import

자바 5버전에서 소개된 스태틱 임포트(Static Import)는 프로그래머가 클래스의 어느 정적 멤버에든 바로 접근할 수 있게 해준다. 클래스 이름을 통하지 않아도 사용이 가능해진다.

* 스태틱 임포트의 장점 : 클래스의 정적 멤버에 몇번이던 바로 접근이 가능하므로 코드의 양이 줄어든다.

* 스태틱 임포트의 단점 : 이 기능을 과하게 사용할 경우, 코드의 가독성이 떨어지며 유지보수가 어려워진다.

* 임포트와 스태틱 임포트의 차이점
  * 임포트
    * 프로그래머가 패키지의 경로를 사용하지 않고 해당 패키지의 클래스에 접근할 수 있게 해준다.
    * 클래스와 인터페이스에 대한 접근성이 제고된다.
  * 스태틱 임포트
    * 프로그래머가 클래스명을 사용하지 않고 해당 클래스의 정적 멤버들에 접근할 수 있게 해준다.
    * 클래스의 정적 멤버들에 대한 접근성이 제고된다.

### :star:클래스패스
클래스를 찾기위한 경로를 클래스패스라고 한다.
JVM이(누가) 프로그램을 실행할 때(언제), 클래스파일을 찾는 데(왜) 클래스 패스(무엇을)를 사용한다.
즉,JVM은 CLASSPATH의 경로를 확인하여 라이브러리 클래스들의위치를 참조하게 된다. 그러나 J2JDK 버전부터는 \jre\lib\ext 폴더에 필요한 클래스 라이브러리들을 복사해 놓으면 사용가능하여 특별한 경우가 아니면 설정을 하지 않는다.
소스 코드(.java로 끝나는 파일)를 컴파일하면 소스 코드가 “바이트 코드"로 변환된다. java runtime(java 또는 jre)으로 이 .class 파일에 포함된 명령을 실행하려면, 이 파일을 찾을 수 있어야 한다.
.class 파일을 찾을 때, classpath에 지정된 경로를 사용한다.

classpath는 .class 파일이 포함된 디렉토리와 파일을 콜론(;)으로 구분한 목록이다.

이 classpath 를 지정하기 위해서는 두 가지 방법이 있다.

* CLASSPATH 환경변수 사용
* java runtime 에 -classpath 옵션 사용

### :star:CLASSPATH 환경변수
CLASSPATH 환경변수는 클래스로더(Application ClassLoader)에 의해 .class 파일들의 경로를 파악하고 불러오기 위해 이용되는 환경변수이다. CLASSPATH 환경변수는 자바 플랫폼의 일부가 아닌 모든 클래스들(third-party and user-defined classes)의 경로를 갖는다.

>CLASSPATH=.;C:\Program Files\Java\jdk-10.0.1\lib\tools.jar

컴퓨터 시스템 변수 설정을 통해 지정할 수 있다.
JVM이 시작될 때 JVM의 클래스 로더는 이 환경 변수를 호출한다. 그래서 환경 변수에 설정되어 있는 디렉토리가 호출되면 그 디렉토리에 있는 클래스들을 먼저 JVM에 로드한다. 그러므로 CLASSPATH 환경 변수에는 필스 클래스들이 위치한 디렉토리를 등록하도록 한다.

### :star:-classpath 옵션
```bash
javac <options> <souce files>
```

컴파일러가 컴파일 하기 위해서 필요로 하는 참조할 클래스 파일들을 찾기 위해서 컴파일시 파일 경로를 지정해주는
옵션

Hello.java파일이 C:\Java 디렉터리에 존재하고,

필요한 클래스 파일들이 C:\Java\EngClasses에 위치한다면,

```bash
javac -classpath C:\Java\EngClasses C:\Java\Hello.java
```

위와 같이 해주면 된다.

만약 참조할 클래스 파일들이 그 외의 다른 디렉터리, 그리고 현 디렉토리에도 존재한다면,

```bash
javac -classpath .;C:\Java\EngClasses;C:\Java\KorClasses C:\Java\Hello.java
```

위와 같이 ";" 으로 구분해줄 수 있다. ( . 은 현 디렉토리, .. 은 현 디렉토리에서 상위 디렉토리를 의미한다.)

또한 classpath 대신 단축어인 cp를 사용해도 된다.

```bash
javac -cp .;C:\Java\EngClasses;C:\Java\KorClasses C:\Java\Hello.java
```

### :star:지시자
자바에는 두가지 종류의 지시자(modifiers)가 있다. 접근지시자(access modifiers) 그리고 비접근지시자(non-access modifiers)이다.

#### :mag:접근지시자
자바의 접근지시자는 필드, 메서드, 생성자, 클래스 등의 접근성(accessibility)이나 범위(scope)를 지정한다.

* Private: 접근 권한이 해당 클래스 내부로 제한된다. 클래스 외부에서는 접근할 수 없다.
* Default: 접근 권한이 해당 패키지 내부로 제한된다. 패키지 외부에서는 접근할 수 없다. 접근지시자를 지정하지 않는 경우 사용되는 기본값이다.
* Protected: Default와 같이 접근 권한이 해당 패키지 내부로 제한되지만 패키지 바깥에 있는 자식 클래스에게도 접근이 허용된다. 패키지 외부에서는 자식 클래스를 만들지 않고는 접근할 수 없다.
* Public: 어디서든 접근이 가능하다. 클래스 내부, 클래스 외부, 패키지 내부, 패키지 외부 관계없이 접근할 수 있다.

#### :mag:접근지시자 비교
![access_modifiers](https://raw.githubusercontent.com/372dev/TIL/main/JAVA/img/05_Class_01_modifier.jpg)

#### :mag:비접근지시자
다양한 비접근지시자(non-access modifiers)들이 존재하는데, 예를 들어 static, abstract, synchronized, native, volatile, transient 등이 있다.

이들 비접근지시자들은 다양한 것들을 컨트롤 하는데, 예를들어 상속가능 여부(inheritance capabilities), 클래스 내에서 멤버 변수의 공유 여부(whether all objects of our class share the same member value or have their own values of those members), 자식 클래스에서 메서드가 오버라이드 될 수 있는지 여부(whether a method can be overridden in a subclass) 등이 있다.

* <b>static</b> - 해당 멤버가 클래스의 객체에 속하는게 아니라 클래스에 속하도록 설정한다.
* <b>final</b> - 상수로 선언하도록 설정한다. 변수의 값이 한번 정해지면 변할 수 없고, 메서드는 오버라이드 될 수 없으며, 클래스는 상속이 불가능해진다.
* <b>abstract</b>
  * 메서드에 적용될 경우 - 추상화 되며, 자식 클래스에서 구현되어야만 한다.
  * 클래스에 적용될 경우 - 추상 메서드를 갖는다.
* <b>synchronized</b> - 코드블럭이나 메서드에 대한 스레드 접근을 결정한다.
* <b>volatile</b> - 변수값이 특정 스레드의 메모리 대신 항상 메인 메모리에서 읽히도록 한다.
* <b>transient</b> - 객체를 직렬화(serializing) 할 때 해당 멤버를 건너 뛴다.
* <b>native</b> - 자바가 아닌 다른 프로그래밍 언어로 구현될 메서드를 표시한다. JNI(Java Native Interface)와 함께 작동한다.

-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://techterms.com/definition/namespace  
https://www.javatpoint.com/package  
https://www.refreshjava.com/java/built-in-packages-in-java  
https://www.javatpoint.com/static-import-in-java  
https://www.javatpoint.com/how-to-set-classpath-in-java  
https://kils-log-of-develop.tistory.com/430  
https://www.javatpoint.com/access-modifiers  
https://stackabuse.com/non-access-modifiers-in-java/