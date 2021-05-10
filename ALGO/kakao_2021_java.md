# KAKAO 채용연계형 인턴십 for Tech Developers 코딩테스트
* ALGO : 바로 해결하지 못하고 검색해본 알고리즘 또는 해결했지만 더 좋은 방법들이 있었던 알고리즘의 기록을 남깁니다.

## 1. 숫자놀이

### 제출한 답
```java
class Solution {
    public int solution(String s) {
        String reg0 = "zero",
                reg1 = "one",
                reg2 = "two",
                reg3 = "three",
                reg4 = "four",
                reg5 = "five",
                reg6 = "six",
                reg7 = "seven",
                reg8 = "eight",
                reg9 = "nine";
        s = s.replaceAll(reg0, "0");
        s = s.replaceAll(reg1, "1");
        s = s.replaceAll(reg2, "2");
        s = s.replaceAll(reg3, "3");
        s = s.replaceAll(reg4, "4");
        s = s.replaceAll(reg5, "5");
        s = s.replaceAll(reg6, "6");
        s = s.replaceAll(reg7, "7");
        s = s.replaceAll(reg8, "8");
        s = s.replaceAll(reg9, "9");
        int answer = Integer.parseInt(s);
        return answer;
    }
}
```
통과

### 문제 해설
```java
업데이트 예정
```

## 2. 대기실 거리두기

### 제출한 답
```java
class Solution {
    public int[] solution(String[][] places) {
        int[] answer = {1,1,1,1,1};
        for(int i=0; i<5; i++) {
            for(int j=0; j<5; j++) {
                places[i][j] = "X" + places[i][j] + "X";
            }
        }
        for(int i=0; i<5; i++) {
            String[] temp = {"XXXXXXX","","","","","","XXXXXXX"};
            for(int m=0; m<5; m++) {
                temp[m+1] = places[i][m];
            }
            for (int j = 1; j < 6; j++) {
                if (answer[i] == 0) break;
                for (int k = 1; k < 6; k++) {
                    if (temp[j].charAt(k) == 'P') {
                        if (temp[j].charAt(k-1) == 'P'
                                || temp[j].charAt(k+1) == 'P'
                                || temp[j-1].charAt(k) == 'P'
                                || temp[j+1].charAt(k) == 'P') {
                            answer[i] = 0;
                        }
                    } else if (temp[j].charAt(k) == 'O') {
                        int pcount = 0;
                        if (temp[j].charAt(k-1) == 'P') pcount++;
                        if (temp[j].charAt(k+1) == 'P') pcount++;
                        if (temp[j-1].charAt(k) == 'P') pcount++;
                        if (temp[j+1].charAt(k) == 'P') pcount++;
                        if (pcount > 1) {
                            answer[i] = 0;
                            break;
                        }
                    }
                }
            }
        }
        return answer;
    }
}
```
통과

### 문제 해설
```java
업데이트 예정
```

## 3. 행 선택, 삭제, 복구

### 제출한 답
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.StringTokenizer;

class Solution {
    public String solution(int n, int k, String[] cmd) {
        ArrayList<String> memory = new ArrayList<String>();
        char[] array = new char[n];
        Arrays.fill(array, 'O');
        for(int i = 0; i < cmd.length; i++) {
            StringTokenizer st = new StringTokenizer(cmd[i]);
            String token = st.nextToken();
            if(token.equals("U") && st.hasMoreTokens()) {
                int x = Integer.valueOf(st.nextToken());
                for(int j = 0; j < x; j++) {
                    k--;
                    while(array[k] == 'X') k--;
                }
            }
            if(token.equals("D") && st.hasMoreTokens()) {
                int x = Integer.valueOf(st.nextToken());
                for(int j = 0; j < x; j++) {
                    k++;
                    while(array[k] == 'X') k++;
                }
            }
            if(token.equals("C")) {
                array[k] = 'X';
                memory.add(String.valueOf(k));
                while(k < n-1 && array[k] == 'X') {
                    k++;
                }
                while(k > 0 && array[k] == 'X') {
                    k--;
                }
            }
            if(token.equals("Z")) {
                int lastIndex = memory.size()-1;
                int tempInt = Integer.parseInt(memory.get(lastIndex));
                array[tempInt] = 'O';
                memory.remove(lastIndex);
            }
        }
        return new String(array);
    }
}
```
정확도 테스트 통과, 효율성 테스트 실패

### 문제 해설
```java
업데이트 예정
```