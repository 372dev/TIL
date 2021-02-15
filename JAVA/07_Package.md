# Java_07_Package

## :muscle:패키지
패키지는 클래스들, 인터페이스들과 참조 변수들의 모음에 이름을 붙여놓은 것이다. 연관되어 있는 클래스들을 그룹지어주고 분류된 그룹별 명칭을 붙여주는 역할을 한다.
자바의 핵심 클래스들은 java 라는 이름의 패키지 안에 들어 있다. 예를 들어, 자바 언어의 기반역할을 하는 클래스들은 java.lang. 패키지 안에 있다. 다양한 유틸리티 클래스들은 java.util. 패키지 안에 있다.
The core classes of the Java platform are in packages whose names begin with java.
For example, the most fundamental classes of the language are in the package
java.lang. Various utility classes are in java.util. Classes for input and output are
in java.io, and classes for networking are in java.net. Some of these packages
contain subpackages, such as java.lang.reflect and java.util.regex. Exten‐
sions to the Java platform that have been standardized by Oracle (or originally Sun)
typically have package names that begin with javax. Some of these extensions, such
as javax.swing and its myriad subpackages, were later adopted into the core plat‐
form itself. Finally, the Java platform also includes several “endorsed standards,”
which have packages named after the standards body that created them, such as
org.w3c and org.omg.
Every class has both a simple name, which is the name given to it in its definition,
and a fully qualified name, which includes the name of the package of which it is a
part. The String class, for example, is part of the java.lang package, so its fully
qualified name is java.lang.String.


### :star:package 키워드
To specify the package a class is to be part of, you use a package declaration. The
package keyword, if it appears, must be the first token of Java code (i.e., the first
thing other than comments and space) in the Java file. The keyword should be
followed by the name of the desired package and a semicolon. Consider a Java file
that begins with this directive:
package org.apache.commons.net;
All classes defined by this file are part of the package org.apache.commons.net.
If no package directive appears in a Java file, all classes defined in that file are part of
an unnamed default package. In this case, the qualified and unqualified names of a
class are the same.
The possibility of naming conflicts means that you should not
use the default package. As your project grows more compli‐
cated, conflicts become almost inevitable—much better to cre‐
ate packages right from the start.


### :star:import 키워드
When referring to a class or interface in your Java code, you must, by default, use
the fully qualified name of the type, including the package name. If you’re writing
code to manipulate a file and need to use the File class of the java.io package, you
must type java.io.File.

This rule has three exceptions:

* Types from the package java.lang are so important and so commonly used
that they can always be referred to by their simple names.
* The code in a type p.T may refer to other types defined in the package p by
their simple names.
* Types that have been imported into the namespace with an import declaration
may be referred to by their simple names.

The first two exceptions are known as “automatic imports.” The types from
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
