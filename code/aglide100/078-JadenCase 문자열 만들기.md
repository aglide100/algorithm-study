# 프로그래머스, JadenCase 문자열 만들기

> 출처: https://school.programmers.co.kr/learn/courses/30/lessons/12951

## 문제 설명

JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 단, 첫 문자가 알파벳이 아닐 때에는 이어지는 알파벳은 소문자로 쓰면 됩니다. (첫 번째 입출력 예 참고)  
문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

##### 제한 조건

-   s는 길이 1 이상 200 이하인 문자열입니다.
-   s는 알파벳과 숫자, 공백문자(" ")로 이루어져 있습니다.
    -   숫자는 단어의 첫 문자로만 나옵니다.
    -   숫자로만 이루어진 단어는 없습니다.
    -   공백문자가 연속해서 나올 수 있습니다.

##### 입출력 예

| s                       | return                  |
| ----------------------- | ----------------------- |
| "3people unFollowed me" | "3people Unfollowed Me" |
| "for the last week"     | "For The Last Week"     |

---

※ 공지 \- 2022년 1월 14일 제한 조건과 테스트 케이스가 추가되었습니다.

# 문제 접근

입출력 예의 따라간다면 정답인 문제이다.

이를 위해서 공백, 숫자, 알파벳의 구별을 위해 아스키코드로 변환해서 체크하는 로직을 이용하였다.

# 문제 풀이 코드

java

```java
class Solution {
    public String solution(String s) {
        String answer = "";
        // a-97, z-122, A-65, Z-90, ' '-32, 1-49, 9-57

        boolean continues = false;
        for (char c:s.toCharArray()) {
            if ((int)c == 32) {
                continues = false;
                answer += " ";
                continue; // 공백
            }

            if ((int)c >= 49 && (int)c <= 57) {
                if (!continues) {
                    continues = true;
                }
                answer += c + "";
                continue; // 숫자
            }

            if (!continues) {
                if ((int)c >= 97 && (int)c <= 122) {
                    int newC = (int)c - 32;
                    answer += (char)newC + "";
                } else {
                    answer += c + "";
                }

                continues = true;
            } else {
                if ((int)c >= 65 && (int)c <= 90) {
                    int newC = (int)c + 32;
                    answer += (char)newC + "";
                } else {
                    answer += c + "";
                }
            }
        }
        return answer;
    }
}
```
