---
layout: post
title: "LIS 최장 증가 수열"
date: 2020-06-16
excerpt: "LIS 알고리즘 시간 복잡도: O(n^2) | 이분탐색 이용 O(nlog n)"
tag:
- algorithm
- lis
- baakjoon
comments: true
---

## LIS 최장 증가 수열 알고리즘  
 - 동적 계획법 -  
문제 : <a href="https://www.acmicpc.net/problem/11053"> 백준 11053 </a>
시간 복잡도 : O(n^2)  

```java  
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class S_11053 {

	public static void main(String[] args) throws Exception {
		// TODO Auto-generated method stub
		
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		int N = Integer.parseInt(br.readLine());
		
		StringTokenizer stk = new StringTokenizer(br.readLine());
		
		int arr[] = new int[N];
		for (int i = 0; i < arr.length; i++) {
			arr[i]=Integer.parseInt(stk.nextToken());
		}
		
		int dp[]= new int[N];
		
		int result = 0;
		
		for (int i = 0; i < N; i++) {
			dp[i]=1;
			for (int j = 0; j < i; j++) {
				
				if(arr[j] < arr[i] && dp[j] >= dp[i]) {
					
					dp[i] = dp[j] + 1;
					
				}
				
			}
			
			if(dp[i] > result) result=dp[i] ;
			
		}
		
				
		System.out.println(result);
		
	}

}
```
## 이분 탐색으로 시간복잡도를 줄일 수 있다.
```java
private static boolean BinarySearch(int[] arr, int i) {
		// TODO Auto-generated method stub
		
		int st = 0;
		int ed = arr.length-1;
		while(true) {
			int ct = (st + ed) / 2;
			if(arr[ct] == i)
				return true;
			else if(arr[ct] < i)
				st = ct + 1;
			else {
				ed = ct-1;
			}	
			if(st > ed)
				break;
		}
		return false;
	}
```
## LowerBound 함수 구현 : 찾고자 하는 값 이상이 처음 나타나는 위치 // 이분 탐색 기반
```java
private static int lowerBound(int[] dp, int idx, int i) {
		// TODO Auto-generated method stub
		int st = 0;
		int ed = idx;
		while(true) {
			int ct = (st + ed) / 2;
			if(dp[ct] < i)
				st = ct + 1;
			else {
				ed = ct;
			}
			if(st>=ed)
				break;
			
		}
		return st;
	}
```


문제 : <a href="https://www.acmicpc.net/problem/12015"> 백준 12015 </a>
시간 복잡도 : O(nlog n)
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

public class S_12015 {

	//6
	//10 20 10 30 20 50
	
	public static void main(String[] args) throws NumberFormatException, IOException {
		// TODO Auto-generated method stub
		
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		int N = Integer.parseInt(br.readLine());
		StringTokenizer stk = new StringTokenizer(br.readLine());
		
		int arr[] = new int[N];
		for (int i = 0; i < arr.length; i++) {
			arr[i]=Integer.parseInt(stk.nextToken());
		}
		
		int dp[] = new int[N];
		
		int idx = 0;
		
		dp[idx]=arr[0];
		
		for (int i = 1; i < N; i++) {
			if(dp[idx] < arr[i] ) {
				idx++;
				dp[idx]=arr[i];
			}
			else {
				dp[lowerBound(dp,idx,arr[i])]=arr[i];
			}
		}
		
		System.out.println(idx+1);
		
	}
```
