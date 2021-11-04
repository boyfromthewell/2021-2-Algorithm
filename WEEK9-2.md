## More Definitions

* Subgraph: 어떤 G=(V,E)에 대해 G'=(V',E') of G : V' -> V and E' -> E
* complete graph: 모든 정점쌍이 간선으로 연결되어있는 그래프   
undirected graph: m=n(n-1)/2를 넘을수 x  
digraph: m=n(n-1)을 넘을수 x
* Adjacency relation: 두 정점이 하나의 엣지로 연결 되는가?
* Path  
<img width="50%" src="https://user-images.githubusercontent.com/86250281/140278217-5a0c0c42-9481-40d0-b7db-f2e43fbdd1c0.png"/>

* simple path: path상의 모든 정점들 distinct한 경우
* reachable: 정점 v,w 가는 길존재하면->reachable
* Connected: 그래프 모든 vertex쌍이 서로 reachable하면 connected graph (undirected graph의 경우)
* Strongly Connected: 위와 같음 (digraph의 경우)
* Cycle: 시작 정점과 끝 정점이 동일한 non-empty path (길이 가장 짧은 cycle: 자기자신 가리키는 cycle: self loop)  
<img width="40%" src="https://user-images.githubusercontent.com/86250281/140279200-d564da4c-f954-47ad-aba8-e8f1acd0401f.png"/>  undirected graph에서 cycle 가장 작은경우 (적어도 3보단 커야한다)

* simple cycle: 시작 정점과 끝 정점은 동일 나머지 정점은 path 상에 한번 나타나는 경우(distinct)
* acyclic: 싸이클이 존재하지 않음 (ex. DAG : Directed Acyclic Graph)
* free tree (undirected tree): 세가지 조건 만족 grpah
    1. connected
    2. acyclic
    3. undirected
* undirected forest
    1. acyclic
    2. undirected  
(connected 해도되고 안해도 됨)
* rooted tree: root가 존재하는 free tree
* Connected component: maximal connected subgraph를 의미 (undirected graph에서)  
<img width="50%" src="https://user-images.githubusercontent.com/86250281/140280872-2bb5a9e1-c1d7-41fd-a6c1-a833bbd39568.png"/>  ex. 3개의 connected component

***

<img width="60%" src="https://user-images.githubusercontent.com/86250281/140281341-8f04f0bf-728b-43fe-beb5-93e0ce2d94ec.png"/>  

in-deg(v)=3  
out-deg(v)=2

<img width="60%" src="https://user-images.githubusercontent.com/86250281/140281586-b95f0ddc-01bb-4a6b-ad39-bc477c64d1af.png"/>
digraph의 경우 모든 정점에 대해 in-degree의 sum은 edge의 개수 m이 된다 (outgoing edge도 반드시 어떤 정점에서는 incoming edge가 되기 때문에), out-degree도 마찬가지

-> 모든 정점에 대한 그냥 degree의 sum은 2m

* If an undirected graph G is connected, then **m>=n-1**
* If an undirected graph G is a tree, then **m=n-1**
* If an undirected graph G is a forest, then **m<=n-1**
---
* m이 O(n^2)에 가까우면, dense graph
* m이 O(n)에 가까우면, sparse graph

## Traversing Graphs

Breadth-first search (BFS) and depth-first search (DFS)  
정확히 한번 각각의 정점과 간선 방문하는 알고리즘 (O(n+m) time)

* vertex 상태
1. undiscovered
2. discovered
3. finished

* edge 상태
1. unexplored
2. explored

## Depth first search for Digraph

* 시작 정점 고름, d=0
* 방문할수있는 정점있으면 계속 방문 (d+1)
* 더이상 방문할수있는 정점 없으면 finish
* backtrack
* 모든 정점 방문했으면 종료

<img width="70%" src="https://user-images.githubusercontent.com/86250281/140285741-d5422162-2a60-40c6-aea2-af6b3d377816.png"/>  

* visited 되는 순서: A, B, C, D, F, E, G
* finished 되는 순서: C, D, B, F, A, G, E