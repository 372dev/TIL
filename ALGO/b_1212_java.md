# BAEKJOON 1212 JAVA
* ALGO : 알고리즘 한번에 해결하지 못하고 검색한 경우, 해결했지만 더 좋은 방법들이 있었던 경우 기록을 남깁니다.

## 8진수 2진수
![1212](https://raw.githubusercontent.com/372dev/TIL/main/ALGO/img/b_1212.jpg)

## 최초 시도
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int octNum = sc.nextInt();
        int decNum = 0, i = 0;
        long binNum = 0;
        sc.close();
        if (octNum == 0) {
            System.out.println(0);
        } else {
            while(octNum != 0) {
                decNum += (octNum % 10) * Math.pow(8, i);
                ++i;
                octNum /= 10;
            }
            i = 1;
            while(decNum != 0) {
                binNum += (decNum % 2) * i;
                decNum /= 2;
                i *= 10;
            }
            System.out.println(binNum);
        }
    }
}
```

런타임 에러 발생. 입력 조건에서 수의 길이가 최대 333,334이므로 숫자형 변수는 사용할 수 없고 문자열로 받아와야 한다. 다시 보니 if-else 구문을 넣을 필요는 없었던 것 같다.

## 다른 방법 1
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class Main {
    static char[] twoCharArr;

    public static void main(String args[]) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String eight = br.readLine();
        char[] eightCharArr = eight.toCharArray();

        int twoLen = getPossibleDigitNumber(eightCharArr);
        twoCharArr = new char[twoLen];

        int index = twoLen - 1;
        // 가장 첫 번째 자리(맨뒤의 수) 부터 탐색 시작
        for(int i = eight.length() - 1; i >= 0; i--) {
            char num = eightCharArr[i];
            index = getTwoDigitNumber(num, index);
        }

        System.out.print(new String(twoCharArr));
    }

    // 8진수 숫자 1개 -> 2진수 숫자 3개 변환
    // 2진수의 현재 index 리턴
    static int getTwoDigitNumber(char ch, int nowIndex) {
        int num = ch - '0';

        // 총 3회 반복
        for(int i = 0; i < 3; i++) {
            twoCharArr[nowIndex--] = (char) ((num % 2) + '0');
            num /= 2;

            if(nowIndex < 0) { // 이미 전체 2진수개수를 알고 있으므로 index로 길이 판단.
                break;
            }
        }

        return nowIndex;
    }

    // 8진수를 2진수로 변환했을 때의 2진수의 길이 리턴
    // 배열의 길이를 구하기 위해서 사용
    static int getPossibleDigitNumber(char[] charArr) {
        int len = charArr.length * 3;
        if(len == 0) {
            return 0;
        }

        int firstNum = charArr[0] - '0';
        if(firstNum / 4 > 0) { // 첫 번째 숫자가 3자리 수 가능
            return len;
        }
        if(firstNum / 2 > 0) { // 첫 번째 숫자가 2자리 수 가능
            return len - 1;
        }

        return len - 2;
    }
}
```

-출처 : https://maivve.tistory.com/198

## 다른 방법 2
```java
String[] eight = {"000","001","010","011","100","101","110","111"};
```

위와 같이 각 자리수 변환 경우의 수를 모두 배열에 담거나 아니면 아래와 같이 일일이 작성해서 하드코딩 하는 방법도 있다.

```java
if (a == '0') result = "000";
    else if (a == '1') result = "001";
    else if (a == '2') result = "010";
.
.
.
```