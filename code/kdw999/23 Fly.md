# SWEA 2001번 문제

> 출처:https://swexpertacademy.com/main/code/problem/problemDetail.do

## 문제 설명
N x N 배열 안의 숫자는 해당 영역에 존재하는 파리의 개수를 의미한다.

아래는 N=5 의 예이다.

![image](https://user-images.githubusercontent.com/84887939/202995202-04bb98dd-c985-4211-8b97-da73bb0312e6.png)

M x M 크기의 파리채를 한 번 내리쳐 최대한 많은 파리를 죽이고자 한다.

죽은 파리의 개수를 구하라!

예를 들어 M=2 일 경우 위 예제의 정답은 49마리가 된다.

![image](https://user-images.githubusercontent.com/84887939/202995289-2f6758d4-17da-4410-b9da-3a6f3d120bf1.png)


[제약 사항]

1. N 은 5 이상 15 이하이다.

2. M은 2 이상 N 이하이다.

3. 각 영역의 파리 갯수는 30 이하 이다.


[입력]

가장 첫 줄에는 테스트 케이스의 개수 T가 주어지고, 그 아래로 각 테스트 케이스가 주어진다.

각 테스트 케이스의 첫 번째 줄에 N 과 M 이 주어지고,

다음 N 줄에 걸쳐 N x N 배열이 주어진다.


[출력]

출력의 각 줄은 '#t'로 시작하고, 공백을 한 칸 둔 다음 정답을 출력한다.

(t는 테스트 케이스의 번호를 의미하며 1부터 시작한다.)

## 예제 입력

1

4
 

## 예제 출력

#1

1

1 1

1 2 1

1 3 3 1

## 문제 접근
for문 반복사용으로 계산하기 헷갈리나 파리채가 M x M 크기의 사각형이라 M x M 크기의 배열들을 다 비교해준 뒤 가장 큰 값을 출력해준다.

## 문제 풀이 코드
```java

import java.util.Scanner;

public class Fly {

	public static void main(String args[]) throws Exception {
		   Scanner sc = new Scanner(System.in);
		
		   int T = sc.nextInt();
		   
		   for(int i=0; i<T; i++) {
		   int N = sc.nextInt();
		   int M = sc.nextInt();
		   
		   int [][]arr= new int[N][N];
		   
		   for(int j=0; j<N; j++) {
			   for(int k=0; k<N; k++) {
				
				arr[j][k] = sc.nextInt();   
			   }   
		   }
		   
		   int max = 0;
		  
		   for(int a=0; a<N-M+1; a++) {
			   for(int b=0; b<N-M+1; b++){
				   int sum = 0;	   
				   for(int c=0; c<M; c++) {
					   for(int d=0; d<M; d++) {
						   sum += arr[a+c][b+d];
					   }
				   }
				   
				   if(max<sum) {
					   max = sum;
				   }
				   }
			   }
		   System.out.println("#"+(i+1) +" " + max);
		   }
		}
	}
