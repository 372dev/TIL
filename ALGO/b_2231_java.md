# BAEKJOON 2231 JAVA
* ALGO : 바로 해결하지 못하고 검색해본 알고리즘 또는 해결했지만 더 좋은 방법들이 있었던 알고리즘의 기록을 남깁니다.

## 분해합
![2231](https://raw.githubusercontent.com/372dev/TIL/main/ALGO/img/b_2231.JPG)

## 첫번째 시도
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        sc.close();
        String b = String.valueOf(a);
        int l = b.length();
        int r = 0;
        for(int i = a - (l * 9); i < a; i++) {
            int sum = 0;
            String c = String.valueOf(i);
            for(int j = 0; j < c.length(); j++) {
                sum += (int)c.charAt(j) - 48;
            }
            if (i + sum == a) {
                r = i;
                break;
            }
        }
        System.out.println(r);
    }
```
아직 브루트 포스 알고리즘에 익숙치 않다. 이번에도 아래 코드의 출처 링크에 있는 블로그에서 도움을 받았다. 항상 글 위쪽에 힌트를 주셔서 그 힌트만 읽고 직접 코드를 짜볼 수 있어서 감사하다. 글쓴이께서 작성하신 코드도 아래에 링크와 함께 첨부한다.

## 다른 풀이
```java
import java.util.Scanner;
 
public class Main {
	public static void main(String[] args) {
    
		Scanner in = new Scanner(System.in);
    
		// 자릿수의 길이를 알기위해 일단 문자열로 입력받는다.
		String str_N = in.nextLine();
 
		// 해당 문자열의 길이 변수
		int N_len = str_N.length();
 
		// 문자열을 정수(int)로 변환 
		int N = Integer.parseInt(str_N);
		int result = 0;
 
		
		// i 는 가능한 최솟값인 N - 9 * N의 각 자릿수부터 시작 
		for(int i = (N - (N_len * 9)); i < N; i++) {
			int number = i;
			int sum = 0;	// 각 자릿수 합 변수 
			
			while(number != 0) {
				sum += number % 10;	// 각 자릿수 더하기
				number /= 10;
			}
			
			// i 값과 각 자릿수 누적합이 같을 경우 (생성자를 찾았을 경우) 
			if(sum + i == N) {
				result = i;
				break;
			}
			
		}
 
		System.out.println(result);
	}
 
}
```