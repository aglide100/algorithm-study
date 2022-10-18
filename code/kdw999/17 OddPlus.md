# SWEA 2072번 문제

> 출처:https://swexpertacademy.com/main/code/problem/problemDetail.do

## 문제 설명
10개의 수를 입력 받아, 그 중에서 홀수만 더한 값을 출력하는 프로그램을 작성하라.

각 수는 0 이상 10000 이하의 정수이다.

가장 첫 줄에는 테스트 케이스의 개수 T가 주어지고, 그 아래로 각 테스트 케이스가 주어진다.

각 테스트 케이스의 첫 번째 줄에는 10개의 수가 주어진다.

출력의 각 줄은 '#t'로 시작하고, 공백을 한 칸 둔 다음 정답을 출력한다.

(t는 테스트 케이스의 번호를 의미하며 1부터 시작한다.)

## 예제 입력
3
3 17 1 39 8 41 2 32 99 2
22 8 5 123 7 2 63 7 3 46
6 63 2 3 58 76 21 33 8 1 

## 예제 출력
#1 200
#2 208
#3 121

## 문제 접근
테스트 케이스와 10개 숫자 입력은 스캐너로 입력하고 입력한 숫자들은 배열에 저장한다. 

2차원 배열이라 이중 for문을 사용하였고 홀수를 구분하기 위해 2로 나눴을 때 나머지가 0이 아닌 조건을 사용하였다.

## 문제 풀이 코드
```java

import java.util.*;

public class OddPlus {

	public static void main(String[] args) {

		Scanner sc = new Scanner(System.in);
		
		int T = sc.nextInt();
		
		int arr[][] = new int[T][10]; // 뒤에 몇행 몇열인지는 확실히
		int sum[] = new int[T];
		
		for(int i=0; i<T; i++) {
			for(int j=0; j<10; j++) {
				arr[i][j] = sc.nextInt();
				
				if(arr[i][j] % 2 != 0) {
					sum[i] += arr[i][j];
				}
			}
		}
		
		for(int i=0; i<T; i++) {
		System.out.println("#"+(i+1)+ " "+sum[i]);
		}
	}

}
