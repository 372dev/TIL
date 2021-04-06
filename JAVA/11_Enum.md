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

* C++와 같은 다른 언어에서는 enum의 역할을 constant integer와 같은 방식으로 제공한다. 하지만 자바의 enum은 더욱 탁월한 type safety(타입 안전성)과 유동성을 제공한다.

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

* 아래는 [Baeldung.com](https://www.baeldung.com)의 enum에 대한 글의 번역이다.
  * 원문(Original Text) : [Baeldung - Attaching Values to Java Enum](https://www.baeldung.com/java-enum-values)  
  * 저자(written by) : baeldung
  * version : March 12, 2021

#### :mag:1. 개요
enum 타입을 통해 자바 언어는 상수 값을 생성하고 사용하는 방법을 제공한다. 한정된 숫자의 변수를 정의함으로서 enum은 String이나 int 같은 constant literal variables(리터럴 상수)보다 더욱 안정적인 타입이다.

유의할 점은, enum의 변수는 유효한 구분자로 이름지어져야 하며, 관습에 따라 SCREAMING_SNAKE_CASE(대문자 스네이크 케이스)를 사용할 것이 권장된다.

그러한 제약 사항들을 고려하면, enum 변수만 가지고는 가독성 있는 문자열이나 문자열 외의 값을 저장하기에 부족함이 있다.

#### :mag:2. Enum을 클래스로 사용하기
enum은 종종 변수의 리스트를 간단히 저장하기 위해 사용된다. 예를 들어 아래와 같이 주기율표의 일부분을 enum 클래스로 저장할 수 있다.

```java
public enum Element {
    H, HE, LI, BE, B, C, N, O, F, NE
}
```

위와 같은 문법을 사용하여, Element라는 이름을 가진 열개의 static, final 성격을 지닌 enum 인스턴스를 생성했다. 효율적으로 작성된 코드이지만, 여기에서 우리가 알 수 있는 정보는 원소의 알파벳이 무엇인가에 국한되며, 심지어 자바 상수가 대문자로 표현되기 때문에 원소 알파벳의 표기 방식에서도 벗어난다.

게다가 원래 주기율표에서 알 수 있는 원소의 다른 성질에 대한 정보도 부족하다. 원소의 이름이나 원자 번호 등의 정보가 빠져있다.

*enum은 자바의 특수한 타입이기는 하지만, 일반 클래스에서와 마찬가지로 생성자나 필드값, 메서드 등을 추가할 수 있다. 그렇기 때문에 필요한 정보를 더욱 상세하게 enum에 담아 활용하는 것이 가능하다.*

#### :mag:3. 생성자와 Final 필드 추가하기
먼저 원소의 이름을 추가하는 작업을 해보자.

*생성자를 이용하여 final 변수를 부여하는 방식으로 원소 이름을 추가할 것이다.*

```java
public enum Element {
    H("Hydrogen"),
    HE("Helium"),
    // ...
    NE("Neon");

    public final String label;

    private Element(String label) {
        this.label = label;
    }
}
```

가장 먼저 눈에 띄는 점은 상수 선언 리스트에서 사용되는 특수한 syntax(구문)이다. enum 타입에서는 이런식으로 생성자가 실행된다. *enum에서 new 연산자를 사용하는 것은 허용되지 않지만, 상수 선언 리스트에서 인자를 전달하는 것이 가능하다.*

뒤이어 인스턴스 변수 label을 선언했다. 이에 대해 몇가지 알아둘 점들이 있다.

1. *예제에서는 name 대신에 label 이라고 구분자를 이름지었다. 멤버 필드에서 name이라는 구분자가 사용 가능하지만 label과 같은 다른 이름을 선택하여 Enum.name() 메서드와의 혼동을 방지하자.*

2. *label 필드는 final으로 선언됐다. enum의 필드 값이 필수적으로 final이어야 하진 않지만, 일반적으로 enum을 사용할 때 label의 값이 변하길 원하진 않을 것이다.* enum의 변수들이 상수라는 점을 고려하면 충분히 설득력이 있는 방식이다.

3. label 필드는 public으로 선언됐다, 그러므로 아래와 같이 label로 바로 접근이 가능하다.

```java
System.out.println(HE.label);
```

물론 field를 private으로 선언하는 것도 가능하다, 그런 경우 필드에 getLabel() 메서드를 통해 접근할 수 있다. 예제를 간결하게 보여주기 위해서 이 글에서는 계속하여 public 필드 스타일을 사용해보자.

#### :mag:4. Enum 값 불러오기
Java provides a valueOf(String) method for all enum types.

Thus, we can always get an enum value based on the declared name:

```java
assertSame(Element.LI, Element.valueOf("LI"));
```

However, we may want to look up an enum value by our label field as well.
To do that, we can add a static method:

```java
public static Element valueOfLabel(String label) {
    for (Element e : values()) {
        if (e.label.equals(label)) {
            return e;
        }
    }
    return null;
}
```

The static valueOfLabel() method iterates the Element values until it finds a match. It returns null if no match is found. Conversely, an exception could be thrown instead of returning null.

Let's see a quick example using our valueOfLabel() method:

```java
assertSame(Element.LI, Element.valueOfLabel("Lithium"));
```

#### :mag:5. 캐시 이용하기
#### :mag:6. 다양한 값을 부여하기
#### :mag:7. 인터페이스를 다루기
#### :mag:8. 결론

#### :mag:custom enum methods
https://www.baeldung.com/a-guide-to-java-enums

### :star:java.lang.Enum
https://www.geeksforgeeks.org/java-lang-enum-class-java/
### :star:EnumSet
https://www.baeldung.com/java-enumset

-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://www.baeldung.com/java-enum-values  