# 用递归二分搜索法法求一个数的第 k 个根的楼层值

> 原文:[https://www . geesforgeks . org/floor-value-kth-number-root-use-recursive-binary-search/](https://www.geeksforgeeks.org/floor-value-kth-root-of-a-number-using-recursive-binary-search/)

给定两个数字 **N** 和 **K** ，任务是找到数字 **N** 的 **Kth 根**的地板值。
数 N 的 Floor **Kth 根**是小于或等于其 **Kth** 根的最大整数。
**举例:**

> **输入:** N = 27，K = 3
> **输出:** 3
> **说明:**
> 27 的 Kth 根= 3。因此 3 是小于等于 27 的 Kth 根的最大整数。
> **输入:** N = 36，K = 3
> **输出:** 3
> **解释:**
> 36 的 Kth 根= 3.30
> 因此 3 是小于等于 36 (3.30)
> 的 Kth 根的最大整数

**天真方法:**想法是从 **1 到 N** 找到数字的第 K 次方，直到某个数字的第 K 次方 **K** 变得大于 **N** 。那么**(K–1)**的值将是 N 的**K 次根的楼层值。
下面是使用朴素方法解决这个问题的算法:** 

*   在 k 中从数字 1 到 N 迭代一个循环
*   对于任意 K，如果它的 K 次方变得大于 N，那么 **K-1** 就是 N 的 K 次方的底值。

**时间复杂度:** O(√N)
**高效进场:**
从天真进场来看，很明显**N 的第 k 根**的地板值将位于**【1，N】**的范围内。因此，我们可以通过使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)在这个范围内有效地搜索所需的号码，而不是检查这个范围内的每个号码。
下面是使用**二分搜索法** :
解决上述问题的递归算法

1.  在 0 到 n 的范围内实施二分搜索法
2.  使用公式
    找到范围的中间值

```
mid = (start + end) / 2
```

2.  **基本情况:**递归调用将被执行，直到**中间**的第 k 次幂小于或等于 **N** 、**中间+1】**的第 k 次幂大于或等于 **N** 。

```
(midK ≤ N) and ((mid + 1)K > N)
```

2.  如果基本情况不满足，那么范围将相应地改变。
    *   如果中间的 **Kth 次方小于等于 **N** ，则范围更新为**【中间+ 1，结束】**** 

```
if(midK ≤ N)
    updated range = [mid + 1, end]
```

*   如果中间的 **Kth 功率大于 **N** ，则范围更新为**【低，中间+1】**** 

```
if(midK > N)
    updated range = [low, mid - 1]
```

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate x raised
// to the power y in O(logn)
int power(int x, unsigned int y)
{
    int temp;
    if (y == 0)
        return 1;
    temp = power(x, y / 2);
    if (y % 2 == 0)
        return temp * temp;
    else
        return x * temp * temp;
}

// Function to find the Kth
// root of the number N using BS
int nthRootSearch(int low, int high,
                  int N, int K)
{

    // If the range is still valid
    if (low <= high) {

        // Find the mid-value of range
        int mid = (low + high) / 2;

        // Base Case
        if ((power(mid, K) <= N)
            && (power(mid + 1, K) > N)) {
            return mid;
        }

        // Condition to check if the
        // left search space is useless
        else if (power(mid, K) < N) {
            return nthRootSearch(mid + 1,
                                 high, N, K);
        }
        else {
            return nthRootSearch(low,
                                 mid - 1,
                                 N, K);
        }
    }
    return low;
}

