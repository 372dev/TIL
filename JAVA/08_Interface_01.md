## :muscle:인터페이스
앞서 우리는 상속에 대해서 알아 보았는데, 자바의 클래스는 한개의 클래스에서만 상속을 받을 수 있다는 것을 알 수 있었다. 상속에 대한 제한이 있다는 것은 객체지향 프로그래밍을 하는데 큰 제약이 될 수 있다. 자바를 만든 개발자들도 이를 알았겠으나, 자바를 이용한 객체지향 프로그래밍이 당시 C++가 그랬듯이 너무 복잡해 지거나 에러가 빈번하게 되길 바라지 않았다. 그 해결책으로 도입된 것이 인터페이스이다. 인터페이스도 클래스 처럼 새로운 레퍼런스 타입을 정의한다.  

#### :mag:인터페이스와 추상클래스
인터페이스는 추상클래스와 비슷하나 추상클래스 보다 추상화 정도가 더 높다. 추상클래스와 달리 모든 변수는 상수형으로 선언되어야 하고 메서드 또한 모두 추상메서드로 선언되어야 한다. 

###### 추상클래스와 인터페이스를 이용하여 객체들을 그룹으로 분류해서 얻는 이점

1. 객체 간의 차이점은 무시하고 객체들 간의 공통점을 파악하기 쉽다
2. 객체의 불필요한 세부사항을 제거함으로써 중요한 부분을 강조할 수 있다

###### 추상클래스와 인터페이스의 공통점, 차이점
* 공통점
   * 자기 자신을 객체화할 수 없으며 다른 객체가 상속(extends), 구현(implements)을 하여 객체를 생성할 수 있다.
   * 상속, 구현을 한 하위 클래스에서는 상위에서 정의한 추상 메서드(abstract method)를 반드시 구현하여야 한다.
* 차이점
   * 추상클래스는 일반 메소드를 포함할 수 있으나 인터페이스의 모든 메서드는 추상메서드이다. (다만, 후술한 대로 자바8 버전 이후부터 default, static, private 메소드가 도입되었다.)
   * 추상클래스는 다중상속이 불가능하나 인터페이스는 다중상속이 가능하다.
   * 추상클래스는 상수, 변수 필드 포함이 가능하나 인터페이스는 상수 필드만 포함할 수 있다.

#### :mag:인터페이스 정의하는 방법
인터페이스의 정의는 클래스를 정의하는 것과 아주 비슷한데, 클래스와 비교해보자면 디폴트 메소드를 제외한 모든 메소드는 추상메소드이어야 하고 class라는 키워드만 interface로 하면 인터페이스가 된다고 보면 된다. 예를 들어 아래의 코드는 Centered 라는 이름의 인터페이스를 정의한다.  

```java  
interface Centered {  
 void setCenter(double x, double y);  
 double getCenterX();  
 double getCenterY();  
}  
```  

인터페이스의 요소들에는 다음과 같이 몇가지 제약이 따른다.  

* 인터페이스는 public API를 정의한다. 인터페이스의 요소들은 암묵적으로 public이며 때문에 제어자(modifier)는 통상적으로 생략된다.  
* 인터페이스의 필수 메소드들은 암묵적으로 추상메소드이고 메소드 바디에 세미콜론을 포함해야 한다. abstract 제어자를 사용할 수 있으나, 주로 생략된다.  
* 인터페이스는 인스턴스 필드를 구현하지 않고 선언만 한다. 인터페이스 내의 모든 변수는 static final으로 선언된다.

* 위 세가지 이유로 인해 인터페이스 내의 모든 메소드는 public abstract 이며 모든 변수는 public static final이다.


#### :mag:인터페이스 구현하는 방법
클래스에서는 extends를 이용해서 부모클래스(superclass)를 지정한다. 하나 또는 여러개의 인터페이스를 구현할 때는 implements 키워드를 이용한다. implements 키워드는 클래스 선언부에서 쓰여지며 extends 구문의 뒤에 자리한다. 한 클래스에 여러개의 인터페이스가 구현될 때는 콤마로 인터페이스들을 구분해주면 된다.

