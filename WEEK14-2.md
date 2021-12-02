2. NP hard  
    1) transformation

        <img width="40%" src="https://user-images.githubusercontent.com/86250281/144382042-a2f2fe15-8333-449e-91c1-d75466b421e1.png"/>  
        
        문제 P의 input G,(x)라고 하고 transformation func 거쳐 TSP문제의 input으로 변환 할것
        
        <img width="30%" src="https://user-images.githubusercontent.com/86250281/144382460-4009c94e-290c-4333-b320-25f9fe4d5eb8.png"/>

        기존의 edge들은 weight를 0으로 초기화 해주고 complete그래프 이기 때문에 없던 edge들은 weight를 1로 초기화해줌, input으로 K주어져야 하기 때문에 K=0으로 만들어줌

        이렇게 변환하는것 다항시간에 할 수있다.
        (complete 그래프는 edge수가 많아야 O(n^2)에 bound되기때문에 input을 O(n^2)에 transformation 할 수 있다)
    
    2) TSP문제의 output과 H.C의 output이 항상 일치함을 보이기

        * TSP의 출력이 yes -> H.C출력 yes 보이기  
        ->K를 0으로 했기 때문에 K이하인 H.C이 존재한다면 그것은 그 edge들의 집합은 모두 weight가 0인 것만 지나가야함  
        그 즉슨, H.C의 input에서 기존에 존재했던 edge들만 지나가는 H.C이 존재한다는것을 의미.  
        따라서 TSP문제에서 weight가 0인 H.C이 존재한다는것은 원래 H.C문제에서의 H.C이 존재한다는것과 일치

        * TSP의 출력이 no -> H.C 출력 no 보이기  
        ->만약 문제의 해를 계산하는데 해가 존재 하지 않는다는것은 K=0인 H.C이 TSP문제에 없다는것 의미. 적어도 한번이라도 weight가 1인 edge를 지나 가야한다는 것을 의미 즉 기존에 G에서 기존의 edge만으로는 H.C이 존재할수 없다는것을 의미  
        따라서 TSP문제의 input에서 H.C의 K=0인 H.C이 존재하지 않는다면, 그래프 G에서 H.C에서도 존재할수 없음

        (두문제의 output 일치)

따라서 TSP 문제는 class NP이면서 NP-hard이기 때문에 NP-Complete이다

* 어떤 문제가 NP-hard 증명하기 위해선 반드시 기존에 증명된 NP-hard or NPC문제 존재해야함. 즉 기존에 증명된 NPC문제 이용해서 계속 NPC문제들이 탄생할수 있음 (transitive한 관계 가짐) 이렇게 하려면 최초의 NPC문제 가지고 있어야함 그것이 무엇일까?

## CIRCUIT-SAT

최초의 NP Complete 문제

0 또는 1의 값을 가진 n개의 boolean값 input으로 주어짐
<img width="60%" src="https://user-images.githubusercontent.com/86250281/144412678-4d10cf94-990b-4e1e-bdef-68e3fcf9a09e.png"/>  
최종 출력이 1이 되는 input의 조합이 존재하는가?  
(total 나올수있는 경우의 수: 2^n가지)  
다항시간에 해결하는것은 쉽지않음, 아직까지 다항시간에 해결하는 방법 찾지 못함 (이 문제들로부터 점점 많은 NPC 문제 증명했음, 모든 NPC 문제들 circuit-sat문제로 reduction 가능)  

## Some NP-Complete problems
* SET-COVER  
    ex) S={{1,2,3},{2,4},{3,4},{4,5}} |S|=m  
        U={1,2,3,4,5} |U|=n  
    Decision problem: k보다 적은수에 set을 union하여 U를 생성할수 있는가?  
    (해=>{1,2,3},{4,5})  
    총 부분집합은 2^m의 경우의수를 가지고 예시에선 쉬워 보이지만 n,m 이 충분히 커지면 다항시간에 찾기 쉽지않음

    (optimization problem-가장 적은 수의 set을 union하여 U를 만들수 있는 집합은) 
     * VERTEX-COVER (기존의 NPC문제)에 의해 NPC 문제임을 증명

* SUBSET-SUM  
    n개의 정수로된 집합 주어지고 {v1,v2,v3...vn}, 정수 k가 주어짐, 집합 원소들의 합이 정확히 k와 같은 부분집합 존재하는가?

    2^n개의 subset가지고, 다항시간에 해결하기 쉽지 않음

    (optimization problem-원소의 합이 k보다 작으면서 가장 큰값을 가지는 부분집합은?)
     * VERTEX-COVER (기존의 NPC문제)에 의해 NPC 문제임을 증명

* 0/1 Knapsack  
    input으로 n개의 item이 주어지고, 각 item마다 무게와 가치가 주어짐 가방의 무게가 W이하 이면서 이익이 적어도 K인 item들의 집합이 존재하는가?  
    (optimization problem-가장 이익이 되는 조합은?)
    * SUBSET-SUM (기존의 NPC문제)에 의해 NPC 문제임을 증명
* Hamiltonian-cycle  
    그래프 G가 주어지면 모든 vertex를 한번만 방문하는 사이클 존재하는가?
    * VERTEX-COVER (기존의 NPC문제)에 의해 NPC 문제임을 증명  
    (optimization problem-TSP 문제로 간주함)
