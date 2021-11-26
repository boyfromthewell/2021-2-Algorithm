## The Boyer-Moore Algorithm

```c++
Algorithm BoyerMooreMatch(T, P, Σ)
    L <- lastOccurenceFunction(P, Σ) // O(m+s) time
    i <- m - 1 // 패턴의 가장 오른쪽 인덱스로 초기화, T의 인덱스
    j <- m - 1 // P의 인덱스
    repeat
    //match 한경우
        if T[i] = P[j]
            if j = 0
                return i { match at i }
            else
                i <- i - 1
                j <- j - 1
    //mismatch한 경우
        else
            { character-jump }
            l <- L[T[i]]
            i <- i + m – min(j, 1 +l) // 두가지 케이스 포함한 수식 : j=case 1, 1+l=case 2
            j <- m - 1 // lookiing-glass 사용하기 위해 항상 P마지막 위치로 업데이트
    until i > n - 1
    return -1 { no match }
```
<img width="60%" src="https://user-images.githubusercontent.com/86250281/143593804-032a5b70-5b8f-4775-adfa-97721e691ee9.png"/>  

mismatch 발생한 경우 두가지 케이스로 구분가능
* case 1: bad-character가 같거나 오른쪽에서 발생한경우 -> 단순하게 패턴 오른쪽으로 한칸만 이동
* case 2: bad-character가 더 왼쪽에서 발생한경우  

주의 해야할 점: 패턴을 이동한다는것은 실제로는 text의 인덱스 i를 증가 시켜줘야함  
위 예시에서 i를 어떻게 증가시키는가?
* case 1: m=패턴 길이=6, j=4, 6-4=2 -> i값 2만큼 증가시켜준다
* case 2: m=6, l=1, 6-(1+1)=4 -> i값 4만큼 증가시켜준다

### example

<img width="70%" src="https://user-images.githubusercontent.com/86250281/143596027-7fe60411-bfdf-4530-8430-c557a707bbc1.png"/>

* 처음부터 mismatch a,b
* a가 패턴에서 상대적으로 왼쪽에 발생 (항상 마지막 위치만 고려해주자)
* 패턴을 a에 align 되도록 이동
* b -> a 일치하다가 (a,c) mismatch
* 패턴에 a가 bad-char보다 더 오른쪽에 위치
* 단순히 한칸 이동
* 처음 a, b mismatch, a가 발생하는 마지막위치 상대적으로 왼쪽
* a align 되도록 패턴 이동
* d, b mismatch
* d 존재 x-> last-occurrence func에 의해 d=-1이므로 패턴이 d이후 align 되도록 이동
* a,b mismatch
* a 상대적으로 왼쪽 위치, a align되도록 패턴 이동
* 패턴 발생, 종료 (13번의 비교)

KMP 알고리즘에 비해 더 빠르게 수행가능

## Analysis

Boyer-Moore 알고리즘 수행시간 : O(nm+s)

* worst case
    * T=aaa..aa
    * P=baaa (항상 매치하다가 마지막에 미스매치 발생하는 경우) 
    
        <img width="50%" src="https://user-images.githubusercontent.com/86250281/143597628-a12e140e-b805-41f7-894c-65a311cf6acc.png"/> 
        
        이런경우 계속 브루트 포스 알고리즘과 똑같이 수행 -> O(nm) time 에 수행
* preprocessing: O(m+s) time
* searching: O(nm) time
* total -> O(nm+s) time

worst case의 경우 english text의 경우 거의 발생 x  
따라서 Boyer-Moore 알고리즘은 worst case에 대한 수행시간은 느리지만, average case에서는 상당히 빠른 수행시간을 가짐

***

# 13. NP-Complete problems
 
 class P, class NP, class NPC가 있음  
 누군가 open problem 제시, P=NP?

## problems and algorithms

각 문제마다 고유의 complexity 가짐, 문제의complexity는 그 문제를 해결하는 가장 좋은 알고리즘의 complexity이다  
가장 좋다는 의미는 현존하는 알고리즘에서 좋다는것이 아닌, 가능한 모든 알고리즘들 중에서 좋다는 것을 의미  
앞으로 나타날수도 알고리즘 까지 포함해서 이 알고리즘보다 더 빠를 수 없다는 best 알고리즘에 대한 complexity가 문제의 복잡도라고 할수 있음

## Optimization Problems Vs. Decision Problems
* Optimization Problems
    * 다양한 솔루션 존재 할수있지만 가장 좋은 솔루션 찾는 문제
    * ex. shortest-path문제
*  Decision Problems (결정 문제)
    * yes or no
    * PATH : 그래프 주어지고 yes or no 로 대답할수있는 정수 k 주어짐-> k 기준으로 k edges만큼 갈수 있는 path존재 하는가?

## Polynomial Time: Class P

Polynomial time에 수행 할수있는 문제 정의
* T(n)=O(n^k) 
* ex. O(n^3logn), O(n^4)

어떤 문제(decision problem)가 polynomial time 알고리즘이 존재한다면 그런 문제들을 class P 라고 부름

그런 알고리즘들은 efficient하다고 볼것임, 문제에 대해서는 easy하다고 표현

## Some Problems are Very Hard

어떤 문제들은 Polynomial Time에해결하는 법 찾지 못했음  
대표적으로 0/1 knapsack problem, traveling salesperson problem(TSP)가 있음
* 0/1 knapsack problem(->NPC)  
동굴에 n개의 보물(item)이 있다.
ith item은 Vi dollars 와 Wi 무게를 갖는다(Vi, Wi는 양수)
가방에 W(integer)무게만큼 담을수 있을때, 도둑은 가능한 비싼 물건(optimization problem)을 담길 원한다. 어느 item을 가져가야 할까?
이때 k 이상의 이득이 되도록 담을 조합이 있는가?-> decision problem  
(단, 도둑은 각 item을 가져가든기 가져가지 않아야함, item의 일부분 가져갈수 없음, 한번이상 가져갈수 없음)
    * Fractional Knapsack problem  
    ->item의 일부분 가져갈수 있음 (다항시간에 해결가능)

* traveling salesperson problem(TSP)(->NPC)  
complete weighted graph가 주어졌을때, 1. 최소비용(optimization problem)으로 모든 vertex를 한번씩만 방문하는 cycle은? 2. cycle의 weight k이하로 -> decision problem)
    * Euler tour problem  
    connected digraph 주어졌을때 모든 edge를 한번씩만 방문하는 cycle 존재하는가?
    (다항시간에 해결가능 O(m) time)

* Undecidable problems : 결정 할수 없는 문제 즉, 컴퓨터로 해결할수 없는 문제 (turing machine 정지 or 무한루프 될것인가)

### Dealing with Hard Problems
Polynomial Time 알고리즘을 찾을수 없었을때, 나만 못찾은것이 아닌 다른사람들도 마찬가지로 모두가 어려워하는 문제라 아직 Polynomial Time 알고리즘 찾을수 없다!!!!! -> NP Complete 문제 증명하는 방법