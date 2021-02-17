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

1. java.lang의 타입들은 자바 언어의 기반이며 매우 중요하기 때문에 패키지 경로 없이 클래스명만으로 어디서든 사용이 가능하다.
2. p.T(패키지.타입) 의 형태로 작성하면 해당 패키지(p)의 다른 타입(T)들을 지칭할 수 있다.
3. 해당 네이스페이스(namespace) 구역 안에서 import문으로 불러와진 타입의 경우 클래스명만으로도 사용할 수 있다.

1번과 2번 예외는 "자동 임포트(automatic imports)"라고 알려져 있다.
java.lang의 타입들과 현재 위치한 패키지는 해당 네임스페이스에 임포트된(imported) 상태이므로 패키지 경로 없이 사용 가능하다. java.lang의 타입들과 현재 경로 패키지를 궂이 경로를 적어가며 FQCN으로 사용하자면 그럴수는 있겠으나 의미없는 일이다.

마찬가지로 현재 네임스페이스에서 다른 패키지의 타입을 명시적으로 임포트할 수 있다. 이는 임포트문을 통해서 가능하다. 임포트 문은 타입 선언부보다 앞에 있어야 하므로 자바 파일의 최상단에 위치한 패키지 선언에 뒤따라 위치해야 한다. 패키지 선언이 없다면 가장 위에 위치하면 된다. 임포트문은 얼마든지 많이 사용해도 괜찮다. 임포트의 선언은 해당 파일 안의 모든 타입의 작성에 적용된다.

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
CLASSPATH is an environment variable which is used by Application ClassLoader to locate and load the .class files. The CLASSPATH defines the path, to find third-party and user-defined classes that are not extensions or part of Java platform. Include all the directories which contain .class files and JAR files when setting the CLASSPATH.


### :star:CLASSPATH 환경변수

### :star:-classpath 옵션

### :star:접근지시자
There are two types of modifiers in Java: access modifiers and non-access modifiers.

The access modifiers in Java specifies the accessibility or scope of a field, method, constructor, or class. We can change the access level of fields, constructors, methods, and class by applying the access modifier on it.

There are four types of Java access modifiers:

Private: The access level of a private modifier is only within the class. It cannot be accessed from outside the class.
Default: The access level of a default modifier is only within the package. It cannot be accessed from outside the package. If you do not specify any access level, it will be the default.
Protected: The access level of a protected modifier is within the package and outside the package through child class. If you do not make the child class, it cannot be accessed from outside the package.
Public: The access level of a public modifier is everywhere. It can be accessed from within the class, outside the class, within the package and outside the package.
There are many non-access modifiers, such as static, abstract, synchronized, native, volatile, transient, etc. Here, we are going to learn the access modifiers only.

#### :mag:접근지시자 비교
![access_modifiers](https://raw.githubusercontent.com/372dev/TIL/main/JAVA/img/05_Class_01_modifier.jpg)

-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://techterms.com/definition/namespace  
https://www.javatpoint.com/static-import-in-java  
https://www.javatpoint.com/how-to-set-classpath-in-java  
https://www.javatpoint.com/access-modifiers  