// Driver Code
int main()
{

    // Given N and K
    int N = 16, K = 4;

    // Function Call
    cout << nthRootSearch(0, N, N, K)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to calculate x raised
// to the power y in O(logn)
static int power(int x, int y)
{
    int temp;
    if (y == 0)
        return 1;

    temp = power(x, y / 2);
    if (y % 2 == 0)
        return temp * temp;
    else
        return x * temp * temp;
}

// Function to find the Kth
// root of the number N using BS
static int nthRootSearch(int low, int high,
                         int N, int K)
{

    // If the range is still valid
    if (low <= high)
    {

        // Find the mid-value of range
        int mid = (low + high) / 2;

        // Base Case
        if ((power(mid, K) <= N) &&
            (power(mid + 1, K) > N))
        {
            return mid;
        }

        // Condition to check if the
        // left search space is useless
        else if (power(mid, K) < N)
        {
            return nthRootSearch(mid + 1,
                                 high, N, K);
        }
        else
        {
            return nthRootSearch(low,
                                 mid - 1, N, K);
        }
    }
    return low;
}

// Driver Code
public static void main(String s[])
{

    // Given N and K
    int N = 16, K = 4;

    // Function Call
    System.out.println(nthRootSearch(0, N, N, K));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate x raised
# to the power y in O(logn)
def power(x, y):

    if (y == 0):
        return 1;
    temp = power(x, y // 2);
    if (y % 2 == 0):
        return temp * temp;
    else:
        return x * temp * temp;

# Function to find the Kth
# root of the number N using BS
def nthRootSearch(low, high, N, K):

    # If the range is still valid
    if (low <= high):

        # Find the mid-value of range
        mid = (low + high) // 2;

        # Base Case
        if ((power(mid, K) <= N) and
            (power(mid + 1, K) > N)):
            return mid;

        # Condition to check if the
        # left search space is useless
        elif (power(mid, K) < N):
            return nthRootSearch(mid + 1,
                                 high, N, K);
        else:
            return nthRootSearch(low,
                                 mid - 1,
                                 N, K);

    return low;

# Driver Code

# Given N and K
N = 16; K = 4;

# Function Call
print(nthRootSearch(0, N, N, K))

# This code is contributed by Code_Mech
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to calculate x raised
// to the power y in O(logn)
static int power(int x, int y)
{
    int temp;
    if (y == 0)
        return 1;

    temp = power(x, y / 2);
    if (y % 2 == 0)
        return temp * temp;
    else
        return x * temp * temp;
}

// Function to find the Kth
// root of the number N using BS
static int nthRootSearch(int low, int high,
                         int N, int K)
{

    // If the range is still valid
    if (low <= high)
    {

        // Find the mid-value of range
        int mid = (low + high) / 2;

        // Base Case
        if ((power(mid, K) <= N) &&
            (power(mid + 1, K) > N))
        {
            return mid;
        }

        // Condition to check if the
        // left search space is useless
        else if (power(mid, K) < N)
        {
            return nthRootSearch(mid + 1,
                                 high, N, K);
        }
        else
        {
            return nthRootSearch(low,
                                 mid - 1, N, K);
        }
    }
    return low;
}

// Driver Code
public static void Main()
{

    // Given N and K
    int N = 16, K = 4;

    // Function Call
    Console.Write(nthRootSearch(0, N, N, K));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to calculate x raised
// to the power y in O(logn)
function power(x, y)
{
    let temp;
    if (y == 0)
        return 1;

    temp = power(x, Math.floor(y / 2));
    if (y % 2 == 0)
        return temp * temp;
    else
        return x * temp * temp;
}

// Function to find the Kth
// root of the number N using BS
function nthRootSearch(low, high,
                         N, K)
{

    // If the range is still valid
    if (low <= high)
    {

        // Find the mid-value of range
        let mid = Math.floor((low + high) / 2);

        // Base Case
        if ((power(mid, K) <= N) &&
            (power(mid + 1, K) > N))
        {
            return mid;
        }

        // Condition to check if the
        // left search space is useless
        else if (power(mid, K) < N)
        {
            return nthRootSearch(mid + 1,
                                 high, N, K);
        }
        else
        {
            return nthRootSearch(low,
                                 mid - 1, N, K);
        }
    }
    return low;
}

// Driver code

    // Given N and K
    let N = 16, K = 4;

    // Function Call
    document.write(nthRootSearch(0, N, N, K));

 // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
2
```

**时间复杂度:** *O(log N)*
***辅助空间:** O(1)*