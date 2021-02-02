## :muscle:인터페이스의 메소드
앞서 우리는 인터페이스의 정의와 구현, 상속에 대해서 알아 보았다. 이어서 인터페이스에서 사용되는 메소드들에 대해서 알아보자.

#### :mag:인터페이스의 기본 메소드 (Default Method), 자바 8
자바 8버전부터는 인터페이스에서 코드를 포함한 메소드를 구현하는것이 가능해졌다. 먼저 기본 메소드를 알아보자.
메소드 선언시에 default를 명시하게 되면 인터페이스 내부에서도 코드가 포함된 메소드를 선언할 수 있다. default 키워드는 접근제어자에서는 아무것도 명시되지 않았을 경우이지만 인터페이스 메소드의 경우엔 default를 명시할 경우에 메소드 안에 코드를 작성할 수 있다.
상속받은 클래스는 인터페이스의 기본 메소드를 상속받아서 사용할 수 있으나 선택적으로 구현하지 않을수도 있다.

사실 인터페이스는 기능에 대한 구현보다는, 기능에 대한 '선언'에 초점을 맞추어서 사용 하는데, 디폴트 메소드는 왜 등장했을까?
이는 하위호완성 때문이다. 기존에 존재하던 인터페이스를 이용하여서 구현된 클래스를 만들고 사용하고 있는데, 
인터페이스를 보완하는 과정에서 추가적으로 구현해야 할, 혹은 필수적으로 존재해야 할 메소드가 있다면, 
이미 이 인터페이스를 구현한 클래스와의 호환성이 떨어지게 된다. 이러한 경우 default 메소드를 추가하게 된다면

하위 호환성은 유지되고 인터페이스의 보완을 진행 할 수 있다.


#### :mag:인터페이스의 static 메소드, 자바 8
자바 8버전부터는 또한 인터페이스에서 static 메소드를 사용하는 것이 가능해졌다. 이전 버전의 자바에서는 불가능한 일이었는데, static 메소드가 사용 불가능한 것은 자바 언어의 결함이라는 견해가 지배적이었다.

인스턴스 생성과 상관없이 인터페이스 타입으로 호출하는 메소드이다.
static 예약어를 사용하고, 접근제어자는 항상 public이며 생략 할 수 있다.
static method는 일반적으로 우리가 정의하는 메소드와는 다르다.

#### :mag:인터페이스의 private 메소드, 자바 9
자바 9버전부터는, 인터페이스에 private 메소드 또한 사용이 가능해 졌다. 제한적인 용도로만 사용될 뿐이지만 바뀌어버린 인터페이스 구조로 인해 없애기도 어려운 기능이 되어버렸다. 

자바 8버전에서 도입된 default 메서드와 static 메서드가 자바 9버전부터는 private 메서드와 private static 메서드로 사용이 가능해졌다.

-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://dev-coco.tistory.com/13  
https://k3068.tistory.com/34  
https://www.notion.so/8-0cc8c251d5374ac882a4f22fa07c4e6a  