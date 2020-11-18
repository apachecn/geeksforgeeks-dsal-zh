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

## C++

```cpp

// Simple C++ program to multiply two polynomials 
#include <iostream> 
using namespace std; 

// A[] represents coefficients of first polynomial 
// B[] represents coefficients of second polynomial 
// m and n are sizes of A[] and B[] respectively 
int *multiply(int A[], int B[], int m, int n) 
{ 
   int *prod = new int[m+n-1]; 

   // Initialize the porduct polynomial 
   for (int i = 0; i<m+n-1; i++) 
     prod[i] = 0; 

   // Multiply two polynomials term by term 

   // Take ever term of first polynomial 
   for (int i=0; i<m; i++) 
   { 
     // Multiply the current term of first polynomial 
     // with every term of second polynomial. 
     for (int j=0; j<n; j++) 
         prod[i+j] += A[i]*B[j]; 
   } 

   return prod; 
} 

// A utility function to print a polynomial 
void printPoly(int poly[], int n) 
{ 
    for (int i=0; i<n; i++) 
    { 
       cout << poly[i]; 
       if (i != 0) 
        cout << "x^" << i ; 
       if (i != n-1) 
       cout << " + "; 
    } 
} 

// Driver program to test above functions 
int main() 
{ 
    // The following array represents polynomial 5 + 10x^2 + 6x^3 
    int A[] = {5, 0, 10, 6}; 

    // The following array represents polynomial 1 + 2x + 4x^2 
    int B[] = {1, 2, 4}; 
    int m = sizeof(A)/sizeof(A[0]); 
    int n = sizeof(B)/sizeof(B[0]); 

    cout << "First polynomial is n"; 
    printPoly(A, m); 
    cout << "nSecond polynomial is n"; 
    printPoly(B, n); 

    int *prod = multiply(A, B, m, n); 

    cout << "nProduct polynomial is n"; 
    printPoly(prod, m+n-1); 

    return 0; 
} 

```

## Java

```java

// Java program to multiply two polynomials 
class GFG 
{ 

    // A[] represents coefficients  
    // of first polynomial 
    // B[] represents coefficients  
    // of second polynomial 
    // m and n are sizes of A[] and B[] respectively 
    static int[] multiply(int A[], int B[],  
                            int m, int n)  
    { 
        int[] prod = new int[m + n - 1]; 

        // Initialize the porduct polynomial 
        for (int i = 0; i < m + n - 1; i++)  
        { 
            prod[i] = 0; 
        } 

        // Multiply two polynomials term by term 
        // Take ever term of first polynomial 
        for (int i = 0; i < m; i++)  
        { 
            // Multiply the current term of first polynomial 
            // with every term of second polynomial. 
            for (int j = 0; j < n; j++)  
            { 
                prod[i + j] += A[i] * B[j]; 
            } 
        } 

        return prod; 
    } 

    // A utility function to print a polynomial 
    static void printPoly(int poly[], int n)  
    { 
        for (int i = 0; i < n; i++)  
        { 
            System.out.print(poly[i]); 
            if (i != 0)  
            { 
                System.out.print("x^" + i); 
            } 
            if (i != n - 1)  
            { 
                System.out.print(" + "); 
            } 
        } 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        // The following array represents  
        // polynomial 5 + 10x^2 + 6x^3 
        int A[] = {5, 0, 10, 6}; 

        // The following array represents  
        // polynomial 1 + 2x + 4x^2 
        int B[] = {1, 2, 4}; 
        int m = A.length; 
        int n = B.length; 

        System.out.println("First polynomial is n"); 
        printPoly(A, m); 
        System.out.println("nSecond polynomial is n"); 
        printPoly(B, n); 

        int[] prod = multiply(A, B, m, n); 

        System.out.println("nProduct polynomial is n"); 
        printPoly(prod, m + n - 1); 
    } 
} 

// This code contributed by Rajput-Ji 

```

## Python3

