# 프로그래머스, H-Index

> 출처: https://school.programmers.co.kr/learn/courses/30/lessons/42747

## 문제 설명

H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과[1](#fn1)에 따르면, H-Index는 다음과 같이 구합니다.

어떤 과학자가 발표한 논문 `n`편 중, `h`번 이상 인용된 논문이 `h`편 이상이고 나머지 논문이 h번 이하 인용되었다면 `h`의 최댓값이 이 과학자의 H-Index입니다.

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

* 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
* 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.

##### 입출력 예

| citations | return |
| --- | --- |
| \[3, 0, 6, 1, 5\] | 3   |

##### 입출력 예 설명

이 과학자가 발표한 논문의 수는 5편이고, 그중 3편의 논문은 3회 이상 인용되었습니다. 그리고 나머지 2편의 논문은 3회 이하 인용되었기 때문에 이 과학자의 H-Index는 3입니다.

##### 문제가 잘 안풀린다면😢

힌트가 필요한가요? \[코딩테스트 연습 힌트 모음집\]으로 오세요! → [클릭](https://school.programmers.co.kr/learn/courses/14743?itm_content=lesson42747)

※ 공지 \- 2019년 2월 28일 테스트 케이스가 추가되었습니다.

* * *

1.  [https://en.wikipedia.org/wiki/H-index](https://en.wikipedia.org/wiki/H-index) "위키백과" [↩](#fnref1)
# 문제 접근

본 문제는 제목 그대로 H-Index를 구하는 문제이다. 이에 대해서 자세한 설명은 친절하게도 위키의 링크를 통해서 설명하고 있다.

H-Index란 문제설명처럼 n편 중 h 번 이상 인용된 논문이 h편이상이고 나머지 논문이 h번 이하 인용되었을 때 h의 최댓값을 구하는 것이다.

이를 수식으로 표현하자면 아래와 같다

내림차순으로 정렬되었을 때 max값이 문제에서 요구하는 H-Index이다.

<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/d94958e3aa230763f408edfe59576e00a3688583" />

H-Index를 구하는 것을 알았지만 반례가 여럿 존재한다.

인용이 0으로만 이루어진 경우([0,0,0,0]),
인용과 index값이 같은 경우가 있다.

이 둘만 조심한다면 문제는 쉽게 해결이 된다.

# 문제 풀이 코드

java

```java
import java.util.*;

class Solution {
    public int solution(int[] citations) {
        int answer = 0;
        
        // 내림차순 정렬
        Integer[] tmp = Arrays.stream(citations).boxed().toArray(Integer[]::new);
        Arrays.sort(tmp, Comparator.reverseOrder());
        
        for (int i=0; i<tmp.length; i++) {
            if (tmp[i] >= i) {
                if (tmp[i] == 0) {
                    // 인용이 0일 경우
                    break;
                } else if (tmp[i] == i) {
                    // 테케 11번, h-index가 같을 경우도 있을지도
                    answer = i;
                } else {
                    answer = i + 1;  
                }
            }
        }
        
        return answer;
    }
}

```
