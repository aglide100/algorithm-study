# SWEA 1206번 문제

> 출처:https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV134DPqAA8CFAYh

## 문제 설명
강변에 빌딩들이 옆으로 빽빽하게 밀집한 지역이 있다.

이곳에서는 빌딩들이 너무 좌우로 밀집하여, 강에 대한 조망은 모든 세대에서 좋지만 왼쪽 또는 오른쪽 창문을 열었을 때 바로 앞에 옆 건물이 보이는 경우가 허다하였다.

그래서 이 지역에서는 왼쪽과 오른쪽으로 창문을 열었을 때, 양쪽 모두 거리 2 이상의 공간이 확보될 때 조망권이 확보된다고 말한다.

빌딩들에 대한 정보가 주어질 때, 조망권이 확보된 세대의 수를 반환하는 프로그램을 작성하시오.

[제약 사항]

가로 길이는 항상 1000이하로 주어진다.

맨 왼쪽 두 칸과 맨 오른쪽 두 칸에는 건물이 지어지지 않는다. (예시에서 빨간색 땅 부분)

각 빌딩의 높이는 최대 255이다.
 
[입력]

총 10개의 테스트케이스가 주어진다.

각 테스트케이스의 첫 번째 줄에는 건물의 개수 N이 주어진다. (4 ≤ N ≤ 1000)

그 다음 줄에는 N개의 건물의 높이가 주어진다. (0 ≤ 각 건물의 높이 ≤ 255)

맨 왼쪽 두 칸과 맨 오른쪽 두 칸에 있는 건물은 항상 높이가 0이다. (예시에서 빨간색 땅 부분)
 
[출력]

#부호와 함께 테스트케이스의 번호를 출력하고, 공백 문자 후 조망권이 확보된 세대의 수를 출력한다.

## 예제 입력


## 예제 출력


## 문제 접근
해당 건물의 높이와 -2, -1, +1, +2번째 건물의 높이를 비교 후 해당 건물의 높이가 제일 크다면 그 차이만큼 더해준다.

Math.max 사용 시 쉽게 해결할 수 있다.

## 문제 풀이 코드
```java

import java.util.*;

public class View {

	public static void main(String[] args) {

		Scanner sc = new Scanner(System.in);
		
		int tc = 1;
		int n;
		int []bd;
		
		for(int i=1; i<=tc; i++) { // 10번의 테스트 케이스
			n = sc.nextInt(); // 건물 개수 = 가로 길이
			bd = new int[n];
		    for(int j=0; j<n; j++) {
		    	bd[j] = sc.nextInt();
		    }
		    
		    int count =0;
		    for(int j=2; j< n-2; j++) { // 앞, 뒤 2구역은 건물 안지음
		    	int max = Math.max(bd[j-2], Math.max(bd[j-1], Math.max(bd[j+1], bd[j+2])));
		        if(bd[j]- max > 0) {
		        	count += bd[j]-max;
		        }
		    
		    }
		        System.out.println("#"+i+" "+ count);
		}
	}
}
