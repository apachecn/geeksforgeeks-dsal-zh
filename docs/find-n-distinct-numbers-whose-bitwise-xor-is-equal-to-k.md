# 找到 N 个不同的数字，其按位异或等于 K

> 原文:[https://www . geesforgeks . org/find-n-distinct-numbers-其位异或等于-k/](https://www.geeksforgeeks.org/find-n-distinct-numbers-whose-bitwise-xor-is-equal-to-k/)

给定两个正整数 **N** 和 **X** ，任务是构造 **N** 个正整数，所有这些整数的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)等于 **K** 。

**示例:**

> **输入:** N = 4，K = 6
> **输出:** 1 0 2 5
> **解释:**按位异或整数{1，0，2，5} = 1 异或 0 异或 2 异或 5 = 6(= K)。
> 
> **输入:** N = 1，K = 1
> T3】输出: 1

**方法:**解决这个问题的思路是把第一个**(N–3)**个自然数包含进去，计算它们的**位异或**，根据计算出的异或值选择剩下的 3 个整数。按照以下步骤解决问题:

*   **如果 N = 1:** 打印整数 **K** 本身。
*   **如果 N = 2:** 打印 **K** 和 **0** 作为所需输出。
*   否则，考虑第一个**(N–3)**自然数。
*   现在，计算**(N–3)**元素的按位异或，并将其存储在一个变量中，比如**值**。可以根据以下条件选择其余三个元素:
    *   **情况 1:** 如果**值**等于 **K** ，执行以下步骤:
        *   在这种情况下，剩余三个元素的按位异或需要等于零，才能使所有整数的按位异或等于 **K** 。
        *   因此，剩下的三个元素必须是 **P，Q，P 异或 Q** ，从而使它们的按位异或等于 **0** 。
    *   **情况 2:** 如果**值**不等于 **K** ，执行以下步骤:
        *   在这种情况下，剩余三个元素与前**(N–3)**元素的按位异或需要等于 **K** 。
        *   通过考虑最后 3 个元素等于 **0，P，P 异或 K 异或值**，这三个元素的按位异或等于 **K 异或值**。
*   **选择 P 和 Q:** 对于这两种情况， **P** 和 **Q** 的值要求与第一个**(N–3)**元素不同。因此，考虑 **P** 和 **Q** 为**(N–2)**和**(N–1)**。

下面是上述解决方案的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find N integers
// having Bitwise XOR equal to K
void findArray(int N, int K)
{

    // Base Cases
    if (N == 1)
    {
        cout << " " << K;
        return;
    }

    if (N == 2)
    {
        cout << 0 << " " << K;
        return;
    }

    // Assign values to P and Q
    int P = N - 2;
    int Q = N - 1;

    // Stores Bitwise XOR of the
    // first (N - 3) elements
    int VAL = 0;

    // Print the first N - 3 elements
    for(int i = 1; i <= (N - 3); i++)
    {
        cout << " " << i;

        // Calculate Bitwise XOR of
        // first (N - 3) elements
        VAL ^= i;
    }

    if (VAL == K)
    {
        cout << P << " " << Q
             << " " << (P ^ Q);
    }

    else
    {
        cout << 0 << " " << P
             << " " << (P ^ K ^ VAL);
    }
}

