---
layout: post
title: "BFS 미로탐색"
date: 2020-06-18
excerpt: "Queue를 사용하여 BFS를 구현해 미로 탐색 문제를 해결"
tag:
- algorithm
- bfs
- expert
comments: true
---

- BFS -
문제 : [sw expert 1226](hhttps://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV14vXUqAGMCFAYD)  
시간 복잡도 : O(n^2)
## KeyPoint
 - Point Class 에 좌표를 저장하여 Queue의 Type Parameters 로 사용  
 - 자료 구조 Queue 이용 BFS 구현 
## Code Snippets  

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.LinkedList;
import java.util.Queue;

public class S_1226 {

	static class Point {
		int x, y;

		public Point(int x, int y) {
			super();
			this.x = x;
			this.y = y;
		}

	}

	static int dx[] = { 0, 0, 1, -1 };
	static int dy[] = { 1, -1, 0, 0 };

	public static void main(String[] args) throws NumberFormatException, IOException {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		for (int i = 0; i < 10; i++) {
			int T = Integer.parseInt(br.readLine());
			int arr[][] = new int[16][16];
			boolean visited[][] = new boolean[16][16];
			int result = 0;
			int tx = 0,ty = 0;
			
			for (int j = 0; j < 16; j++) {
				String s = br.readLine();
				for (int k = 0; k < 16; k++) {
					arr[j][k] = s.charAt(k) - '0';
					if(arr[j][k] == 3) {
						tx=j;
						ty=k;
					}
				}
			}
			Point p = new Point(1, 1);
			Queue<Point> q = new LinkedList<Point>();
			q.add(p);
			visited[1][1]=true;
			
			loop: while (!q.isEmpty()) {
				Point tmp = q.poll();
				for (int k = 0; k < 4; k++) {
					int nx = tmp.x+dx[k];
					int ny = tmp.y+dy[k];
					if (nx < 0 || nx >= 16 || ny < 0 || ny >= 16)
						continue;
					if (visited[nx][ny])
						continue;
					if(arr[nx][ny]==1)
						continue;
					
					if (nx == tx && ny == ty) {
						result = 1;
						break loop;
					}
					visited[nx][ny] = true;
					q.add(new Point(nx, ny));
				}
			}
			System.out.println("#"+T+" "+result);
		}

	}

}

```
