---
layout: post
title:  "2020_상반기_넷마블_2번"
date:   2020-06-27
excerpt: "문제 풀이 (문제 공유 불가...)"
tag:
- algorithm
- netmable
comments: true
---

## 문제 풀이
 - 양궁에서 과녁과 화살 10발의 위치가 주어졌을 경우 점수를 구하는 단순 구현




## Code Snippets

```java

public class test2 {
	public static void main(String[] args) {
		//중심으로부터 과녁의 각 점수별 거리
		int[] target = {2, 2, 2, 2, 2};
		//주어진 화살 10개의 위치
		int[][] position = {{0, 0}, {0, 1}, {1, 1}, {-3, 5}, {7,5}, {10, 0}, {-15, 22}, {-6, -5}, {3, 3}, {5, -5}};
		
		System.out.println(solution(target,position));
	}
	
	public static int solution(int[] target, int[][] positions) {
        int answer = 0;
        //주어진 과녁의 각 거리를 원점에서의 거리로 수정
        for (int i = 1; i < 5; i++) {
			target[i]+=target[i-1];
		}
        //화살의 거리와 비교하기 위해 제곱의 값으로 수정
        for (int j = 0; j < 5; j++) {
        	target[j]=target[j]*target[j];        	
        }
        //좌표 x,y를 이용하여 원점에서 거리를 구해서 점수를 얻어 총점에 더한다 
        for (int i = 0; i <10; i++) {
			int x=positions[i][0];
			int y=positions[i][1];
			int dist = x*x+y*y;
			answer+=get_score(target,dist);
		}
        
        return answer;
    }
	
	//좌표의 거리와 각 점수별 거리를 비교하여 점수책정
	private static int get_score(int[] target, int dist) {
		// TODO Auto-generated method stub
		if( dist<=target[0] )
			return 10;
		else if( dist<=target[1] )
			return 8;
		else if( dist<=target[2] )
			return 6;
		else if( dist<=target[3] )
			return 4;
		else if( dist<=target[4] )
			return 2;
		return 0;
	}

	
}


```

## Improvements
```java  
double dist = Math.sqrt(x*x+y*y);
```
 (전)거리 비교를 위해 과녁을 for문을 돌며 제곱값으로 수정한 부분 
```  
54
실행시간 : 1.591672872994867E12
 ```  
 (후)원점으로부터 거리 수정시 double형으로 캐스팅 후 10개의 화살을 Math.sqrt() 메소드 이용하여 제곱근거리로함
 
 ```  
54
실행시간 : 1.591672821168744E12
 ```  

과녁의 각 거리가 5개로 고정되어있어 큰 차이를 보이진 않으나 조금 더 빨라진걸 볼 수 있다.  
과녁의 점수 분포 수가 커질수록 더 많은 성능차이를 보일 수 있다.
 


