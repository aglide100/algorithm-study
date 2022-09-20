# 백준 1931번 문제

> 출처: https://www.acmicpc.net/problem/1931

## 문제 설명

한 개의 회의실이 있는데 이를 사용하고자 하는 N개의 회의에 대하여 회의실 사용표를 만들려고 한다.

각 회의 I에 대해 시작시간과 끝나는 시간이 주어져 있고, 각 회의가 겹치지 않게 하면서 회의실을 사용할 수 있는 회의의 최대 개수를 찾아보자. 

단, 회의는 한번 시작하면 중간에 중단될 수 없으며 한 회의가 끝나는 것과 동시에 다음 회의가 시작될 수 있다. 

회의의 시작시간과 끝나는 시간이 같을 수도 있다. 이 경우에는 시작하자마자 끝나는 것으로 생각하면 된다.

첫째 줄에 회의의 수 N(1 ≤ N ≤ 100,000)이 주어진다. 

둘째 줄부터 N+1 줄까지 각 회의의 정보가 주어지는데 이것은 공백을 사이에 두고 회의의 시작시간과 끝나는 시간이 주어진다. 

시작 시간과 끝나는 시간은 231-1보다 작거나 같은 자연수 또는 0이다.

첫째 줄에 최대 사용할 수 있는 회의의 최대 개수를 출력한다.

## 예제 입력

11

1 4

3 5

0 6

5 7

3 8

5 9

6 10

8 11

8 12

2 13

12 14


## 예제 출력
4

## 문제 접근

배열을 활용하여 회의 시작시간과 종료시간을 저장 후 Comparator와 sort로 시작,종료시간을 비교, 정렬한다.

정렬 후 변수 endTime을 통해 종료시간과 시작시간을 비교해 시작시간이 크거나 같을 경우 카운팅한다.

## 문제 풀이 코드
```java

import java.util.*;
import java.util.Comparator;
import java.util.Arrays;

public class ConferRoomDistribute {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		int i, count=0;
		i = sc.nextInt(); // 회의실 갯수
		
		int arr[][] = new int[i][2]; 
		
		for(int j=0; j<i; j++) {
			int k = sc.nextInt();
			int l = sc.nextInt();
			
			arr[j][0] = k; // 회의 시작시간
		    arr[j][1] = l; // 회의 종료시간
			
		}
		
		
		// 종료 시간을 정렬해서 비교
		// 회의의 시작시간과 종료시간을 삽입한 2차원 배열을 비교하기 위해 Comparator 사용
		// 기존엔 부등호로 비교를 하나 비교 객체가 여러 개일 경우 Comparator 등을 사용
		Arrays.sort(arr, new Comparator<int[]>(){
			
			
			public int compare(int[] a1, int[] a2) { //Comparator 인터페이스를 사용하기 위해 compare 메소드 정의
				
				// a1은 선행 매개변수, a2는 후행 매개변수
				if(a1[1] == a2[1]) { // 종료 시간이 같을 경우
					return a1[0] - a2[0]; // 시작 시간이 빠른 순으로 정렬
				}
				
				return a1[1] - a2[1];
			}
		});

		int endTime = 0; // 회의 종료시간과 시작시간을 비교하기 위한 매개체
		
		for(int m=0; m< i; m++) {
			
			if(endTime <= arr[m][0]) {
				endTime = arr[m][1];
				count++;
				
			}
		}
		
		System.out.println(count);
	}

}
