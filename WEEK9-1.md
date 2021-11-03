# 7. Graphs and Graph Traversals

* Airline routes 그래프를 이용해 표현가능   
(vertex와 edge이용)

* Binary relation   
<img width="60%" src="https://user-images.githubusercontent.com/86250281/140087201-de9b69ee-bd0b-4a38-9fcf-d134147a5e15.png"/>  
x는 y의 진 인수이다 (proper factor), S={1,2,... ,10}  
y가 12라면 x!=y이고 x/y의 나머지가 0이면 x는 y의 proper factor

## Directed Graph (유향 그래프)
* digraph라도 부르기도함, G=(V,E) (vertex, edge의 집합)
* V는 vertices의 집합
* E는 양끝의 V로 정의 가능 (순서중요, (v,w) != (w,v) )
    * E는 edges, directed edges, arcs로 불림
    * (v,w) = v -> w
    * 간단하게 vw도 가능

## Undirected Graph (무향 그래프)
* G=(V,E)
* V는 vertices의 집합
* E는 두개의 unordered V (ex.(v,w)=(w,v))
* 자기 자신으로 가는 edge 정의 안됨 (v,v)->x
* incident (인접한) vs adjacent (인접한)
    * incident - 간선과 정점의 관계
    * adjacent - 정점과 정점의 관계

## Weighted Graph (가중 그래프)

* (V,E,W)의 집합
* W는 하나의 함수, edge 집합의 원소의값 실수로 mapping
* 어떤 edge e에 대해, W(e)는 e의 가중치

## Graph Representations

G=(V,E), vertex의 원소의 수=n, edge의 원소의 수=m로 정의
* input size : n+m
1. Adjacency matrix representation (인접 행렬 표현) 
2. Array of adjacency lists representaion (인접 리스트 표현)

<img width="70%" src="https://user-images.githubusercontent.com/86250281/140093081-09453771-f84f-4ee3-9caf-29bde7aaf990.png"/>

* 인접리스트 표현의 각각의 정점은 array, edge의 연결 유무에 대해 linked list로 구현
* array는 n, list는 2m -> O(n+m) space 사용
* 인접 행렬 표현 O(n^2) space 사용

### v.incidentEdges() vs v.isAdjacentTo(w)
* v.incidentEdges()
    * matrix : O(n) time
    * list : 리스트 한번 스캔해주기 = list의 사이즈 = O(deg(v)) time
* v.isAdjacentTo(w)
    * matrix : O(1) time (해당 인덱스 한번만 접근해주면됨)
    * list : 두 정점중에 list 사이즈 작은것 선택->O(min(deg(v), deg(w))) time

***

* weighted digraph의 예  
<img width="60%" src="https://user-images.githubusercontent.com/86250281/140095218-17cf1fbc-bcf0-4409-8379-12aa06960e0c.png"/>