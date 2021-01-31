## :muscle:클래스
모든 자바 프로그램은 객체를 활용한다. 그리고 그 객체들은 클래스와 인터페이스를 통해서 만들어진다. 어느 프로그램이라도 한개의 클래스는 갖게 되며,
복잡한 프로그램이라면 다수의 클래스와 인터페이스들을 포함하고 있을것이다.
그렇게 클래스는 모든 자바 프로그램의 기본 구조적 요소이다. 클래스를 정의하지 않고는 자바 코드를 짤 수 없다고 보아도 된다.

>클래스  
클래스는 값을 가진 데이터 필드와 그 필드를 이용하는 메소드들의 집합이다. 그 필드와 메소드들을 사용하는 새로운 레퍼런스 타입을 정의하며, 그 타입의 새로운 객체가 생성될 수 있는 블루프린트나 프로토타입의 역할을 하는것이 클래스이다.

>객체  
객체는 클래스의 인스턴스이다. 객체지향 프로그래밍의 기본 요소이며 일반적으로 자바 프로그램은 여러개의 객체를 갖는다. 한 프로그램 안의 여러개의 객체들이 메소드를 통해서 상호작용 하게 된다.

#### :mag:클래스 정의하는 방법
가장 기본적인 형태의 클래스는 class 키워드에 클래스 이름(MyClass)이 따라오는 형태로 작성할 수 있다. 뒤따르는 대괄호 안에 클래스의 요소가 들어가면 된다.

```java
class MyClass {
    // 필드, 생성자, 메소드 선언
}
```

클래스 키워드의 앞에는 접근지정자(public)나 어노테이션(@Override)이 올 수 있다.
클래스명 뒤로는 extends 키워드와 함께 상속할 클래스 이름(MySuperClass)이 따라올 수 있다. 인터페이스를 구현하는 경우에는 맨 마지막에 implements 키워드와 함께 하나 혹은 다수의 인터페이스 이름을 적어주면 되는데, 다수일 경우엔 콤마로 구분한다(YourInterface, MyInterface).

```java
@Override
public class MyClass extends MySuperClass implements YourInterface, MyInterface {
    // 필드, 생성자, 메소드 선언
}
```

#### :mag:메소드 정의하는 방법
보통 다른언어에는 함수라는 것이 별도로 존재한다. 하지만 자바는 클래스를 떠나 존재하는 것은 있을 수 없기 때문에 자바의 함수는 따로 존재하지 않고 클래스 내에 존재한다. 자바는 이 클래스 내의 함수를 메소드라고 부른다.

#### :mag:객체 만드는 방법 (new 키워드 이해하기)
Now that we’ve covered fields and methods, let’s move on to other important mem‐
bers of a class. In particular, we’ll look at constructors—these are class members
whose job is to initialize the fields of a class as new instances of the class are created.
Take another look at how we’ve been creating Circle objects:
Circle c = new Circle();
This can easily be read as creating a new instance of Circle, by calling something
that looks a bit like a method. In fact, Circle() is an example of a constructor. This
is a member of a class that has the same name as the class, and has a body, like a
method.
Here’s how a constructor works. The new operator indicates that we need to create a
new instance of the class. First of all, memory is allocated to hold the new object
instance. Then, the constructor body is called, with any arguments that have been
specified. The constructor uses these arguments to do whatever initialization of the
new object is necessary.
Every class in Java has at least one constructor, and their purpose is to perform any
necessary initialization for a new object. If the programmer does not explicitly
define a constructor for a class, the javac compiler automatically creates a construc‐
tor (called the default constructor) that takes no arguments and performs no special
initialization. The Circle class seen in Example 3-1 used this mechanism to auto‐
matically delcare a constructor.

#### :mag:this 키워드 이해하기


#### :mag:생성자 정의하는 방법
--A constructor is called "Default Constructor" when it doesn't have any parameter.

if we don’t declare a constructor for the PlaneCircle class, Java
implicitly inserts this constructor:

public MyClass() { super(); }

--Java Parameterized Constructor
A constructor which has a specific number of parameters is called a parameterized constructor.


--Constructor Overloading in Java
In Java, a constructor is just like a method but without return type. It can also be overloaded like Java methods.

Constructor overloading in Java is a technique of having more than one constructor with different parameter lists. They are arranged in a way that each constructor performs a different task. They are differentiated by the compiler by the number of parameters in the list and their types.

--자바에서의 생성자와 메소드의 차이

| 자바 생성자                                                          | 자바 메소드                                                       |
|----------------------------------------------------------------------|-------------------------------------------------------------------|
| 해당 클래스의 인스턴스인 객체를 생성하기 위해서 생성자가 이용된다    | 객체의 능동적인 기능을 정의하기 위해서 이용된다                   |
| 생성자에는 리턴타입이 없다                                           | 메소드는 리턴 타입을 갖는다                                       |
| 생성자는 묵시적으로 이용된다                                         | 메소드는 명시적으로 이용된다                                      |
| 생성자를 작성하지 않을 경우, 자바 컴파일러가 기본생성자를 제공해준다 | 메소드는 어떤 경우에도 컴파일 단계에서 자동적으로 제공되지 않는다 |
| 생성자 이름은 클래스 이름과 같아야 한다                              | 메소드 이름은 클래스 이름과 같을수도 다를수도 있다                |


-References :
Java in a Nutshell by Benjamin J.Evans & David Flanagan  
https://www.geeksforgeeks.org/classes-objects-java/  