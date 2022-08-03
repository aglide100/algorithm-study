# 백준 4344번 문제

> 출처: https://www.acmicpc.net/problem/4344

## 문제 설명

대학생 새내기들의 90%는 자신이 반에서 평균은 넘는다고 생각한다. 당신은 그들에게 슬픈 진실을 알려줘야 한다.

첫째 줄에는 테스트 케이스의 개수 C가 주어진다.

둘째 줄부터 각 테스트 케이스마다 학생의 수 N(1 ≤ N ≤ 1000, N은 정수)이 첫 수로 주어지고, 이어서 N명의 점수가 주어진다. 점수는 0보다 크거나 같고, 100보다 작거나 같은 정수이다.

각 케이스마다 한 줄씩 평균을 넘는 학생들의 비율을 반올림하여 소수점 셋째 자리까지 출력한다.

## 예제 입력
5

5 50 50 70 80 100

7 100 95 90 80 70 60 50

3 70 90 80

3 70 90 81

9 100 99 98 97 96 95 94 93 91

## 예제 출력

40.000%

57.143%

33.333%

66.667%

55.556%

## 문제 접근

간단한 문제 설명에 비해 처음 접근할 때 2차원 배열을 쓰는 등 고민이 많았다. 

처음에 테스트 케이스의 갯수를 입력해주고 그 갯수만큼 돌리는 반복문을 작성한다.

반복문 내에서 각 테스트 케이스에 해당하는 배열을 생성하며 각 배열마다 학생 수를 할당 뒤 점수도 입력 후 계산하였다.

## 문제 풀이 코드
```java

import java.util.*;
public class Average {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		int c = sc.nextInt(); // 테스트 케이스를 받는 변수
		int arr[];
		
		for(int i=0 ; i<c ; i++) {
			int sn = sc.nextInt();	//학생 수를 받는 변수
			arr = new int[sn];
			
			float sum = 0;	// 성적 합을 받을 변수
			
			for(int j=0 ; j < sn ; j++) {
				int score = sc.nextInt();	// 성적 입력 
				arr[j] = score;
				sum += score;	// 점수를 차곡차곡 합산 
			}
			
			float avr = (sum / sn) ; // 평균 값을 받는 변수
			float ct = 0; // 평균 넘는 학생 수
			
			// 평균 넘는 학생 수 계산
			for(int k=0 ; k<sn ; k++) {
				if(arr[k] > avr) {
					ct++;
				}
			}
			
			System.out.printf("%.3f%%\n", (ct/sn)*100);
		
		}
		sc.close();
 }
}
