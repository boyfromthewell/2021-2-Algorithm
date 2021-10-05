# Heap and Heapsort

heap 기본적으로 세가지 기능 지원(maxheap 기준)
1. insert()
2. findMax()
3. deleteMax()

heap은 구조 조건과 순서조건 만족시켜줘야 함

* 구조조건
1. binary tree T는 depth h-1까지는 꽉 차있어야함
2. 모든 leaf노드의 depth는 h or h-1
3. leaf노드 왼쪽부터 채워진다, 삭제는 오른쪽부터 삭제

(이런트리 left-complete binary tree라고도 부름)

* 순서조건
    * 임의의 노드의 키값이 자식노드보다 크거나 같다 (parent(v).key >= v.key)

## heapsort Strategy

원소들이 힙으로 잘 정렬되었다면, maxheap이기 때문에 root노드 삭제하면서 가장 뒤에다가 추가

<img width="60%" src="https://user-images.githubusercontent.com/86250281/135981017-a02f56dc-3004-46f6-9106-3e0724790a53.png"/>
(순서 조건 만족시키기 위해 upheap() 함수 사용)

* insert() : O(logn) time
* deleteMax() : root부터 leaf까지 내려갈수 있으므로 O(logn) time
* findMax() : O(1) time (그냥 root노드 찾기)

```c
heapSort(E, n) // Outline
construct H from E, the set of n elements to be sorted // 힙 생성 먼저하기 (O(n) time에 수행)
for (i = n; i ≥ 1; i--)
    curMax = getMax(H)
    deleteMax(H);
    E[i] = curMax;
```
```
deleteMax(X)

가장 아래 level 오른쪽에 있는 key값을 임시변수 K에 카피하고 삭제-> fixHeap 수행 = downHeap
```
```c
fixHeap(H, K) // Outline
if (H is a leaf)
    insert K in root(H);
else
    set largerSubHeap to leftSubtree(H) or rightSubtree(H), whichever
    has larger key at its root. This involves one key comparison. // 두 자식들 대소비교 (1회비교 연산)
    if (K.key ≥ root(largerSubHeap.key) // key값과 자식노드 중에 큰 자식과 대소 비교 (1회 비교연산) -> 총 2회 비교연산
        insert K in root(H);
    else //만약 자식이 더 크다 ? -> swap시켜줌
        insert root(largerSubHeap) in root(H);
        fixHeap(largerSubHeap, K);
return;
```
높이를 h라하면 최대 2h의 비교연산 -> W(n)=2log(n)에 bound

<img width="60%" src="https://user-images.githubusercontent.com/86250281/135983816-55b284a2-b98b-40b7-b673-3ea895a2232d.png"/>

### Construct Heap Outline (O(n) time)
* input : complete binary tree의 구조는 만족하지만 순서조건은 만족하지 않는 H
* Output : 순서조건까지 만족하는 H

```c
void constructHeap(H) // Outline
if (H is not a leaf)
    constructHeap (left subtree of H); 
    constructHeap (right subtree of H);
    Element K = root(H);
    fixHeap(H, K);
return;
```
왼쪽 서브트리와 오른쪽 서브트리 힙 만족시킨후 원소하나 root에 추가하고 fixHeap해주기

<img width="60%" src="https://user-images.githubusercontent.com/86250281/135984708-6c8749a5-0878-489b-9d6e-d596531dca9d.png"/>

***
constructHeap 분석

<img width="70%" src="https://user-images.githubusercontent.com/86250281/135989398-b2c34568-6b3d-43fa-94de-ec2210d65353.jpg"/>

## Heap implementation using and Array

* 인덱스 1부터 사용
* 나의 index i일때
    * left child index -> 2i
    * right child index -> 2i+1
    * parent -> i//2

### heapsort Analysis

n번의 deleteMax(), fixHeap은 n-1개의 노드에서 수행

-> 2log(n-1)+2log(n-2)+....+2log1 = 2log{(n-1)* (n-2)* ...*1}=2log(n-1)!

* stitrling's approximation에 의해 log(n!)=>θ(nlogn) -> 2log(n-1)!은 θ(nlogn)에 bound

* heapsort에서 비교연산의 총수는 2nlog(n)=fixheap + O(n) = heap construct => θ(nlogn)에 bound

    * merge, heap sort 모두 optimal

## Accelerated heapsort

* 앞선 heapsort보다 2배의 속도 개선 (h comparisons)
* 분할 정복법 적용 (binary search와 비슷)
    1. 서브 heap의 높이 h라했을떄 h/2 까지 내려감
    2. 나의 값 K와 parent 값과 비교
    3. K가 더크면 위쪽 살펴보기 (아래쪽 볼 필요 x)
    4. parent가 더 크면, 재귀적으로 또 h/2 수행(아래로)

```c
void bubbleUpHeap (Element[] E, int root, Element K, int vacant)
if (vacant == root)
    E[vacant] = K;
else // p가 크면 더이상 올라갈 필요 x
    int parent = vacant / 2;
    if (K.key ≤ E[parent].key)
        E[vacant] = K;
    else
        E[vacant] = E[parent]; //k가 p보다 크면 재귀적으로 계속 p와 swap하기
        bubbleUpHeap (E, root, K, parent);
```
```c
void fixHeapFast(Element[] E, int n, Element K, int vacant, int h)
if (h ≤ 1)
    Process heap of height 0 or 1
else
    int hStop = h/2 // h/2까지 promote함수 통해 내려가기
    int vacStop = promote (E, hStop, vacant, h);
    // vacStop is new vacant location, at height hStop
    int vacParent = vacStop / 2;
    if (E[vacParent].key ≤ K.key) //P값과 나의 값 비교 (내가 더 크면 bubbleupheap 수행)
        E[vacStop] = E[vacParent];
        bubbleUpHeap (E, vacant, K, vacParent);
    else // 내가 작으면 제대로 내려온것, 재귀적 fixheapfast수행
        fixHeapFast (E, n, K, vacStop, hStop);
```
```c
int promote (Element[] E, int hStop, int vacant, int h)
int vacStop;
if (h ≤ hStop)
    vacStop = vacant;
else if (E[2*vacant].key ≤ E[2*vacant+1].key) // 왼쪽자식 오른쪽 자식 비교해서 큰쪽으로 내려가기
    E[vacant] = E[2*vacant+1];
    vacStop = promote (E, hStop, 2*vacant+1, h-1)
else //왼쪽 자식이 큰 경우
    E[vacant] = E[2*vacant];
    vacStop = promote (E, hStop, 2*vacant, h-1);
return vacStop;
```
ex

<img width="50%" src="https://user-images.githubusercontent.com/86250281/135995960-5e3643bf-a577-4b7f-97e0-2d17bcf2e161.png"/><img width="50%" src="https://user-images.githubusercontent.com/86250281/135996027-5ec93365-cc82-4070-965a-0322a2791476.png"/>
