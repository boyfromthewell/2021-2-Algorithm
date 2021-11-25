## The KMP algorithm

브루트 포스 알고리즘에 비해 더 shift 할 수 없을까?

* 왼쪽부터 오른쪽으로 비교해가다가 mismatch 발생하면 패턴을 얼만큼 shift 할 수 있을까 즉 가장 멀리 뛸수있는게 어딜까 생각 해 볼수 있음
* 중복되는 비교연산 피하기위해 패턴을 얼만큼 이동 시킬까
* 가장 긴 j번쨰 prefix와 suffix를 가지고 비교하기

### idea
<img width="60%" src="https://user-images.githubusercontent.com/86250281/143400790-c14cfd9f-bcdc-4063-995b-f2e450bf77d8.png"/>

지금까지 match 되었던 prefix안에서 일치하는 최장 proper prefix 정보와 proper suffix정보 이용

* 길이 1인 proper prefix, proper suffix -> a, b -> mismatch
* 길이 2인 proper prefix, proper suffix -> ab, ab -> match
* 길이 3인 proper prefix, proper suffix -> aba, aab -> mismatch ...

즉 패턴 내에서 가장 일치하는 proper prefix, proper suffix 정보는 ab, 이정보를 가지고 패턴을 멀리 shift할것

proper prefix(ab)와 text상의 ab를 align 시킴

## KMP Failure Function

패턴 preprocessing 하는 failure func먼저 계산해주어야함

<img width="60%" src="https://user-images.githubusercontent.com/86250281/143402543-59f0d7f2-551e-43e9-a8b9-a04fe7efde7c.png"/> 

첫번째 의미: 패턴의 index를 j라 했을때 j까지 prefix내에서 일치하는 가장 긴 prefix와 proper suffix의 길이를 저장 (길이 m인 array 하나로 계산가능 O(m))

* F(0): index 0 내에 일치하는 최대 proper prefix, proper suffix 길이 저장, but a에서 proper prefix, proper suffix는 empty string 밖에 없음 따라서 F(0)은 무조건 0
* F(1): a, b 비교 -> 다름 -> 0 저장
* F(2): 길이 1인 prefix, suffix 비교 (a,a) -> 일치, ab, ba 불일치 -> 최종 1 저장
* F(3): a, a 일치, ab, aa 불일치, aba, baa 불일치 -> 최종 1 저장
* F(4): a, b 불일치, ab, ab 일치, aba, aab 불일치, abaa, baab 불일치 -> 최종 길이 2 저장
* F(5): a, a 일치, ab ba 불일치, aba, aba 일치, abaa, aaba 불일치, abaab, baaba 불일치-> 가장 길게 일치하는 길이 3 저장

두번째 의미: 다음에 비교할 pattern의 index를 의미 (단, index가 0 based일때)

<img width="60%" src="https://user-images.githubusercontent.com/86250281/143404568-ae195f14-2043-424b-9987-7b008d4181c9.png"/>

지금까지 match된 정보를 가지고 failure func이용

* index 4까지 일치
* f(4) 이용!! (2 저장되있는 상태)
* 패턴이 shift하고 나서 다음에 비교할 char의 인덱스가 2라는 것 의미 -> 인덱스 2에 있는 값으로 다음 비교

정리: j=0에서 mismatch 발생한경우 brute-force, 
j>0이면 failure func 이용

```C++
Algorithm KMPMatch(T, P)
    F <- failureFunction(P) // O(m) time
    i <- 0 // text의 인덱스
    j <- 0 // pattern의 인덱스
    while i < n
        //match 부분
        if T[i] = P[j]
            if j = m - 1
                return i - j { match }
            i <- i + 1
            j <- j + 1
        //
        //mismatch 부분
        else if j > 0
            j <- F[j - 1] // failure func이용
        else //j=0일때 (브루트 포스)
            i <- i + 1
        //
    return -1 { no match }
```
* i 증가하는 case 최대 n까지 증가가능
* i 가만히 있는부분(mismatch)에서 추가적 loop실행 -> 패턴 많아야 n번 shift 가능
* 총 while loop의 worst case = 2n을 넘지 않음
* 따라서 KMP 알고리즘의 총 수행시간 O(m+n)

### Computing the Failure function

