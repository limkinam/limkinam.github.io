---
layout: post
title:  "2020_상반기_넷마블_SQL"
date:   2020-06-27
excerpt: "문제 풀이 (문제 공유 불가...)"
tag:
- SQL
- netmable
comments: true
---

## 문제 풀이
 - 하나의 테이블에서 WHERE절 + 간단한 함수(not in)와 ORDER BY 이용




## Code Snippets

```

select id from game_users
    where id not in (select id1 from friends)
    and id not in (select id2 from friends)
    order by id;


```

## Improvements
```
select id from game_users
    where id not in (select distinct id1 from friends)
    and id not in (select distinct id2 from friends)
    order by id;
```  

비교할 id1과 id2의 중복을 제거하여 비교할 대상을 줄여 성능향상가능하다고 생각한다. 
 


