# Java_04_Control_flow

## :muscle:분기문(Control flow)  

### :star:조건문(if / if...else statement)  

우리는 살아가며 종종 상황을 보고 그 상황에 맞게 결정을 내려야 할 때가 있습니다. 예를 들어, 비가 오고 있다면 우산을 챙겨야 하고 하늘이 맑다면 우산을 챙기지 않습니다. 같은 판단의 과정을 통해 어떤 정수가 2로 나눠진다면 우린 그 숫자가 짝수라고 할 수 있고 2로 나눠지지 않는다면 홀수라고 결론지을 수 있습니다.  

#### :mag:if statement  

다시 우산의 예를 들어봅시다.  

* 비가 오는지를 보고 우산을 가져갈지 판단하는 내용으로 조건문의 기본 신텍스를 표현하면 다음과 같습니다.  

>if(비가온다){<br/>
>	우산을 챙긴다.<br/>
>}<br/>

* if(비가온다) - 괄호 안에 조건이 들어갑니다. 값은 true or false의 boolean 이어야 하며, boolean 값을 가진 변수를 담을 수도 있고 연산을 통해 조건을 만들 수 도 있습니다.
* {우산을 챙긴다.} - 조건에 뒤따르는 코드블럭 {} 안에는 조건이 참일 경우 실행할 코드가 들어가게 됩니다.
* 비교연산을 이용한 실제 코딩의 예를 들면 다음과 같습니다.  

```java
int a=10,b=20;
if(a < b){
	System.out.println("b는 a보다 크다");
}
```  

* 정수 값을 입력받아 짝수인지 홀수인지 판단하는 코드.  

```java
public void method1() {
	int num = 0;	

	System.out.println("정수값 입력 : ");
	num = scanner.nextInt();

	if(num % 2 == 0) {
		System.out.printf("%d은(는) 짝수이다.\n", num);
	}
	if(num % 2 != 0) {
		System.out.printf("%d은(는) 홀수이다.\n", num);
	}
}
```  

#### :mag:if...else statement  

위에서 if 구문이 조건의 결과 참/거짓에 따라 참일 경우에 코드블럭을 실행하는 것을 확인했습니다. 여기에 else를 덧붙이면 if 구문의 조건 결과가 거짓일 경우에 실행할 코드블럭을 추가할 수 있습니다.  

* 집에 들어오기 전에 우산을 사용했는지 여부에 따라 우산을 말릴지 아니면 그냥 넣어둘지 판단하는 내용으로 조건문의 기본 신텍스를 표현하면 다음과 같습니다.  

>if(우산을 사용했다){<br/>
>	우산을 펼쳐두어 말린다.<br/>
>}  else {<br/>
>	우산을 그냥 넣어둔다.<br/>
>}<br/>

* if(우산을 사용했다) - 괄호 안에 조건이 들어갑니다. 값은 마찬가지로 true or false의 boolean 입니다.
* {우산을 펼쳐두어 말린다.} - 조건에 뒤따르는 코드블럭 {} 안에는 조건이 참일 경우 실행할 코드가 들어가게 됩니다.
* else {우산을 그냥 넣어둔다.} - 앞선 조건이 false일 경우 뒤따르는 코드블럭 {} 안의 코드를 실행합니다.
* 비교연산을 이용한 실제 코딩의 예를 들면 다음과 같습니다.  

```java
int temperature;

if(temperature <= 0) {
    System.out.println("강물이 얼었습니다.");
} else {
    System.out.println("강물이 녹았습니다.");
}
```  

* if구문을 알아볼 때 살펴본 두개의 if 구문을 사용하여 정수 값을 입력받아 짝수인지 홀수인지 판단하는 코드 또한 먼저 오는 if 구문이 거짓일 경우 뒤에 오는 if 구문이 무조건 참이기 때문에 if...else 구문을 이용하도록 바꿔줄 수 있습니다.  

```java
public void method1() {
	int num = 0;	

	System.out.println("정수값 입력 : ");
	num = scanner.nextInt();

	if(num % 2 == 0) {
		System.out.printf("%d은(는) 짝수이다.\n", num);
	} else {
		System.out.printf("%d은(는) 홀수이다.\n", num);
	}
}
```  

