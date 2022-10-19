# 백준 2525번 문제

> 출처: https://www.acmicpc.net/problem/2525

## 문제 설명
강호는 코딩 교육을 하는 스타트업 스타트링크에 지원했다. 오늘은 강호의 면접날이다. 하지만, 늦잠을 잔 강호는 스타트링크가 있는 건물에 늦게 도착하고 말았다.

스타트링크는 총 F층으로 이루어진 고층 건물에 사무실이 있고, 스타트링크가 있는 곳의 위치는 G층이다. 

강호가 지금 있는 곳은 S층이고, 이제 엘리베이터를 타고 G층으로 이동하려고 한다.

보통 엘리베이터에는 어떤 층으로 이동할 수 있는 버튼이 있지만, 강호가 탄 엘리베이터는 버튼이 2개밖에 없다. 

U버튼은 위로 U층을 가는 버튼, D버튼은 아래로 D층을 가는 버튼이다. (만약, U층 위, 또는 D층 아래에 해당하는 층이 없을 때는, 엘리베이터는 움직이지 않는다)

강호가 G층에 도착하려면, 버튼을 적어도 몇 번 눌러야 하는지 구하는 프로그램을 작성하시오. 

만약, 엘리베이터를 이용해서 G층에 갈 수 없다면, "use the stairs"를 출력한다.

첫째 줄에 F, S, G, U, D가 주어진다. (1 ≤ S, G ≤ F ≤ 1000000, 0 ≤ U, D ≤ 1000000) 건물은 1층부터 시작하고, 가장 높은 층은 F층이다.

첫째 줄에 강호가 S층에서 G층으로 가기 위해 눌러야 하는 버튼의 수의 최솟값을 출력한다. 만약, 엘리베이터로 이동할 수 없을 때는 "use the stairs"를 출력한다.
## 예제 입력
10 1 10 2 1

100 2 1 1 0

## 예제 출력
6

use the stairs

## 문제 접근

시작 위치에서 BFS 탐색 방법을 사용하여 각 층을 다 확인한다.

## 문제 풀이 코드
```java

import java.util.*;

public class StartLink {

	static int F, S, G, U, D; // bfs 메소드에서도 사용하기 위해 클래스에서 선언
	static int move_Sum[];
	static int updown[] = new int[2];
	
	
	public static void main(String[] args) {

		Scanner sc = new Scanner(System.in);
		
		 F = sc.nextInt();
		 S = sc.nextInt();
		 G = sc.nextInt();
		 updown[0] = sc.nextInt();
		 updown[1] = -sc.nextInt();
		
		move_Sum = new int[F+1]; 
		bfs(S);

		// 배열은 for문 안에서 초기화해줘도 전역에서도 사용 가능..?
		// int형 변수는 for문 안에서 설정해주면 전역에서 저장되지 않는다..?
	}
	
	static void bfs(int st) {
		Queue<Integer> q = new LinkedList<>();
		boolean check[] = new boolean[F+1];
		
		q.add(st); // bfs메소드의 매개변수 current = S값(시작 위치), 현재 위치를 큐에 삽입
		check[st] = true; // 현재 층은 true로 해줌
		move_Sum[st] = 0;
	
	
		while(!q.isEmpty()) { // 문자열의 길이가 0이면 true 반환, 큐가 비어있지 않다면
			int position = q.poll(); // 큐 맨 앞에 있는 값 반환 후 삭제, position에 큐 맨 앞 값이 들어감
			                    // 큐가 비어있을 경우 null 반환

			if(position == G) { // 현재 위치가 G와 같다면
				System.out.println(move_Sum[position]); // 움직인 총 횟수 출력
				return; // 후 값 리턴
			}
		
			for(int i=0; i<2; i++) {
				int next = position + updown[i]; // next에 현재 층에서 up, down한 값을 대입
				
				if(next > F || next <1){  
                continue; // next가 최고층 보다 크거나 0층으로 가게되면 다음 반복문 실행
				}
				
				if(!check[next]) { // 현재 위치가 true가 아닐 시, 안가본 층일 경우
					check[next] = true; // true로 바꾸어서 확인한 층임을 표시
					q.add(next); // 안가본 층이므로 확인하기 위해 큐에 삽입
					move_Sum[next] = move_Sum[position]+1; // position의 경우는 항상 현재 층을 갖고 있다
					                                       // next는 현재 층에서 up하거나 down한 층
					
					// Ex) 10 1 5 2 1의 경우 첫 시작 시
					// move_Sum[3] = move_Sum[1]+1가 된다 move_sum[1] = 0
					// for문을 한 바퀴 돌고 다시 while문 맨 위에서 시작하게 되면 position은 큐에서 3을 받는다 
					// 그 후 다시 for문이 실행되면 이 때 next는 5(up), 2(down)가 된다.
					// 그럼 5, 2는 큐에 들어가게 되고 
					// move_Sum[5] = move_Sum[3]+1
					// move_Sum[2] = move_Sum[3]+1 가 된다. 
					// move_Sum[3]은 앞선 반복문에서 1이기 때문에 위에 두 배열의 값들은 2가된다.
					// 이런 식으로 하나 씩 탐색하면서 움직인 횟수를 카운팅한다.
				}
			}
		}
		System.out.println("use the stairs");
	}
}
