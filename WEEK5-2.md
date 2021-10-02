## * Outline of average case analysis for quick sort (informal analysis)

<img width="60%" src="https://user-images.githubusercontent.com/86250281/135719123-18c60da5-1916-494d-95ba-e6edf4104363.png"/>

다음과 같이 정렬된 배열이 있다 했을 때 best의 경우는 pivot이 가운데 위치하는 경우  (2/n 지점)

그럼 average의 경우는 best와 worst case 중간지점 쯤 되는 경우라고 볼 수 있다 n/4과 3n/4 각각 지점


L : G 그룹이 있으면 1 : 3의 비율로 partition 된다 가정 (n/4, 3n/4)

<img width="60%" src="https://user-images.githubusercontent.com/86250281/135719768-09fb87ea-bee3-4fdb-bc87-2cc8b0df33ed.png"/> 

* 가정에 의해 l g 그룹으로 나누면 이런 형식으로 남은 원소가 1이 될때까지 나눌것임 (g쪽이 더 길게)

* 각각의 level에서 partition O(n)에 수행

* 가장 깊은 height k라 하고 구하기 (g라인)

* n 에서 3/4를 얼만큼 곱해야 1이 될까?

<img width="60%" src="https://user-images.githubusercontent.com/86250281/135720110-50257dd7-9aab-4331-9251-e23a92d97da2.png"/>

따라서 k <= c * logn 를 만족하는 c가 존재할것임 -> 트리의 height : θ(logn)에 bound

그러므로 총 알고리즘 평균시간 O(nlogn) time 이라고 볼 수있다

(꼭 1:3으로 하지않고 1:9, 1:99 등으로 해도 성립함)

## In-place Quick sort

* In-place : space를 적게 사용하는 경우를 말함 (additional O(1) space)

O(logn)도 재귀의 경우에선 in-place라고 허용해줌

```c
Algorithm inPlaceQuickSort(S, l, r)
    Input sequence S, ranks l and r //rank : index 라고 생각
    Output sequence S with the
        elements of rank between l and r
        rearranged in increasing order
    if l >= r
        return
    i <- a random integer between l and r
    x <= S.elemAtRank(i)
    (h, k) <- inPlacePartition(x)
    inPlaceQuickSort(S, l, h - 1) // L 그룹에 대한 재귀
    inPlaceQuickSort(S, k + 1, r)// G 
```
랜덤으로 피벗 i를 고름

L 그룹 (l : h-1), E 그룹(h : k), G그룹 (k+1, r)로 분할 가능

## in-place partitioning

* L그룹과 E U G 그룹으로 partition
<img width="60%" src="https://user-images.githubusercontent.com/86250281/135721833-f33d7880-40cc-4269-919e-f4588f707973.png"/>

* 밑의 과정 j과 k 가 만날때까지 반복

    1. j를 pivot 보다 크거나 같은값 만날때까지 오른쪽으로 찾기
    2. k를 pivot 보다 작거나 같은값 만날때까지 왼쪽으로 찾기
    3. j, k swap

계속 하다보면 j와 k는 9에서 만나게됨, 마지막으로 9와 pivot 6의 위치를 swap해준다

<img width="60%" src="https://user-images.githubusercontent.com/86250281/135722221-a450863f-4651-459f-9895-043846e4cfad.png"/>

j 와 k 만난 index를 경계로 왼쪽에는 pivot보다 작은 수들이 오른쪽에는 pivot보다 큰 수들과 pivot이 위치 하게됨 (L과 E U G 로 파티션)

(상수 크기의 O(1) space이용해서 파티션 수행가능)

*** 

# Merge sort

* Problem
    * 오름차순 정렬된 시퀀스 A,B -> 하나의 정렬 시퀀스 C로 merge하기
* Strategy
    * A, B 첫번쨰 원소 비교해서 작은 값 C 맨앞으로 이동시켜 주기 , 점점 작은거 앞으로 채워주면 정렬된 merge 시퀀스 C 얻을수 있다

```C
Merge(A, B, C)
    if (A is empty)
        rest of C = rest of B //A가 빈경우 B 나머지 C에 채우기
    else if (B is empty)
        rest of C = rest of A //B가 빈경우
    else if (first of A ≤ first of B)
        first of C = first of A
        Merge (rest of A, B, rest of C)
    else
        first of C = first of B
        Merge (A, rest of B, rest of C)
    return
```
최악의 경우 : 빈경우 나머지 채워주는 부분 발생되지 않고, 원소간의 비교연산 많이 하는경우 (A,B 앞부분 번갈아가면서 C에 채워지는 경우)

W(n) = n-1 -> θ(n) time 에 수행

<img width="60%" src="https://user-images.githubusercontent.com/86250281/135723150-6003feab-22ed-419f-9ac4-9f32dbe806a6.png"/>

* 위와 같이 계속 재귀적으로 leaf사이즈 1이 될때까지 나눠줌

* 사이즈 1인 원소끼리 비교해서 정렬 merge

ex) 
[6] [5] [3] [1] [8] [7] [2] [4] ->

[5, 6] [1, 3] [7, 8] [2, 4] -> 

[1, 3, 5, 6] [2, 4, 7, 8] 

-> merge [1, 2, 3, 4, 5, 6, 7, 8]

<img width="60%" src="https://user-images.githubusercontent.com/86250281/135723779-36282964-b810-4845-8ac0-9f01df21297f.png"/>

merge 알고리즘과 각각의 level 수행하는데 각각 θ(n) 타임이 걸림, 이것의 height k를 구해보자

마찬가지로 n x (1/2)^k =1, n= 2^k 이라 할수 있으므로 k=logn

그러므로 총 수행시간 W(n/2)+W(n/2)+Wmerge(n) -> θ(nlogn)

* Wmerge(n)=n-1
* W(1)=0


** merge sort = postorder 순서대로 수행 , quick sort= preorder순서로 수행
