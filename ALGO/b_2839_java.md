# BAEKJOON 2839 JAVA
* ALGO : 바로 해결하지 못하고 검색해본 알고리즘 또는 해결했지만 더 좋은 방법들이 있었던 알고리즘의 기록을 남깁니다.

## 설탕 배달
![2839](https://raw.githubusercontent.com/372dev/TIL/main/ALGO/img/b_2839.JPG)

## 성공
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        sc.close();
        int b = -1;
        if(a != 4 && a != 7) {
            int c = a / 5;
            switch (a % 5) {
                case(0): b = c;
                break;
                case(1):
                case(3): b = c + 1;
                break;
                default: b = c + 2;
            }
        }
        System.out.println(b);
    }
}
```

이번에도 kdgyun님의 블로그 Stranger's LAB에 방문하여 힌트를 얻었다. 해결할 방법이 떠오르지 않을 때 이 블로그를 방문하는 이유는 이분의 글이 항상 코드 작성으로 넘어가기 전에 수학적 풀이를 설명해둔다는 것인데, 그걸 읽고 이해가 된다면 코딩은 내가 직접 해볼 수 있어서이다.  
바로 해결하지 못해서 해답을 찾아보았더라도 적어도 코딩은 직접 해본다면, 정답 코드를 읽어보고 푸는 것과 비교해서 다음번에 비슷한 문제가 나왔을 때 내가 혼자서 풀 수 있을 가능성이 높아지지 않을까?

- Reference : https://st-lab.tistory.com/72

블로그 포스트를 읽은 후, 경우의 수를 나열해 규칙을 찾는 과정부터 직접 해보았다.

![2839_2](https://raw.githubusercontent.com/372dev/TIL/main/ALGO/img/b_2839_2.JPG)

## kdgyun님의 풀이방법
```java
import java.io.InputStreamReader;
import java.io.BufferedReader;
import java.io.IOException;
 
public class Main {
 
    public static void main(String[] args) throws IOException {
        
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        
 
        if (N == 4 || N == 7) {
            System.out.println(-1);
        }
        else if (N % 5 == 0) {
            System.out.println(N / 5);
        }
        else if (N % 5 == 1 || N % 5 == 3) {
            System.out.println((N / 5) + 1);
        }
        else if (N % 5 == 2 || N % 5 == 4) {
            System.out.println((N / 5) + 2);
        }
    }
}
```

BufferedReader가 더 빠른건 당연하지만, if-else 구문으로 한 경우가 switch 구문으로 한 경우 보다 빠르고, 입력값을 5로 나누는 등의 작업을 미리 해서 변수에 담아 두기보다 위의 코드처럼 출력시 하는 것이 더 빠르다. 이 점 참고하자.

## 또 다른 풀이 방법
```java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();

        int cnt = 0;
        while(N % 5 != 0 && N>0) {
            N -= 3;
            cnt++;
        }
        if(N%5 != 0) {
            cnt = -1;
        }
        System.out.println(N/5 + cnt);
    }
}
```

문제 유형을 보면

* 수학
* 다이나믹 프로그래밍
* 그리디 알고리즘

세가지가 포함되어 있었다. 제출한 답안이 정답으로 판정되고 나서 다른 사람의 풀이도 찾아보니, 그리디 알고리즘으로 풀어낸 방식들도 있었다. 멋져!

- Reference : https://www.acmicpc.net/source/26430879