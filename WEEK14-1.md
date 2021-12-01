## Non-Deterministic Polynomial Time: Class NP

non-determinitstic하다를 의미 (deterministic이란 용어는 오토마타 분야에서 옴)  
* DFA : deterministic finite automata
* NFA : Non-deterministic finite automata
    * determiistic: 하나의 입력(state)에서 하나의 transition (다음상태) 결정 되있는 상태
    * non-deterministic : 같은 입력에서 알고리즘이 다르게 수행되는 경우
    <img width="60%" src="https://user-images.githubusercontent.com/86250281/144185320-707c7900-1b7d-4242-95e0-1a39c455c7aa.png"/>

따라서 그 문제를 해결하는 non-deterministic polynomial-time algorithm 존재한다면 그런 decision problem을 class NP라고 함

다른 정의 방식: 어떤 certificate(근거)가 주어지면 그것을 polynomial time에 검증할수 있어야함 (우리는 이것으로 정의할것)

* P의 문제는 NP의 부분집합이기도 하다 (P⊆NP)
* open problem (P=NP, P!=NP->아직 증명못함)
* 많은 연구자들은 P와 NP는 다를것이라고 믿고 있음

## NP Example

|certificate|output of verification algorithm|
|---|----------|
|참|yes|
|거짓|...(대답할수없음, no output)|

ex) UFO가 존재할것인가, 존재 하지않는가?  
누군가 UFO가 있다고 말하면서, 사진이나 동영상 공개(certificate)->근거가 참이면 UFO 존재한다고 할 수 있음, but 근거가 거짓이라고해서 UFO가 존재하지 않는다고 확실히 말할 수 없음(no output)

* 문제: 입력으로 그래프 주어졌을때 weight K이하인 MST 존재하는가? (yes or no)
* 검증 알고리즘
    1. certificate y 주어짐(n-1개의 edge로 구성된 집합 T)
    2. T가 spanning tree의 모양을 갖는가?
    3. T의 weight가 K이하인가? -> 다항시간에 보여주기, 가능하면 yes 아니면 no output
* 테스트 하는데 O(n+m) time 소요, 따라서 이 알고리즘은 다항시간에 검증가능->class NP

* class P : the class of decision problems that are polynomially bounded (다항시간에 해결되는 문제를 의미)
* class NP : the class of decision problems for which there is a polynomially bounded non-deterministic algorithm (다항시간에 검증할수 있는 decision problem의 집합을 의미)

## The class NP-Complete

* 어떤 문제 Q가 NP-hard이다-> class NP에 있는 어떤 문제에 대해, 그 문제만큼은 어려운 문제
    * class NP에 있는 어떤 문제를 문제 Q로 reducible 할수 있으면 된다 (reduction: 축소변환)
* ex) 문제 P(최대값 찾기 문제)를 문제 Q(정렬문제)로 reducible 할수 있다 (문제 Q를 해결 할수 있으면 P도 해결할수 있다는 소리)--> 정렬 문제가 적어도 최대값 찾기 문제만큼은 어렵다고 할 수 있다 (이런 방식이 NP-hard 증명 방법)

* 어떤 문제 Q가 NP-complete이다 -> 이 문제가 만약 class NP이고 NP-hard이면 그 문제를 NP-complete라 함

따라서 어떤 문제 만났을때 NP-complete 증명하려면 두가지 (NP, NP-hard) 증명 해야함  
NP-hard를 증명하는 것은 reducible하다라는것을 보이면 됨 -> NP hard임을 증명하고 싶은 문제를 문제 Q로 놓고, 기존에 알려져있는 NP-complete문제를 문제 P로 놓으면 됨  
즉, 우리의 문제를 가지고 기존에 알려져 있는 문제(NP-complete)를 해결할수 있음을 보이면 됨

## Polynomial reductions
문제 P에 대한 input을 문제 Q에 대한 input으로 다항시간에 변환할수 있음을 보여야함, 그 함수를 reduction function이라 함(다항시간에 변할수 있음을 보이기)

<img width="70%" src="https://user-images.githubusercontent.com/86250281/144192684-44e934e9-7e14-437f-a6fe-660e15c275ca.png"/>  

P를 우리의 문제 Q(NP-hard임을 증명하고 싶은 문제)로 해결할수 있음을 보이기

* input x (기존에 알려진 문제 P)
1. 다항시간에 문제 P에 대한 input을 문제 Q에대한 input으로 변할 수 있음을 증명(transformation function T)  
T(x): 문제 Q에대한 input으로 바뀐 것 의미
2. 이것에 대해 문제 Q를 해결한다면 문제 Q에서 나온 output이 완전하게 문제 P의 output과 동일하다는것을 보이면 됨, 즉 문제 Q에 대한 output이 yes이면 항상 문제 P에서도 yes임을 보이고, 문제 Q에서 output이 no이면 항상 문제 P에서도 no가 된다는것을 증명

* P <= pQ (p: 다항시간에 reduction됨을 의미, <=: 문제 Q가 적어도 문제 P만큼은 어렵다 의미)

### example
* P : Hamiltonian-cycle problem : given a graph G, is there a cycle in G that visits each vertex exactly once?(그냥 그래프 주어졌을때, 모든 vertex한번씩 방문하는 cycle 존재하는가?, 이미 NPC라고 증명 되있음)
* Q : Traveling-salesperson problem : given a complete weighted graph G, is there a cycle in G that visits each vertex exactly once and has total cost at worst K?

Problem Q가 NPC임을 증명
1. class NP  
(input, certificate)가 주어졌을때, 다항시간에 검증 할 수 있음을 보인다  
certificate로 n개의 edge가 주어지면, n개의 edge를 따라가면서
    1. 각 vertex를 한번씩만 방문하는 cycle인지 확인
    2. edge들의 weight의 sum이 K이하인지 확인  
    -> O(n) time에 검증 할 수있다(polynomial time)  
    결과는 yes or no-output  
    검증은 완료