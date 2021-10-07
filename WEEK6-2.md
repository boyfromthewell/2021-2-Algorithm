## Analysis : fixHeapFast

promote, bubbleUpHeap 함수가 알고리즘 수행시간에 많은 영향 끼친다

* promote나 bubbleUpHeap 한번의 비교연산은 수행해야함 
* promote에 의해 h/2만큼 내려간다 가정
    1. 만약 bubbleUpHeap 조건에 걸려 올라간다면 ? 최악의 경우 내려온만큼 다시 올라갈수 있음
    h/2+h/2 -> h
    2. 만약 다시 내려가고, bubbleUpHeap 수행하면
    h/2+h/4+h/4 -> h
    3. h/2+h/4+h/8+h/8 (promote에 의해 계속 내려가고, 마지막에 올라간 경우) -> 이것도 total h

* promote로 계속 내려간 경우는? 
    
    height 1까지 내려갈것임  (worst case)

    h/2+h/4+h/8+.....+1 -> h x (1/2)^k 
    
    (위로갈지 아래로갈지 check 비교 연산수 -> k=logh)

    따라서 w1 = h+log(h) 
    
    (이 때 h는 logn에 bound되므로) w1 = logn+loglogn 이 된다

    Wn = n(logn+loglogn) -> fixHeapFast의 total 수행시간, 따라서 Accelerated Heapsort의 worst case는 nlog(n)+θ(nloglog(n))

    (이론적으로 orginal heapsort 2nlog(n)이었는데 약 2배정도 빨라짐)

# Radix Sort

정렬 O(n)에 수행가능한 알고리즘, 알고리즘의 basic operation 다르기에 가능

지금까지는 input 데이터에 대해 선형으로 정렬시킬수 있다고 가정했고, 기본연산은 두개의 키값에 비교연산이었음

만약 key값에 어떤 가정을 더 추가하면, 다른 basic oper 더 고려 가능하다

### using properties of the keys
* 키값이 이름일때 //이름의 첫 알파벳에 따라 분류
* 다섯자리의 십진수
* key값들이 제한된 범위로 구성 되었을때 [1, m] -> [1,m/k], [m/k+1, 2m/k], ..... [m/k*(k-1)+1, m]

***
* 각각의 다른 파일(bucket)들로 분류해주고
* 각 파일을 독립적으로 정렬
* 모든 정렬된 파일 combine (기본적으로 분할정복법 idea사용)

키값 구조적, 범위 제한이 있으면 linear time에 수행가능

* Radix sort의 놀라운점 : 각 바구니에 분배할때 아래자리부터 우선 정렬하면 sort과정 생략 가능하다 

<img width="60%" src="https://user-images.githubusercontent.com/86250281/136422842-89799597-31b0-4ded-9f9d-81404493f793.png"/>

bucket 10개 만들어주기 

pass1: 1의자리 1이다 -> 버킷 1에 채우기 ..... ->
pass2: 10의 자리 숫자에 따라 분배, 순서유지되도록 combine ..... -> pass 5 까지 수행

* loop invairant로 증명가능
1. 첫번쨰 pass잘 수행해주면 첫번째 자리수에 대해 오름차순으로 잘 정렬됨
2. i번째 step : i번째 pass 시작하기 전에 i-1 자리까지는 오름차순으로 잘 정렬되어있다 , i번째 수행하면 i번째 자리까지는 오름차순으로 잘 정렬되어있음
3. termianation step : 마지막까지 잘 수행해주면 오름차순으로 정렬 잘 되어있음

### stable sort란

a1,a2,a3 인 순서를 가지는 원소가 있고 각각 값이 다 같다고 할때 정렬을 수행한 경우 상대적인 순서 그대로 유지할 때 -> stable 하다

<img width="60%" src="https://user-images.githubusercontent.com/86250281/136425340-47766fbd-3708-4274-8934-54cb1b3b0672.png"/>

(ex. pass 3 수행하는중)

41983, 90283, 90287, 78397만 남은 상황

bucket에 삽입할때 해당 index list head에 삽입

분배 단계에서 하나의 원소 distribute할때 상수시간에 처리가능, n개의 원소 처리해줘야 하므로

* distribution : θ(n) time
* combine : 하나의 원소 삭제할때 head에서 삭제, 삽입 연산 : O(n) time -> 추가적으로 각 bucket k개의 index에 접근해야 하므로 총 θ(k+n) time


* i th pass : θ(k+n) time
* 자리수가 d개 있다고 가정하면, pass 역시 d번의 pass수행해야함, Total : θ(d(k+n)) time (when k, d가 상수이면 θ(n) time 에 수행가능)

## Radix Sort : analysis

* distribute : θ(n)
* combine : θ(k+n)
* 시간 복잡도 : θ(d(k+n)) time
* 공간 복잡도 : θ(k+n) space