```c++
Algorithm failureFunction(P) // O(m) time에 계산 가능
    F[0] <- 0
    i <- 1
    j <- 0
    while i < m
        if P[i] = P[j]
            {we have matched j + 1 chars}
            F[i] <- j + 1
            i <- i + 1
            j <- j + 1
        else if j > 0
            {use failure function to shift P}
            j <- F[j - 1]
        else
            F[i] <- 0 { no match }
            i <- i + 1
```
* while loop 2m 넘을수 없음

### F(j) 구하기 example

<img width="70%" src="https://user-images.githubusercontent.com/86250281/143432534-e5a20af3-e6f0-4483-b8f4-f4fc182f0df4.jpg"/>

<img width="70%" src="https://user-images.githubusercontent.com/86250281/143432650-5f4a29d3-6341-4eb6-93a9-86bd3f0944da.jpg"/>

### Example

<img width="70%" src="https://user-images.githubusercontent.com/86250281/143432762-2afb86bb-1d14-474a-9110-cc559ac4f53f.png"/>

* 처음 b에서 mismatch
* 직전 index 4 -> F(4) 확인 : 1
* 다음 패턴 index 1 에 맞춰줌
* a, b 불일치 -> F(0) 확인 : 0
* 다음패턴 index 0 에 맞춰줌
* c, a 불일치
* 직전 index 3 -> F(3) 확인 : 0
* 다음패턴 index 0 에 맞춰줌
* c, a 또 불일치 (j=0)
* brute-force 실행
* 패턴 일치

19번의 비교연산으로 탐색 완료

## Boyer-Moore Heurisitics

두가지 Heuristics 전략 사용 알고리즘 

Heuristics-어떤 알고리즘이 Heuristics이라 하는것은 최적해를 찾는것인데 그중에서 global optimal solution이 있고, local optimal solution이 있음  
global optimal solution은 전체 input에 대해 최적해를 찾는것이고, local optimal solution은 전체적으로는 최적이 아닐수 있지만, 최적에 가까운 지역적으로는 최적의 solution 찾는 방법이 있음.  
그중에 Heuristics 알고리즘은 global optimal solution 찾는데 굉장히 오랜시간 걸릴 수 있고 빠른시간에 local optimal solution 계산 보장하는 알고리즘 - Heuristics 알고리즘  
(global opimal solution 보장하지 않지만 빠른시간에 global에 가까운 optimal solution 계산해줄수 있다.)

1. Looking-glass (거꾸로의, 반대의) heuristic : pattern의 오른쪽부터 왼쪽으로 비교
2. Character-jump heuristic: mismatch 발생한경우 text에 char을 기준으로 그 char가 패턴에서 마지막으로 발생한 위치가 어디인지를 살펴 보는 것 (더 앞에있다면, 그 위치가 align되도록 패턴을 shift해줌), 어떤 text에 char가 패턴에는 존재하지 않는다면 (bad character) 그 다음 index에 align 하도록 점프 많이해줌

### example
<img width="70%" src="https://user-images.githubusercontent.com/86250281/143436021-25cd13f8-c1ab-4299-9c25-72a0f249cd34.png"/> 

어떤 char가 존재하는지 존재하지 않는지 해당 char가 마지막에 발생 위치어디인지 미리 preprocessing 해줘야함 -> Last-occurrence function

## Last-occurrence function

Σ= {a, b, c, d}, P = abacab라면 그것에 대한 string은 a,b,c,d로만 이뤄져야함  
Last-occurrence function의 크기->|Σ|=s

<img width="70%" src="https://user-images.githubusercontent.com/86250281/143437865-9467115f-4923-46a8-ba2e-307425be5665.png"/>

* 처음에 모든 data -1로 초기화
* index 0에서 발썡 -> 함수 +1
* index 1에서 b 발생 -> 함수 b 1로 업데이트
* 그다음 a (index 2)-> 함수 a 2로 업데이트
* 그다음 c (index 3) -> 함수 c 3으로 업데이트
* 그다음 a (index 4) -> 함수 a 4로 업데이트
* b (index 5) -> 함수 b 5로 업데이트

Last-occurrence function : O(m+s) time 에 수행가능(P사이즈: m, 시그마사이즈: s)