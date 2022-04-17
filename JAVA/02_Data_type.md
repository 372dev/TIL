# Java_02_Data_type

## :muscle:자바 데이터 타입, 변수 그리고 배열

### :star:프리미티브 타입 종류와 값의 범위 그리고 기본 값
자바에는 여덜가지의 기본자료형(Primitive data types)이 있다. 참/거짓 타입(Boolean), 문자형 타입(Character), 네개의 정수형 타입(Integer) 그리고 두개의 실수형(Floating point) 타입이 있다. 숫자를 나타내는 타입이 여섯가지가 있는데는 이유가 있는데, 정수형과 네가지, 실수형 두가지 각각 다른 데이터 크기를 사용하며 이에 따라 각 자료형에 담을 수 있는 숫자의 크기가 정해진다.  
-Source : Java in a nut shell 7th edition by Benjamin J. Evans and David Flanagan  

![whiteship02_1](https://raw.githubusercontent.com/372dev/372dev.github.io/master/_posts/imgs/whiteship02_1.jpg)  
-Source :  
[https://techvidvan.com/tutorials/data-types-in-java](https://techvidvan.com/tutorials/data-types-in-java)  

![whiteship02_2](https://raw.githubusercontent.com/372dev/372dev.github.io/master/_posts/imgs/whiteship02_2.jpg)  
-Source :  
[https://www.geeksforgeeks.org/data-types-in-java](https://www.geeksforgeeks.org/data-types-in-java/)  

### :star:프리미티브 타입과 레퍼런스 타입의 차이
* 형태의 차이 - 여덜개의 기본자료형(Primitive types)은 자바 언어에 의해 정의되어 있고 각각의 특성을 사용자가 변경할 수 없다. 참조자료형(Reference types)은 사용자가 자유롭게 정의할 수 있다. 예를 들어 프로그램에 "Point"라는 클래스를 정의하고 두개의 Double 값을 가지게 하여 x, y 좌표를 저장하게 할 수도 있다.
* 크기의 차이 - 기본자료형은 각각 1에서 8 바이트 사이의 크기를 갖게 되는데 이 기본자료형이 변수에 저장되어 있을 때 그 자료형의 정해진 크기만큼 메모리를 복사해 온다. 참조자료형, 에를 들어 오브젝트의 경우엔 이와 다르게 훨씬 많은 메모리를 차지할 수 있다. 오브젝트가 생성되고 힙 메모리에 유동적으로 저장되며 이 오브젝트가 사용되지 않을 때는 "가비지 콜렉터"에 의해 메모리에서 자동으로 삭제된다.
* 비교연산자의 이용의 차이 - 기본 자료형 에서의 연산자 이용은 명료하다. == 연산자를 이용한다면 결과는 두개의 값이 같은지를 판단한다. 하지만 참조 자료형에 비교연산자를 이용한다면 결과는 두 비교 대상이 같은 오브젝트나 어레이인지를 판단한다. 쉽게 말해 참조자료형의 연산자를 이용한 비교는 메모리 위치를 비교하게 되며 이에 따라 연산자로 값을 비교할 수 없다.  
-Source : Java in a nut shell 7th edition by Benjamin J. Evans and David Flanagan  

![whiteship02_3](https://raw.githubusercontent.com/372dev/372dev.github.io/master/_posts/imgs/whiteship02_3.jpg)  
-Source :  
[https://www.geeksforgeeks.org/data-types-in-java](https://www.geeksforgeeks.org/data-types-in-java/)

### :star:리터럴
자바에서의 리터럴은 Boolean, Character, Numeric, String 그리고 Null 데이터를 나타내는 구문이다. 사용자는 리터럴을 통해 프로그램 안에서 특정 값을 표현할 수 있다. 예를 들어, 아래의 구문에서 count 라는 이름의 정수형 변수가 선언되었다. 리터럴 '0'은 자연스럽게 변수에 들어갈 값 0을 뜻한다.  

``` Java
int count = 0;
```  

-Source :
[https://www.geeksforgeeks.org/data-types-in-java](https://www.geeksforgeeks.org/data-types-in-java/)  

![whiteship02_4](https://raw.githubusercontent.com/372dev/372dev.github.io/master/_posts/imgs/whiteship02_4.jpg)  
-Source :  
[https://techvidvan.com/tutorials/literals-in-java/](https://techvidvan.com/tutorials/literals-in-java/)  

### :star:변수 선언 및 초기화하는 방법
변수를 선언하기 위해서, 우선 자료형을 정하고 변수명과 함께 입력해야 한다. 변수를 선언한다는 것은 곧 변수를 생성하는 것이다. 기본자료형의 변수를 선언하면 자바는 그 자료형에 맞는 메모리를 할당해 주며 지정한 변수명에 그 메모리를 연결해 준다.  
자바의 로컬 변수들은 기본값이 주어지지 않는다. 프로그램이 변수를 사용하기 전에 먼저 컴파일 단계에서 변수에 값이 들어가 있는지 확인하는 과정을 거친다. 다음과 같은 방법으로 초기화가 가능하다.  
* 선언하면서 초기화 하기 - 리터럴을 사용하거나 다른 변수의 값을 가져와서 선언과 동시에 초기화 할 수 있다.  

```java
int x = 0;

String lastName = "Lowe";

int y = x;
```  

* 미리 선언된 변수를 초기화 하기 - 위 방법과 비슷하다.  

```java
int x;

x = 0;
```  

* 참조자료형의 선언 - new 키워드를 이용하기.  

```java
User user = new User();
```  

* 어떤 방법이던 근본적인 형태는 다음과 같다.  

```java
type variableName = expression;
```  

-Sources :  
[https://runestone.academy/runestone/books/published/apcsareview/VariableBasics/declareVars.html](https://runestone.academy/runestone/books/published/apcsareview/VariableBasics/declareVars.html)  
[https://www.baeldung.com/java-initialization](https://www.baeldung.com/java-initialization)  

### :star:변수의 스코프와 라이프타임
스코프(Scope)와 라이프타임(Lifetime)의 관점에서 변수는 세가지 항목으로 분류된다.  
1. 인스턴스 변수(Instance Variables)
  * 스코프: 스테틱 메소드를 제외하고는 클래스 전반에 거친다.
  * 라이프타임: 클래스의 객체가 메모리에 상주하는 동안.
2. 클래스 변수(Class Variables)
  * 스코프: 클래스 전반에 거친다.
  * 라이프타임: 프로그램이 종료할 때 까지.
3. 지역 변수(Local Variables)
  * 스코프: 선언된 코드 블럭 안.
  * 라이프타임: 선언된 코드 블럭이 실행되는 동안.  
-Source :  
[https://www.learningjournal.guru/article/programming-in-java/scope-and-lifetime-of-a-variable/](https://www.learningjournal.guru/article/programming-in-java/scope-and-lifetime-of-a-variable/)  

### :star:타입 변환, 캐스팅 그리고 타입 프로모션
* 자동 형변환(Widening Casting / Automatically)
서로 다른 기본자료형의 변수들이 연산되거나 연산된 후에 대입될 때, 값의 범위가 작은 자료형의 연산 결과는 값이 더 큰 자료형으로 타입 프로모션(Type Promotion) 되어 대입될 수 있으며 컴파일러가 자동으로 형변환을 수행한다.  
* 강제 형변환(Narrowing Casting / Manually)
변수, 리터럴, 혹은 이것들과 연산자의 혼합의 결과를 강제로 형변환 시킬 수 도 있다. 괄호 안에 자료형의 이름을 적은 뒤에 자료형을 변경할 내용의 앞에 위치하도록 한다. 강제 형변환을 할 경우 자료형의 범위가 좁아져서 데이터의 손실이 올 수 있으므로 주의해야 하며, 자료의 손실이 없을 것이라는 확신이 있거나 혹은 자료의 손실을 의도적으로 이용할 경우 아래와 같은 방식으로 사용한다.  

```java
int i = 13;
byte b = (byte) i; // Force the int to be converted to a byte
i = (int) 13.456; // Force this double literal to the int 13
```  

-Sources :  
Java in a nut shell 7th edition by Benjamin J. Evans and David Flanagan  

### :star:1차 및 2차 배열 선언하기
* 1차원 배열의 선언  

```java
type var-name[];
OR
type[] var-name;
```  

* 1차원 배열의 선언과 할당  

```java
type var-name[] = new type[size];
OR
type[] var-name = new type[size];
```  

* 2차원 배열의 선언  

```java
type var-name[][];
OR
type[] var-name[];
OR
type[][] var-name;
```  

* 2차원 배열의 선언과 할당  

```java
type var-name[][] = new type[size][size];
OR
type[] var-name[] = new type[size][size];
OR
type[][] var-name = new type[size][size];
```  

-Sources :  
[https://www.geeksforgeeks.org/arrays-in-java/](https://www.geeksforgeeks.org/arrays-in-java/)  

### :star:타입 추론, var
JDK 10 에서 추가된 기능이다. 자바 컴파일러가 상황에 걸맞도록 변수의 타입을 추론하게 된다. 이에 따라 사용자가 데이터 타입을 확정하지 않고도 이용할 수 있는 옵션이 주어진다. 아래와 같은 구문이 로컬 변수로 선언되었다고 했을 때,  

```java
List<String> list = new ArrayList<String>();
```  

보이는 바와 같이, 위의 변수 선언에서 자료형의 정보 List와 String이 반복적으로 사용 되었다. 이런 무의미한 코드의 반복을 막고자 아래와 같이 var이 사용될 수 있다.  

```java
var list = new ArrayList<String>();
```  

-Sources :  
[https://www.codejava.net/java-core/the-java-language/var-keyword-in-java](https://www.codejava.net/java-core/the-java-language/var-keyword-in-java)  