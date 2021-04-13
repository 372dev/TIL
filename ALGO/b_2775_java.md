# BAEKJOON 2775 JAVA
* ALGO : 바로 해결하지 못하고 검색해본 알고리즘 또는 해결했지만 더 좋은 방법들이 있었던 알고리즘의 기록을 남깁니다.

## 부녀회장이 될테야
![2775](https://raw.githubusercontent.com/372dev/TIL/main/ALGO/img/b_2775.JPG)

## 성공
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int t = sc.nextInt();
        int[][] apt = new int[15][15];
        for(int i = 1; i < 15; i++) {
            apt[i][1] = 1;
            apt[0][i] = i;
        }
        for (int i = 1; i < 15; i++) {
            for(int j = 2; j < 15; j++) {
                apt[i][j] = apt[i][j-1] + apt[i-1][j];
            }
        }
        for(int i = 0; i < t; i++) {
            int k = sc.nextInt();
            int n = sc.nextInt();
            System.out.println(apt[k][n]);
        }
        sc.close();
    }
}
```

배열을 사용하면 될 것을, 수식으로 만드려고 연습장만 가득 채웠다. 결국 코딩은 손도 못대고 자주 찾는 블로그에서 해답을 얻어 풀었다. 문제안에 답이 있다. 다시한번 들여다 보자.

- Reference : https://st-lab.tistory.com/78