# 9. Transitive Closure, All-pairs Shortest paths

Floyd-warshall's algorithm 이용 그래프의 Transitive Closure 찾기

## Transitive Closure

digraph G가 주어졌을때 G*는 G와 같은 정점 정보 가짐 대신 edge 정보 추가  

<img width="60%" src="https://user-images.githubusercontent.com/86250281/142233445-b9b700cb-931d-4c57-abe0-4f1d5b82c5de.png"/> ex) B에서 E path 존재하면 B에서 E로 한번에 가는 directly connected edge 추가해주기  
모든 이런 path에 대해 다 추가해준것이 G의 Transitive closure G*

Transitive closure는 n번의 dfs로도 가능 => O(n(n+m)), 만약 m이 O(n^2)에 바운드된다면 이때 수행시간은 O(n^3)이 됨

## Floyd-warshall Transitive Closure
1. 모든 정점에 대해 번호를 매겨줌
2. 번호매긴 정점을 이용해서 바로 연결할수있는 edge 만들기

```c
Algorithm FloydWarshall(G)
    Input digraph G
    Output transitive closure G* of G
    i <- 1
    for all v bound G.vertices()
        denote v as vi
        i <- i + 1
    G0 <- G
    for k <- 1 to n do
        Gk <- Gk - 1
        for i <- 1 to n (i != k) do
            for j <- 1 to n (j != i, k) do
                if Gk - 1.areAdjacent(vi
, vk) and Gk - 1.areAdjacent(vk, vj)
                if not Gk.areAdjacent(vi, vj)
                     Gk.insertDirectedEdge(vi, vj , k)
    return Gn
```
어떤 step Gk에 대한 계산 하기위해 기존에 계산된 Gk-1로부터 계산 : 다이나믹 프로그래밍 기법 활용  

adjacency matrix 활용했을때 O(n^3) time, when areAdjacent is O(1)

## Example

<img width="70%" src="https://user-images.githubusercontent.com/86250281/142237354-26598c65-551c-4ad3-83c6-b7898310ad4c.png"/> 

* 각 정점에 대해 outgoing 엣지 유무 1로 업데이트 (input G)

<img width="70%" src="https://user-images.githubusercontent.com/86250281/142238185-5d96abb8-1519-45d7-b0e9-e34be516cd30.png"/>

* column을 위에서 아래로 스캔
* edge 3에서 존재, (3,1) 이라고 볼수 있음
* 1번 row를 스캔
* (1,4) edge 존재
* (3,1)->(1.4) = (3,4)
* 이미 기존에 (3,4)에 edge 존재 -> pass
* 이런 단계로 알고리즘 진행

<img width="70%" src="https://user-images.githubusercontent.com/86250281/142239194-0ff2f988-b5ad-4b83-9779-dccdfdfae4f4.png"/>

* (5,1) edge 존재
* 1 row 확인
* (1,4) edge 존재
* (5, 1) -> (1, 4) = (5,4)
* (5,4)에 1 업데이트
* phase 1 끝

Phase 2
* 2 row 에 존재 edge 없음, 종료

Phase 3

<img width="70%" src="https://user-images.githubusercontent.com/86250281/142240444-e7fcf263-18ce-4b94-b39c-e1e7a8fd2fd5.png"/>

* (4,3) 존재
* 3 row 확인
* (3,1), (3,2) (3,4) 존재
* (4,1) (4,2)에 1 업데이트 ((4,4) 자기자신은 제외)

* (5,3) 존재
* 3 row 확인
* (3,1), (3,2) (3,4) 존재
* (5,1), (5,2), (5,4) 1 업데이트 

* (6,3) 존재
* 3 row 확인
* (3,1), (3,2) (3,4) 존재
* (6,1), (6,4) 1 업데이트  
.  
.  
.  
<img width="70%" src="https://user-images.githubusercontent.com/86250281/142242353-0bc3c91d-868e-4615-9ea9-42d41eb80fa0.png"/> 최종 결과 Gn=G*

## All-pairs shortest path

앞선 알고리즘 좀만 변경하면 all-pairs shortest path 찾을 수 있음 (모든 정점 쌍에대한 shortest distance 찾기)

* n번의 다익스트라 알고리즘 사용하면 찾을수 있음
* O(nmlogn) time 소요 (힙이용 다익스트라 O(mlogn))
* m -> O(n^2)이면 O(n^3logn)에도 수행 = O(n^3)

### example

* phase 1

<img width="70%" src="https://user-images.githubusercontent.com/86250281/142436859-65705f8f-c024-4e40-ba77-c433b92abf35.jpg"/>

* phase 2

<img width="70%" src="https://user-images.githubusercontent.com/86250281/142437036-051c1337-5169-4853-846b-f8dd2687b600.jpg"/>  

이런 방식으로 알고리즘 수행  
분석 : n phases-> O(n) time  
scan 하는데 O(N) * O(N)=> O(N^3)에 수행가능