# BAEKJOON 1193 JAVA
* ALGO : 바로 해결하지 못하고 검색해본 알고리즘 또는 해결했지만 더 좋은 방법들이 있었던 알고리즘의 기록을 남깁니다.

## 분수찾기
![1193](https://raw.githubusercontent.com/372dev/TIL/main/ALGO/img/b_1193.JPG)

## 성공
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        sc.close();
        int prevRowsSum = 0;
        int currRow = 1;
        while(true) {
            int currRowMax = prevRowsSum + currRow;
            if(a <= currRowMax) {
                int x = a - prevRowsSum;
                int y = (currRowMax - a) + 1;
                if(currRow % 2 == 0) {
                    System.out.println(x + "/" + y);
                    break;
                } else {
                    System.out.println(y + "/" + x);
                    break;
                }
            } else {
                prevRowsSum += currRow;
                currRow++;
            }
        }
    }
}
```
지그재그로 값이 주어진 순서를 행으로 봤을 때, 각 행의 마지막 열 순번 증가는 삼각수라는 점. 그리고 각 행의 열에 주어진 분자 분모를 더한 값은 동일한 것을 알았으나, 주어진 순번 값으로 해당 행을 찾아가는 방법을 알지 못했다.
아래 글에서 이전 행의 열의 개수를 누적하여 더하는 방법을 찾은 뒤 작성하여 제출, 성공.


## 참고
```java
import java.util.Scanner;
 
public class Main {
 
	public static void main(String[] args) {
 
		Scanner in = new Scanner(System.in);
		int X = in.nextInt();
 
		int cross_count = 1, prev_count_sum = 0;
 
		while (true) {
        
			// 직전 대각선 누적합 + 해당 대각선 개수 이용한 범위 판별
			if (X <= prev_count_sum + cross_count) {	
				
				if (cross_count % 2 == 1) {	// 대각선의 개수가 홀수라면 
					// 분모가 큰 수부터 시작
					// 분모는 대각선 개수 - (X 번째 - 직전 대각선까지의 누적합 - 1) 
					// 분자는 X 번째 - 직전 대각선까지의 누적합 
					System.out.print((cross_count - (X - prev_count_sum - 1)) + "/" + (X - prev_count_sum));
					break;
				} 
				
				else {	// 대각선의 개수가 짝수라면 
					// 홀수일 때의 출력을 반대로 
					System.out.print((X - prev_count_sum) + "/" + (cross_count - (X - prev_count_sum - 1)));
					break;
				}
 
			} else {
				prev_count_sum += cross_count;
				cross_count++;
			}
		}
	}
}
```

- Reference : https://st-lab.tistory.com/74