클래스가 implements 구문을 사용한다는 것은, 구문에서 선언된 인터페이스들의 필수 메소드들을 구현하겠다는 의미이다.
만약, 클래스가 인터페이스를 구현하고 있지만 모든 필수 메소드들을 구현하지 않는다면, 구현되지 않은 추상메소드들을 상속받게 되며 필히 추상메소드임을 표기해주어야 한다.
이는 여러개의 인터페이스가 구현될때에도 모든 인터페이스의 필수 메소드들에 전부 해당된다.


#### :mag:인터페이스 레퍼런스를 통해 구현체를 사용하는 방법
다형성의 특징을 활용하여 인터페이스를 타입으로써 사용할 수 있다.

```java
interface Flyable{
    void fly();
}

interface Jumpable {
	 void jump();
}

class Bird implements Flyable, Jumpable {
    @Override
    public void fly() {
        System.out.println("Bird's Flying");
    }
		@Override
		public void jump() {
        System.out.println("Bird's Jumping");
		}
}
```

Flyable을 통해서 선언한 Bird 객체는 Flyable을 통해 구현된 메소드만 사용할 수 있다.

```java
Flyable bird = new Bird();
bird.fly();
bird.jump(); // Cannot resolve method 'jump' in 'Flyable'
```

이는 자바의 다형성의 대표적인 예시로 활용된다.

```java
List<Flyable> list = ArrayList<Flyable>();
list.add(new Bird());
list.add(new Airplane());
list.add(new SuperMan());

for (Flyable element : list) {
	element.fly(); // fly 메소드로 통일하여 호출
}
```

#### :mag:인터페이스 상속
앞서 추상클래스와 인터페이스의 차이점에 대해서 언급할 때 인터페이스는 다중상속이 가능하다고 이야기 했다. 클래스가 인터페이스를 구현할때도 다중상속이 가능하지만 인터페이스도 다른 인터페이스를 다중상속할 수 있다.

###### 인터페이스가 인터페이스를 상속
인터페이스는 다른 인터페이스를 상속받을 수 있다. 클래스와 마찬가지로 인터페이스도 extends 구문을 통해 상속이 이루어 진다. 상속을 하게 되면 상위 인터페이스의 모든 메소드와 상수를 상속받으며 자신만의 새로운 메소드와 상수를 사용할 수도 있다. 
클래스의 상속과 다른 점은 상속할 때도 다중상속이 가능하다는 것이다.

즉, 인터페이스는 다른 여러개의 인터페이스를 상속할 수 있으며 상속한 각각의 상위 인터페이스가 가진 모든 메소드와 상수를 상속 받는다.

###### 클래스가 구현한 인터페이스가 상속한 인터페이스
그렇게 다수의 인터페이스를 상속받은 인터페이스를 클래스가 구현하게 되면, 클래스는 구현하는 인터페이스의 메소드와 상수를 모두 구현해야 하고, 또한 구현하는 인터페이스의 상위 인터페이스들의 모든 추상메소드와 상수들도 구현해야 한다.

```java
interface Drawble {
  void draw();
}
interface Printable extends Drawble {
  void print();
}

class Circle implements Printable {
  @Override
  public void draw() {
  }
  @Override
  public void print() {
  }
}
```

인터페이스의 메소드들은 추상 메소드이기 때문에 동일한 메소드가 상위 인터페이스들 에서 선언되었더라도 구현 시점에서는 문제가 되지 않는다.

```java
interface Dancable {
  void perform();
}
interface Flyable {
  void perform();
}

interface Perfomable extends Dancable, Flyable {
}

class Superman implements Perfomable {
  @Override
  public void perform() {
  }
}
```

다만 리턴 타입이 다른 경우 컴파일 에러가 발생할 수 있다.

```java
interface Dancable {
    void perform();
}

interface Flyable {
    boolean perform();
}

interface Perfomable extends Flyable,Dancable {
} //'perform()' in 'Dancable' clashes with 'perform()' in 'Flyable'; methods have unrelated return types
```

-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://dev-coco.tistory.com/13  
https://k3068.tistory.com/34  
https://www.notion.so/8-0cc8c251d5374ac882a4f22fa07c4e6a  