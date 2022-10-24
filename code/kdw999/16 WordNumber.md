# 백준 1152번 문제

> 출처: https://www.acmicpc.net/problem/1152

## 문제 설명
영어 대소문자와 공백으로 이루어진 문자열이 주어진다. 

이 문자열에는 몇 개의 단어가 있을까? 이를 구하는 프로그램을 작성하시오. 

단, 한 단어가 여러 번 등장하면 등장한 횟수만큼 모두 세어야 한다.

첫 줄에 영어 대소문자와 공백으로 이루어진 문자열이 주어진다. 이 문자열의 길이는 1,000,000을 넘지 않는다. 

단어는 공백 한 개로 구분되며, 공백이 연속해서 나오는 경우는 없다. 또한 문자열은 공백으로 시작하거나 끝날 수 있다.

첫째 줄에 단어의 개수를 출력한다.

## 예제 입력
The Curious Case of Benjamin Button

## 예제 출력
6

## 문제 접근

자바에선 StringTokenizer로 입력한 문자열을 공백을 기준으로 토큰으로 나눌 수 있고 countTokens()함수로 나눈 토큰들을 셀 수 있다.

## 문제 풀이 코드
```java

import java.io.InputStreamReader;
import java.io.BufferedReader;
import java.io.IOException;
import java.util.*;

public class WordNumber {

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine()," ");

		
		System.out.println(st.countTokens());
	
	}

}