```py

# Simple Python3 program to multiply two polynomials 

# A[] represents coefficients of first polynomial 
# B[] represents coefficients of second polynomial 
# m and n are sizes of A[] and B[] respectively 
def multiply(A, B, m, n): 

    prod = [0] * (m + n - 1); 

    # Multiply two polynomials term by term 

    # Take ever term of first polynomial 
    for i in range(m): 

        # Multiply the current term of first  
        # polynomial with every term of  
        # second polynomial. 
        for j in range(n): 
            prod[i + j] += A[i] * B[j]; 

    return prod; 

# A utility function to print a polynomial 
def printPoly(poly, n): 

    for i in range(n): 
        print(poly[i], end = ""); 
        if (i != 0): 
            print("x^", i, end = ""); 
        if (i != n - 1): 
            print(" + ", end = ""); 

# Driver Code 

# The following array represents 
# polynomial 5 + 10x^2 + 6x^3 
A = [5, 0, 10, 6]; 

# The following array represents  
# polynomial 1 + 2x + 4x^2 
B = [1, 2, 4]; 
m = len(A); 
n = len(B); 

print("First polynomial is "); 
printPoly(A, m); 
print("\nSecond polynomial is "); 
printPoly(B, n); 

prod = multiply(A, B, m, n); 

print("\nProduct polynomial is "); 
printPoly(prod, m+n-1); 

# This code is contributed by chandan_jnu 

```

## C#

```cs

// C# program to multiply two polynomials 
using System; 

class GFG  
{ 

    // A[] represents coefficients  
    // of first polynomial 
    // B[] represents coefficients  
    // of second polynomial 
    // m and n are sizes of A[]  
    // and B[] respectively 
    static int[] multiply(int []A, int []B,  
                            int m, int n)  
    { 
        int[] prod = new int[m + n - 1]; 

        // Initialize the porduct polynomial 
        for (int i = 0; i < m + n - 1; i++)  
        { 
            prod[i] = 0; 
        } 

        // Multiply two polynomials term by term 
        // Take ever term of first polynomial 
        for (int i = 0; i < m; i++) 
        { 
            // Multiply the current term of first polynomial 
            // with every term of second polynomial. 
            for (int j = 0; j < n; j++)  
            { 
                prod[i + j] += A[i] * B[j]; 
            } 
        } 

        return prod; 
    } 

    // A utility function to print a polynomial 
    static void printPoly(int []poly, int n) 
    { 
        for (int i = 0; i < n; i++) { 
            Console.Write(poly[i]); 
            if (i != 0) { 
                Console.Write("x^" + i); 
            } 
            if (i != n - 1) { 
                Console.Write(" + "); 
            } 
        } 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 

        // The following array represents  
        // polynomial 5 + 10x^2 + 6x^3 
        int []A = {5, 0, 10, 6}; 

        // The following array represents 
        // polynomial 1 + 2x + 4x^2 
        int []B = {1, 2, 4}; 
        int m = A.Length; 
        int n = B.Length; 

        Console.WriteLine("First polynomial is n"); 
        printPoly(A, m); 
        Console.WriteLine("nSecond polynomial is n"); 
        printPoly(B, n); 

        int[] prod = multiply(A, B, m, n); 

        Console.WriteLine("nProduct polynomial is n"); 
        printPoly(prod, m + n - 1); 
    } 
} 

// This code has been contributed by 29AjayKumar  

```

## PHP

```php

<?php 
// Simple PHP program to multiply two polynomials 

// A[] represents coefficients of first polynomial 
// B[] represents coefficients of second polynomial 
// m and n are sizes of A[] and B[] respectively 
function multiply($A, $B, $m, $n) 
{ 
    $prod = array_fill(0, $m + $n - 1, 0); 

    // Multiply two polynomials term by term 

    // Take ever term of first polynomial 
    for ($i = 0; $i < $m; $i++) 
    { 
        // Multiply the current term of first  
        // polynomial with every term of  
        // second polynomial. 
        for ($j = 0; $j < $n; $j++) 
            $prod[$i + $j] += $A[$i] * $B[$j]; 
    } 

    return $prod; 
} 

// A utility function to print a polynomial 
function printPoly($poly, $n) 
{ 
    for ($i = 0; $i < $n; $i++) 
    { 
        echo $poly[$i]; 
        if ($i != 0) 
            echo "x^" . $i; 
        if ($i != $n - 1) 
        echo " + "; 
    } 
} 

// Driver Code 

// The following array represents 
// polynomial 5 + 10x^2 + 6x^3 
$A = array(5, 0, 10, 6); 

// The following array represents  
// polynomial 1 + 2x + 4x^2 
$B = array(1, 2, 4); 
$m = count($A); 
$n = count($B); 

echo "First polynomial is \n"; 
printPoly($A, $m); 
echo "\nSecond polynomial is \n"; 
printPoly($B, $n); 

$prod = multiply($A, $B, $m, $n); 

echo "\nProduct polynomial is \n"; 
printPoly($prod, $m+$n-1); 

// This code is contributed by chandan_jnu 
?> 

```