#### :mag:if...else if...else statement  

먼저 살펴본 if...else 구문을 중첩해서 사용할 수 있습니다.  

* 귀찮지 않다면 펼쳐둔 우산이 다 말랐는지 확인하고 우산을 접을지 아니면 더 말릴지 판단하는 내용으로 조건문의 기본 신텍스를 표현하면 다음과 같습니다.  

>if(귀찮다) {<br/>
>	내일 확인한다.<br/>
>} else if(우산이 다 말랐다) {<br/>
>	우산을 접는다.<br/>
>}  else {<br/>
>	우산을 더 말린다.<br/>
>}<br/>

* if(귀찮다) - 괄호 안에 먼저 처리할 조건이 들어갑니다. 값은 마찬가지로 true or false의 boolean 입니다.
* {내일 확인한다.} - 조건에 뒤따르는 코드블럭 {} 안에는 조건이 참일 경우 실행할 코드가 들어가게 됩니다.
* else if(우산이 다 말랐다) - 앞선 조건이 거짓일 경우 이 조건을 확인합니다.
* {우산을 접는다.} - 조건에 뒤따르는 코드블럭 {} 안에는 조건이 참일 경우 실행할 코드가 들어가게 됩니다.
* else {우산을 더 말린다.} - 앞선 모든 조건이 false일 경우 뒤따르는 코드블럭 {} 안의 코드를 실행합니다.
* 비교연산을 이용한 실제 코딩의 예를 들면 다음과 같습니다.  

```java
int temperature;

if(temperature <= 0) {
    System.out.println("물은 고체상태입니다.");
} else if (temperature < 100) {
	System.out.println("물은 액체상태입니다.");
} else {
    System.out.println("물은 기체상태입니다.");
}
```  

### :star:선택문(switch statement)

앞서 살펴본 조건문의 경우, 한가지 조건의 참/거짓 여부에 따라 실행할 코드블럭을 각각 작성합니다. 하지만 우리가 살아가며 둘중 하나의 조건만 주어지는게 아니라 여러가지 선택이 주어질 때가 있습니다. if...else 구문을 중첩시켜서 다중 구문으로 이를 표현할 수 있겠지만 그보다 더 효율적일 수 있는 방법으로 선택문이 있습니다.  

* 주어진 달에 따라 계절을 알려주는 내용으로 선택문의 기본 신텍스를 표현하면 다음과 같습니다.  

>switch(이번달){<br/>
>	case 12월, 1월, 2월 :<br/>
>		겨울입니다.<br/>
>		break;<br/>
>	case 3월, 4월, 5월 :<br/>
>		봄입니다.<br/>
>		break;<br/>
>	case 6월, 7월, 8월 :<br/>
>		여름입니다.<br/>
>		break;<br/>
>	case 9월, 10월, 11월 :<br/>
>		가을입니다.<br/>
>		break;<br/>
>	default:<br/>
>		몇월인지 다시 입력하세요.<br/>
>}<br/>

* switch(이번달) - 괄호 안에 비교대상인 값이 들어갑니다. 조건문에서의 참/거짓값이 아닌 숫자 혹은 문자값이 들어갑니다.
* case 12월, 1월, 2월 - 위에 나온 값과 비교할 고정값들입니다. 일치하는 값이 있는 경우 뒤따르는 코드를 실행합니다.
* 봄입니다. break; - 앞선 고정값 중에 비교대상과 일치하는 값이 있는 경우 이 코드를 실행합니다. 봄입니다 라는 코드가 실행되고 나면 그 다음 뒤따르는 고정값과의 비교를 계속 이어가는데, 이를 방지하기 위해 break;를 사용할 경우 비교를 중단합니다.
* default: - 위의 고정값들과 비교가 끝나고 일치하는 값이 없어 break;가 실행되지 않았다면, 혹은 일치하는 값의 실행 코드에 break;가 없었다면 마지막에 default:에 뒤따르는 코드가 기본값으로 실행됩니다.  

~~Java8 에서는 이렇게 고정값을 한줄에 나열해서 쓸 수 없다.. 어느 버전부터 이게 가능한지도 찾아서 추가하자~~  

