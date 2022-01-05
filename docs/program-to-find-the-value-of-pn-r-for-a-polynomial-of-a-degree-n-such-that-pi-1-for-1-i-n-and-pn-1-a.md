# 求 N 次多项式的 P(N + r)值的程序，使得 P(i) = 1 对 1 ≤ i ≤ N，P(N + 1) = a

> 原文:[https://www . geesforgeks . org/program-to-find-值-pn-r-for-a-次多项式-n-so-pi-1 for-I-n-and-pn-1-a/](https://www.geeksforgeeks.org/program-to-find-the-value-of-pn-r-for-a-polynomial-of-a-degree-n-such-that-pi-1-for-1-i-n-and-pn-1-a/)

给定三个正整数 **N** 、 **R** 、 **A** 和一个多项式 **P(X)** 的次数 **N** 、 **P(i) = 1** 对于 **1 ≤ i ≤ N** ， **P(N + 1)** 的值为 **A** ，任务是求 **P(N)的值**

**示例:**

> **输入:** N = 1，R = 3，A = 2
> **输出:** 4
> **说明:**
> 给定多项式的方程为 P(x) = x，因此 P(N + R) = P(4) = 4。
> 
> **输入:** N = 2，R = 3，A = 1
> T3】输出: 1

**逼近:**给定问题可以通过求给定多项式的表达式 **P(X)** 然后计算 **P(N + R)** 的值来求解。次数为 **N** 的多项式的一般形式是:

> **P(x)= k *(x–x<sub>1</sub>)*(x–x<sub>2</sub>)*(x–x<sub>3</sub>)*……*(x–x<sub>n</sub>)+c**
> 其中 x <sub>1</sub> ，x <sub>2</sub> ，x <sub>3</sub> ，…，x <sub>n</sub> 为根

> **考虑 F(x)是另一个 N 次多项式，使得
> F(x) = P(x) + c — (1)**
> 
> **现在，如果 c = -1，F(x) = 0，因为 P(x) = 1 代表 x ∈ [1，N]。
> F(x)有 N 个根，等于 1，2，3，…，N.
> 因此，对于所有 c = -1，F(x)= k *(x–1)*(x–2)*…*(x–N)。**
> 
> **重新排列等式(1)中的项，
> P(x)= F(x)–c
> P(x)= k *(x–1)*(x–2)*……*(x–N)+1—(2)**
> 
> **将 x = N + 1 放入等式(2)中，
> k =(a–1)/N！**
> 
> **因此，**P(x)=((a–1)/N！)*(x–1)*(x–2)*……*(x–N)+1—(3)****

**因此，想法是将公式(3)中 **(N + R)** 的值代入，并将表达式的值打印为结果。按照以下步骤解决问题:**

*   **初始化一个变量，比如**和**，作为**(A–1)/N 的值！**。**
*   **[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，并将 **ans** 的值更新为**ans *(N+R–I)**。**
*   **完成上述步骤后，打印 **(ans + 1)** 的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// factorial of N
int fact(int n)
{

    // Base Case
    if (n == 1 || n == 0)
        return 1;

    // Otherwise, recursively
    // calculate the factorial
    else
        return n * fact(n - 1);
}

// Function to find the value of
// P(n + r) for polynomial P(X)
int findValue(int n, int r, int a)
{

    // Stores the value of k
    int k = (a - 1) / fact(n);

    // Store the required answer
    int answer = k;

    // Iterate in the range [1, N] and
    // multiply (n + r - i) with answer
    for(int i = 1; i < n + 1; i++)
        answer = answer * (n + r - i);

    // Add the constant value C as 1
    answer = answer + 1;

    // Return the result
    return answer;
}

// Driver Code
int main()
{
    int N = 1;
    int A = 2;
    int R = 3;

    cout << (findValue(N, R, A));

    return 0;
}

// This code is contributed by mohit kumar 29
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to calculate
// factorial of N
static int fact(int n)
{

    // Base Case
    if (n == 1 || n == 0)
        return 1;

    // Otherwise, recursively
    // calculate the factorial
    else
        return n * fact(n - 1);
}

// Function to find the value of
// P(n + r) for polynomial P(X)
static int findValue(int n, int r, int a)
{

    // Stores the value of k
    int k = (a - 1) / fact(n);

    // Store the required answer
    int answer = k;

    // Iterate in the range [1, N] and
    // multiply (n + r - i) with answer
    for(int i = 1; i < n + 1; i++)
        answer = answer * (n + r - i);

    // Add the constant value C as 1
    answer = answer + 1;

    // Return the result
    return answer;
}

// Driver Code
public static void main(String args[])
{
    int N = 1;
    int A = 2;
    int R = 3;
    System.out.print(findValue(N, R, A));
}

}

// This code is contributed by SURENDRA_GANGWAR.
```

## **蟒蛇 3**

```
# Python program for the above approach

# Function to calculate
# factorial of N
def fact(n):

    # Base Case
    if n == 1 or n == 0:
        return 1

    # Otherwise, recursively
    # calculate the factorial
    else:
        return n * fact(n-1)

# Function to find the value of
# P(n + r) for polynomial P(X)
def findValue(n, r, a):

    # Stores the value of k
    k = (a-1) // fact(n)

    # Store the required answer
    answer = k

    # Iterate in the range [1, N] and
    # multiply (n + r - i) with answer
    for i in range(1, n + 1):
        answer = answer*(n + r-i)

    # Add the constant value C as 1
    answer = answer + 1

    # Return the result
    return answer

# Driver Code

N = 1
A = 2
R = 3

print(findValue(N, R, A))
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate
// factorial of N
static int fact(int n)
{

    // Base Case
    if (n == 1 || n == 0)
        return 1;

    // Otherwise, recursively
    // calculate the factorial
    else
        return n * fact(n - 1);
}

// Function to find the value of
// P(n + r) for polynomial P(X)
static int findValue(int n, int r, int a)
{

    // Stores the value of k
    int k = (a - 1) / fact(n);

    // Store the required answer
    int answer = k;

    // Iterate in the range [1, N] and
    // multiply (n + r - i) with answer
    for(int i = 1; i < n + 1; i++)
        answer = answer * (n + r - i);

    // Add the constant value C as 1
    answer = answer + 1;

    // Return the result
    return answer;
}

// Driver Code
static public void Main()
{
    int N = 1;
    int A = 2;
    int R = 3;

    Console.Write((findValue(N, R, A)));
}
}

// This code is contributed by code_hunt
```

## **java 描述语言**

```
<script>

// JavaScript program to implement
// the above approach

// Function to calculate
// factorial of N
function fact(n)
{

    // Base Case
    if (n == 1 || n == 0)
        return 1;

    // Otherwise, recursively
    // calculate the factorial
    else
        return n * fact(n - 1);
}

// Function to find the value of
// P(n + r) for polynomial P(X)
function findValue(n, r, a)
{

    // Stores the value of k
    let k = (a - 1) / fact(n);

    // Store the required answer
    let answer = k;

    // Iterate in the range [1, N] and
    // multiply (n + r - i) with answer
    for(let i = 1; i < n + 1; i++)
        answer = answer * (n + r - i);

    // Add the constant value C as 1
    answer = answer + 1;

    // Return the result
    return answer;
}

// Driver code
    let N = 1;
    let A = 2;
    let R = 3;
    document.write(findValue(N, R, A));

 // This code is contributed by code_hunt.
</script>
```

****Output:** 

```
4
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**