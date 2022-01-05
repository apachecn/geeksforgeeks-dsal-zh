# 通过将每一步乘以 2、3、4 或 5 从 1 到 N 的最小步数

> 原文:[https://www . geeksforgeeks . org/每一步乘以 2-3-4 或-5 得出的最小步骤数/](https://www.geeksforgeeks.org/minimum-steps-to-reach-n-from-1-by-multiplying-each-step-by-2-3-4-or-5/)

给定一个整数 **N** ，任务是通过将每一步乘以 2、3、4 或 5，从 1 中找到达到数字 **N** 的最小步数。如果无法到达 N，打印-1。
**例:**

> **输入:** N = 10
> **输出:** 2
> **说明:**
> 初始数= 1
> 第一步:乘以 2，当前数= 2
> 第二步:乘以 5，当前数= 10
> 因此，达到 10 至少需要 2 步。
> **输入:** N = 13
> **输出:** -1
> **解释:**
> 使用任何给定的操作都无法到达 13

**方法:**思路是用[贪婪算法](https://www.geeksforgeeks.org/greedy-approach-vs-dynamic-programming/)选择每一步应该执行的操作，并以相反的方式执行操作，即不是从 1 到 N，而是找到达到 N 到 1 所需的操作。以下是步骤说明:

*   应用以下操作，直到 N 大于 1。
*   检查 N 是否能被 5 整除，然后将步长增加 1，并将 N 减少到 N/5
*   否则，检查 N 是否能被 4 整除，然后将步长增加 1，并将 N 减少到 N/4
*   否则，检查 N 是否能被 3 整除，然后将步长增加 1，并将 N 减少到 N/3
*   否则，检查 N 是否能被 2 整除，然后将步长增加 1，并将 N 减少到 N/2
*   如果在任何步骤都不能应用任何操作，那么就没有可能的操作集从 1 到达 N。因此，返回-1。

以下是上述方法的实现:

## C++

```
// C++ implementation to find
// minimum number of steps
// to reach N from 1

#include <bits/stdc++.h>

using namespace std;

// Function to find a minimum number
// of steps to reach N from 1
int Minsteps(int n)
{
    int ans = 0;

    // Check until N is greater
    // than 1 and operations
    // can be applied
    while (n > 1) {

        // Condition to choose the
        // operations greedily
        if (n % 5 == 0) {

            ans++;
            n = n / 5;
            continue;
        }
        else if (n % 4 == 0) {
            ans++;
            n = n / 4;
            continue;
        }
        else if (n % 3 == 0) {
            ans++;
            n = n / 3;
            continue;
        }
        else if (n % 2 == 0) {
            ans++;
            n = n / 2;
            continue;
        }
        return -1;
    }
    return ans;
}

// Driver code
int main()
{
    int n = 10;
    cout << Minsteps(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// minimum number of steps
// to reach N from 1

import java.util.*;

class GFG{

// Function to find a minimum number
// of steps to reach N from 1
static int Minsteps(int n)
{
    int ans = 0;

    // Check until N is greater
    // than 1 and operations
    // can be applied
    while (n > 1)
    {

        // Condition to choose the
        // operations greedily
        if (n % 5 == 0)
        {
            ans++;
            n = n / 5;
            continue;
        }
        else if (n % 4 == 0)
        {
            ans++;
            n = n / 4;
            continue;
        }
        else if (n % 3 == 0)
        {
            ans++;
            n = n / 3;
            continue;
        }
        else if (n % 2 == 0)
        {
            ans++;
            n = n / 2;
            continue;
        }
        return -1;
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int n = 10;
    System.out.print(Minsteps(n));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation to find
# minimum number of steps
# to reach N from 1

# Function to find a minimum number
# of steps to reach N from 1
def Minsteps(n):

    ans = 0

    # Check until N is greater
    # than 1 and operations
    # can be applied
    while (n > 1):

        # Condition to choose the
        # operations greedily
        if (n % 5 == 0):
            ans = ans + 1
            n = n / 5
            continue

        elif (n % 4 == 0):
            ans = ans + 1
            n = n / 4
            continue

        elif (n % 3 == 0):
            ans = ans + 1
            n = n / 3
            continue

        elif (n % 2 == 0):
            ans = ans + 1
            n = n / 2
            continue

        return -1

    return ans

# Driver code
n = 10
print(Minsteps(n))

# This code is contributed by Pratik
```

## C#

```
// C# implementation to find
// minimum number of steps
// to reach N from 1
using System;

class GFG{

// Function to find a minimum number
// of steps to reach N from 1
static int Minsteps(int n)
{
    int ans = 0;

    // Check until N is greater
    // than 1 and operations
    // can be applied
    while (n > 1)
    {

        // Condition to choose the
        // operations greedily
        if (n % 5 == 0)
        {
            ans++;
            n = n / 5;
            continue;
        }
        else if (n % 4 == 0)
        {
            ans++;
            n = n / 4;
            continue;
        }
        else if (n % 3 == 0)
        {
            ans++;
            n = n / 3;
            continue;
        }
        else if (n % 2 == 0)
        {
            ans++;
            n = n / 2;
            continue;
        }
        return -1;
    }
    return ans;
}

// Driver code
public static void Main()
{
    int n = 10;
    Console.Write(Minsteps(n));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation to find
// minimum number of steps
// to reach N from 1

// Function to find a minimum number
// of steps to reach N from 1
function Minsteps(n)
{
    var ans = 0;

    // Check until N is greater
    // than 1 and operations
    // can be applied
    while (n > 1)
    {

        // Condition to choose the
        // operations greedily
        if (n % 5 == 0)
        {
            ans++;
            n = n / 5;
            continue;
        }
        else if (n % 4 == 0)
        {
            ans++;
            n = n / 4;
            continue;
        }
        else if (n % 3 == 0)
        {
            ans++;
            n = n / 3;
            continue;
        }
        else if (n % 2 == 0)
        {
            ans++;
            n = n / 2;
            continue;
        }
        return -1;
    }
    return ans;
}

// Driver code
var n = 10;

// Function Call
document.write(Minsteps(n));

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
2
```

时间复杂度:0(对数 n)

辅助空间:0(1)