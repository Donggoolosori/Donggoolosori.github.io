---
layout: post
title: "[프로그래머스] 프린터 - C++"
subtitle: "level2"
date: 2021-1-1 18:40:00
author: "dongjune"
header-img: "img/in_post/1.jpg"
catalog: true
tags:
  - Programmers
---
# 문제

[프로그래머스 프린터](https://programmers.co.kr/learn/courses/30/lessons/42587){:target="_blank"}

# 풀이

큐와 우선순위 큐를 같이 사용하여 풀이 했습니다.

큐에는 주어지는 우선순위와 index 번호를 pair 형태로 넣어주고, 우선순위 큐에는 우선순위만 넣어줍니다.

```cpp
queue<pair<int,int>> q;
priority_queue<int> pq;

int index=0;
for(const auto &p:priorities){
    q.push({p,index++});
    pq.push(p);
}
```
  
이제 큐가 다 비워질때까지 while문을 돕니다. 코드는 주석을 통해 설명했습니다.
```c++
int order=1;
while(!q.empty()){
    pair<int,int> cur = q.front();
    
    // 프린트 할 수 있다면
    if(pq.top() <= cur.first){
        // 찾고자 하는 index의 요소면 바로 order값 return
        if(cur.second==location){
            return order;
        }
        // 큐와 우선순위 큐를 둘다 pop해주고 순서값 1 증가
        q.pop();
        pq.pop();
        order++;
    // 프린트 할 수 없으면 큐의 앞 원소를 뒤로 보낸다.
    }else{
        q.push(cur);
        q.pop();
    }
}
```
  
이제 전체 코드를 확인해봅시다.
# 코드

```cpp
#include <string>
#include <vector>
#include <queue>

using namespace std;

int solution(vector<int> priorities, int location) {
    int answer = 0;
    queue<pair<int,int>> q;
    priority_queue<int> pq;
    int index=0;

    for(const auto &p:priorities){
        q.push({p,index++});
        pq.push(p);
    }
    
    int order=1;
    while(!q.empty()){
        pair<int,int> cur = q.front();
        
        if(pq.top() <= cur.first){
            if(cur.second==location){
                return order;
            }
            q.pop();
            pq.pop();
            order++;
        }else{
            q.push(cur);
            q.pop();
        }
    }
}
```