## :muscle:인터페이스의 메소드
앞서 우리는 인터페이스의 정의와 구현, 상속에 대해서 알아 보았다. 이어서 인터페이스에서 사용되는 메소드들에 대해서 알아보자.

#### :mag:인터페이스의 기본 메소드 (Default Method), 자바 8

#### :mag:인터페이스의 static 메소드, 자바 8
As of Java 8, an interface may contain static methods. Previous versions of Java
did not allow this, and this is widely believed to have been a flaw in the design
of the Java language

#### :mag:인터페이스의 private 메소드, 자바 9
As of Java 9, an interface may contain private methods. These have limited use
cases, but with the other changes to the interface construct, it seems arbitary to
disallow them. It is a compile-time error to try to define a protected method
in an interface.
