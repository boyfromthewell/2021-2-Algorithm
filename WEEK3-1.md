## Properties of O(g), Ω(g), θ(g)

* Transitive(이행성) : f ∈ O(g) 이고 g ∈ O(h) 이면 f ∈ O(h) 이다 (Ω, θ, o, w도 만족)

* Reflexive(반사성): f ∈ θ(f)

* Symmetric(대칭성): f ∈ θ(g) 이면 , g ∈ θ(f)

* θ 는 동치관계 (위의 세가지 다만족)

* f ∈ O(g) <-> g ∈ Ω(f)

* O(f+g) = O(max(f,g)): 최고차항만 고려

***

* O(1) - input size n이 어떻던 항상 같은 연산개수, 같은 크기 사용

* f ∈ θ(n) : f는 일차식(linear)
* f ∈ θ(n^2) : f는 이차식(quadratic), f ∈ θ(n^3) : f는 3차식(cubic)

* log n ∈ o(n^α) : log n 에대한 증가율은 다항함수보다 증가율이 작다

* n^k ∈ o(c^n) (k>0 and c>1) : 다항함수는 지수함수보다 더 작은 증가율 보임

<img width="50%" src="https://user-images.githubusercontent.com/86250281/133279751-316caf6e-70d7-4e3a-add1-0b5e4a85e2ce.png"/>
n^d+1 생략하면 안됨!

but 2^n+1 의 지수 1 생략가능 (2^n+1 ∈ θ(2^n))

2*2^n이기 떄문에 앞에 계수 무시 가능

<img width="50%" src="https://user-images.githubusercontent.com/86250281/133280973-d017b31e-19fe-41b3-aa4a-6060553de08a.png"/>

log1 + log2 +...+ logn

=log(1 * 2 * ....* n)=log(n!)

따라서 log(n!)은 θ(nlog n)이다

* Stirling's approximation
    * n! ∈ O(n^n) (n!이 더 낮은 증가율 보인다)
    * n! ∈ w(2^n) (n!은 2^n보단 증가율 크다)
    * log(n!) ∈ θlog(n^n) (증가율 같아진다)

## Searching an ordered Array

* 문제 : 배열 탐색
    * 배열 E와 키값 K, 만약 찾는값 배열에 있으면 K=E[index] 해당 인덱스 리턴, 없으면 리턴 -1
* 전략 A
    * 정렬되지 않은 배열 사용
    * 순차 탐색
* 알고리즘 A
    * int seqSearch(int [] E, int n, int K)
* 분석 A
    * W(n) = n
    * A(n) = q[(n+1)/2]+(1-q)n
* Optimality A
    * F(n)=n
    * 알고리즘 A는 optimal하다

* 전략 B
    * input data가 정렬된 배열 이라면?
    * 순차 탐색
* 알고리즘 B
    * int seqSearch(int [] E, int n, int K)
* 분석 B
    * W(n) = n
    * A(n) = q[(n+1)/2]+(1-q)n

* Optimality B
    * 오름차순 정렬된 배열이라는 정보사용 X
    * 추가 정보 사용해서 알고리즘 개선하자

* 전략 C
    * input data 오름차순 정렬 배열
    * K보다 더 큰값을 만나면 그 이후는 다 K보다 큰 값이기 때문에 return -1

```C
int seqSearchMod(int[] E, int n, int k)
1. int ans, index;
2. ans = -1;
3. for(index = 0; index < n; index++)
4.    if(K > E[index])
5.        continue;
6.    if(K < E[index])
7.        break;
8.    //K==E[index]
9.    ans=index;
10.   break;
11. return ans;
```

* W(n)=n+1 ≒ n

배열 맨끝에서 찾은경우가 worst case

4번에서 인덱스 0 부터 n-1까지 비교연산 n번 수행

k와 마지막 k가 같을때 비교연산 1번수행

so, k가 마지막에 있던지, n-2보단 크고 n-1보단 작던지 (최악의 경우)

Total: n+1의 비교

* Average case

A(n)=Pr(succ) * Asucc(n) + Pr(fail) * Afail(n)

보통 Pr(succ)= q, pr(fail)= 1-q 

<img width="70%" src="https://user-images.githubusercontent.com/86250281/133286336-ce827826-10e8-409a-a86a-5ba115345aaf.png"/>

<img width="50%" src="https://user-images.githubusercontent.com/86250281/133287299-25830edd-662c-4b80-8c09-77e679bfab93.png"/>

n개의 case에서 각각의 확률 동일하다 가정 -> n/1

<img width="30%" src="https://user-images.githubusercontent.com/86250281/133287414-dc2296da-fdc2-42aa-83a1-ef52b6ed9f86.png"/>

t(I)->인덱스 0에 k있으면? 비교 한번, 인덱스 1에 k있으면 비교 2번..... 인덱스 i에 k있으면 비교 i+1번 

***

<img width="70%" src="https://user-images.githubusercontent.com/86250281/133288008-0f43e969-7db8-4d07-b28f-501e1c174276.png"/>

<img width="70%" src="https://user-images.githubusercontent.com/86250281/133288156-653b1e95-bf8b-4fce-bf85-b0364291e073.png"/>

total n+1개의 case (gaps)존재

<img width="60%" src="https://user-images.githubusercontent.com/86250281/133288559-df041b9f-d7a4-4321-8f1b-d664bbf62cf6.png"/>

각각의 확률 case n+1/1로 동일하다

<img width="30%" src="https://user-images.githubusercontent.com/86250281/133287414-dc2296da-fdc2-42aa-83a1-ef52b6ed9f86.png"/>

t(I)-> 
n cases : (1/(n+1))(i+1) [i+1번의 비교연산 필요]

1 case : n/(n+1) [n번의 비교연산이 필요]

* So, A(n) = q (1+n)/2 + (1-q) ( n /(n+1) + n/2 ) ≒ n/2