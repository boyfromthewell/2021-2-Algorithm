## Breadth-first Search for Digraph

* 임의의 정점 선택, d=0으로 초기화  
(다른 정점까지 최단거리, 경로 계산 가능)
* d=1 정점 다찾고, d=2 정점 다찾기 ....-> 영역 넓히듯이 탐색

## BFS example

가정 : 방문할수있는 여러개 정점 있는경우 알파벳 작은거 부터 방문

<img width="70%" src="https://user-images.githubusercontent.com/86250281/140634441-9489d438-e266-4c64-a9dd-f189444cd4bc.png"/>

* starting 정점 : A (BFS는 하나의 큐 필요)
* A 큐에 삽입, d=0으로
* A를 dequeue, A에서 갈수 있는 정점 탐색
* B,C,F 삽입 (d=1)
* B dequeue, B에서 갈수있는 정점 탐색 (c는 이미 discovered, D 삽입(d=2))
* C, F dequeue
* D dequeue
* 더 이상 갈수있는 곳 x, d=0으로 초기화 starting 정점 E 추가
* E dequeue, G 삽입(d=1), G dequeue

->모든 정점 엣지 한번씩 순회 가능

최단 경로, 최단 거리를 구하려면 E,G 부분에서 d=무한대 로 저장하도록 계산

또한 각 노드에서 나를 탐색하게 한 정점에대한 정보 저장 할 것 필요-> predecessor(parent)

<img width="60%" src="https://user-images.githubusercontent.com/86250281/140634669-dd2891f9-94b9-49ed-9fb1-3d4e57c94ad0.png"/>

index D 에는 B 저장

A부터 D까지의 최단 경로는? D부터 역순으로 출력해주기 P[D]=B, P[B]=A, 스택 같은거에 삽입 ->A,B,D -> pop -> 최단경로 A,B,D

O(n+m) time 에 수행가능

## Strongly Connected Components (SCC)

임의의 digraph D에서 SCC 찾기

<img width="60%" src="https://user-images.githubusercontent.com/86250281/140634848-9bd1c7a1-4f5e-4e34-b124-0f97e3541a7f.png"/>  
어디에 적용? 사람들 팔로우 관계성(sns) 

### 코사라주 알고리즘

2번의 dfs 이용 

phase 1  
* 입력으로 주어진 G에 대해 DFS 적용  
* finishing time에 스택에 정점 삽입 
<img width="15%" src="https://user-images.githubusercontent.com/86250281/140635287-3a8dcee7-1bae-49cc-afe2-e2dcd3f4ff05.png"/> (finish stack)

phase 2
* transpose graph G^T생성 (원래 그래프 엣지 방향 반대로)
* G^T에 대해 두번째 DFS 수행
    * 처음 발견되는 starting 정점에 대해 leader라고 부를 것

<img width="60%" src="https://user-images.githubusercontent.com/86250281/140635560-b82e3554-3613-419c-8b04-520fbdff0325.png"/> phase 2 DFS 하기전까지 수행한 것, 그다음

* SCC 정보 저장할 array 생성
* finish stack에서 pop 해서 나온 E를 reader로 설정
* E부터 dfs 수행, 결과 array에 저장
<img width="60%" src="https://user-images.githubusercontent.com/86250281/140635682-a23b2ad8-1a9a-491d-a7c2-877d11f063f4.png"/>

* reader A  
<img width="60%" src="https://user-images.githubusercontent.com/86250281/140635874-8dd0b8bb-17e7-4555-9929-a459856633da.png"/>

* reader C  
<img width="60%" src="https://user-images.githubusercontent.com/86250281/140635941-dff4d86a-b8b2-44c8-8c58-1f6edc21506b.png"/>

위 과정을 완료하면 SCC 찾기 가능 (같은 리더 가진 경우 같은 SCC) SCC개수=리더의 수

#### 분석
phase 1: O(n+m) time  
phase 2 : transpose graph 생성 -> O(n+m) time, 2nd DFS : O(n+m) time

total : O(n+m) time

# 8. Graph optimization problems and Greedy Algorithms

## optimization problems

최적의 해를 찾는 문제  

비용의 측면: 비용 최소화 하기  
이득의 측면: 이득 최대화 하기

가장 best한 결과 찾아내자, 어떤 일련의 선택들 optimal 되도록 하자

## Greedy algorithms
선택할때 제일 이익이 되도록 선택  
짧은 시간내에 best 찾기, 번복 불가

* minimum spaning tree 찾기
* single source shortest path 찾기

## minimum spaning tree
input: connected, undirected graph 주어짐

spanning tree = G'=(V', E')라 하면  
V`=V and E'->E and connected, acyclic해야함
<img width="60%" src="https://user-images.githubusercontent.com/86250281/140636437-818b8b9c-969e-4da2-81c4-1c1f3f3207c7.png"/>
minimum weight 가지는 spanning tree찾기 -> b와 c만 만족 (최소 weight 6)