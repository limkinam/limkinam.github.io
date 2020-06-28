---
layout: post
title:  "2020_상반기_넷마블_3번"
date:   2020-06-27
excerpt: "문제 풀이 (문제 공유 불가...)"
algorithm: true
tag:
- algorithm
- netmable
- bfs
comments: true
---

## 문제 풀이
 - 지뢰찾기 게임에서 첫 시행 후 결과를 출력하는 문제
 - bfs를 통해 구현




## Code Snippets

```java

import java.util.LinkedList;
import java.util.Queue;

public class test3 {

	public static void main(String[] args) {
		long start = System.currentTimeMillis();
		String[] board = {"EEEEE","EEMEE","EEEEE", "EEEEE"};
		int y=2;
		int x=0;
		
		
		String[] answer = solution(board,y,x);
		for (int i = 0; i < answer.length; i++) {
			System.out.println(answer[i]);
		}
		long end = System.currentTimeMillis();
		System.out.println("실행시간 : "+ (end-start/1000.0));
	}

	static class Point {
		int y, x;

		public Point(int y, int x) {
			super();
			this.y = y;
			this.x = x;
		}

	}
	//8방향
	static int dy[] = { 0, 0, 1, 1, 1, -1, -1, -1 };
	static int dx[] = { 1, -1, 1, 0, -1, 1, 0, -1 };

	private static String[] solution(String[] board, int y, int x) {// 행 열

		int N = board.length;
		int M = board[0].length();
		String[] answer=new String[N];
		char arr[][] = new char[N][M];
		boolean flag = true;
		//주어진 보드판 그리기
		for (int i = 0; i < N; i++) {
			for (int j = 0; j < M; j++) {
				arr[i][j] = board[i].charAt(j);
			}
		}
		//BFS를 위해 큐 사용
		Queue<Point> q = new LinkedList<>();
		boolean[][] visited = new boolean[N][M];
		
		q.add(new Point(y, x));
		visited[y][x] = true;
		

		//누른 위치가 지뢰면 해당 값을 X로 바꿔준다
		if (arr[y][x] == 'M') {
			flag = false;
			arr[y][x] = 'X';
		//누른 위치가 지뢰가 아닐시 BFS 실행
		} else {

			while (!q.isEmpty()) {
				Point temp = q.poll();
				int cnt = 0;
				int ny;
				int nx;
				for (int i = 0; i < 8; i++) {
					ny = temp.y + dy[i];
					nx = temp.x + dx[i];

					if (ny < 0 || ny >= N || nx < 0 || nx >= M)
						continue;
					if (visited[ny][nx])
						continue;
					//각 방향에 지뢰의 갯수를 저장
					if (arr[ny][nx] == 'M')
						cnt++;
				}
				//지뢰의 갯수를 해당 위치에 적어준다.
				arr[temp.y][temp.x] = (char) (cnt+'0');
				//8방향 모두 지뢰가 없을시 B를 적어주고 모든 방향을 큐에 넣어준다.
				if (cnt == 0) {
					arr[temp.y][temp.x]='B';
					for (int i = 0; i < 8; i++) {
						ny = temp.y + dy[i];
						nx = temp.x + dx[i];

						if (ny < 0 || ny >= N || nx < 0 || nx >= M)
							continue;
						if (visited[ny][nx])
							continue;
						q.add(new Point(ny,nx));
						visited[ny][nx]=true;
					}
				}
				
			}
		}
		// 출력 자료형에 맞게 수정한다.
		for (int i = 0; i < N; i++) {
			String tmp ="";
			for (int j = 0; j < M; j++) {
				// 지뢰를 누르지 않은 경우  출력시 지뢰를 E로 기록한다.
				if(arr[i][j]=='M' && flag)
					arr[i][j]='E';
				tmp+=arr[i][j];
			}
			answer[i]=tmp;
		}
		

		return answer;
	}
}


```

## Result

```  
B1E1B
B1E1B
B111B
BBBBB
실행시간 : 1.59167465520787E12
```   
 
 