// Driver Code
int main()
{
    int N = 4, X = 6;

    // Function Call
    findArray(N, X);

    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program for the above approach
#include <stdio.h>

// Function to find N integers
// having Bitwise XOR equal to K
void findArray(int N, int K)
{
    // Base Cases
    if (N == 1) {
        printf("%d", K);
        return;
    }

    if (N == 2) {
        printf("%d %d", 0, K);
        return;
    }

    // Assign values to P and Q
    int P = N - 2;
    int Q = N - 1;

    // Stores Bitwise XOR of the
    // first (N - 3) elements
    int VAL = 0;

    // Print the first N - 3 elements
    for (int i = 1; i <= (N - 3); i++) {

        printf("%d ", i);

        // Calculate Bitwise XOR of
        // first (N - 3) elements
        VAL ^= i;
    }

    if (VAL == K) {
        printf("%d %d %d", P, Q, P ^ Q);
    }

    else {
        printf("%d %d %d", 0,
               P, P ^ K ^ VAL);
    }
}

// Driver Code
int main()
{
    int N = 4, X = 6;

    // Function Call
    findArray(N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find N integers
// having Bitwise XOR equal to K
static void findArray(int N, int K)
{

    // Base Cases
    if (N == 1)
    {
        System.out.print(K + " ");
        return;
    }

    if (N == 2)
    {
        System.out.print(0 + " " + K);
        return;
    }

    // Assign values to P and Q
    int P = N - 2;
    int Q = N - 1;

    // Stores Bitwise XOR of the
    // first (N - 3) elements
    int VAL = 0;

    // Print the first N - 3 elements
    for(int i = 1; i <= (N - 3); i++)
    {
        System.out.print(i + " ");

        // Calculate Bitwise XOR of
        // first (N - 3) elements
        VAL ^= i;
    }

    if (VAL == K)
    {
        System.out.print(P + " " +
                         Q + " " + (P ^ Q));
    }
    else
    {
        System.out.print(0 + " " +
                         P + " " +
                        (P ^ K ^ VAL));
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 4, X = 6;

    // Function Call
    findArray(N, X);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find N integers
# having Bitwise XOR equal to K
def findArray(N, K):

    # Base Cases
    if (N == 1):
        print(K, end = " ")
        return

    if (N == 2):
        print("0", end = " ")
        print(K, end = " ")
        return

    # Assign values to P and Q
    P = N - 2
    Q = N - 1

    # Stores Bitwise XOR of the
    # first (N - 3) elements
    VAL = 0

    # Print the first N - 3 elements
    for i in range(1, N - 2):
        print(i, end = " ")

        # Calculate Bitwise XOR of
        # first (N - 3) elements
        VAL ^= i

    if (VAL == K):
        print(P, end = " ")
        print(Q, end = " ")
        print(P ^ Q, end = " ")

    else:
        print("0", end = " ")
        print(P , end = " ")
        print(P ^ K ^ VAL, end = " ")

# Driver Code
N = 4
X = 6

# Function Call
findArray(N, X)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find N integers
// having Bitwise XOR equal to K
static void findArray(int N, int K)
{
    // Base Cases
    if (N == 1) {
        Console.Write(K + " ");
        return;
    }

    if (N == 2) {
        Console.Write(0 + " " + K);
        return;
    }

    // Assign values to P and Q
    int P = N - 2;
    int Q = N - 1;

    // Stores Bitwise XOR of the
    // first (N - 3) elements
    int VAL = 0;

    // Print the first N - 3 elements
    for (int i = 1; i <= (N - 3); i++) {

        Console.Write(i + " ");

        // Calculate Bitwise XOR of
        // first (N - 3) elements
        VAL ^= i;
    }

    if (VAL == K) {
        Console.Write(P + " " + Q + " " + (P ^ Q));
    }

    else {
        Console.Write(0 + " " + P + " " + (P ^ K ^ VAL));
    }
}

// Driver Code
public static void Main()
{
    int N = 4, X = 6;

    // Function Call
    findArray(N, X);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find N integers
// having Bitwise XOR equal to K
function findArray(N, K)
{

    // Base Cases
    if (N == 1)
    {
        document.write(K + " ");
        return;
    }

    if (N == 2)
    {
        document.write(0 + " " + K);
        return;
    }

    // Assign values to P and Q
    let P = N - 2;
    let Q = N - 1;

    // Stores Bitwise XOR of the
    // first (N - 3) elements
    let VAL = 0;

    // Prlet the first N - 3 elements
    for(let i = 1; i <= (N - 3); i++)
    {
        document.write(i + " ");

        // Calculate Bitwise XOR of
        // first (N - 3) elements
        VAL ^= i;
    }

    if (VAL == K)
    {
        document.write(P + " " +
                         Q + " " + (P ^ Q));
    }
    else
    {
        document.write(0 + " " +
                         P + " " +
                        (P ^ K ^ VAL));
    }
}

// Driver Code

      let N = 4, X = 6;

    // Function Call
    findArray(N, X);

</script>
```

**输出:**

```
1 0 2 5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)