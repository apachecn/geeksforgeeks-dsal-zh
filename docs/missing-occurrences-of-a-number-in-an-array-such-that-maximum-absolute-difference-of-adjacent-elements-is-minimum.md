# 一个数组中缺少一个数字，使得相邻元素的最大绝对差最小

> 原文:[https://www . geeksforgeeks . org/数组中缺少一个数字，因此相邻元素的最大绝对差值最小/](https://www.geeksforgeeks.org/missing-occurrences-of-a-number-in-an-array-such-that-maximum-absolute-difference-of-adjacent-elements-is-minimum/)

给定一些正整数的数组 **arr[]** ，并且缺少由-1 表示的特定整数的出现，任务是找到缺少的数，使得相邻元素之间的最大绝对差最小。
**例:**

> **输入:** arr[] = {-1，10，-1，12， -1}
> **输出:** 11
> **解释:**
> 相邻元素的差异–
> =>a[0]–a[1]= 11–10 = 1
> =>a[2]–a[1]= 11–10 = 1
> =>a[3]–a[2]= 12–11 = 1
> =>a[3]–a 5，2，-1，5}
> **输出:** 4
> **解释:**
> 相邻元素的差异–
> =>a[1]–a[0]= 4–1 = 3
> =>a[2]–a[1]= 7–4 = 3
> =>a[2]–a[3]= 7–5 = 2
> =>a[3]

**方法:**思想是找到与缺失数相邻的最大和最小元素，缺失数可以是这两个值的平均值，使得最大绝对差最小。

```
=> max = Maximum adjacent element
=> min = Minimum adjacent element

Missing number = (max + min)
                -------------
                      2
```

以下是上述方法的实现:

## C++

```
// C++ implementation of the missing
// number such that maximum absolute
// difference between adjacent element
// is minimum

#include <bits/stdc++.h>

using namespace std;

// Function to find the missing
// number such that maximum
// absolute difference is minimum
int missingnumber(int n, int arr[])
{
    int mn = INT_MAX, mx = INT_MIN;
    // Loop to find the maximum and
    // minimum adjacent element to
    // missing number
    for (int i = 0; i < n; i++) {

        if (i > 0 && arr[i] == -1 &&
                 arr[i - 1] != -1) {
            mn = min(mn, arr[i - 1]);
            mx = max(mx, arr[i - 1]);
        }

        if (i < (n - 1) && arr[i] == -1 &&
                       arr[i + 1] != -1) {
            mn = min(mn, arr[i + 1]);
            mx = max(mx, arr[i + 1]);
        }
    }

    long long int res = (mx + mn) / 2;
    return res;
}

// Driver Code
int main()
{
    int n = 5;
    int arr[5] = { -1, 10, -1,
                       12, -1 };
    int ans = 0;

    // Function Call
    int res = missingnumber(n, arr);
    cout << res;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the missing
// number such that maximum absolute
// difference between adjacent element
// is minimum
import java.util.*;
class GFG{

// Function to find the missing
// number such that maximum
// absolute difference is minimum
static int missingnumber(int n, int arr[])
{
    int mn = Integer.MAX_VALUE,
        mx = Integer.MIN_VALUE;

    // Loop to find the maximum and
    // minimum adjacent element to
    // missing number
    for (int i = 0; i < n; i++)
    {
        if (i > 0 && arr[i] == -1 &&
                     arr[i - 1] != -1)
        {
            mn = Math.min(mn, arr[i - 1]);
            mx = Math.max(mx, arr[i - 1]);
        }

        if (i < (n - 1) && arr[i] == -1 &&
                           arr[i + 1] != -1)
        {
            mn = Math.min(mn, arr[i + 1]);
            mx = Math.max(mx, arr[i + 1]);
        }
    }

    int res = (mx + mn) / 2;
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;
    int arr[] = { -1, 10, -1,
                    12, -1 };

    // Function Call
    int res = missingnumber(n, arr);
    System.out.print(res);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the missing
# number such that maximum absolute
# difference between adjacent element
# is minimum
import sys

# Function to find the missing
# number such that maximum
# absolute difference is minimum
def missingnumber(n, arr) -> int:

    mn = sys.maxsize;
    mx = -sys.maxsize - 1;

    # Loop to find the maximum and
    # minimum adjacent element to
    # missing number
    for i in range(n):
        if (i > 0 and arr[i] == -1 and
                      arr[i - 1] != -1):
            mn = min(mn, arr[i - 1]);
            mx = max(mx, arr[i - 1]);

        if (i < (n - 1) and arr[i] == -1 and
                            arr[i + 1] != -1):
            mn = min(mn, arr[i + 1]);
            mx = max(mx, arr[i + 1]);

    res = (mx + mn) / 2;

    return res;

# Driver Code
if __name__ == '__main__':

    n = 5;
    arr = [ -1, 10, -1, 12, -1 ];

    # Function call
    res = missingnumber(n, arr);
    print(res);

# This code is contributed by amal kumar choubey
```

## C#

```
// C# implementation of the missing
// number such that maximum absolute
// difference between adjacent element
// is minimum
using System;
class GFG{

// Function to find the missing
// number such that maximum
// absolute difference is minimum
static int missingnumber(int n, int []arr)
{
    int mn = Int32.MaxValue,
        mx = Int32.MinValue;

    // Loop to find the maximum and
    // minimum adjacent element to
    // missing number
    for (int i = 0; i < n; i++)
    {
        if (i > 0 && arr[i] == -1 &&
                     arr[i - 1] != -1)
        {
            mn = Math.Min(mn, arr[i - 1]);
            mx = Math.Max(mx, arr[i - 1]);
        }

        if (i < (n - 1) && arr[i] == -1 &&
                           arr[i + 1] != -1)
        {
            mn = Math.Min(mn, arr[i + 1]);
            mx = Math.Max(mx, arr[i + 1]);
        }
    }

    int res = (mx + mn) / 2;
    return res;
}

// Driver Code
public static void Main()
{
    int n = 5;
    int []arr = new int[]{ -1, 10, -1, 12, -1 };

    // Function Call
    int res = missingnumber(n, arr);
    Console.WriteLine(res);
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>

// JavaScript implementation of the missing
// number such that maximum absolute
// difference between adjacent element
// is minimum

// Function to find the missing
// number such that maximum
// absolute difference is minimum
function missingnumber(n, arr)
{
    let mn = 10000;
    let mx = -10000;

    // Loop to find the maximum and
    // minimum adjacent element to
    // missing number
    for (let i = 0; i < n; i++)
    {
        if (i > 0 && arr[i] == -1 && arr[i - 1] != -1)
        {
            mn = Math.min(mn, arr[i - 1]);
            mx = Math.max(mx, arr[i - 1]);
        }

        if (i < (n - 1) && arr[i] == -1 &&
                        arr[i + 1] != -1)
        {
            mn = Math.min(mn, arr[i + 1]);
            mx = Math.max(mx, arr[i + 1]);
        }
    }

    let res = (mx + mn) / 2;
    return res;
}

// Driver Code

let n = 5;
let arr = [-1, 10, -1, 12, -1];

// Function Call
let res = missingnumber(n, arr);

document.write(res);

</script>
```

**Output:** 

```
11
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)