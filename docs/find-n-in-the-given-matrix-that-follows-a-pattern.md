# 在给定的矩阵中找到 N，该矩阵遵循一个模式

> 原文:[https://www . geeksforgeeks . org/find-n-in-the-给定矩阵-遵循-a-pattern/](https://www.geeksforgeeks.org/find-n-in-the-given-matrix-that-follows-a-pattern/)

给定一个充满自然数的无限矩阵，如下所示:

```
1 2 4 7 . . .
3 5 8 . . . .
6 9 . . . . .
10  . . . . .
. . . . . . .
```

另外，给定一个整数 **N** ，任务是在给定的矩阵中找到整数 **N** 的行和列。
**例:**

```
Input: N = 5
Output: 2 2
5 is present in the 2nd row 
and the 2nd column.

Input: N = 3
Output: 2 1
```

**方法:**仔细观察问题，先从 **N** 中减去 **x** 个自然数，使其满足条件**N –( x *(x+1))/2≥1**即可得到行号，所得值即为所需行号。
要得到对应的列，先将 **x** 自然数加到 **1** 上，使其满足条件 **1 + (y * (y + 1)) / 2 ≤ A** 。从 **N** 中减去该合成值，得到基底与给定值之间的间隙，再从 **y + 1** 中减去该间隙。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the row and
// the column of the given integer
pair<int, int> solve(int n)
{

    int low = 1, high = 1e4, x = n, p = 0;

    // Binary search for the row number
    while (low <= high) {
        int mid = (low + high) / 2;
        int sum = (mid * (mid + 1)) / 2;

        // Condition to get the maximum
        // x that satisfies the criteria
        if (x - sum >= 1) {
            p = mid;
            low = mid + 1;
        }
        else {
            high = mid - 1;
        }
    }

    int start = 1, end = 1e4, y = 1, q = 0;

    // Binary search for the column number
    while (start <= end) {
        int mid = (start + end) / 2;
        int sum = (mid * (mid + 1)) / 2;

        // Condition to get the maximum
        // y that satisfies the criteria
        if (y + sum <= n) {
            q = mid;
            start = mid + 1;
        }
        else {
            end = mid - 1;
        }
    }

    // Get the row and the column number
    x = x - (p * (p + 1)) / 2;
    y = y + (q * (q + 1)) / 2;
    int r = x;
    int c = q + 1 - n + y;

    // Return the pair
    pair<int, int> ans = { r, c };
    return ans;
}

// Driver code
int main()
{
    int n = 5;

    pair<int, int> p = solve(n);
    cout << p.first << " " << p.second;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the row and
    // the column of the given integer
    static int[] solve(int n)
    {
        int low = 1, high = (int)1e4, x = n, p = 0;

        // Binary search for the row number
        while (low <= high)
        {
            int mid = (low + high) / 2;
            int sum = (mid * (mid + 1)) / 2;

            // Condition to get the maximum
            // x that satisfies the criteria
            if (x - sum >= 1)
            {
                p = mid;
                low = mid + 1;
            }
            else
            {
                high = mid - 1;
            }
        }

        int start = 1, end = (int)1e4, y = 1, q = 0;

        // Binary search for the column number
        while (start <= end)
        {
            int mid = (start + end) / 2;
            int sum = (mid * (mid + 1)) / 2;

            // Condition to get the maximum
            // y that satisfies the criteria
            if (y + sum <= n)
            {
                q = mid;
                start = mid + 1;
            }
            else
            {
                end = mid - 1;
            }
        }

        // Get the row and the column number
        x = x - (p * (p + 1)) / 2;
        y = y + (q * (q + 1)) / 2;
        int r = x;
        int c = q + 1 - n + y;

        // Return the pair
        int ans[] = { r, c };
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 5;

        int []p = solve(n);
        System.out.println(p[0] + " " + p[1]);

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the row and
# the column of the given integer
def solve(n):

    low = 1
    high = 10**4
    x, p = n, 0

    # Binary search for the row number
    while (low <= high):
        mid = (low + high) // 2
        sum = (mid * (mid + 1)) // 2

        # Condition to get the maximum
        # x that satisfies the criteria
        if (x - sum >= 1):
            p = mid
            low = mid + 1
        else :
            high = mid - 1

    start, end, y, q = 1, 10**4, 1, 0

    # Binary search for the column number
    while (start <= end):
        mid = (start + end) // 2
        sum = (mid * (mid + 1)) // 2

        # Condition to get the maximum
        # y that satisfies the criteria
        if (y + sum <= n):
            q = mid
            start = mid + 1
        else:
            end = mid - 1

    # Get the row and the column number
    x = x - (p * (p + 1)) // 2
    y = y + (q * (q + 1)) // 2
    r = x
    c = q + 1 - n + y

    # Return the pair
    return r, c

# Driver code
n = 5

r, c = solve(n)
print(r, c)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the row and
    // the column of the given integer
    static int[] solve(int n)
    {
        int low = 1, high = (int)1e4, x = n, p = 0;

        // Binary search for the row number
        while (low <= high)
        {
            int mid = (low + high) / 2;
            int sum = (mid * (mid + 1)) / 2;

            // Condition to get the maximum
            // x that satisfies the criteria
            if (x - sum >= 1)
            {
                p = mid;
                low = mid + 1;
            }
            else
            {
                high = mid - 1;
            }
        }

        int start = 1, end = (int)1e4, y = 1, q = 0;

        // Binary search for the column number
        while (start <= end)
        {
            int mid = (start + end) / 2;
            int sum = (mid * (mid + 1)) / 2;

            // Condition to get the maximum
            // y that satisfies the criteria
            if (y + sum <= n)
            {
                q = mid;
                start = mid + 1;
            }
            else
            {
                end = mid - 1;
            }
        }

        // Get the row and the column number
        x = x - (p * (p + 1)) / 2;
        y = y + (q * (q + 1)) / 2;
        int r = x;
        int c = q + 1 - n + y;

        // Return the pair
        int []ans = {r, c};
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 5;

        int []p = solve(n);
        Console.WriteLine(p[0] + " " + p[1]);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the row and
    // the column of the given integer
function solve(n)
{
    let low = 1, high = 1e4, x = n, p = 0;

        // Binary search for the row number
        while (low <= high)
        {
            let mid = Math.floor((low + high) / 2);
            let sum = Math.floor((mid * (mid + 1)) / 2);

            // Condition to get the maximum
            // x that satisfies the criteria
            if (x - sum >= 1)
            {
                p = mid;
                low = mid + 1;
            }
            else
            {
                high = mid - 1;
            }
        }

        let start = 1, end = 1e4, y = 1, q = 0;

        // Binary search for the column number
        while (start <= end)
        {
            let mid = Math.floor((start + end) / 2);
            let sum = Math.floor((mid * (mid + 1)) / 2);

            // Condition to get the maximum
            // y that satisfies the criteria
            if (y + sum <= n)
            {
                q = mid;
                start = mid + 1;
            }
            else
            {
                end = mid - 1;
            }
        }

        // Get the row and the column number
        x = x - Math.floor((p * (p + 1)) / 2);
        y = y + Math.floor((q * (q + 1)) / 2);
        let r = x;
        let c = q + 1 - n + y;

        // Return the pair
        let ans = [ r, c ];
        return ans;
}

// Driver code
let n = 5;
let p = solve(n);
document.write(p[0] + " " + p[1]);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
2 2
```

**时间复杂度:** O(log(N))