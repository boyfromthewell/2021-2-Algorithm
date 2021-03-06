## Step 4: Constructing an Optimal Solution
```c++
PRINT-OPTIMAL-PARENS(๐ , ๐,๐) //i=1, j=4
1   if ๐ = ๐
2       then print โAโi //base case
3   else print โ(โ
4       PRINT-OPTIMAL-PARENS(๐ , ๐, ๐ [๐,๐]) //s[i,j]์๋ k๊ฐ ์ ์ฅ (Ai..Ak) -> left child
5       PRINT-OPTIMAL-PARENS(๐ , ๐ [๐,๐]+1, ๐) //s[i,j]+1=k+1 (Ak+1...Aj) -> right child
6       print โ)
```
recursion tree๋ก ํํ ๊ฐ๋ฅ

* ์ด๊ธฐ๊ฐ s[1,4]์ ๋ํ k ๊ฐ=1  

    <img width="60%" src="https://user-images.githubusercontent.com/86250281/142971067-9ce94e8f-8fc9-404c-9e00-cfc8becc90e0.png"/><img width="30%" src="https://user-images.githubusercontent.com/86250281/143447485-066492c6-d05f-4318-90a2-6b32cf0d718d.png"/>

* (1,4)์ left child๋ i,k๋ก ๋ํ๋ผ์ ์์ผ๋ฏ๋ก (1, 1)
* right child๋ k+1, j ๋ก ๋ํ๋ผ์ ์์ผ๋ฏ๋ก (2,4)
* ์์ ๊ฐ์ ๋ฐฉ์์ผ๋ก ํธ๋ฆฌ ๋ง๋ค ์ ์์

* ์ผ์ชฝ ์์ ํธ์ถ๋๊ธฐ์  "(" ์ถ๋ ฅ
* ์ค๋ฅธ์ชฝ ์์์ด ํธ์ถ๋๊ณ  ๋ํ ์งํ ๋์์ฌ๋ ")" ์ถ๋ ฅ

    <img width="60%" src="https://user-images.githubusercontent.com/86250281/142971481-849aa51c-0889-4396-9d39-0876320695b8.png"/> in order ์ํ ๋ฐฉ์์ผ๋ก ์ถ๋ ฅ

-> (A1((A2A3)A4)) ๊ณฑ์ ์์ ์ถ๋ ฅ ๊ฐ๋ฅ!!

### ๋ถ์

Step 3 : matrix chain ๊ธธ์ด 1 ์ผ๋ ๊ณ์ฐ, 2์ผ๋ ๊ณ์ฐ, 3์ผ๋ ๊ณ์ฐ,,,, n์ผ๋๊น์ง ๊ณ์ฐ -> n+(n-1)+...+1 = O(n^2)์ ์ ์กด์ฌ  
ํ๋์ ์ ๊ณ์ฐํ๋๋ฐ o(n) time ๊ฑธ๋ฆผ  
๋ฐ๋ผ์ O(n^3) time, O(n^2) space

Step 4 : recursion tree๋ธ๋ ๊ฐ์ ๋ถ์  
n๊ฐ์ leaf ์กด์ฌ, n-1๊ฐ์ internal node๊ฐ์ง -> ์ด 2n-1๊ฐ์ ๋ธ๋ ๊ฐ์ง ๋ฐ๋ผ์ O(n) time ์ ์ํ๊ฐ๋ฅ  
O(n^2) space (s ํ์ด๋ธ์ ๊ณ์ ์ฌ์ฉํ๊ธฐ ๋๋ฌธ)

# 11. String Matching

Pattern matching์ด๋ผ๊ณ ๋ ๋ถ๋ฆ

* input์ผ๋ก ๊ธด ์คํธ๋ง์ธ text T์
์๋์ ์ผ๋ก ์งง์ ์คํธ๋ง์ธ pattern P ์ฃผ์ด์ง
* T์์ P๊ฐ ๋ฐ์ํ๋ ์์น ์ฐพ๋ ๋ฌธ์  -> String matching

## Strings

*   string=characters์ ๋์ด

    * c++ ํ๋ก๊ทธ๋จ
    * html ๋ฌธ์
    * DNA ์ผ๊ธฐ์์ด
    * Digitized ์ด๋ฏธ์ง

* alphabet ฮฃ =์คํธ๋ง ๊ตฌ์ฑํ๋ ๋ฌธ์์งํฉ ์๋ฏธ 
    * ASCII
    * {0,1} // binary alphabet
    * {A,C,G,T} // DNA alphabet

* ํ๋์ ์คํธ๋ง์ P๋ผ๊ณ  ์ ์ํ๊ณ , ๊ทธ ์ฌ์ด์ฆ๋ฅผ m์ด๋ผ ์ ์ํ์
    * substring(๋ถ๋ถ๋ฌธ์์ด)-์์์ ์ธ๋ฑ์ค i๋ถํฐ j๊น์ง ์ฐ์๋ char์๋ฏธ
    * prefix(์ ๋์ฌ)-substring of p[0..i]
    * suffix(์ ๋ฏธ์ฌ)-substring of p[i.. m-1]

        <img width="60%" src="https://user-images.githubusercontent.com/86250281/142973578-fccd741f-c733-46bf-a907-dc17a7881cdc.png"/> Example
    * ์์ฉ๋ถ์ผ-ํ์คํธ ์๋ํฐ, ๊ฒ์ ์์ง, ์๋ฌผํ ์ฐ๊ตฌ

## Brute-Force Algorithm

๋จ์ํ๊ฒ ๋ชจ๋  ๊ฒฝ์ฐ์ ๋ํด ์ํํ๊ธฐ
* T์ P๊ฐ์ ๋น๊ต์ฐ์ฐ
* Text ์ผ์ชฝ๋ถํฐ ํจํด ํ์, ๋ชจ๋  pattern๊ณผ T์ Substring ์ผ์นํ๋๊ฒ ๋ฐ๊ฒฌํ ๋๊น์ง 

```c++
Algorithm BruteForceMatch(T, P)
    Input text T of size n and pattern
    P of size m
    Output starting index of a substring of T equal to P
    or -1 if no such substring exists

    for i <- 0 to n - m{ test shift i of the pattern } //n-m๊น์ง ํ์์งํ, i=text์ ์ธ๋ฑ์ค
        j <- 0 //j=pattern์์ ์ธ๋ฑ์ค
        while j < m and T[i + j] = P[j]
            j <- j + 1
        if j = m
            return i {match at i}
    return -1 {no match anywhere}
```

* ์๊ฐ๋ณต์ก๋ O(nm)
* worst case ์
    * T=aaa...ah
    * P=aaah (m๋ฒ ๋น๊ต)
    * n๊ฐ์ ์์น์์ m๋ฒ ๋น๊ตํ ์ ์์
    * ์ด๋ฏธ์ง ํ์ผ์ด๋ DNA ์ผ๊ธฐ์์ ๊ฐ๋ ๋ฐ์
    * ์ผ๋ฐ ํ์คํธ์์๋ ๊ฑฐ์ ๋ฐ์ X
