# 백준 25304번 문제

> 출처: https://www.acmicpc.net/problem/25304

## 문제 설명
준원이는 저번 주에 살면서 처음으로 코스트코를 가 봤다. 정말 멋졌다. 

그런데, 몇 개 담지도 않았는데 수상하게 높은 금액이 나오는 것이다! 

준원이는 영수증을 보면서 정확하게 계산된 것이 맞는지 확인해보려 한다.

영수증에 적힌,
구매한 각 물건의 가격과 개수
구매한 물건들의 총 금액을 보고, 구매한 물건의 가격과 개수로 계산한 총 금액이 영수증에 적힌 총 금액과 일치하는지 검사해보자.

첫째 줄에는 영수증에 적힌 총 금액 X가 주어진다.

둘째 줄에는 영수증에 적힌 구매한 물건의 종류의 수 N이 주어진다.

이후 N개의 줄에는 각 물건의 가격 a와 개수 b가 공백을 사이에 두고 주어진다.

구매한 물건의 가격과 개수로 계산한 총 금액이 영수증에 적힌 총 금액과 일치하면 Yes를 출력한다. 일치하지 않는다면 No를 출력한다.

## 예제 입력
260000

4

20000 5

30000 2

10000 6

5000 8

## 예제 출력
Yes

## 문제 접근

총 금액과 물품 종류 입력 후 각 물품의 종류만큼 가격과 개수의 배열을 생성

종류만큼 돌아가는 반복문에 가격, 개수 배열에 차례대로 가격과 개수 입력, sum에 각 배열의 i번 째 물품의 가격과 개수를 곱한 값을 

차례대로 저장한 뒤 if문으로 sum과 처음에 입력한 총 금액을 비교한다.

## 문제 풀이 코드
```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Receipt {

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		int total_Amount = Integer.parseInt(br.readLine());
		int kind = Integer.parseInt(br.readLine());
		
		int arr_Cost[] = new int[kind];
		int arr_Number[] = new int[kind];
		int sum = 0;
		
		for(int i=0; i<kind; i++) {
			StringTokenizer st = new StringTokenizer(br.readLine(), " ");
			arr_Cost[i] = Integer.parseInt(st.nextToken());
			arr_Number[i] = Integer.parseInt(st.nextToken());
			sum += arr_Cost[i] * arr_Number[i];
		}

		if(sum == total_Amount) {
			System.out.println("Yes");
		}
		else {
			System.out.println("No");
		}
	}

}
