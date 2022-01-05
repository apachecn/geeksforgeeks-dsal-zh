# 通过投掷 N 个骰子获得的值的乘积获得素数的概率

> 原文:[https://www . geeksforgeeks . org/通过投掷 n 个骰子获得的值的乘积获得素数的概率/](https://www.geeksforgeeks.org/probability-of-obtaining-prime-numbers-as-product-of-values-obtained-by-throwing-n-dices/)

给定一个表示骰子点数的整数 **N** ，任务是找出出现在 **N** 掷出的骰子的顶面上的数字乘积为[素数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)的[概率](https://www.geeksforgeeks.org/mathematics-probability/)。所有 **N** 骰子必须同时投掷。

**示例:**

> **输入** : N = 2
> **输出:** 6 / 36
> **解释:**
> 在同时投掷 N(=2)个骰子时，乘积等于素数的 N(=2)个骰子顶面上的可能结果为:{(1，2)，(1，3)，(1，5)，(2，1)，(3，1)，(1)，(3，1)，(5，1)}。
> 因此，有利结果的计数= 6，样本空间的计数= 36
> 因此，所需的输出为(6 / 36)
> 
> **输入:**N = 3
> T3】输出: 9 / 216

**天真方法:**解决这个问题最简单的方法是通过同时投掷 **N** 个骰子，在 **N** 个骰子的顶面上生成所有可能的结果，并针对每个可能的结果检查顶面上的数字乘积是否为[素数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)。如果发现为真，则递增计数器。最后，把顶面上的数字乘积作为素数打印出来。

***时间复杂度:**O(6<sup>N</sup>* N)*
***辅助空间:** O(1)*

**高效方法:**优化上述方法的思路是，仅当**(N–1)**数为 **1** 且剩余数为素数时，利用 **N** 数的乘积为素数的事实。以下是观察结果:

> 如果 N 个数的乘积是素数，那么(N–1)个数的值必须是 1，剩余的数必须是素数。
> 范围[1，6]内素数的总数为 3。
> 因此，顶面上的 N 个数的乘积为素数的结果总数= 3 * N .
> P(E)= N(E)/N(S)
> P(E)=得到 N 个骰子顶面上的数的乘积为素数的概率。
> N(E) =有利结果总数= 3 * N
> N(S) =样本空间中事件总数= 6<sup>N</sup>T8】

按照以下步骤解决此问题:

*   初始化一个变量，比如 **N_E** 来存储有利结果的计数。
*   初始化一个变量，比如 **N_S** 来存储样本空间的计数。
*   更新 **N_E = 3 * N** 。
*   更新**N _ S = 6<sup>N</sup>T3】。**
*   最后打印 **(N_E / N_S)** 的值。

下面是上述方法的实现

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the value
// of power(X, N)
long long int power(long long int x,
                    long long int N)
{
    // Stores the value
    // of (X ^ N)
    long long int res = 1;

    // Calculate the value of
    // power(x, N)
    while (N > 0) {

       // If N is odd
       if(N & 1) {

           //Update res
           res = (res * x);
       }

       //Update x
       x = (x * x);

       //Update N
       N = N >> 1;

    }
    return res;
}

// Function to find the probability of
// obtaining a prime number as the
// product of N thrown dices
void probablityPrimeprod(long long int N)
{
    // Stores count of favorable outcomes
    long long int N_E = 3 * N;

    // Stores count of sample space
    long long int N_S = power(6, N);

    // Print the required probability
    cout<<N_E<<" / "<<N_S;
}

// Driver code
int main()
{
    long long int N = 2;
    probablityPrimeprod(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the value
// of power(X, N)
static int power(int x, int N)
{

    // Stores the value
    // of (X ^ N)
    int res = 1;

    // Calculate the value of
    // power(x, N)
    while (N > 0)
    {

        // If N is odd
        if (N % 2 == 1)
        {

            // Update res
            res = (res * x);
        }

        // Update x
        x = (x * x);

        // Update N
        N = N >> 1;
    }
    return res;
}

// Function to find the probability of
// obtaining a prime number as the
// product of N thrown dices
static void probablityPrimeprod(int N)
{

    // Stores count of favorable outcomes
    int N_E = 3 * N;

    // Stores count of sample space
    int N_S = power(6, N);

    // Print the required probability
    System.out.print(N_E + " / " + N_S);
}

// Driver code
public static void main(String[] args)
{
    int N = 2;

    probablityPrimeprod(N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the value
# of power(X, N)
def power(x, N):

    # Stores the value
    # of (X ^ N)
    res = 1

    # Calculate the value of
    # power(x, N)
    while (N > 0):

        # If N is odd
        if (N % 2 == 1):

            # Update res
            res = (res * x)

        # Update x
        x = (x * x)

        # Update N
        N = N >> 1

    return res

# Function to find the probability of
# obtaining a prime number as the
# product of N thrown dices
def probablityPrimeprod(N):

    # Stores count of favorable outcomes
    N_E = 3 * N

    # Stores count of sample space
    N_S = power(6, N)

    # Print required probability
    print(N_E, " / ", N_S)

# Driver code
if __name__ == '__main__':

    N = 2

    probablityPrimeprod(N)

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to find the
// value of power(X, N)
static int power(int x,
                 int N)
{   
  // Stores the value
  // of (X ^ N)
  int res = 1;

  // Calculate the value
  // of power(x, N)
  while (N > 0)
  {
    // If N is odd
    if (N % 2 == 1)
    {
      // Update res
      res = (res * x);
    }

    // Update x
    x = (x * x);

    // Update N
    N = N >> 1;
  }
  return res;
}

// Function to find the probability
// of obtaining a prime number as
// the product of N thrown dices
static void probablityPrimeprod(int N)
{   
  // Stores count of favorable
  // outcomes
  int N_E = 3 * N;

  // Stores count of sample
  // space
  int N_S = power(6, N);

  // Print the required
  // probability
  Console.Write(N_E + " / " + N_S);
}

// Driver code
public static void Main(String[] args)
{
  int N = 2;
  probablityPrimeprod(N);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to implement the above approach

// Function to find the value
// of power(X, N)
function power(x, N)
{

    // Stores the value
    // of (X ^ N)
    let res = 1;

    // Calculate the value of
    // power(x, N)
    while (N > 0)
    {

        // If N is odd
        if (N % 2 == 1)
        {

            // Update res
            res = (res * x);
        }

        // Update x
        x = (x * x);

        // Update N
        N = N >> 1;
    }
    return res;
}

// Function to find the probability of
// obtaining a prime number as the
// product of N thrown dices
function probablityPrimeprod(N)
{

    // Stores count of favorable outcomes
    let N_E = 3 * N;

    // Stores count of sample space
    let N_S = power(6, N);

    // Print the required probability
    document.write(N_E + " / " + N_S);
}

// Driver Code
    let N = 2;
    probablityPrimeprod(N);

    // This code is contributed by susmitakunndugoaldanga.

</script>
```

**Output:** 

```
6 / 36
```

***时间复杂度:**O(log<sub>2</sub>N)*
*T8】辅助空间: O( 1 )*