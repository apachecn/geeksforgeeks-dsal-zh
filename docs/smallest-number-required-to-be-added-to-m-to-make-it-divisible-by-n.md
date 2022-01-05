# 为使 M 能被 N 整除而需要加到 M 上的最小数

> 原文:[https://www . geeksforgeeks . org/最小需要加到 m 上的数字才能被 n 整除/](https://www.geeksforgeeks.org/smallest-number-required-to-be-added-to-m-to-make-it-divisible-by-n/)

给定两个正整数 **M** 和 **N** ，任务是计算需要加到 **M** 上的最小数，使其能被 **N** 整除。

**示例:**

> **输入:** M = 6，N = 7
> **输出:** 1
> **说明:** 1 是可加 6 使其可被 7 整除的最小数。
> 
> **输入:** M = 100，N = 28
> T3】输出: 12

**逼近:**思路是找到大于等于 **M** 的[最小数，即被**N**T7】整除，然后从中减去 **M** 。要得到 **N** **≥ M** 的最小倍数，将 **M + N** 除以 **N** 。如果余数为 **0** ，则值为 **M** 。否则，值为**M+N–余数**。](https://www.geeksforgeeks.org/smallest-number-greater-than-or-equal-to-n-divisible-by-k/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest
// number greater than or equal
// to N, that is divisible by k
int findNum(int N, int K)
{
    int rem = (N + K) % K;

    if (rem == 0)
        return N;
    else
        return N + K - rem;
}

// Function to find the smallest
// number required to be added to
// to M to make it divisible by N
int findSmallest(int M, int N)
{
    // Stores the smallest multiple
    // of N, greater than or equal to M
    int x = findNum(M, N);

    // Return the result
    return x - M;
}

// Driver Code
int main()
{
    // Given Input
    int M = 100, N = 28;

    // Function Call
    cout << findSmallest(M, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the smallest
// number greater than or equal
// to N, that is divisible by k
public static int findNum(int N, int K)
{
    int rem = (N + K) % K;

    if (rem == 0)
        return N;
    else
        return N + K - rem;
}

// Function to find the smallest
// number required to be added to
// to M to make it divisible by N
public static int findSmallest(int M, int N)
{

    // Stores the smallest multiple
    // of N, greater than or equal to M
    int x = findNum(M, N);

    // Return the result
    return x - M;
}

// Driver Code
public static void main(String args[])
{

    // Given Input
    int M = 100, N = 28;

    // Function Call
    System.out.println(findSmallest(M, N));
}}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the smallest
# number greater than or equal
# to N, that is divisible by k
def findNum(N, K):

    rem = (N + K) % K

    if (rem == 0):
        return N
    else:
        return N + K - rem

# Function to find the smallest
# number required to be added to
# to M to make it divisible by N
def findSmallest(M, N):

    # Stores the smallest multiple
    # of N, greater than or equal to M
    x = findNum(M, N)

    # Return the result
    return x - M

# Driver Code
if __name__ == '__main__':

    # Given Input
    M = 100
    N = 28

    # Function Call
    print(findSmallest(M, N))

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the smallest
// number greater than or equal
// to N, that is divisible by k
public static int findNum(int N, int K)
{
    int rem = (N + K) % K;

    if (rem == 0)
        return N;
    else
        return N + K - rem;
}

// Function to find the smallest
// number required to be added to
// to M to make it divisible by N
public static int findSmallest(int M, int N)
{

    // Stores the smallest multiple
    // of N, greater than or equal to M
    int x = findNum(M, N);

    // Return the result
    return x - M;
}

// Driver Code
public static void Main()
{

    // Given Input
    int M = 100, N = 28;

    // Function Call
    Console.WriteLine(findSmallest(M, N));
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the smallest
// number greater than or equal
// to N, that is divisible by k
function findNum(N, K)
{
    var rem = (N + K) % K;

    if (rem == 0)
        return N;
    else
        return N + K - rem;
}

// Function to find the smallest
// number required to be added to
// to M to make it divisible by N
function findSmallest(M, N)
{

    // Stores the smallest multiple
    // of N, greater than or equal to M
    var x = findNum(M, N);

    // Return the result
    return x - M;
}

// Driver Code

// Given Input
var M = 100, N = 28;

// Function Call
document.write(findSmallest(M, N));

// This code is contributed by itsok

</script>
```

**Output:** 

```
12
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)