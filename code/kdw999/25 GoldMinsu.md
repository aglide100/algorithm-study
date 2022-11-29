# 백준 1526번 문제

> 출처: https://www.acmicpc.net/problem/1526

## 문제 설명
은민이는 4와 7을 좋아하고, 나머지 숫자는 싫어한다. 금민수는 어떤 수가 4와 7로만 이루어진 수를 말한다.

N이 주어졌을 때, N보다 작거나 같은 금민수 중 가장 큰 것을 출력하는 프로그램을 작성하시오.

## 입력

첫째 줄에 N이 주어진다. N은 4보다 크거나 같고 1,000,000보다 작거나 같은 자연수이다.

## 출력

첫째 줄에 N보다 작거나 같은 금민수 중 가장 큰 것을 출력한다.

## 예제 입력

100

474747
 

## 예제 출력

77

474747

## 문제 접근

4와 7로만 이루어진 숫자를 찾는 계산식을 떠올리는데 어려움이 있었으나 가장 큰 4와 7로 이루어진 수를 찾는 것이기에 입력한 수 부터 1씩 감소하는

반복문 내에서 계속 10으로 나눈 나머지와 몫을 활용하여 4와 7로만 이루어진 숫자인지 확인한다.

## 문제 풀이 코드
```java

import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		int N = sc.nextInt();

		for (int i = N; i >= 4; i--) { // 가장 큰 수를 출력하기 위해 큰 수부터 아래로
			
			boolean check = true; // 가장 큰 수 판독기
			int n = i;
			
			while(n !=0) { 
				if(n % 10 == 4 || n % 10 == 7) { // 10으로 나눈 나머지가 4, 7이면 
					n = n / 10; // 다시 10으로 나눈 몫을 4, 7인지 확인하기 위한 계산
					            // 이후 다시 while을 돌아 n % 10 계산에서 4, 7 조건에 적합하면
					            // if문을 계산하여 while(n!=0)에서 탈출하게 됨 이후 i 출력
				}
				else {
					check = false;
					break;
				}
			}

			if(check) {
				System.out.println(i);
				break;
			}
		}
	}

}
