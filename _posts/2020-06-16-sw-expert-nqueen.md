---
layout: post
title: "Back Tracking(DFS)"
date: 2020-06-18
excerpt: "DFS를 이용한 백트래킹을 이용해 N-Queen 문제를 해결 "
tag:
- algorithm
- dfs
- back tracking
- expert
comments: true
---

- DFS -
문제 : [sw expert 2806][https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV7GKs06AU0DFAXB]
시간 복잡도 : O(n^2)
## 함수  

1. solve : 백트래킹 구현
2. solve2 : 대각선 검사

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class S_2806 {
	
	static int result;
	static int N;
	
	
	public static void main(String[] args) throws NumberFormatException, IOException {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int T = Integer.parseInt(br.readLine());
		for (int tc = 0; tc < T; tc++) {
			result = 0;
			N = Integer.parseInt(br.readLine());
			int arr[][] = new int[N][N];
			
			solve(arr,0);
			System.out.println("#"+(tc+1)+" "+result);
		}
	}

	static int[] dx= {1,1,1,0,0,-1,-1,-1};
	static int[] dy= {1,0,-1,1,-1,1,0,-1};

	private static void solve(int[][] arr, int i) {
		// TODO Auto-generated method stub
		if(i==N) {
			result++;
			return;
		}
		for (int j = 0; j < N; j++) {
			if(solve2(arr,i,j)) {
				arr[i][j]=1;
				solve(arr,i+1);
				arr[i][j]=0;
			}
		}
	}

	private static boolean solve2(int[][] arr, int i, int j) {
		// TODO Auto-generated method stub
		for (int k = 0; k < 8; k++) {
			int ni = i;
			int nj = j;
			while(true) {
				ni += dx[k];
				nj += dy[k];
				if(ni<0 || ni>=N || nj<0 || nj>=N)
					break;
				if(arr[ni][nj]==1)
					return false;
			}
		}
		return true;
	}

}

```
