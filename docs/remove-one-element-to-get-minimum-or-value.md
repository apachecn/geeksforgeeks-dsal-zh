# 去掉一个元素得到最小或值

> 原文:[https://www . geesforgeks . org/remove-一个元素获取最小值或最大值/](https://www.geeksforgeeks.org/remove-one-element-to-get-minimum-or-value/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是从数组中移除一个元素，使得数组的或值最小。打印最小值。

**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 3
> 删除一个元素及其对应的
> OR 值的所有可能方式将是:
> a)删除 1 - > (2 | 3) = 3
> b)删除 2 - > (1 | 3) = 3
> c)删除 3 - > (1 | 2) = 3
> 这样，答案将是 3。
> **输入:** arr[] = {2，2，2}
> **输出:** 2

**天真的方法:**一种方法是逐个移除每个元素，然后找到剩余元素的 OR。这种方法的时间复杂度为 0(N<sup>2</sup>)。

**高效的方法:**为了高效地解决问题，**(OR(arr[0…I-1])| OR(arr[I+1…N-1])**的值必须为任意元素 **arr[i]** 确定。为此，可以计算前缀和后缀或数组，如 **pre[]** 和 **suf[]** ，其中 **pre[i]** 存储 **OR(arr[0…i])** 和**suf[I]**存储 **OR(arr[i…N-1])** 。那么删除 **i <sup>th</sup>** 元素后数组的 OR 值可以计算为**(pre[I-1]| suf[I+1])**，答案将是所有可能的 OR 值中的最小值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimized OR
// after removing an element from the array
int minOR(int* arr, int n)
{
    // Base case
    if (n == 1)
        return 0;

    // Prefix and suffix OR array
    int pre[n], suf[n];
    pre[0] = arr[0], suf[n - 1] = arr[n - 1];

    // Computing prefix/suffix OR arrays
    for (int i = 1; i < n; i++)
        pre[i] = (pre[i - 1] | arr[i]);
    for (int i = n - 2; i >= 0; i--)
        suf[i] = (suf[i + 1] | arr[i]);

    // To store the final answer
    int ans = min(pre[n - 2], suf[1]);

    // Finding the final answer
    for (int i = 1; i < n - 1; i++)
        ans = min(ans, (pre[i - 1] | suf[i + 1]));

    // Returning the final answer
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3 };
    int n = sizeof(arr) / sizeof(int);

    cout << minOR(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimized OR
// after removing an element from the array
static int minOR(int []arr, int n)
{
    // Base case
    if (n == 1)
        return 0;

    // Prefix and suffix OR array
    int []pre = new int[n];
    int []suf = new int[n];
    pre[0] = arr[0];
    suf[n - 1] = arr[n - 1];

    // Computing prefix/suffix OR arrays
    for (int i = 1; i < n; i++)
        pre[i] = (pre[i - 1] | arr[i]);
    for (int i = n - 2; i >= 0; i--)
        suf[i] = (suf[i + 1] | arr[i]);

    // To store the final answer
    int ans = Math.min(pre[n - 2], suf[1]);

    // Finding the final answer
    for (int i = 1; i < n - 1; i++)
        ans = Math.min(ans, (pre[i - 1] |
                             suf[i + 1]));

    // Returning the final answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3 };
    int n = arr.length;

    System.out.print(minOR(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimized OR
# after removing an element from the array
def minOR(arr, n):

    # Base case
    if (n == 1):
        return 0

    # Prefix and suffix OR array
    pre = [0] * n
    suf = [0] * n
    pre[0] = arr[0]
    suf[n - 1] = arr[n - 1]

    # Computing prefix/suffix OR arrays
    for i in range(1, n):
        pre[i] = (pre[i - 1] | arr[i])
    for i in range(n - 2, -1, -1):
        suf[i] = (suf[i + 1] | arr[i])

    # To store the final answer
    ans = min(pre[n - 2], suf[1])

    # Finding the final answer
    for i in range(1, n - 1):
        ans = min(ans, (pre[i - 1] | suf[i + 1]))

    # Returning the final answer
    return ans

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3]
    n = len(arr)

    print(minOR(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimized OR
    // after removing an element from the array
    static int minOR(int []arr, int n)
    {
        // Base case
        if (n == 1)
            return 0;

        // Prefix and suffix OR array
        int []pre = new int[n];
        int []suf = new int[n];

        pre[0] = arr[0];
        suf[n - 1] = arr[n - 1];

        // Computing prefix/suffix OR arrays
        for (int i = 1; i < n; i++)
            pre[i] = (pre[i - 1] | arr[i]);

        for (int i = n - 2; i >= 0; i--)
            suf[i] = (suf[i + 1] | arr[i]);

        // To store the final answer
        int ans = Math.Min(pre[n - 2], suf[1]);

        // Finding the final answer
        for (int i = 1; i < n - 1; i++)
            ans = Math.Min(ans, (pre[i - 1] |
                                 suf[i + 1]));

        // Returning the final answer
        return ans;
    }

    // Driver code
    static public void Main ()
    {
        int []arr = { 1, 2, 3 };
        int n = arr.Length;

        Console.WriteLine(minOR(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimized OR
// after removing an element from the array
function minOR(arr, n)
{
    // Base case
    if (n == 1)
        return 0;

    // Prefix and suffix OR array
    var pre = Array(n), suf = Array(n);
    pre[0] = arr[0], suf[n - 1] = arr[n - 1];

    // Computing prefix/suffix OR arrays
    for (var i = 1; i < n; i++)
        pre[i] = (pre[i - 1] | arr[i]);
    for (var i = n - 2; i >= 0; i--)
        suf[i] = (suf[i + 1] | arr[i]);

    // To store the final answer
    var ans = Math.min(pre[n - 2], suf[1]);

    // Finding the final answer
    for (var i = 1; i < n - 1; i++)
        ans = Math.min(ans, (pre[i - 1] | suf[i + 1]));

    // Returning the final answer
    return ans;
}

// Driver code
var arr = [1, 2, 3];
var n = arr.length;
document.write( minOR(arr, n));

</script>
```

**Output:** 

```
3
```