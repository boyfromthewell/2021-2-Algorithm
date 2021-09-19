# divide and conquer

* Strategy D
    * K와 배열의 가운데 비교
    * 한번의 비교연산으로 엔트리 절반 고려 안해도됨
    * 재귀적으로 적용
* Algorithm D : binary search (반드시 정렬된 배열만 가능)
    * Input : E, first, last, K
    * Output : 해당 index 리턴, 존재하지 않으면 -1

```c
int binaraySearch(int[] E, int first, int last, int K)

1. if(last < first)
2.    index = -1;
3. else
4.    int mid = (first + last) / 2
5.    if(K== E[mid])
6.            index = mid;
7.    else if(K < E[mid])
8.            index = binarySearch(E, first, mid-1, K);
9.     else
10          index = binarySearch(E, mid+1, last, K);
11.    return index;
```
base case : 라인1, 2 (key값 못찾음 의미)

## Worst Case of Binary Search

* Basic operation : K와 배열 엔트리간의 비교 연산
    * 한번의 비교연산은 <, >, == 비교연산 한번이라 가정

    <img width="80%" src="https://user-images.githubusercontent.com/86250281/133919813-9c53f9b1-eb98-41ce-9e5f-360b5b86c782.png"/>

## Average case of Binary Search

<img width="60%" src="https://user-images.githubusercontent.com/86250281/133919979-8ee549ba-caec-4595-9c84-ce55ae4a9fd1.png"/> 
<img width="40%" src="https://user-images.githubusercontent.com/86250281/133919993-c8e4c937-5cc0-4da1-bf30-65409fdb032a.png"/>

<img width="60%" src="https://user-images.githubusercontent.com/86250281/133920070-e98bc691-c73a-4382-953c-8e328cbe7f90.jpg"/>

***

<img width="80%" src="https://user-images.githubusercontent.com/86250281/133920091-45f427d8-90d6-4006-9e49-db758c0410e2.jpg"/>

***

<img width="80%" src="https://user-images.githubusercontent.com/86250281/133920462-41377021-f11f-4652-988a-142db78c2d7f.jpg"/>
