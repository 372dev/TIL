# BAEKJOON 2798 JAVA
* ALGO : 바로 해결하지 못하고 검색해본 알고리즘 또는 해결했지만 더 좋은 방법들이 있었던 알고리즘의 기록을 남깁니다.

## 블랙잭
![2798](https://raw.githubusercontent.com/372dev/TIL/main/ALGO/img/b_2798.JPG)

## 첫번째 시도
```java
import java.util.Arrays;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a, sum;
        a = sc.nextInt();
        sum = sc.nextInt();
        int[] arr = new int[a];
        for (int i = 0; i < a; i++) {
            arr[i] = sc.nextInt();
        }
        sc.close();

        Arrays.sort(arr);

        int result = 3;

        for (int i = 0; i < a - 2; i++) {
            int ptr1 = i + 1, ptr2 = a - 1;
            // While there could be more pairs to check
            while (ptr1 < ptr2) {
                // Calculate the sum of the current triplet
                int temp = arr[i] + arr[ptr1] + arr[ptr2];

                // If the sum is more closer than
                // the current closest sum
                if (Math.abs(sum - temp) < Math.abs(sum - result)) {
                    result = temp;
                }
                // If sum is greater then x then decrement
                // the second pointer to get a smaller sum
                if (temp > sum) {
                    ptr2--;
                }
                // Else increment the first pointer
                // to get a larger sum
                else {
                    ptr1++;
                }
            }
        }
        System.out.println(result);
    }
}
```
geeksforgeeks을 참고하여 작성했다.
처음으로 풀어보는 부르트 포스 문제이다. 예제를 실행해본 결과는 정답이 나왔지만 제출 후 판정은 실패가 떴다.

- Reference : https://www.geeksforgeeks.org/find-a-triplet-in-an-array-whose-sum-is-closest-to-a-given-number/

## 두번째 시도
```java
import java.util.Arrays;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a, sum;
        a = sc.nextInt();
        sum = sc.nextInt();
        int[] arr = new int[a];
        for (int i = 0; i < a; i++) {
            arr[i] = sc.nextInt();
        }
        sc.close();
        Arrays.sort(arr);
        int result = test(arr, a, sum);
        System.out.println(result);
    }

    static int test(int[] arr, int a, int sum) {
        int result = 3;

        for (int i = 0; i < a - 2; i++) {
            if(result == sum) return result;
            int p1 = i + 1, p2 = a - 1;
            while (p1 < p2 && result != sum) {
               int temp = arr[i] + arr[p1] + arr[p2];
               if ((sum >= temp)&&(sum - temp < sum - result)) {
                    result = temp;
               }
               if (temp > sum) {
                    p2--;
               } else {
                    p1++;
               }
            }
        }
        return result;
    }
}
```

성공. 메서드를 분리했고, 불필요한 반복문 실행을 줄이려 중간에 조건문과 return을 넣었다. 첫번째 시도에서 세 값의 합과 목표 값의 비교에서 음수가 나올 수 있는게 실패 판정의 원인이 아닐까 싶다. 참고한 원문에서는 음수 입력값도 있고 목표값을 초과하더라도 가장 가까운 값을 찾는 요구사항에 따라 절대값으로 변경 후 비교하는 로직이었는데 여기에서는 정수만 주어졌다. 때문에 세 값의 합이 목표값을 넘어가지 않아야 한다는 조건을 추가했다.