* Traveling saleperson tour  
    입력으로 complete weighted graph G가 주어지고 weight가 K이하인 헤밀토니안 사이클 존재하는가?  
    (optimization problem-weight가 최소인 헤밀토니안 사이클은?)

## SAT

유명한 NPC 문제  
각각 0또는 1로 구성된 boolean 변수 주어지고, 허용된 연산은 or, and, not 연산  
ex) (a+b+¬d+e)(¬a+¬c)(¬b+c+d+e)(a+¬c+¬e)  
(정의: 항 하나하나를 literal이라고 부름, 괄호안의 수식: clause, 전체수식: CNF)

**CNF가 주어졌을때 결과를 1로 만드는 input의 조합이 존재하는가?**

clause의 조합 0또는 1로 주어지면 O(nm) time에 검증 가능 (CIRCUIT-SAT문제에 의해 NPC라고 증명됨)

### 3SAT

모든 clause를 3개 literal로 제한  
ex) (a+b+¬d)(¬a+¬c+e)(¬b+d+e)(a+¬c+¬e)  
(2SAT문제는 다항시간에 해결가능), SAT문제에 의해 NPC라고 증명됨

## Vertex Cover

input으로 그래프가 주어지고, k개 이내에 모든 vertex를 cover하는 정점 집합 존재하는가? (vertex cover: 정점들의 부분집합으로, 그래프의 모든 edge들은 vertex cover의 정점중 하나 이상에 인접하는것)

(optimization problem-최소크기의 vertex cover 찾기)

O(n^2) edges - 다항시간에 검증가능(class NP)  
3SAT문제에 의해 NPC라고 증명됨

***
## Undirected Hamiltonain cycle NPC임을 증명하기

P: Directed Hamiltonian cycle (기존에 NPC라 증명)  
Q: Undirected Hamiltonain cycle

Q가 NPC임을 증명하자

1. Class NP임을 보이기  
undirected graph 주어지고 누군가 certificate 제시할것임, 어떤 path를 제시했을때 그 path가 1. vertex를 한번씩만 방문하는가, 2.Hamiltonain cycle인지 다항시간에 검증하면 됨  
만나는 edge의 수 O(n^2)으로 bound될 것이고 이는 **즉, O(n^2)에 검증 가능할 것이다**   
(yes이면 yes, no이면 no-output)

2. NP-hard임을 보이기  
    1. transformation  
    문제 P의 input을 G라고 하면  
    <img width="30%" src="https://user-images.githubusercontent.com/86250281/144421490-b7660953-c21b-4930-926e-cd8a20d4f349.jpg"/>  
    다항시간에 문제 Q의 input으로 transform할수 있음을 보이자  
    모든 vertex들을 먼저 triple로 생성해주고 각각 연결시킴, 그다음 G에서 directed edge가 있으면 3번째 vertex에서 1번째 vertex로 가는 edge하나 생성해줌  
    <img width="40%" src="https://user-images.githubusercontent.com/86250281/144423021-cbfa76c5-da58-41d6-8747-58ecffe7079d.jpg"/>  
    따라서 G와 G'의 vertex개수와 edge개수의 관계에 의해 입력 G를 G`로 변환하는데 O(n+m) time에 변환 가능하다

    2. Undirected Hamiltonain cycle의 output과 Directed Hamiltonian cycle의 output이 항상 일치함을 보이기

         * yes -> yes임을 보이기  
        G'에서 edge가 다 undirected 그래프이기 때문에 방향이 1,2,3->1,2,3 or 3,2,1->3,2,1 이렇게 진행 할 것임  
        만약 1,2,3 으로 진행한다면 G에서도 똑같은 순서로 방향을 가지게 됨 따라서 G'에서 1,2,3 순서로 가고 H.C.가 존재한다면 G에서도 H.C.이 존재하게 됨 (역순에서도 존재 할 수 있음(3,2,1 존재 한다는것은 거꾸로 1,2,3도 존재함을 의미))  
        따라서 yes -> yes를 증명가능

         * no -> no 임을 보이기  
         대우를 이용해서 증명 할수 있음 (Directed Hamiltonian cycle의 output이 yes이면 Undirected Hamiltonain cycle의 output도 yes이다)  
         G의 H.C.가 <v1,v2,....,vn>으로 존재 한다면 G`에서는 <v1^1, v1^2, v1^3, v2^1, v2^2, v2^3....vn^1, vn^2, vn^3> 으로 존재 할 수 밖에 없다 (그래프의 모양 때문에)  
        따라서 no -> no를 증명 가능
        그러므로 Undirected Hamiltonain cycle은 NP-hard이다

**따라서 Undirected Hamiltonain cycle문제는 class NP이며 NP-hard이기 때문에 NPC이다**

## Some Thoughts about P and NP

* 많은 연구자들은 P는 NP의 부분집합일 것이라 믿음
* NPC 문제는 NP class에 있는 가장 어려운 문제라고 할수있음
* NPC가 가장 어려운 문제이기 때문에 다항시간에 해결 할수 있으면 NP문제를 다항시간에 해결 가능
* NPC문제 중 하나라도 다항시간에 해결할수 있다면 P=NP이다 라고 할수 있음 (but 아직 성공 못함)
* 만약 NPC를 만난다면 approximation algorithm을 개발하는것을 추천 (최적의 해를 찾지말고 근사한 해를 찾는 것)