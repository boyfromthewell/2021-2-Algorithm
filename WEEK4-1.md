## Optimality of Binary Search

* 그동안의 방법을 통해 θ(n)에서 θ(logn) 까지 개선
    * 더 빠른 알고리즘 존재 할까?
    * 알고리즘 of class : 비교연산

* Decision tree : 알고리즘 a와 input size n이 같으면 항상 같은 모양 생성, o부터 n-1까지의 label생성

1. root -> 최초로 비교하는 index
2. left child -> k가 entry보다 작을때 다음 비교할 index
   right child-> k가 entry보다 클때 다음 비교할 index

<img width="60%" src="https://user-images.githubusercontent.com/86250281/134621959-e4a2c662-8c60-4d0f-a8cb-750406e31853.png"/>

n=10일때 decision tree example

<img width="60%" src="https://user-images.githubusercontent.com/86250281/134622627-bb10b913-9c93-4fd9-be84-766ca05c2bcc.png"/>

decision tree의 다른 예
* 알고리즘 a,b 선형탐색의 경우
* 알고리즘 c : input이 오름차순 상태이고 input 값이 k보다 큰값이 나온경우 탐색 종료하기때문에 left child는 x

## Decision Tree for Analysis

* Worst case : root부터 leaf까지에 있는 가장 긴 path에 있는 node의 수(p)로 따져볼수 있다
* decision tree의 노드 수 :N 으로 가정
* 가장 노드가 많을 떄 : complete binary tree의 모양 

<img width="60%" src="https://user-images.githubusercontent.com/86250281/134623123-32fd3a2b-a2fa-481b-8c8a-ba7796b25705.png"/> complete binary tree의 경우 이런 비교연산의 수와 노드의 수를 가지게 된다

따라서 N <= 1 + 2 + 4 + ... + 2^p-1 = (2^p)-1

-> N+1 <= 2^p  -> 2^p >= (N+1)

* N>=n 임을 증명하자 (decsion tree의 노드의 수는 input size n 보다 항상 크거나 같다)

## Proof by 모순법

* N<n -> 모순이다

* N < n 이라면 어떤 index i에 대해 decision tree에 노드론 없지만 값이 있을 수 있다
* input size가 n인 배열 E1, E2가 있고 E1[i] : 50, E2[i] : 70 이라고 할 때 찾고자 하는 값 K가 50이라면 E1에서는 찾고, E2에서는 못 찾기 때문에 서로 다른 리턴 값 가져야함
* 하지만 decision tree i에 대한 노드가 존재하지 않기 때문에 두 배열은 같은 리턴값을 가지게됨 -> 모순
* 따라서 N>=n

* now, 2^p >= (N+1) >= (n+1)
* p >= log(n+1)

최소 p = log(n+1)의 올림 -> 적어도 log(n+1)의 비교 연산 사용해야 한다 = F(n)

알고리즘 D도 log(n+1)의 올림 = w(n)이다, 따라서 F(n)=w(n)이므로 binary search : optimal

* 따라서 θ(logn)보다 빠른 알고리즘 존재 x -> 알고리즘 d (optimal)

***

# 2. Data Abstraction and basic data structrue

## Abstract Data Type(ADT)

* Structures : 멤버 변수, 멤버 함수
* Functions : 수행하는 operation (push, pop...) 

## tree 용어

<img width="60%" src="https://user-images.githubusercontent.com/86250281/134625039-e487b7d7-99d9-4e29-b4f8-77c5b1e20010.png"/>

* Root : 부모 노드 없는 노드
* Degree : 그 노드의 자식 수 degree(B)=2
* external node(leaf) : 자식노드 없는 노드
* internal node
* Ancestor : 어떤 노드 x에서 root부터 x까지 path의 노드들 -> x의 ancestor (자기자신 제외 : proper ancestor)
* Descendant : ancestor정의의 반대
* Subtree : 어떤 루트 노드가 x이고 x의 descendants로 이루어진 부분 tree

* root 의 depth : 0
* 트리의 level : 같은 depth의 노드들 (level2 : a, c, e)
* 트리의 height : 4
* 노드의 height : 그 노드가 root의 subtree의 height