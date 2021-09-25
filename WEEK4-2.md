## Binary Tree ADT

1. depth가 d이면 많아야 2^d개의 노드를 가진다 (완전이진트리일때)

<img width="60%" src="https://user-images.githubusercontent.com/86250281/134760380-1bdb07aa-912a-4981-977c-31da88fbc25c.png"/>

2. 높이가 h이면 최대 (2^h+1)-1 의 노드를 가진다

<img width="60%" src="https://user-images.githubusercontent.com/86250281/134760388-846a2e6f-8506-479e-ad45-0e30eb488d76.png"/>

3. 노드가 n개인 binary tree는 적어도 log(n+1)-1의 height가진다

<img width="60%" src="https://user-images.githubusercontent.com/86250281/134760457-181d401d-94de-4f49-ae2b-806560840bd6.png"/>

***

* Stack
    * 선형 구조
    * 삽입연산 push, 삭제연산 pop
    * last in, first out(LIFO)
* Queue
    * 선형구조
    * 삽입연산 enqueue 삭제연산 dequeue (가장앞의 값)
    * first in, first out(FIFO)

* Priority Queue
    * 데이터 도착시간 우선순위로 두고 동작, 가장 먼저 도착 데이터 삭제
    * cost viewpoint : 비용적을수록 우선순위 주는것 (min priority queue)
    * profit viewpoint : 이익 많을수록 우선 순위 (max priority queue)
    
    |      |unsorted sequence|sorted sequence|(binary) heap
    |------|----|----|----|
    |insert|O(1)|O(n)|O(logn)
    |removeMin|O(n)|O(1)|O(logn)
    |getMin|O(n)|O (1)|O(1)|

## Union-find ADT for Disjoint sets

* Union, find 연산
* connected component 찾는 문제에 적용가능 (undirected graph)
* 각각의 집합 id s,t라 하면 둘다 다를때만 union시켜줌, union 된 집합 키 s or t
* find - set id 리턴

### Dictionary ADT

* (key, element) 로 구성
* hashing, binary search tree등오로 구현

# 4. Sorting

* Insertion sort/ O(n^2)
* Quick sort/ O(n^2) (기대 수행시간 : O(nlogn))
* Merge sort/ O(nlogn) 
* Heap sort/ O(nlogn)
* Radix sort/ O(n) (input에 특정 제한사항이 있을경우, O(n)에 수렴)

## Insertion Sort

* 인덱스 0은 정렬된 상태라 가정(sorted segment), 나머지 요소들은 (unsorted segment) 
* 인덱스 1 x라 하면 일단 밖으로 빼고 인덱스1 vacancy로 남겨둠(빈공간)
* x가 sorted segment보다 작으면 swap
* n-1번 반복

<img width="60%" src="https://user-images.githubusercontent.com/86250281/134761529-0b745646-e164-4679-8454-78f507272f4b.png"/>

* loop invariant 분석방법 (수학적 귀납법과 유사)
    1. Initalization -  알고리즘이 loop에서 첫번째 iteration 수행전에 그 알고리즘이 어떤 속성 만족시켜야함
    2. Maintenance - loop에서 어떤 iteration 수행전에 참이면 다음 iteration 수행도 참
    3. Termination - 모든 loop 가 종료되고, 알고리즘이 정확히 수행됬음을 보여줘야함

* insertion sort 에 적용
    1. index 0 - 초기화 단계, 정렬된 상태이다 
    2. 어느 한 인덱스에서 loop 수행하면 정렬된 상태 만족
    3. 모든 loop 끝나면 정렬상태 만족 

```python 3
def insertion_sort(arr):
    n=len(arr)
    for i in range (1, n):
        # i 번 위치의 값을 key로 저장
        key=arr[i]
        # j를 i 바로 왼쪽 위치로 저장
        j=i-1
        #리스트의 j번 위치의 값과 key를 비교해 key 삽입 위치 찾기
        while j>=0 and arr[j]>key:
            arr[j+1]=arr[j] # 삽입할 공간 생기도록 값을 오른쪽 한칸 이동
            j-=1
        arr[j+1]=key # 찾은 삽입 위치에 key를 저장
        
data=[2,4,5,1,3]
insertion_sort(data)

print(data)
```


