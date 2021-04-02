# Java_11_Enum

## :muscle:Enum
자바의 타입 시스템에 특수한 기능을 수행하기 위한 특별한 형태의 타입이 Java 5버전에서 소개되었고 이를 enumerated types(열거 타입)이라고 한다. 또한 줄여서 enum이라고도 불리운다.
enum은 클래스의 변형인데 제한적인 기능을 가지며 해당 타입에서 허용된 몇가지의 변수만 가질 수 있다.

### :star:enum 정의하는 방법
빨간색, 녹색, 파란색의 삼원색을 정의하려고 할 때, 이 세가지 변수만 사용 가능한 타입을 만들어 보자. enum 키워드를 사용하여 아래와 같이 타입을 생성할 수 있다.

```java
public enum PrimaryColor {
	// 세미콜론(;)은 인스턴스 목록의 끝에 붙여줄 필요 없다.
	RED, GREEN, BLUE
}
```

PrimaryColor 타입의 인스턴스들은 이제 static 필드의 값처럼 참조될 수 있다.  
>PrimaryColor.RED  
>PrimaryColor.GREEN  
>PrimaryColor.BLUE  

* C++와 같은 다른 언어에서는 enum의 역할을 constant integer로 제공한다. 하지만 자바의 enum이 더 좋은 type safety와 유동성을 제공한다.

* enum의 특성
  * 모든 enum은 java.lang.Enum을 상속한다
  * generic(제네릭)으로 사용될 수 없다.
  * 인터페이스를 구현할 수 있다.
  * 상속될 수 없다.
  * 모든 enum 값이 implementation body를 제공하는 경우 추상 메서드만 가질 수 있다.
  * new 키워드를 통해 직접 인스턴스화 될 수는 없다.

enum은 특성화된 클래스이다. 멤버 클래스와 메서드를 가질 수 있다. 인스턴스들만 있는 경우 세미콜론을 사용하지 않지만, 필드와 바디의 내용이 있다면 인스턴스들의 마지막에 세미콜론을 사용해줘야 한다. 이 경우에도 enum 상수들은 클래스의 최상단에 위치한다.

예를 들어 몇가지 정다각형을 다루는 enum을 만드려 하고, 메서드를 갖도록 하고 싶을 때. 아래와 같이 파라미터 값을 갖는 enum을 사용할 수 있다.

```java
public enum RegularPolygon {
	// enum이 파라미터 값을 갖는 경우 세미콜론을 끝에 꼭 붙여야 한다.
	TRIANGLE(3), SQUARE(4), PENTAGON(5), HEXAGON(6);
	private Shape shape;

	public Shape getShape() {
		return shape;
	}

	private RegularPolygon(int sides) {
		switch (sides) {
			// 각 면의 길이와 모서리의 각도를 받아서 도형을
			// 만들어주는 생성자가 있다는 가정하에 작성되었다.
			case 3:
			shape = new Triangle(1,1,1,60,60,60);
			break;
			case 4:
			shape = new square(1,1,1,1,90,90,90,90);
			break;
			case 5:
			shape = new Pentagon(1,1,1,1,1,108,108,108,108,108);
			break;
			case 6:
			shape = new Hexagon(1,1,1,1,1,1,120,120,120,120,120,120);
			break;
		}
	}
}
```

이렇게 파라미터 값들이(위의 예제에서는 파라미터 하나가) 생성자로 전달되어 enum 인스턴스가 생성된다.
enum 인스턴스들이 자바 런타임에서 생성되고, 외부에서 인스턴스화 될 수 없으므로 생성자들은 private으로 선언된다.

### :star:enum 메서드 - values() & valueOf()
-Original Text [Baeldung - Attaching Values to Java Enum](https://www.baeldung.com/java-enum-values)  
#### :mag:1. 개요
The Java enum type provides a language-supported way to create and use constant values. By defining a finite set of values, the enum is more type safe than constant literal variables like String or int.

However, enum values are required to be valid identifiers, and we're encouraged to use SCREAMING_SNAKE_CASE by convention.

Given those limitations, the enum value alone is not suitable for human-readable strings or non-string values.
#### :mag:2. Enum을 클래스로 사용하기
#### :mag:3. 생성자와 Final 필드 추가하기
#### :mag:4. 개요
#### :mag:5. 개요
#### :mag:


#### :mag:custom enum methods
https://www.baeldung.com/a-guide-to-java-enums

### :star:java.lang.Enum
https://www.geeksforgeeks.org/java-lang-enum-class-java/
### :star:EnumSet
https://www.baeldung.com/java-enumset

-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://www.baeldung.com/java-enum-values  