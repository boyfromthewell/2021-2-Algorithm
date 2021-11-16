## problem: single source shortest paths

source: starting 정점 주어짐  
source부터 reachable한 모든 shortest path찾는 문제
(이 교재에선 single source는 source, destination 모두 주어진거 말함)

1. single-source shortest paths : 입력으로 source 정점 주어짐
2. single-pair shortest paths: 입력으로 source와 destination 주어짐
3. single-destination shortest paths: destination만 주어짐
4. all-pairs shortest paths: 입력으로 주어진 모든 정점쌍에 대한 shortest path 구하기

## shortest path property
* x부터 z까지의 shortest path있다고 가정  
* 중간에 y 정점있다
* 이 shortest path는 x부터 y의 P와 y부터 z까지의 Q로 구성되있다 하겠음
* then, P도 shortest path이고 Q도 shortest path이다 (optimal substructure)  

but, 이 역은 성립하지 않음. 예를 들어 x는 인천, y는 부산, z는 서울이라 할때 인천에서 부산까지 shortest path P, 부산에서 서울까지 shortest path Q있다. 이 두 shortest path를 합친다해도 인천에서 서울까지의 shortest path라 할 수 없음.

## Dijkstra's shortest path algorithm

조건: weight가 음수가 되면 안됨  
Prim 알고리즘과 거의 유사하게 동작
```c
dijkstraSSSP(G,n) // OUTLINE
    Initialize all vertices as unseen.
    Start the tree with the specified source vertex s; reclassify it as tree; //root
    define d(s,s) = 0. //자기자신 distance 0으로 초기화
    Reclassify all vertices adjacent to s as fringe. // s와 인접한 모든 정점들 fringe상태로 업데이트
    -------------------초기화 단계
    while there are fringe vertices: // 우선순위 큐로 구현 (unsorted sequence(O(N^2))) or heap(O(mlogn)))
        Select an edge between a tree vertex t and a fringe vertex v
            such that (d(s,t)+W(tv)) is minimum; //s부터 t까지의 거리+tv거리
        Reclassify v as tree; add edge tv to the tree;
        define d(s,v) = (d(s,t)+W(tv)). // 제일 작은 path선택
        Reclassify all unseen vertices adjacent to v as fringe.
```

###  Example

<img width="70%" src="https://user-images.githubusercontent.com/86250281/141901367-b88817fc-3c18-4f3f-8024-ab34e2804fe9.png"/>

* 시작 정점 A
* 가장 작은 weight 가진 B를 Tree상태로 업데이트

* B에서 인접한 A, G, C 체크
* G는 기존에 A에서 G로 가는 weight가 더 작기때문에 그대로, C는 unseen 상태였기 떄문에 fringe 상태로 업데이트
* Tn까지 수행하고, 이 때의 상태가 A로부터 다른 모든 정점까지의 shortest path 계산한것

### Unsorted sequence 이용

<img width="70%" src="https://user-images.githubusercontent.com/86250281/141922182-793dba8a-9b8c-4d65-97d9-5c4e89d8de18.jpg"/>

#### weight 음수 안되는 이유

<img width="60%" src="https://user-images.githubusercontent.com/86250281/141921924-d4a6d0cf-b2f4-411c-b7ba-67e8ac482f43.png"/>

다익스트라 알고리즘은 한번 계산되면(d(A,B)=2) shortest path fix되기 때문에 음의 edge가 존재하면 이런 경우 발생가능 