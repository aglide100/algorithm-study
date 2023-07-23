# 백준 4344번 문제

> 출처: https://www.acmicpc.net/problem/2869

## 문제 설명

땅 위에 달팽이가 있다. 이 달팽이는 높이가 V미터인 나무 막대를 올라갈 것이다.

달팽이는 낮에 A미터 올라갈 수 있다. 하지만, 밤에 잠을 자는 동안 B미터 미끄러진다. 또, 정상에 올라간 후에는 미끄러지지 않는다.

달팽이가 나무 막대를 모두 올라가려면, 며칠이 걸리는지 구하는 프로그램을 작성하시오.

## 예제 입력
1. 2 1 5

2. 5 1 6

## 예제 출력
1. 4

2. 2

## 문제 접근

겉으론 스캐너를 사용하여 올라가는 높이, 미끄러지는 높이, 총 높이, 며칠 걸리는 지 받는 변수를 반복문으로 돌리면 쉽게 풀릴거라 생각했으나 

그럴 경우 돌아가기는 하나 시간 초과가 나오게 된다.

문제 정답률이 생각보다 낮았던 이유가 이런 이유였던 것 같다.

속도를 높이기 위해서 일단 반복문을 쓰지 않고 단순 계산식으로 답을 도출하고 스캐너보다 처리 속도가 빠른 버퍼를 사용하는 법을 참고하였다.


## 문제 풀이 코드
```java

import java.util.*;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
import java.util.StringTokenizer;


public class Snail {

	public static void main(String[] args) throws IOException {  // 버퍼를 쓰기위한 예외처리
		
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine(), " "); 
		// read한 데이터는 Line 단위로만 나눠져 입력한 값을 공백 단위로 나누려면 StringTokenizer 사용
		
		
		// readLine()은 자료형이 String만 가능하다, 다른 자료형 쓰려면 형변환
        int A = Integer.parseInt(st.nextToken()); // 올라가는 높이
        int B = Integer.parseInt(st.nextToken()); // 미끄러지는 높이
        int V = Integer.parseInt(st.nextToken()); // 총 높이
		    int count; // 며칠 걸렸는지 받는 변수
		
		count = (V - B) /  (A - B); 
		// 문제 조건 중 정상에 도달하면 미끄러지지 않는다는 조건이 있다.
		// 해당 조건이 없다면 V / (A-B)의 식이 가능하나 
		// 2 1 5로 예를 들었을 경우 5 / (2-1) = 5로 올라가는데 5일이 걸린다는 계산이 나온다.
		// 그러나 미끄러지지 않는 경우엔 실제로 4일 밖에 걸리지 않는다.
		// 그래서 총 높이 V에서 미끄러지는 높이 B를 빼주어서 계산식이 떨어지게 해준다. (하루를 빼준다는 느낌)
		
		if((V - B) % (A - B) !=0) { // 위의 계산식 에서 나머지가 0으로 딱 떨어진다면 며칠이 걸렸는지 바로 나오나
			                        // 나머지가 0이 아닐 경우 다음 날 한 번 더 올라가야 하기 때문에 하루를 추가해준다.
			count++;
		}
		
		System.out.println(count);

	}
}
