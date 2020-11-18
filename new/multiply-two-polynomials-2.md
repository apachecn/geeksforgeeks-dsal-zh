# 乘以两个多项式

给定两个由两个数组表示的多项式，编写一个将给定两个多项式相乘的函数。

**示例：**

```
Input:  A[] = {5, 0, 10, 6} 
        B[] = {1, 2, 4} 
Output: prod[] = {5, 10, 30, 26, 52, 24}

The first input array represents "5 + 0x^1 + 10x^2 + 6x^3"
The second array represents "1 + 2x^1 + 4x^2" 
And Output is "5 + 10x^1 + 30x^2 + 26x^3 + 52x^4 + 24x^5"

```

一个简单的解决方案是逐个考虑第一多项式的每一项并将其与第二多项式的每一项相乘。 以下是此简单方法的算法。

```
multiply(A[0..m-1], B[0..n01])
1) Create a product array prod[] of size m+n-1.
2) Initialize all entries in prod[] as 0.
3) Traverse array A[] and do following for every element A[i]
...(3.a) Traverse array B[] and do following for every element B[j]
          prod[i+j] = prod[i+j] + A[i] * B[j]
4) Return prod[].
```

以下是上述算法的实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// Simple C++ program to multiply two polynomials``#include <iostream>``using` `namespace` `std;``// A[] represents coefficients of first polynomial``// B[] represents coefficients of second polynomial``// m and n are sizes of A[] and B[] respectively``int` `*multiply(` `int` `A[],` `int` `B[],` `int` `m,` `int` `n)``{` `int` `*prod =` `new` `int` `[m+n-1];`的 `// Initialize the porduct polynomial` `for` `(` `int` `i = 0; i<m+n-1; i++)` `prod[i] = 0;` `// Multiply two polynomials term by term` `// Take ever term of first polynomial` `for` `(` `int` `i=0; i<m; i++)` `{` `// Multiply the current term of first polynomial` `// with every term of second polynomial.` `for` `(` [HTG5 6] `j=0; j<n; j++)` `prod[i+j] += A[i]*B[j];` `}` [ `return` `prod;``}``// A utility function to print a polynomial``void` `printPoly(` `int` `poly[],` `int` `n)``{` `for` `(` `int` `i=0; i<n; i++)` `{` `cout << poly[i];` `if` `(i != 0)` `cout <<` `"x^"` `<< i ;` `if` `(i != n-1)` `cout <<` `" + "` `;` `}``}` [`// Driver program to test above functions``int` `main()``{` `// The following array represents polynomial 5 + 10x^2 + 6x^3`[ `int` `A[] = {5, 0, 10, 6};` `// The following array represents polynomial 1 + 2x + 4x^2` `int` `B[] = {1, 2, 4};` `int` `m =` `sizeof` `(A)/` `sizeof` `(A[0]);` `int` `n =` `sizeof` `(B)/` `sizeof` `(B[0]);` `cout <<` `"First polynomial is n"` `;`​​  `printPoly(A, m);` `cout <<` `"nSecond polynomial is n"` `;` `printPoly(B, n);` `int` `cout <<` `"nProduct polynomial is n"` `;` `printPoly(prod, m+n-1);` `return` ] `0;``}` |

*chevron_right**filter_none*