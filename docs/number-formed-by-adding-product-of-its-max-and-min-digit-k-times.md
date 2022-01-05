# 最大和最小数字 K 次的乘积形成的数

> 原文:[https://www . geeksforgeeks . org/number-通过添加其最大和最小数字 k 倍的乘积形成/](https://www.geeksforgeeks.org/number-formed-by-adding-product-of-its-max-and-min-digit-k-times/)

给定两个整数 **N** 和 **K** ，任务是打印其最大值和最小值的乘积 K 次形成的数字。
![M(N+1) = M(N) + maxDigit(M(N)) * minDigit(M(N))  ](img/158f9666a0e4cbd82439a067f6b72621.png "Rendered by QuickLaTeX.com")

**示例**

> **输入:** N = 14，K = 3
> **输出:** 26
> **解释:**
> M(0)= 14
> M(1)= 14+1 * 4 = 18
> M(2)= 18+1 * 8 = 26
> 
> **输入:** N = 487，K = 100000000
> T3】输出 : 950

**接近**

*   一个自然的直觉是运行一个循环 K 次，不断更新 n 的值。
*   但是可以观察到，在一些迭代之后，数字的最小值可能为零，并且在此之后，N 永远不会被更新，因为:

> M(N+1)= M(N)+0 *(max _ digit)
> M(N+1)= M(N)

*   因此，我们只需要算出最小数字何时变为 0。

下面是上述方法的实现:

## C++

```
// C++ Code for the above approach

#include <bits/stdc++.h>
using namespace std;

// function that returns the product of
// maximum and minimum digit of N number.
int prod_of_max_min(int n)
{
    int largest = 0;
    int smallest = 10;

    while (n) {

        // finds the last digit.
        int r = n % 10;

        largest = max(r, largest);
        smallest = min(r, smallest);

        // Moves to next digit
        n = n / 10;
    }

    return largest * smallest;
}

// Function to find the formed number
int formed_no(int N, int K)
{

    if (K == 1) {
        return N;
    }
    K--; // M(1) = N

    int answer = N;
    while (K--) {

        int a_current
            = prod_of_max_min(answer);

        // check if minimum digit is 0
        if (a_current == 0)
            break;

        answer += a_current;
    }

    return answer;
}

// Driver Code
int main()
{

    int N = 487, K = 100000000;

    cout << formed_no(N, K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

// Function to find the formed number
public static int formed_no(int N, int K)
{
    if (K == 1)
    {
        return N;
    }
    K--; // M(1) = N

    int answer = N;
    while(K != 0)
    {
        int a_current = prod_of_max_min(answer);

        // Check if minimum digit is 0
        if (a_current == 0)
            break;

        answer += a_current;
    }
    return answer;
}

// Function that returns the product of
// maximum and minimum digit of N number.
static int prod_of_max_min(int n)
{
    int largest = 0;
    int smallest = 10;

    while(n != 0)
    {

        // Finds the last digit.
        int r = n % 10;

        largest = Math.max(r, largest);
        smallest = Math.min(r, smallest);

        // Moves to next digit
        n = n / 10;
    }
    return largest * smallest;
}

// Driver code
public static void main(String[] args)
{
    int N = 487, K = 100000000;

    System.out.println(formed_no(N, K));
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the formed number
def formed_no(N, K):

    if (K == 1):
        return N
    K -= 1 # M(1) = N

    answer = N
    while (K != 0):

        a_current = prod_of_max_min(answer)

        # Check if minimum digit is 0
        if (a_current == 0):
            break

        answer += a_current
        K -= 1

    return answer

# Function that returns the product of
# maximum and minimum digit of N number.
def prod_of_max_min(n):

    largest = 0
    smallest = 10

    while (n != 0):

        # Find the last digit.
        r = n % 10

        largest = max(r, largest)
        smallest = min(r, smallest)

        # Moves to next digit
        n = n // 10

    return largest * smallest

# Driver Code
if __name__ == "__main__":

    N = 487
    K = 100000000

    print(formed_no(N, K))

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG {

// Function to find the formed number
public static int formed_no(int N, int K)
{
    if (K == 1)
    {
        return N;
    }
    K--; // M(1) = N

    int answer = N;
    while(K != 0)
    {
        int a_current = prod_of_max_min(answer);

        // Check if minimum digit is 0
        if (a_current == 0)
            break;

        answer += a_current;
    }
    return answer;
}

// Function that returns the product of
// maximum and minimum digit of N number.
static int prod_of_max_min(int n)
{
    int largest = 0;
    int smallest = 10;

    while(n != 0)
    {

        // Finds the last digit.
        int r = n % 10;

        largest = Math.Max(r, largest);
        smallest = Math.Min(r, smallest);

        // Moves to next digit
        n = n / 10;
    }
    return largest * smallest;
}

// Driver code
public static void Main(String[] args)
{
    int N = 487, K = 100000000;

    Console.WriteLine(formed_no(N, K));
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// JavaScript Code for the above approach

// Function that returns the product of
// maximum and minimum digit of N number.
function prod_of_max_min(n)
{
    var largest = 0;
    var smallest = 10;

    while (n)
    {

        // Finds the last digit.
        var r = n % 10;

        largest = Math.max(r, largest);
        smallest = Math.min(r, smallest);

        // Moves to next digit
        n = parseInt(n / 10);
    }
    return largest * smallest;
}

// Function to find the formed number
function formed_no(N, K)
{
    if (K == 1)
    {
        return N;
    }
    K--; // M(1) = N

    var answer = N;

    while (K--)
    {
        var a_current = prod_of_max_min(answer);

        // Check if minimum digit is 0
        if (a_current == 0) break;

        answer += a_current;
    }
    return answer;
}

// Driver Code
var N = 487,
K = 100000000;

document.write(formed_no(N, K) + "<br>");

// This code is contributed by rdtank

</script>
```

**Output:** 

```
950
```

***时间复杂度:** O(K)*
***辅助空间:** O(1)*