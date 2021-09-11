## how to show an algorithm is Optimal

효율적인 알고리즘 구별법 : worst case complexity W(n) 분석, 적어도 이만큼의 연산 사용해야 한다는 F(n) 구하기

만약 W(n)=F(n)? 

* 이 알고리즘은 optimal 하다!! (현존하는 알고리즘중 가장 좋다, 더 좋은거 나올 수 x)

* 일치하지 않으면 2가지 경우->더 좋은 알고리즘(upper bound)이 존재할수 있거나, 더 좋은 lower bound(문제복잡도)가 존재 할 것이다

* 행렬 곱셈의 예
    * 아직 optimal한 알고리즘 찾지못함 
## Optimality의 예
```c++
int findMax(int[], int n){
int max
max = E[0];
for(index = 1; index < n; index++)
    if(max < E[index]) //basic operation
        max = E[index];
return max;
}
```
1. W(n) 찾기

    * basic operation : 저장되어있는 원소들간의 비교연산
    * 어떤 input size n에 대해 정확히 n-1번 수행함
    * W(n)=n-1

2. F(n) 찾기

    * class of 알고리즘 : 비교연산과 copy연산 사용
    
    Finding F(n)

    * 배열안의 값 다 다르다고 가정(같은값 있어도 사실 상관 x)
    * n개의 다른 요소들, n-1 개의 엔트리는 max값이 아니다.
    * n-1의 값들이 max값이 아닌거 알려면 최소한 한번의 비교는 해봐야함
    * 적어도 n-1번의 기본연산 수행해야함
    * F(n)=n-1

So, 이 알고리즘은 optimal하다

***

## 점근적 증가율에 의한 함수 정의

input size n이 충분히 커지면 어떤 증가율을 보이나 -> 점근적 증가율
(최고차항만 가지고 함수 비교)

* O(g):  함수들 g보다 더 빠르게 증가할수 x (증가율 같거나 더작은 함수 집합), upper bound
* Ω(g): 함수들 g보다 더 빠르게 증가
(증가율 같거다 더 큰 함수 집합), lower bound
* θ(g): 위 두함수의 교집합 (함수 최고차항 같음)

어떤 c와 n0에 대해 각각의 부등호 식 만족하면->
<img width="60%" src="https://user-images.githubusercontent.com/86250281/132954841-6d38ce33-341b-4a9f-9ef2-54dfc13a18e7.png"/>

<img width="70%" src="https://user-images.githubusercontent.com/86250281/132954969-31c8d479-57f3-406b-ad33-d244220f0487.png"/>

* <무한대, 0 or 상수 C

    ex) lim 7n+100/n^2+3=0

    lim 7n^2/n^2+3=7

    f -> O(g)

* C or 무한대

    f -> Ω(g)
* =c and 0 < c < 무한대 (항상 최고차항 같은경우)

    f -> θ(g)

***

<img width="70%" src="https://user-images.githubusercontent.com/86250281/132955160-f8ef8a8a-0d4d-4964-8533-f017fb157b49.png"/>

알고리즘 A=O(n^2)

알고리즘 B=O(n)

일반적인 경우 알고리즘 B를 선택할것

but, input size가 25보다 작다면? 알고리즘 A가 더좋음 (복잡도 더 크더라도 input에 따라 선택 다를수 있음!!)



