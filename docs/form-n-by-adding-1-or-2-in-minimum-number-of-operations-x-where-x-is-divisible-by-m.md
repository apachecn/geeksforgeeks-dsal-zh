# 在最小运算次数 X 中加 1 或 2 形成 N，其中 X 可被 M 整除

> 原文:[https://www . geesforgeks . org/form-n-by-add-1-or-2-in-最小操作数-x-其中-x-可被-m 除尽/](https://www.geeksforgeeks.org/form-n-by-adding-1-or-2-in-minimum-number-of-operations-x-where-x-is-divisible-by-m/)

给定一个数 N，任务是通过在最小操作数 X 中加 1 或 2 形成 N(从 0 开始)，使得 X 可被 m 整除
**示例:**

> **输入:** N = 10，M = 2
> **输出:** X = 6
> **解释:**
> 采取的操作是 2 2 2 2 1 1
> X = 6 可被 2 整除
> **输入:** N = 17，M = 4
> **输出:** 12

**进场:**

*   因为我们一次可以走 1 步或 2 步，所以我们可以说最小步数为 n/2，最大步数为 n，而不管步数是否能被 m 整除。
*   所以我们必须数 n/2 步，才能得到最少的步数。如果 n 是偶数，那么最小步数将是 n/2，但是如果是奇数，那么它将是 n/2+1，而不考虑步数可被 m 整除。为了使最小步数为 m 的倍数，我们可以做 floor((minimum _ steps+m–1)/m)* m
*   同样，如果 n 小于 m，则不可能找到最小步数，在这种情况下，我们将返回-1。

以下是上述方法的实现:

## C++

```
// C++ program to find minimum
// number of steps to cover distance x

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum number of steps required
// total steps taken is divisible
// by m and only 1 or 2 steps can be taken at // a time
int minsteps(int n, int m)
{

    // If m > n ans is -1
    if (m > n) {
        return -1;
    }
    // else discussed above approach
    else {
        return ((n + 1) / 2 + m - 1) / m * m;
    }
}

// Driver code
int main()
{
    int n = 17, m = 4;
    int ans = minsteps(n, m);
    cout << ans << '\n';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// number of steps to cover distance x
class GFG
{

    // Function to calculate the
    // minimum number of steps required
    // total steps taken is divisible
    // by m and only 1 or 2 steps can be
    // taken at // a time
    static int minsteps(int n, int m)
    {

        // If m > n ans is -1
        if (m > n)
        {
            return -1;
        }

        // else discussed above approach
        else
        {
            return ((n + 1) / 2 + m - 1) / m * m;
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 17, m = 4;
        int ans = minsteps(n, m);
        System.out.println(ans);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find minimum
# number of steps to cover distance x

# Function to calculate the minimum number of
# steps required total steps taken is divisible
# by m and only 1 or 2 steps can be taken at a time
def minsteps(n, m):

    # If m > n ans is -1
    if (m > n):
        return -1

    # else discussed above approach
    else :
        return ((n + 1) // 2 + m - 1) // m * m;

# Driver code
n = 17
m = 4
ans = minsteps(n, m)
print(ans)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find minimum
// number of steps to cover distance x
using System;

class GFG
{

    // Function to calculate the
    // minimum number of steps required
    // total steps taken is divisible
    // by m and only 1 or 2 steps can be
    // taken at // a time
    static int minsteps(int n, int m)
    {

        // If m > n ans is -1
        if (m > n)
        {
            return -1;
        }

        // else discussed above approach
        else
        {
            return ((n + 1) / 2 + m - 1) / m * m;
        }
    }

    // Driver code
    public static void Main (String[] args)
    {
        int n = 17, m = 4;
        int ans = minsteps(n, m);
        Console.WriteLine(ans);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program to find minimum
// number of steps to cover distance x

// Function to calculate the
// minimum number of steps required
// total steps taken is divisible
// by m and only 1 or 2 steps can be
// taken at // a time
function minsteps(n , m)
{

    // If m > n ans is -1
    if (m > n)
    {
        return -1;
    }

    // else discussed above approach
    else
    {
        return ((n + 1) / 2 + m - 1) / m * m;
    }
}

// Driver code

var n = 17, m = 4;
var ans = minsteps(n, m);
document.write(ans);

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
12
```

**时间复杂度:** O(1)