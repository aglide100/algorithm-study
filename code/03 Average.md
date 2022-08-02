# 백준 4344번 문제

> 출처: https://www.acmicpc.net/problem/4344

## 문제 설명

대학생 새내기들의 90%는 자신이 반에서 평균은 넘는다고 생각한다. 당신은 그들에게 슬픈 진실을 알려줘야 한다.

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
