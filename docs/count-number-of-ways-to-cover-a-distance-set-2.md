# 计算走完一段距离的路数|设置 2

> 原文:[https://www . geesforgeks . org/count-覆盖距离集的路数-2/](https://www.geeksforgeeks.org/count-number-of-ways-to-cover-a-distance-set-2/)

给定距离 **N** 。任务是用 **1** 、 **2** 、 **3** 步数合计走完这段距离的路数。
**举例:**

> **输入:** N = 3
> **输出:** 4
> 所有需要的方式都是(1 + 1 + 1)、(1 + 2)、(2 + 1)和(3)。
> **输入:** N = 4
> **输出:** 7

**方法:**在[之前的](https://www.geeksforgeeks.org/count-number-of-ways-to-cover-a-distance/)文章中，已经讨论了基于递归和动态编程的方法。这里我们将降低空间复杂度。值得注意的是，要计算覆盖距离 **i** 的步数，只需要最后三个状态(**I–1，I–2，I–3**)。因此，可以使用最后三种状态来计算结果。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the count of the
// total number of ways to cover the
// distance with 1, 2 and 3 steps
int countWays(int n)
{
    // Base conditions
    if (n == 0)
        return 1;
    if (n <= 2)
        return n;

    // To store the last three stages
    int f0 = 1, f1 = 1, f2 = 2, ans;

    // Find the numbers of steps required
    // to reach the distance i
    for (int i = 3; i <= n; i++) {
        ans = f0 + f1 + f2;
        f0 = f1;
        f1 = f2;
        f2 = ans;
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int n = 4;

    cout << countWays(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to return the count of the
// total number of ways to cover the
// distance with 1, 2 and 3 steps
static int countWays(int n)
{
    // Base conditions
    if (n == 0)
        return 1;
    if (n <= 2)
        return n;

    // To store the last three stages
    int f0 = 1, f1 = 1, f2 = 2;
    int ans=0;

    // Find the numbers of steps required
    // to reach the distance i
    for (int i = 3; i <= n; i++)
    {
        ans = f0 + f1 + f2;
        f0 = f1;
        f1 = f2;
        f2 = ans;
    }

    // Return the required answer
    return ans;
}

// Driver code
public static void main (String[] args)
{

    int n = 4;
    System.out.println (countWays(n));
}
}

// This code is contributed by jit_t
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return the count of the
# total number of ways to cover the
# distance with 1, 2 and 3 steps
def countWays(n):

    # Base conditions
    if (n == 0):
        return 1
    if (n <= 2):
        return n

    # To store the last three stages
    f0 = 1
    f1 = 1
    f2 = 2
    ans = 0

    # Find the numbers of steps required
    # to reach the distance i
    for i in range(3, n + 1):
        ans = f0 + f1 + f2
        f0 = f1
        f1 = f2
        f2 = ans

    # Return the required answer
    return ans

# Driver code
n = 4

print(countWays(n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of the
// total number of ways to cover the
// distance with 1, 2 and 3 steps
static int countWays(int n)
{
    // Base conditions
    if (n == 0)
        return 1;
    if (n <= 2)
        return n;

    // To store the last three stages
    int f0 = 1, f1 = 1, f2 = 2;
    int ans = 0;

    // Find the numbers of steps required
    // to reach the distance i
    for (int i = 3; i <= n; i++)
    {
        ans = f0 + f1 + f2;
        f0 = f1;
        f1 = f2;
        f2 = ans;
    }

    // Return the required answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int n = 4;
    Console.WriteLine (countWays(n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the count of the
    // total number of ways to cover the
    // distance with 1, 2 and 3 steps
    function countWays(n)
    {
        // Base conditions
        if (n == 0)
            return 1;
        if (n <= 2)
            return n;

        // To store the last three stages
        let f0 = 1, f1 = 1, f2 = 2;
        let ans = 0;

        // Find the numbers of steps required
        // to reach the distance i
        for (let i = 3; i <= n; i++)
        {
            ans = f0 + f1 + f2;
            f0 = f1;
            f1 = f2;
            f2 = ans;
        }

        // Return the required answer
        return ans;
    }

    let n = 4;
    document.write(countWays(n));

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
7
```

**时间复杂度:**O(N)
T3】空间复杂度 O(1)