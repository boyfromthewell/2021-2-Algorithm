## Step 4: Constructing an Optimal Solution
```c++
PRINT-OPTIMAL-PARENS(𝑠, 𝑖,𝑗) //i=1, j=4
1   if 𝑖 = 𝑗
2       then print “A”i //base case
3   else print “(”
4       PRINT-OPTIMAL-PARENS(𝑠, 𝑖, 𝑠[𝑖,𝑗]) //s[i,j]에는 k값 저장 (Ai..Ak) -> left child
5       PRINT-OPTIMAL-PARENS(𝑠, 𝑠 𝑖,𝑗 + 1,𝑗) //s[i,j]+1=k+1 (Ak+1...Aj) -> right child
6       print “)
```
recursion tree로 표현 가능

* 초기값 s[1,4]에 대한 k 값=1  

    <img width="60%" src="https://user-images.githubusercontent.com/86250281/142971067-9ce94e8f-8fc9-404c-9e00-cfc8becc90e0.png"/>

* (1,4)의 left child는 i,k로 나타낼수 있으므로 (1, 1)
* right child는 k+1, j 로 나타낼수 있으므로 (2,4)
* 위와 같은 방식으로 트리 만들 수 있음

* 왼쪽 자식 호출되기전 "(" 출력
* 오른쪽 자식이 호출되고 난후 직후 돌아올때 ")" 출력

    <img width="60%" src="https://user-images.githubusercontent.com/86250281/142971481-849aa51c-0889-4396-9d39-0876320695b8.png"/> in order 순회 방식으로 출력

-> (A1((A2A3)A4)) 곱셈 순서 출력 가능!!

### 분석

Step 3 : matrix chain 길이 1 일때 계산, 2일때 계산, 3일때 계산,,,, n일때까지 계산 -> n+(n-1)+...+1 = O(n^2)의 셀 존재  
하나의 셀 계산하는데 o(n) time 걸림  
따라서 O(n^3) time, O(n^2) space

Step 4 : recursion tree노드 개수 분석  
n개의 leaf 존재, n-1개의 internal node가짐 -> 총 2n-1개의 노드 가짐 따라서 O(n) time 에 수행가능  
O(n^2) space (s 테이블을 계속 사용하기 때문)

# 11. String Matching

Pattern matching이라고도 부름

* input으로 긴 스트링인 text T와
상대적으로 짧은 스트링인 pattern P 주어짐
* T에서 P가 발생하는 위치 찾는 문제 -> String matching

## Strings

*   string=characters의 나열

    * c++ 프로그램
    * html 문서
    * DNA 염기서열
    * Digitized 이미지

* alphabet Σ =스트링 구성하는 문자집합 의미 
    * ASCII
    * {0,1} // binary alphabet
    * {A,C,G,T} // DNA alphabet

* 하나의 스트링을 P라고 정의하고, 그 사이즈를 m이라 정의하자
    * substring(부분문자열)-임의의 인덱스 i부터 j까지 연속된 char의미
    * prefix(접두사)-substring of p[0..i]
    * suffix(접미사)-substring of p[i.. m-1]

        <img width="60%" src="https://user-images.githubusercontent.com/86250281/142973578-fccd741f-c733-46bf-a907-dc17a7881cdc.png"/> Example
    * 응용분야-텍스트 에디터, 검색 엔진, 생물학 연구

## Brute-Force Algorithm

단순하게 모든 경우에 대해 수행하기
* T와 P간의 비교연산
* Text 왼쪽부터 패턴 탐색, 모든 pattern과 T의 Substring 일치하는것 발견할때까지 

```c++
Algorithm BruteForceMatch(T, P)
    Input text T of size n and pattern
    P of size m
    Output starting index of a substring of T equal to P
    or -1 if no such substring exists

    for i <- 0 to n - m{ test shift i of the pattern } //n-m까지 탐색진행, i=text상 인덱스
        j <- 0 //j=pattern상의 인덱스
        while j < m and T[i + j] = P[j]
            j <- j + 1
        if j = m
            return i {match at i}
    return -1 {no match anywhere}
```

* 시간복잡도 O(nm)
* worst case 예
    * T=aaa...ah
    * P=aaah (m번 비교)
    * n개의 위치에서 m번 비교할수 있음
    * 이미지 파일이나 DNA 염기에서 가끔 발생
    * 일반 텍스트에서는 거의 발생 X