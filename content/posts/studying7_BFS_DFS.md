---
title: "BFS: 너비우선탐색, DFS: 깊이우선탐색(1)"
date: 2021-11-29T21:40:04+09:00
tags: ["알고리즘","bfs","dfs","너비우선탐색","깊이우선탐색"]
categories: ["algorithm"]
---
음... 나는 탐색알고리즘을 매우 어려워 하는 사람이다...😭😭 
<br>
이것에 이어서 길찾기를 무서워하는데..😱 프로그래머로서 이런것들은 좀 이겨내야하지 않을까? 라는 생각이 들어서..
<br>
원래 무서운 것은 몰라서 그런거라고 했으니, 나는 이 녀석들을 공부해서 안무서워해야겠다.😋😋😋

## {{< color color="#FFD400" text="Graph(그래프)" >}}는 무엇일까? 🧐
BFS, DFS를 알기전에 `그래프`라는 자료구조를 먼저 알아야한다.
- 그래프는 `정점(V)`과 `간선(E)`들의 집합이다.
- 간선은 `정점과 정점 사이를 직접 연결하는 선`을 말한다.
- `G = (V,E)`로 수학적으로 표기한다.

💚 그래프의 표현방법
1. 인접 행렬
```csharp
int V; //정점의 갯수
int E; //간선의 갯수

int[,] Graph = new int[V, V]; //N x N 행렬

for (int i = 0; i < E; i++)
{
    Graph[v1,v2] = 1;//방향 그래프 인접행렬로의 표현
}
```
2. 인접 리스트
```csharp
int V; //정점의 갯수
int E; //간선의 갯수

List<int>[] Graph = new List<int>[V + 1];

for (int i = 1; i < N + 1; i++)
{
    Graph[i] = new List<int>();
    foreach(v in AdjacencyVertices) 
    {
        Graph[i].Add(v);//간선으로 연결된 정점들을 모두 추가
    }
}
```
## {{< color color="#FFD400" text="BFS" >}}를 알아보자 🧐

- `BFS(Breadth First Search)`는 너비우선탐색으로 어떠한 정점으로부터 인접한 정점을 먼저 방문하는 탐색 알고리즘이다.

🍑 코드 구현
```csharp
List<int>[] ve;//정점과 정점마다 연결된 다른 정점들의 리스트의 배열
List<int> visited;//방문한 정점

void BFS(int v)//시작 정점
{
    Queue<int> queue_bfs = new Queue<int>();
    queue_bfs.Enqueue(v);
    visited.Add(v);//방문함!

    while (queue_bfs.Count > 0)//큐의 갯수가 1개 이상일 때,
    {
        var w = queue_bfs.Dequeue();//방문한 정점을 빼면서
    
        for (int i = 0; i < ve[w].Count; i++)//인접한 정점들을 탐색
        {
            if (!visited.Contains(ve[w][i]))//방문하지 않은 정점이 있다면
            {
                queue_bfs.Enqueue(ve[w][i]);
                visited.Add(ve[w][i]);//방문!
            }
        }
    }
}
```

<br>

## {{< color color="#FFD400" text="DFS" >}}를 알아보자 🧐

- `DFS(Depth First Search)`는 깊이우선탐색으로
1. 시작 정점으로 부터 인접한 정점 중 한 정점을 방문한다. 
2. 그 정점을 기준으로 1을 반복한다.
3. 더 이상 인접한 정점이 없으면, 다시 이전 정점으로 돌아간다(백트래킹).
4. 모든 정점을 방문할 때까지 1~3을 반복한다.

🍑 코드 구현
```csharp
List<int>[] ve;//정점과 정점마다 연결된 다른 정점들의 리스트의 배열
List<int> visited;//방문한 정점

void DFS(int v)//시작 정점
 {
    if (visited.Contains(v)) //이미 방문한  곳이라면 return
    {
        return;
    }
    visited.Add(v);//방문한 정점추가
    for (int i = 0; i < ve[v].Count; i++)
    {
        if (!visited.Contains(ve[v][i]))//방문하지 않은 인접 정점을 방문하러가자!
        {
            DFS(ve[v][i]);
        }
    }
 }```
