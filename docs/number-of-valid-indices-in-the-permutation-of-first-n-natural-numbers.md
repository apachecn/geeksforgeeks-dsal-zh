# 前 N 个自然数排列中有效指数的个数

> 原文:[https://www . geeksforgeeks . org/第一个 n 个自然数排列中的有效索引数/](https://www.geeksforgeeks.org/number-of-valid-indices-in-the-permutation-of-first-n-natural-numbers/)

给定第一个 **N** 自然数的排列 **P** 。任务是找到第一个 **N** 自然数排列中所有 **1 ≤ j ≤ i** 的 **i 的**数，使得**P<sub>I</sub>≤P<sub>j</sub>T11】。
**举例:**** 

> **输入:** arr[] = {4，2，5，1，3}
> **输出:** 3
> 0，1，3 就是这样的指数。
> **输入:** arr[] = {4，3，2，1}
> **输出:** 4

**方法:**对于 **i = 1，…，N** ，定义 **M <sub>i</sub> = min{ P <sub>j</sub> ，1 ≤ j ≤ i}** 。现在，当 **i(1 ≤ i ≤ N)** 固定时，**M<sub>I</sub>= P<sub>I</sub>**成立当且仅当对于所有 **j(1 ≤ j ≤ i)，P <sub>i</sub> ≤ P <sub>j</sub>** 成立。因此，计算所有的 **M <sub>i</sub>** 就足够了。这些可以按照 **i** 的递增顺序计算，所以问题总共可以在 **O(N)** 时间内解决。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of i's
// such that Pi <= Pj for all 1 <= j <= i
// in the permutation of first N natural numbers
int min_index(int p[], int n)
{

    // To store the count of such indices
    int ans = 0;

    // Store the mini value
    int mini = INT_MAX;

    // For all the elements
    for (int i = 0; i < n; i++) {
        if (p[i] <= mini)
            mini = p[i];

        if (mini == p[i])
            ans++;
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int P[] = { 4, 2, 5, 1, 3 };
    int n = sizeof(P) / sizeof(int);

    cout << min_index(P, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    static int INT_MAX = Integer.MAX_VALUE;

    // Function to return the number of i's
    // such that Pi <= Pj for all 1 <= j <= i
    // in the permutation of first N natural numbers
    static int min_index(int p[], int n)
    {

        // To store the count of such indices
        int ans = 0;

        // Store the mini value
        int mini = INT_MAX;

        // For all the elements
        for (int i = 0; i < n; i++)
        {
            if (p[i] <= mini)
                mini = p[i];

            if (mini == p[i])
                ans++;
        }

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int P[] = { 4, 2, 5, 1, 3 };
        int n = P.length;

        System.out.println(min_index(P, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

INT_MAX = sys.maxsize

# Function to return the number of i's
# such that Pi <= Pj for all 1 <= j <= i
# in the permutation of first N natural numbers
def min_index(p, n) :

    # To store the count of such indices
    ans = 0;

    # Store the mini value
    mini = INT_MAX;

    # For all the elements
    for i in range(n) :
        if (p[i] <= mini) :
            mini = p[i];

        if (mini == p[i]) :
            ans += 1;

    # Return the required answer
    return ans;

# Driver code
if __name__ == "__main__" :

    P = [ 4, 2, 5, 1, 3 ];
    n = len(P);
    print(min_index(P, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int INT_MAX = int.MaxValue;

    // Function to return the number of i's
    // such that Pi <= Pj for all 1 <= j <= i
    // in the permutation of first N natural numbers
    static int min_index(int []p, int n)
    {

        // To store the count of such indices
        int ans = 0;

        // Store the mini value
        int mini = INT_MAX;

        // For all the elements
        for (int i = 0; i < n; i++)
        {
            if (p[i] <= mini)
                mini = p[i];

            if (mini == p[i])
                ans++;
        }

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void Main ()
    {
        int []P = { 4, 2, 5, 1, 3 };
        int n = P.Length;

        Console.WriteLine(min_index(P, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the number of i's
// such that Pi <= Pj for all 1 <= j <= i
// in the permutation of first N natural numbers
function min_index(p, n)
{

    // To store the count of such indices
    let ans = 0;

    // Store the mini value
    let mini = Number.MAX_SAFE_INTEGER;

    // For all the elements
    for (let i = 0; i < n; i++) {
        if (p[i] <= mini)
            mini = p[i];

        if (mini == p[i])
            ans++;
    }

    // Return the required answer
    return ans;
}

// Driver code

    let P = [ 4, 2, 5, 1, 3 ];
    let n = P.length;

    document.write(min_index(P, n));

// This code is contributed by Manoj.

</script>
```

**Output:** 

```
3
```