**Output:**

```
First polynomial is
5 + 0x^1 + 10x^2 + 6x^3
Second polynomial is
1 + 2x^1 + 4x^2
Product polynomial is
5 + 10x^1 + 30x^2 + 26x^3 + 52x^4 + 24x^5
```

上述解决方案的时间复杂度为O（mn）。 如果两个多项式的大小相同，则时间复杂度为O（n <sup>2</sup> ）。

**我们可以做得更好吗？**
有一些方法可以比O（n <sup>2</sup> ）时间更快地进行乘法。 这些方法主要基于[分而治之](https://www.geeksforgeeks.org/divide-and-conquer-set-1-find-closest-pair-of-points/)。 以下是一种简单的方法，该方法将给定的多项式（次数为n）分为两个多项式，一个包含较低次项（小于n / 2），另一个包含较高次项（大于或等于n / 2）

```
Let the two given polynomials be A and B.  
For simplicity, Let us assume that the given two polynomials are of
same degree and have degree in powers of 2, i.e., n = 2i

The polynomial 'A' can be written as A0 + A1*xn/2
The polynomial 'B' can be written as B0 + B1*xn/2

For example 1 + 10x + 6x2 - 4x3 + 5x4 can be
written as (1 + 10x) + (6 - 4x + 5x2)*x2

A * B  = (A0 + A1*xn/2) * (B0 + B1*xn/2)
       = A0*B0 + A0*B1*xn/2 + A1*B0*xn/2 + A1*B1*xn
       = A0*B0 + (A0*B1 + A1*B0)xn/2 + A1*B1*xn  
```

因此，上述分治法需要4次乘法和O（n）时间才能将所有4个结果相加。 因此，时间复杂度为T（n）= 4T（n / 2）+ O（n）。 递归的解为O（n <sup>2</sup> ），与上述简单解相同。

想法是将乘法次数减少到3，并使递归为T（n）= 3T（n / 2）+ O（n）

***如何减少乘法次数？***
这需要一点技巧，类似于 [Strassen的矩阵乘法。](https://www.geeksforgeeks.org/strassens-matrix-multiplication/) 我们进行以下3个乘法。

```
X = (A0 + A1)*(B0 + B1) // First Multiplication
Y = A0B0  // Second 
Z = A1B1  // Third

The missing middle term in above multiplication equation A0*B0 + (A0*B1 + 
A1*B0)xn/2 + A1*B1*xn can obtained using below.
A0B1 + A1B0 = X - Y - Z  
```

***深入说明***
常规多项式乘法使用4个系数乘法：

```
(ax + b)(cx + d) = acx2 + (ad + bc)x + bd
```

但是，请注意以下关系：

```
(a + b)(c + d) = ad + bc + ac + bd
```

这两个分量的其余部分恰好是两个多项式乘积的中间系数。 因此，乘积可以计算为：

```
(ax + b)(cx + d) = acx2 + 
((a + b)(c + d) - ac - bd )x + bd
```

因此，后一个表达式只有三个乘法。

因此，该算法花费的时间为T（n）= 3T（n / 2）+ O（n）
上述重现的解决方案是O（n <sup>Lg3</sup> ），它比O（n n <sup>2</sup> ）。

我们将很快讨论上述方法的实现。

还有一种O（nLogn）算法，该算法也使用快速傅立叶变换将两个多项式相乘（有关详细信息，请参阅[和](https://www.cs.iastate.edu/~cs577/handouts/polymultiply.pdf)[。）](http://www.cs.cmu.edu/afs/cs/academic/class/15451-s10/www/lectures/lect0423.txt)

**来源：**
[http://www.cse.ust.hk/~dekai/271/notes/L03/L03.pdf](http://www.cse.ust.hk/~dekai/271/notes/L03/L03.pdf)

本文由Harsh贡献。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

