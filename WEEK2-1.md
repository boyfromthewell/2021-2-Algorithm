# Analyzing algorithms and problems

알고리즘의 성능을 분석해야함, 기존의 알고리즘 개선도 하기위해
* correctness
* amount of work done(시간 복잡도), space used (일, space양)
* Optimality, Simplicity
---
* correctness는 수학적, 논리적으로 설명할수 있어야함

    * input(precondition)이 만족하고,
    * 알고리즘이 끝나면,
    * output(postconditions)도 true일 것이다
    
* 알고리즘의 효율성을 따질 때 '일의 양'을 빼 놓을수 없다
    * 컴퓨터 하드웨어, 프로그램 언어, 프로그래머, 다른 디테일도 독립적으로 분석
    * 대개 input size(n)으로 정의

* Basic Operation (가장 기본이 되는 연산)
    
    ex) n개의 정수에서 key값 K를 찾는 문제 -> 비교 연산이 basic operation

    * 기본연산의 수를 count한 다음에 n에 대해 대략적으로 정리한뒤 함수로 나타냄->일의 양 측정가능

    * input property 잘 파악해야함 (알고리즘의 행동 바뀔수 있기 떄문)
    
        * ex) input이 정렬된 상태인가?, input data의 값이 제한 되어있는가?

## Worst-Case Complexity

Worst-case analysis(보수적 접근 분석 방법)

* Dn -> 모든 가능한 input size 집합 의미
* I -> Dn의 원소 중 하나
* t(I) -> 특정 input I에 대해 basic operation의 수

* W(n)=max{t(I)|I -> Dn} 
(사이즈 n인 임의의 입력에 대해 알고리즘이 수행하는 basic operation의 max값)

## Average Complexity
(Worst case와 best case의 평균 아님!!)

Pr(I) -> 특정 input이 발생할수 있는 확률

<img width="50%" src="https://user-images.githubusercontent.com/86250281/132365540-8bbc756b-e4f2-43a7-b69a-a956f1444061.png"/> W(n)과 같이 함수로 나타낼수 있음

Pr(I)는 분석적으로 하기 어렵, 통계적인 수치가 필요 or 가정(모든 경우가 발생할 확률은 같다) 

## Space usage and Simplicity

* input size n에 대해 사용한 space의 양 분석하기, worst case, average case 모두 분석가능
* time and space Tradeoff (한쪽이 좋으면 한쪽이 안좋음)

* Simplicity의 중요성
    * 알고리즘의 correctness에 대한 증명을 더 쉽게 가능
    * 프로그램의 작성, 디버깅, 수정이 더 쉽다

## Optimality (최적)

모든 문제는 고유의 복잡도 가지고 있음(문제 A의 해결에 필요한 최소한의 일의양 정해져 있다)

* 알고리즘의 연산 명시 해주기 (basic operation) 선택하고 count 해주기 ->  complexity
* 문제를 해결하기 위해 실제 필요한 연산수가 얼마나 많이 필요하나?

어떤 알고리즘이 optimal이다? -> 현재 알려진 가장 좋은 알고리즘이다 (x)

모든 가능한 알고리즘 중에서 가장 효율적인 알고리즘 이다. (o) the best possible