* 실제 코딩의 예를 들면 다음과 같습니다.  

```java
switch(num) {
	case 1:
	case 3:
	case 5:
	case 7:
	case 8:
	case 10:
	case 12:
		System.out.println(num + "월은 31일까지 있습니다.");
		break;
	case 4:
	case 6:
	case 9:
	case 11:
		System.out.println(num + "월은 30일까지 있습니다.");
		break;
	case 2:
		System.out.println(num + "월은 28일 혹은 29일까지 있습니다.");
}
```  

-References :  
[https://www.codesdope.com/java-decide-if-or-else/](https://www.codesdope.com/java-decide-if-or-else/)  
[https://devqa.io/java-if-else-switch-statements/](https://devqa.io/java-if-else-switch-statements/)  

### :star:반복문(Iteration)

루프(loop)라고 불리우는 반복문들은 어느 프로그래밍 언어에서나 기능을 반복적으로 수행하기 위해 사용됩니다. 자바에는 세가지 종류의 루프가 있는데 먼저 표를 보며 이 세가지를 비교해보고 시작하겠습니다.  

![whiteship04_7](https://raw.githubusercontent.com/372dev/372dev.github.io/master/_posts/imgs/whiteship04_7.PNG)  

#### :mag:while statement
While 구문은 자바의 가장 기본적인 반복문이다. 기본적인 신택스는 다음과 같다.  

>while (조건식) {  
>  실행할 구문  
>}  
  
While 구문은 실행시, 먼저 조건을 확인하며 이 조건식에는 Boolean 변수나 Boolean 값(true/false)이 들어가야 한다. 값이 거짓이라면, 인터프리터는 뒤따르는 실행 구문을 건너뛰고 다음 코드를 읽는다. 한편 값이 참인 경우, 인터프리터는 뒤따르는 실행 구문을 실행하고 난 뒤 Boolean 값을 다시 한번 확인한다. 재확인된 값이 거짓이라면 실행 구문을 건너뛰고 참이라면 실행 구문을 다시 한번 더 실행하며 이와 같은 순환이 계속해서 반복된다. 언제까지? 조건의 값이 true인 경우 계속(false가 된 경우 멈춘다). 반복이 모두 끝나야만 인터프리터는 다음으로 넘어간다.  

다음 신택스를 이용해서 무한반복 구문을 만들 수 도 있다.  

>while(true)  

다음은 While 구문으로 0부터 9까지 모든 숫자를 실행하는 예문이다.  

```java
int count = 0;
while (count < 10) {
 System.out.println(count);
 count++;
}
```  

위와 같이 count라는 변수가 0으로 시작되고 while 루프가 반복되는 동안 매번 1씩 증가한다. 루프가 10번 반복되고 나면 조건식은 false(10보다 작지 않기 때문에)가 되며 while 구문은 종료된다. 반복문이 종료되고 나서야 인터프리터는 다음 코드로 넘어갈 수 있다. 반복문은 이렇듯 카운터의 역할을 하는 변수를 갖는 경우가 많다. 카운터의 변수명은 i, j, k의 순으로 주로 쓰이며 의미를 가진 변수명을 사용하는 것 또한 좋다.  

#### :mag:do...while statement

do...while 구문은 while 구문과 비슷하다. 다만, 조건의 확인이 반복문 실행 후에 이루어진다는 차이가 있다. 때문에 조건의 확인 이전에 무조건 한번은 구문을 실행하게 된다. 신택스는 다음과 같다.

>do {  
>  실행할 구문  
>} while (조건식);  

do...while 구문과 while 구문의 차이점에 주목하라. 먼저, do...while 구문은 do 라는 키워드로 반복문의 시작을 표시하며, 뒤따르는 while 키워드로 반복 실행할 구문의 끝을 표시하는 동시에 조건식을 정해준다.  
또한, while 구문과 달리 do...while 구문은 끝에 세미콜론(;)을 붙여줘야 한다. 이는 while 키워드와 조건식 뒤에 중괄호(코드블럭)가 오지 않고 끝마침을 표현하는 것이다.  
다음의 do...while 구문은 앞서 살펴본 while 구문 예제와 같은 결과를 도출한다.  

```java
int count = 0;
do {
 System.out.println(count);
 count++;
} while(count < 10);
```  

do...while 구문은 while 구문에 비해 자주 쓰이지 않는다. 그 이유는 실무에서 반복문을 조건과 관계 없이 무조건 한번 실행해야 할 경우가 그리 많지 않기 때문이다.  

#### :mag:for statement

for 구문은 while 구문이나 do while 구문보다 사용하기 편리한 면이 있다. for 구문은 일반적이고 자주 사용되는 반복 구조를 활용한다. 반복이 실행되기 전에 먼저 카운터의 역할을 할 변수가 지정되고, 이 카운터의 크기가 조건에 부합하는지 확인한 이후에
코드가 실행되고, 마지막에 카운터의 크기가 주어진 규칙에 따라 증감된다. 카운터의 초기화, 조건 확인, 증감식 까지 이 세가지가 for 구문의 핵심 요소이다. 이 세 요소가 반복문의 조건을 명확하게 표현하게 된다.  

>for(초기값; 조건식; 증감식) {  
> 실행할 구문  
>}  

같은 내용을 while 구문으로 표현하면 다음과 같다.  

>초기값;  
>while (조건식) {  
> 실행할 구문;  
> 증감식;  
>}  

초기값, 조건식, 증감식 모두 첫번째 줄에 들어간다는 특징으로 인해, for 구문은 한눈에 이해하기 좋다는 장점이 있다. 그러므로 초기값 설정을 까먹거나 증감식을 넣지 않는 등의 실수를 방지할수 있게 된다. 초기값과 증감식은 반복문이 종료된 후에 폐기되므로 반복문 실행 중에 잘 활용하는 것이 좋다. 초기값은 주로 대입연산으로, 증감식은 주로 증감연산자 혹은 다른 방식으로 정해진다.  
다음은 for 구문을 이용하여, 앞선 while 구문과 do...while 구문처럼 0부터 9까지 모든 숫자를 실행하는 예문이다.  

```java
int count;
for(count = 0 ; count < 10 ; count++)
 System.out.println(count);
```  

앞서 말했듯이 for 구문에서는 반복을 정의하는 모든 주요 정보가 한줄에 들어가므로 쉽게 구조 파악이 가능하다. 또한 증감식이 조건식과 함께 오므로 코드의 길이 또한 비교적 짧아질 수 있다. 게다가 한줄의 코드만 반복실행 할 경우 중괄호를 사용하지 않아도 된다.  
for 구문을 더욱 더 편리하게 이용할 수 있는 신텍스도 사용 가능하다. 반복문에서 초기값은 종종 그 반복문에서만 사용되기 때문에 for 구문 안에서 초기값을 선언할 수 있다. 그렇게 함으로 초기값은 반복문의 스코프 안에 포함되게 된다. 예를 들어 다음과 같이 사용할 수 있다.  

```java
for(int count = 0 ; count < 10 ; count++)
 System.out.println(count);
```  

심지어 두개의 초기값을 사용하는 것도 가능하다. 초기값, 증감식, 조건식 각각의 변수를 콤마(,)로 구분하여 사용하면 된다. 예를들어 아래와 같은 신텍스도 가능하다.  

```java
for(int i = 0, j = 10 ; i < 10 ; i++, j--)
 sum += i * j;
```  

지금까지 보여준 예는 모두 숫자의 연산을 이용한 반복이지만, 숫자만 이용할 수 있는건 아니다. 예를 들어 링크드 리스트의 요소들을 for 구문을 통해 조회할 수 도 있다.  

```java
for(Node n = listHead; n != null; n = n.nextNode())
 process(n);
```  

for 구문에서 초기값, 조건식, 증감식은 모두 생략이 가능하다. 다만 그 세가지를 구분하는 세미콜론(;)은 꼭 필요하다. 조건식이 생략된 경우엔 조건이 true인 것으로 판정된다. 그러므로 for 구문을 이용한 무한반복 구문은 다음과 같이 만들 수 있다.  

>for(;;)  

-References :  
[https://www.javatpoint.com/java-for-loop](https://www.javatpoint.com/java-for-loop)  
Java in a Nutshell by Benjamin J.Evans & David Flanagan  