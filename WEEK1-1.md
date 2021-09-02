# Analyzing Algorithms and Problems : Principles and Examples

알고리즘 = 어떤 문제를 해결하기 위한 것

 * 명령어들의 집합 (step by step)
 * 유한시간내에 풀수 있어야함
 * 컴퓨터를 사용

## 알고리즘 만드는 순서

1. Problem (문제 정의)

    * input, output으로 정의

        ex) input : 3, 7 ,20, 11 (n개의 정수), output : 3, 7, 11, 20 (n개의 정수가 오름차순으로 정렬)
2. Strategy (전략)
3. Algorithm
    * input
    * output
    * step (ex. 슈도-코드)

4. Analysis (분석)
    * Correctness (정확하게 작동하는가?)
    * Time & Space (시간과 공간 효율적으로 쓰는가?)
    * Optimality (최적성 분석)

5. Implementation (구현)
6. Verification (확인, 검증)

***

EX) 정렬되지 않은 배열에서의 search

1. Problem

    Input : n 개의 엔트리를 가진 배열을 E라고 하자 (특정한 순서 x)

    Output : key 값 K를 찾으면 그 키값의 인덱스 불러옴, 존재 하지 않으면 -1 리턴

2. Strategy

    특정 K를 찾을때 까지 가장 왼쪽 인덱스 부터 차례로 살펴보기

    배열안에 K가 없으면 알고리즘은 -1을 리턴

3. Algorithm (input, output, step)

    Input: E, n, k (심플함을 위해 정수라 가정)

    Output : 변수 ans를 리턴 (E안의 K의 위치)

    ```
    int seqSearch(int [] E, int n, int K){

        int ans, index;
        ans = -1; //assume failure
        for(index = 0; index < n; index++)
            if(K == E[index])
                ans=index; // success!
                break; // done!
        return ans;
    }
    ```

*** 

* 실험적 분석 방법의 한계

    1. 구현이 필수적이다

    2. 실험에 포함되지 않은 input에 대해선 수행시간 알수 x

    3. 같은 문제를 해결하는 동일한 알고리즘 A, B 를 비교 하려면 hw, sw스펙이 같아야 하는 한계

* 알고리즘을 이용하면 좋은점

    1. 구현하지 않아도 서술 가능하다

    2. input size n에 대한 
    함수로 정의 가능, 수행시간 알수 있다

    3. 모든 가능한 input에 대해 고려 가능

    4. sw, hw 환경에 독립적으로 성능 평가 가능

***

앞선 예의 알고리즘 일의 양 어떻게 측정 할것 이냐?

* basic operation

    배열 엔트리와 K간의 비교 연산
* 최악 수행시간

    직관적으로 보아도 W(n)=n (계속 찾아도 안나와서 배열의 맨끝까지 가야하는 경우)

* 다른 분석 방법

    평균 수행시간 분석, optimality, Correctness


## 필요한 수학적 배경

<img width="100%" src="https://user-images.githubusercontent.com/86250281/131844307-64c84760-20d8-4534-9896-d6b88756d9e0.png"/>

밑에 두개 증명과정 꼭 알고있기

### Logic (논리식)

<img width="100%" src="https://user-images.githubusercontent.com/86250281/131844588-4fee2459-18f3-4cd8-85f5-c81f389a1419.png"/>

* Counterexample (반례)

* Contraposition (대우)

    ex) p->q <-> ~q->~p

* Contradicion (모순법, 귀류법 : 결론을 부정->그것을 서술해가며 모순 보여주는 방법)

* Mathematical Induction (수학적 귀납법)

