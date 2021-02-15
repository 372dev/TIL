# Java_07_Package

## :muscle:패키지
패키지는 클래스들, 인터페이스들과 참조 변수들의 모음에 이름을 붙여놓은 것이다. 연관되어 있는 클래스들을 그룹지어주고 분류된 그룹별 명칭을 붙여주는 역할을 한다.
자바의 핵심 클래스들은 다음과 같이 java 라는 이름의 패키지 안에 들어 있다.

* 자바 언어의 기반역할을 하는 클래스들은 java.lang. 패키지 안에 있다.
* 다양한 유틸리티 클래스들은 java.util. 패키지 안에 있다.
* 입출력을 위한 클래스들은 java.io 패키지에 있다
* 네트워킹을 위한 클래스들은 java.net. 패키지 안에 있다.

이들 패키지들은 서브패키지를 갖고 있기도 한다. 예를 들자면 java.lang 안에는 java.lang.reflect 이 있고 java.util 안에는 java.util.regex 가 있다.

Oracle(과거에는 Sun)에 의해서 규정된 추가기능(extension)들의 패키지는 javax로 시작한다. 이들 추가기능의 일부는 시간이 지나며 자바 기본 기능으로 편입되기도 했다.

마지막으로, "보증된 표준"이 몇가지 있다. 이들 패키지들은 해당 보증을 작성한 기관을 따라 이름지어졌다. 예를들어 org.w3c 이나 org.omg가 있다.

모든 클래스는 정식명칭과 별칭을 갖고 있다. 정식 명칭은 FQN(fully qualified name) 이라고도 하며 패키지 경로를 모두 포함한 이름이고, 별칭(Alias)은 클래스가 작성될때 지어진 이름이다.
예를 들어 String 클래스의 경우 "String"은 별칭이고, 위치는 java.lang 패키지 안에 있으므로 정식 명칭은 java.lang.String 이다.

### :star:package 키워드
클래스가 위치한 패키지를 기술하기 위해 package 키워드를 통해 선언한다. package 선언은 자바 파일의 페이지 최 상단에 작성하며 다른 코멘트나 빈 공간을 두지 않아야 한다. package 키워드를 쓰고 그 뒤에 패키지 경로를 기술한뒤 세미콜론으로 닫는다.

>package org.apache.commons.net;

위와 같은 패키지가 선언되었다고 했을 때, 해당 파일에서 선언된 클래스들은 org.apache.commons.net 패키지에 포함되게 된다.

아무런 패키지가 선언되지 않았다면, 모든 클래스는 이름이 정해지지 않은 기본 패키지에 포함되게 된다. 이 경우에는 패키지 경로가 없기 때문에 클래스의 별칭과 정식 명칭이 같다.
중복된 이름으로 충돌이 일어나는 것을 방지하기 위해서 기본 패키지는 사용하지 않아야 한다. 프로젝트가 더 복잡해질 수록 충돌을 피하기 힘들어진다. 때문에 프로젝트를 시작할 때 부터 패키지를 설정해 주는 것이 좋다.

### :star:import 키워드
자바 코드를 작성하며 클래스나 인터페이스를 불러올 때, 기본적으로 정식 명칭을 사용해야 한다. 패키지 경로를 포함한 클래스와 인터페이스 이름을 적어야 한다는 것인데 예를들어 파일을 조작하는 File 클래스를 사용하고 싶다면 java.io.File이라고 작성해야 한다.

이 규칙에는 세가지 예외가 있는데,

1. java.lang의 타입들은 자바 언어의 기반이며 매우 중요하기 때문에 패키지명 없이 별칭만으로 어디서든 사용이 가능하다.
2. p.T(패키지.타입) 의 형태로 작성하면 해당 패키지 밖의 다른 패키지(p)의 타입(T)을 지칭할 수 있다.
3. 해당 구역 안에서 import문으로 불러와진 타입의 경우 별칭만으로도 사용할 수 있다.

1번과 2번 예외는 "자동 임포트(automatic imports)"라고 알려져 있다.

The types from
java.lang and the current package are “imported” into the namespace so that they
can be used without their package name. Typing the package name of commonly
used types that are not in java.lang or the current package quickly becomes tedi‐
ous, and so it is also possible to explicitly import types from other packages into the
namespace. This is done with the import declaration.
import declarations must appear at the start of a Java file, immediately after the
package declaration, if there is one, and before any type definitions. You may use
any number of import declarations in a file. An import declaration applies to all
type definitions in the file (but not to any import declarations that follow it).
The import declaration has two forms. To import a single type into the namespace,
follow the import keyword with the name of the type and a semicolon:

```java
import java.io.File;
```

// Now we can type File instead of java.io.File
This is known as the “single type import" declaration.
The other form of import declaration is the “on-demand type import.” In this form,
you specify the name of a package followed by the characters .* to indicate that any
type from that package may be used without its package name. Thus, if you want to
use several other classes from the java.io package in addition to the File class, you
can simply import the entire package:

```java
import java.io.*;
```

// Use simple names for all classes in java.io
This on-demand import syntax does not apply to subpackages. If I import the
java.util package, I must still refer to the java.util.zip.ZipInputStream class
by its fully qualified name.
Using an on-demand type import declaration is not the same as explicitly writing
out a single type import declaration for every type in the package. It is more like an
explicit single type import for every type in the package that you actually use in your
code. This is the reason it’s called "on demand"; types are imported as you use them.

#### :mag:Java Static Import

The static import feature of Java 5 facilitate the java programmer to access any static member of a class directly. There is no need to qualify it by the class name.

Advantage of static import:
Less coding is required if you have access any static member of a class oftenly.

Disadvantage of static import:
If you overuse the static import feature, it makes the program unreadable and unmaintainable.

What is the difference between import and static import?
The import allows the java programmer to access classes of a package without package qualification whereas the static import feature allows to access the static members of a class without the class qualification. The import provides accessibility to classes and interface whereas static import provides accessibility to static members of the class.

### :star:클래스패스

### :star:CLASSPATH 환경변수

### :star:-classpath 옵션

### :star:접근지시자

#### :mag:접근지시자 비교
![access_modifiers](https://raw.githubusercontent.com/372dev/TIL/main/JAVA/img/05_Class_01_modifier.jpg)

-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
