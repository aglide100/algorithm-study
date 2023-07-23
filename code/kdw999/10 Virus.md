# 백준 2606번 문제

> 출처: https://www.acmicpc.net/problem/2606

## 문제 설명

신종 바이러스인 웜 바이러스는 네트워크를 통해 전파된다. 

한 컴퓨터가 웜 바이러스에 걸리면 그 컴퓨터와 네트워크 상에서 연결되어 있는 모든 컴퓨터는 웜 바이러스에 걸리게 된다.

예를 들어 7대의 컴퓨터가 <그림 1>과 같이 네트워크 상에서 연결되어 있다고 하자. 

1번 컴퓨터가 웜 바이러스에 걸리면 웜 바이러스는 2번과 5번 컴퓨터를 거쳐 3번과 6번 컴퓨터까지 전파되어 

2, 3, 5, 6 네 대의 컴퓨터는 웜 바이러스에 걸리게 된다. 하지만 4번과 7번 컴퓨터는 1번 컴퓨터와 네트워크상에서 

연결되어 있지 않기 때문에 영향을 받지 않는다.

어느 날 1번 컴퓨터가 웜 바이러스에 걸렸다. 컴퓨터의 수와 네트워크 상에서 서로 연결되어 있는 정보가 주어질 때, 
1번 컴퓨터를 통해 웜 바이러스에 걸리게 되는 컴퓨터의 수를 출력하는 프로그램을 작성하시오.

첫째 줄에는 컴퓨터의 수가 주어진다. 컴퓨터의 수는 100 이하이고 각 컴퓨터에는 1번 부터 차례대로 번호가 매겨진다. 둘째 줄에는 네트워크 상에서 직접 연결되어 있는 컴퓨터 쌍의 수가 주어진다.

이어서 그 수만큼 한 줄에 한 쌍씩 네트워크 상에서 직접 연결되어 있는 컴퓨터의 번호 쌍이 주어진다.

1번 컴퓨터가 웜 바이러스에 걸렸을 때, 1번 컴퓨터를 통해 웜 바이러스에 걸리게 되는 컴퓨터의 수를 첫째 줄에 출력한다.

## 예제 입력
7

6

1 2

2 3

1 5

5 2

5 6

4 7

## 예제 출력
4

## 문제 접근

너비 우선 탐색과 깊이 우선 탐색 방법이 있다.

BFS

컴퓨터 수에 맞춰 2차원 배열을 생성하고 연결 쌍의 갯수와 쌍을 입력한다.

방문 여부 확인을 위한 boolean형 배열을 생성

변수 v에 q값을 넣고 탐색을 시작한다 방문하지 않은 지점을 만나면 그 값을 큐에 넣어서 방문처리하고 count를 증가

## 문제 풀이 코드
```java

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
import java.util.StringTokenizer;
import java.util.*;

public class Virus {

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

		int com = Integer.parseInt(br.readLine()); // 컴퓨터 갯수
		int pair = Integer.parseInt(br.readLine()); // 연결 쌍 갯수 입력
		
		int arr[][] = new int[com+1][com+1]; // 컴퓨터 수로 2차원 배열 생성
		
		for(int i=0; i<pair; i++) {
			StringTokenizer st = new StringTokenizer(br.readLine());
			int num1 = Integer.parseInt(st.nextToken()); // 연결 쌍 입력
			int num2 = Integer.parseInt(st.nextToken());
			arr[num1][num2] = arr[num2][num1] = 1; // 연결 쌍이 1-2, 2-1이 같은 경우라 
		}
		
		Queue<Integer> q = new LinkedList<>(); // 큐 활용
		boolean visit[] = new boolean[com+1]; // 인접한 컴퓨터를 골라내기 위한 boolean 배열
		
		q.add(1);
		visit[1] = true;
		
		int count = 0;
		while(!q.isEmpty()) { // 큐가 비어있지 않을 경우 반복
			int v = q.poll(); // 큐 맨앞에 있는 값 반환 후 삭제
			
			for(int i=1; i<=com; i++) {
				if(arr[v][i] == 1 && !visit[i]) {
					visit[i] = true;
					q.add(i);
					count++;
				}
			}
		}
		System.out.println(count);
	}

}
