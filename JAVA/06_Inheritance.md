# Java_06_Inheritance

## :muscle:상속
상속은 객체지향 프로그래밍의 가장 중요한 요소중 하나이며, 객체나 클래스를 다른 객체나 클래스에 기반하여 만드는 과정이다.

### :star:자바 상속의 특징
상속은 하나의 객체가 상위 객체의 요소와 특성을 모두 갖게되는 것이다. 자바에서 상속은 이미 존재하는 클래스를 이용하여 새로운 클래스를 만들기 위함인데, 이미 존재하는 클래스를 상속하게 되면 해당 클래스의 메서드와 필드를 가져와서 사용할 수 있다. 나아가 상속을 받은 클래스에 추가적으로 다른 메소드와 필드를 작성할 수 있다.
상속은 IS-A 관계이며 이는 부모-자식 관계로도 불리운다.

상속을 이용하는 근본적 이유
* 메서드 오버라이딩 (런타임 다형성을 위해서).
* 코드의 재사용을 위해서.

상속 용어
* 클래스(Class): 클래스는 공통적인 속성을 지닌 객체들의 집합이다. 객체의 생성을 위한 틀이라고 할수도 설계도면이라고 할수도 있다.
* 하위클래스/자식클래스(Sub Class/Child Class) : 하위클래스는 다른 클래스로부터 상속을 받는다. 파생(derived)클래스, 확장(extended)클래스, 또는 자식클래스 라고도 한다.
* 상위클래스/부모클래스(Super Class/Parent Class) : 하위클래스는 상위클래스로부터 요소들을 상속받는다. (base)클래스, 또는 부모클래스 라고도 한다.
* 재사용성(Reusability) : As the name specifies, reusability is a mechanism which facilitates you to reuse the fields and methods of the existing class when you create a new class. You can use the same fields and methods already defined in the previous class.
#### :mag:클래스의 상속
자바는 C++와 다르게 다중상속을 지원하지 않는다.

#### :mag:인터페이스의 상속
인터페이스는 다른 인터페이스를 상속받을 수 있다. 08_Interface에서 자세히 알아보자.

#### :mag:인터페이스를 상속한 인터페이스를 구현한 클래스
하나 혹은 다수의 인터페이스를 상속받은 인터페이스를 클래스가 구현하게 되면, 클래스는 구현하는 인터페이스의 메소드와 상수를 모두 구현해야 하고, 또한 구현하는 인터페이스의 상위 인터페이스들의 모든 추상메소드와 상수들도 구현해야 한다.
이에 대해서는 08_Interface에서 자세히 알아보자.

### :star:super 키워드

### :star:메소드 오버라이딩

### :star:다이나믹 메소드 디스패치 (Dynamic Method Dispatch)

### :star:추상 클래스

#### :mag:인터페이스와 추상클래스
인터페이스는 추상클래스와 비슷하나 추상클래스 보다 추상화 정도가 더 높다. 08_Interface에서 자세히 알아보자.

### :star:Object 클래스

-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://www.javatpoint.com/inheritance-in-java  