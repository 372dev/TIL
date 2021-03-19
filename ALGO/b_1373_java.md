# BAEKJOON 1373 JAVA
* ALGO : 바로 해결하지 못하고 검색해본 알고리즘 또는 해결했지만 더 좋은 방법들이 있었던 알고리즘의 기록을 남깁니다.

## 2진수 8진수
![1373](https://raw.githubusercontent.com/372dev/TIL/main/ALGO/img/b_1373.jpg)

* 입력 조건에서 수의 길이가 최대 1,000,000이므로 숫자형 변수는 사용할 수 없고 문자열로 받아와야 한다. int는 -2,147,483,648 에서 2,147,483,647 사이의 값을 담을 수 있고, String의 경우 2,147,483,647개의 문자를 담을 수 있다.

* 8은 2의 3승이므로 3비트 2진수는 8진수로, 그 반대로도 표현이 가능하다. 아래 나온 풀이 방식들 모두 이 방법을 사용한다.

![1373_2](https://raw.githubusercontent.com/372dev/TIL/main/ALGO/img/b_1373_2.jpg)

* 다만 한번에 해결하지 못하고 아래 링크를 참고하여 풀었다.

-출처 :
https://velog.io/@dazzlynn/BOJ-백준-1373-2진수-8진수
https://github.com/stack07142/BOJ/blob/master/BOJ%231373_BINToOCT/src/Main.java

## 최초 시도
```java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String binNum = sc.nextLine();
        String octNum = "";
        sc.close();
        int l = binNum.length();
        int n;

        if (l % 3 == 1) {
            binNum = "00" + binNum;
        } else if (l % 3 == 2) {
            binNum = "0" + binNum;
        }

        for (int i = 0; i < l; i += 3) {

            int sum = 0;

            sum += ((int) (binNum.charAt(i) - '0')) * 4;
            sum += ((int) (binNum.charAt(i + 1) - '0')) * 2;
            sum += ((int) (binNum.charAt(i + 2) - '0'));

            octNum += sum;
        }
        System.out.println(octNum);
    }
}
```

실패 - 메모리 초과
많은 문제들이 BufferedReader와 StringBuilder를 사용해야만 하고 그렇지 않은 경우 메모리 초과가 된다. 지금 아직 자바 학습 과정을 마치지 않은 단계라 완전히 이해하지 않고 사용하기 꺼려지기는 하나 어쩔 수 없이 이런 경우 검색해 가며 사용하고 있다. 다행인 것은 다음주 자바 학습 주제가 BufferedReader이다! 오예

## 두번째 시도
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder binNum = new StringBuilder(br.readLine());
        StringBuilder octNum = new StringBuilder();

        int l = binNum.length();

        if (l % 3 == 1) binNum.insert(0, "00");
        else if (l % 3 == 2) binNum.insert(0, "0");

        for (int i = 0; i < l; i += 3) {
            int sum = 0;
            sum += ((int) (binNum.charAt(i) - '0')) * 4;
            sum += ((int) (binNum.charAt(i + 1) - '0')) * 2;
            sum += ((int) (binNum.charAt(i + 2) - '0'));

            octNum.append(sum);
        }
        System.out.println(octNum);
    }
}
```
성공

## 다른 방법
8진수 -> 2진수 때와 마찬가지로
가능한 경우의 수를 미리 준비해 두고 처리하는 방법이 있다. 아래 예제에서는 매핑을 이용한다.

```java
import java.io.*;
import java.util.HashMap;
import java.util.Map;

class Main{

    static void createMap(Map<String, Character> um)
    {
        um.put("000", '0');
        um.put("001", '1');
        um.put("010", '2');
        um.put("011", '3');
        um.put("100", '4');
        um.put("101", '5');
        um.put("110", '6');
        um.put("111", '7');
    }

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder binNum = new StringBuilder(br.readLine());
        StringBuilder octNum = new StringBuilder();

        int l = binNum.length();

        if (l % 3 == 1) binNum.insert(0, "00");
        else if (l % 3 == 2) binNum.insert(0, "0");

        Map<String, Character> bin_oct_map = new HashMap<String, Character>();
        createMap(bin_oct_map);

        int i = 0;
        while (true)
        {
            octNum.append(bin_oct_map.get(binNum.substring(i, i + 3)));
            i += 3;

            if (i >= binNum.length())
                break;
        }
        System.out.println(octNum);
    }
}
```

-출처 :
contributed by jithin // https://www.geeksforgeeks.org/convert-binary-number-octal/

언뜻 매핑을 하는 방법이 더 빠르지 않을까 생각 됐는데 막상 결과는 두번째 시도 때 보다 속도도 느리고 메모리는 두배로 잡아먹는다.