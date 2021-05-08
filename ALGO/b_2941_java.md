# BAEKJOON 2941 JAVA
* ALGO : 바로 해결하지 못하고 검색해본 알고리즘 또는 해결했지만 더 좋은 방법들이 있었던 알고리즘의 기록을 남깁니다.

## 크로아티아 알파벳
![2941](https://raw.githubusercontent.com/372dev/TIL/main/ALGO/img/b_2941.JPG)

## 첫번째 시도
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
public class Main {
    public static void main(String[] g) throws Exception {
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        String a = br.readLine();
        int c = a.length();
        for(int i = 0; i < a.length() - 1; i++) {
            if(i > 0 && a.charAt(i) == 'z' && a.charAt(i-1) == 'd') {
                if (a.charAt(i + 1) == '=') c-=2;
            } else if(a.charAt(i) == 's' || a.charAt(i) == 'z') {
                if (a.charAt(i + 1) == '=') c--;
            } else if(a.charAt(i) == 'c') {
                if (a.charAt(i + 1) == '=') c--;
                if (a.charAt(i + 1) == '-') c--;
            } else if(a.charAt(i) == 'd') {
                if (a.charAt(i + 1) == '-') c--;
            } else if(a.charAt(i) == 'l' || a.charAt(i) == 'n') {
                if (a.charAt(i + 1) == 'j') c--;
            }
        }
        System.out.print(c);
    }
}
```
성공했으나 RegEx를 이용한 간단한 방법이 있었다.

## 다른 사람의 풀이
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String str = sc.nextLine();
        String regExp = "c=|c-|dz=|d-|lj|nj|s=|z=";
        String r = str.replaceAll(regExp, "n");
        System.out.print(r.length());
    }   
}
```

Pattern, Matcher, replaceAll 등을 활용하여 String 코딩의 활용도를 높이자!