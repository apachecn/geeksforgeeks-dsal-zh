# 维埃塔公式

> 原文:[https://www.geeksforgeeks.org/vietas-formulas/](https://www.geeksforgeeks.org/vietas-formulas/)

维埃塔公式将多项式的系数与它们的根的和与积以及以组为单位的根的积联系起来。维埃塔公式描述了多项式的根与其系数之间的关系。考虑下面的例子，找出一个给定根的多项式。(只讨论实值多项式，即多项式的系数是实数)。让我们取一个二次多项式。给定两个实数根![r_{1}  ](img/9465008cdb15c846d2c5752fdc8ca589.png "Rendered by QuickLaTeX.com")和![r_{2}  ](img/a5c521ef9d935e222c96717a25accbcd.png "Rendered by QuickLaTeX.com")，然后求一个多项式。
考虑多项式![a_{2}x^{2} + a_{1}x + a_{0}  ](img/78bb2b656b4900ec413b1a3e2c56e2d4.png "Rendered by QuickLaTeX.com")。给定词根，我们也可以把它写成
![k(x - r_{1})(x - r_{2})  ](img/49f9c7847365af90fa5ff498f4aa7c84.png "Rendered by QuickLaTeX.com")。
由于两个方程都表示同一个多项式，所以将两个多项式
![a_{2}x^{2} + a_{1}x + a_{0} = k(x - r_{1})(x - r_{2})  ](img/f73faeaa7503f95635b6df7400838cc7.png "Rendered by QuickLaTeX.com")
等同起来把上面的方程简化，我们得到
![a_{2}x^{2} + a_{1}x + a_{0} = kx^{2}-k(r_{1} + r_{2})x + k(r_{1}r_{2})  ](img/f12205e5116685a7fd67e5f9d0e946cc.png "Rendered by QuickLaTeX.com")
比较两边的系数，我们得到
为![x^{2}  ](img/24b930099fe42f5dde52621874f7b1ee.png "Rendered by QuickLaTeX.com")、![a_{2} = k  ](img/b16fa94414931804067e478f66a097ea.png "Rendered by QuickLaTeX.com")、
为![x  ](img/69be1d2582da5bcec6e07003b105189f.png "Rendered by QuickLaTeX.com")、![a_{1} = -k(r_{1} + r_{2})  ](img/b8373fc67566921900aa7a6b6d88c251.png "Rendered by QuickLaTeX.com")、
为常数项，![a_{0} = kr_{1}r_{2}  ](img/4570a0a7d6d87d0e3721cf2b3a987470.png "Rendered by QuickLaTeX.com")、
由此给出，
![a_{2} = k  ](img/b16fa94414931804067e478f66a097ea.png "Rendered by QuickLaTeX.com")、
![\frac{a_{1}}{a_{2}} = -(r_{1} + r_{2})........(1)  ](img/369413296ac20a37fd61f7522f01354d.png "Rendered by QuickLaTeX.com")
![\frac{a_{0}}{a_{2}} = r_{1}r_{2}..................(2)  ](img/200fa39f883e59088c4bbe398d6d4182.png "Rendered by QuickLaTeX.com")
方程(1)
一般来说，对于一个![nth  ](img/c3c830ef93d2aa5e36845655ac5ec9c4.png "Rendered by QuickLaTeX.com")次多项式，有 n 个不同的维埃塔公式。它们可以用浓缩的形式写成
For ![0 \leq k \leq n  ](img/2bde958c45feb91ee501dc53ffb1a2a9.png "Rendered by QuickLaTeX.com")
![\sum_{1 \leq i_{1} < i_{2} < ... < i_{k} \leq n} (r_{i_{1}}r_{i_{2}} ... r_{i_{k}}) = (-1)^{k}\frac{a_{n-k}}{a_{n}}.  ](img/4f648ac8c116392f5826bc09fca91d8c.png "Rendered by QuickLaTeX.com")
下面的例子说明了用维埃塔公式解题。
**举例:**

```
Input : n = 2
        roots = {-3, 2}
Output : Polynomial coefficients: 1, 1, -5

Input : n = 4
        roots = {-1, 2, -3, 7}
Output : Polynomial coefficients: 1, -5, -19, 29, 42
```

## C++

```
// C++ program to implement vieta formula
// to calculate polynomial coefficients.
#include <bits/stdc++.h>
using namespace std;

// Function to calculate polynomial
// coefficients.
void vietaFormula(int roots[], int n)
{
    // Declare an array for
    // polynomial coefficient.
    int coeff[n + 1];

    // Set all coefficients as zero initially
    memset(coeff, 0, sizeof(coeff));

    // Set highest order coefficient as 1
    coeff[n] = 1;

    for (int i = 1; i <= n; i++) {
        for (int j = n - i - 1; j < n; j++) {
            coeff[j] = coeff[j] + (-1) *
                roots[i - 1] * coeff[j + 1];
        }
    }

    cout << "Polynomial Coefficients: ";
    for (int i = n; i >= 0; i--) {
        cout << coeff[i] << " ";
    }
}

// Driver code
int main()
{
    // Degree of required polynomial
    int n = 4;

    // Initialise an array by
    // root of polynomial
    int roots[] = { -1, 2, -3, 7 };

    // Function call
    vietaFormula(roots, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement vieta formula
// to calculate polynomial coefficients.
import java.util.Arrays;

class GFG
{

// Function to calculate polynomial
// coefficients.
static void vietaFormula(int roots[], int n)
{
    // Declare an array for
    // polynomial coefficient.
    int coeff[] = new int[++n + 1];
    Arrays.fill(coeff, 0);

    // Set highest order coefficient as 1
    coeff[n] = 1;

    for (int i = 1; i <n; i++)
    {
        for (int j = n - i - 1; j < n; j++)
        {
            coeff[j] = coeff[j] + (-1) *
                roots[i - 1] * coeff[j + 1];
        }
    }

    System.out.print("Polynomial Coefficients: ");
    for (int i = n; i > 0; i--)
    {
        System.out.print(coeff[i] + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    // Degree of required polynomial
    int n = 4;

    // Initialise an array by
    // root of polynomial
    int roots[] = { -1, 2, -3, 7 };

    // Function call
    vietaFormula(roots, n);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to implement
# Vieta's formula to calculate
# polynomial coefficients.
def vietaFormula(roots, n):

    # Declare an array for
    # polynomial coefficient.
    coeff = [0] * (n + 1)

    # Set Highest Order
    # Coefficient as 1
    coeff[n] = 1
    for i in range(1, n + 1):
        for j in range(n - i - 1, n):
            coeff[j] += ((-1) * roots[i - 1] *
                                coeff[j + 1])

    # Reverse Array
    coeff = coeff[::-1]

    print("Polynomial Coefficients : ", end = "")

    # Print Coefficients
    for i in coeff:
        print(i, end = " ")
    print()

# Driver Code
if __name__ == "__main__":

    # Degree of Polynomial
    n = 4

    # Initialise an array by
    # root of polynomial
    roots = [-1, 2, -3, 7]

    # Function call
    vietaFormula(roots, n)

# This code is contributed
# by Arihant Joshi
```

## C#

```
// C# program to implement vieta formula
// to calculate polynomial coefficients.
using System;

class GFG
{

// Function to calculate polynomial
// coefficients.
static void vietaFormula(int []roots, int n)
{
    // Declare an array for
    // polynomial coefficient.
    int []coeff = new int[++n + 1];

    // Set highest order coefficient as 1
    coeff[n] = 1;

    for (int i = 1; i <n; i++)
    {
        for (int j = n - i - 1; j < n; j++)
        {
            coeff[j] = coeff[j] + (-1) *
                roots[i - 1] * coeff[j + 1];
        }
    }

    Console.Write("Polynomial Coefficients: ");
    for (int i = n; i > 0; i--)
    {
        Console.Write(coeff[i] + " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    // Degree of required polynomial
    int n = 4;

    // Initialise an array by
    // root of polynomial
    int []roots = { -1, 2, -3, 7 };

    // Function call
    vietaFormula(roots, n);
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement vieta formula
// to calculate polynomial coefficients.

// Function to calculate polynomial
// coefficients.
function vietaFormula($roots, $n)
{
    // Declare an array for
    // polynomial coefficient.
    $coeff = array_fill(0, $n + 1, 0);

    // Set all coefficients as zero initially

    // Set highest order coefficient as 1
    $coeff[$n] = 1;

    for ($i = 1; $i <= $n; $i++)
    {
        for ($j = $n - $i; $j < $n; $j++)
        {
            $coeff[$j] = $coeff[$j] + (-1) *
                         $roots[$i - 1] *
                         $coeff[$j + 1];
        }
    }

    echo "polynomial coefficients: ";
    for ($i = $n; $i >= 0; $i--)
    {
        echo $coeff[$i]. " ";
    }
}

// Driver code

// Degree of required polynomial
$n = 4;

// Initialise an array by
// root of polynomial
$roots = array(-1, 2, -3, 7);

// Function call
vietaFormula($roots, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to implement vieta formula
// to calculate polynomial coefficients.

// Function to calculate polynomial
// coefficients.
function vietaFormula(roots, n)
{

    // Declare an array for
    // polynomial coefficient.
    let coeff = new Array(++n + 1);
    for(let i = 0; i < coeff.length; i++)
        coeff[i] = 0;

    // Set highest order coefficient as 1
    coeff[n] = 1;

    for (let i = 1; i <n; i++)
    {
        for (let j = n - i - 1; j < n; j++)
        {
            coeff[j] = coeff[j] + (-1) *
                roots[i - 1] * coeff[j + 1];
        }
    }

    document.write("Polynomial Coefficients: ");
    for (let i = n; i > 0; i--)
    {
        document.write(coeff[i] + " ");
    }
}

// Driver code
// Degree of required polynomial
let n = 4;

// Initialise an array by
// root of polynomial
let roots = [ -1, 2, -3, 7 ];

// Function call
vietaFormula(roots, n);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Polynomial Coefficients: 1 -5 -19 29 42 
```

**时间复杂度:** ![\mathcal{O}(n^{2})  ](img/c5dc2e2bdf7beb96608a506905f27ce6.png "Rendered by QuickLaTeX.com")。