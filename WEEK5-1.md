## Insertion Sort : 분석

* Worst Case Complexity

    어떤 index i에 x가 있다면 최악의 경우 앞에 있는 모든 원소들과 비교하는 경우

    <img width="60%" src="https://user-images.githubusercontent.com/86250281/135387898-bafcdc49-f422-431d-90c7-25eb10496b91.png"/>

* Average behavior

    각각의 i에 대한 shiftVacRec 함수의 기본연산수가 핵심

    <img width="60%" src="https://user-images.githubusercontent.com/86250281/135388421-66028a1d-761e-44bf-87da-6602659ec30a.png"/>

    이런 자료형이라고 가정하면 index 5부터 0까지의 비교연산은 1, 2, 3, 4, 5, 5이다 (인덱스 0,1은 비교연산수 동일)
    따라서 index 0에서는 하나의 비교연산 case가 존재하고 index 1~5까지의 경우에는 i cases의 비교연산이 존재한다 -> 총 i+1

    각 케이스 일어날 확률 모두 같다고 가정하므로 1/(i+1), index 0에선 앞에있는 모든 원소와 비교 해야 하므로, i번의 비교연산 수행 -> i/(i+1)

    따라서
    
     <img width="60%" src="https://user-images.githubusercontent.com/86250281/135389134-425b0033-c501-4871-84af-155673cce1a3.png"/>

오직 인접한 element끼리 교환 할때만 optimal 하다고 볼수 있다. (순차접근), 최선의 정렬 알고리즘은 아님

## Qucik Sort 

Worst case : Θ(n^2), but 일반적인 경우 가장 빠름 (평균 Θ(nlogn))

### divide and conquer (분할정복법)

어떤 문제를 해결할 때 여러개의 작은 문제로 쪼개서 해결하기 

1. divide (어떤 문제 여러개의 문제로 쪼개기)
2. conquer (서브 문제들 푸는 단계, 대개 재귀적으로 품  )
3. combine (서브 문제들 해결법 합쳐주는 단계)

### Quick sort

divide and conquer와 randomization 전략 사용

n개의 원소중에 임의의 원소 선택 (pivot)

pivot을 기준으로 세개의 그룹으로 나눠줌
* L - pivot보다 작은 원소들
* E - pivot과 같은 원소들
* G - pivot 보다 큰 원소들

<img width="60%" src="https://user-images.githubusercontent.com/86250281/135392788-455b7ccc-3466-44c6-9c83-026572b3270a.png"/> 위와같이 계속 재귀적 수행

```c
partition(S, p)
//자료형 리스트라고 가정(배열도 가능(환형배열))

    Input: sequence S, position p of pivot
    Output: subsequences L, E, G of the
        elements of S less than, equal to,
        or greater than the pivot, resp.
    L, E, G <- empty sequences
    x <- S.remove(p) // O(1) time
    while !S.isEmpty() // O(n) iterations
        y <- S.remove(S.first()) // O(1) time
        if y < x
            L.insertLast(y) // O(1) time
        else if y = x
            E.insertLast(y) // O(1) time
        else { y > x }
            G.insertLast(y) // O(1) time
    return L, E, G
```

* Worst case 

    pivot이 가장 작은 값이거나 가장 큰 값으로 선택된 
    
    L 이나 G는 n-1의 사이즈 가지게 되고 다른 하나는 0 일것

    <img width="60%" src="https://user-images.githubusercontent.com/86250281/135393779-66c19812-7da0-46d1-8374-ca7030f71161.png"/>

    피벗 e를 제외한 나머지 원소 n-1, n-2, ... 2, 1번의 비교 연산 수행 

    따라서  n+(n-1)+...+2+1 -> O(n^2) worst case