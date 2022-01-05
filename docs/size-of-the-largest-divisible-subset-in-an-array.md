# 数组中最大可分子集的大小

> 原文:[https://www . geesforgeks . org/最大可分数组子集大小/](https://www.geeksforgeeks.org/size-of-the-largest-divisible-subset-in-an-array/)

给定一个大小为 **N** 的数组 **arr[]** 。任务是从给定的数组中找到这组数字的大小，这样每个数字都可以除以另一个数字或者被另一个数字整除。

**示例:**

> **输入:** arr[] = {3，4，6，8，10，18，21，24}
> **输出:** 3
> 最大大小的可能集合之一是{3，6，18}
> 
> **输入:** arr[] = {2，3，4，8，16 }
> T3】输出: 4

**进场:**

1.  让我们把所有的数字按升序排列。
2.  注意设置 **X = x <sub>i</sub> ，…，？x <sub>k</sub> }** 可接受如果 **x <sub>i</sub>** 将 **x <sub>i+1</sub>** 除以**(1≤I≤k–1)**。
3.  因此， **dp[x]** 等于从数字 **x** 开始的最长合适的递增子序列的长度。
4.  差压关系:**差压[x] =最大值(差压[x]，1 +差压[y])** 如果 **x** 除 **y** 。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

#define N 1000005

// Function to find the size of the
//largest divisible subarray
int maximum_set(int a[], int n)
{
    int dp[N] = { 0 };

    // Mark all elements of the array
    for (int i = 0; i < n; i++)
        dp[a[i]] = 1;

    int ans = 1;

    // Traverse reverse
    for (int i = N - 1; i >= 1; i--) {

        if (dp[i] != 0) {
            // For all multiples of i
            for (int j = 2 * i; j < N; j += i) {
                dp[i] = max(dp[i], 1 + dp[j]);
                ans = max(ans, dp[i]);
            }
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 3, 4, 6, 8, 10, 18, 21, 24 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << maximum_set(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    final static int N = 1000005 ;

    // Function to find the size of the
    //largest divisible subarray
    static int maximum_set(int a[], int n)
    {
        int dp[] = new int[N] ;

        // Mark all elements of the array
        for (int i = 0; i < n; i++)
            dp[a[i]] = 1;

        int ans = 1;

        // Traverse reverse
        for (int i = N - 1; i >= 1; i--)
        {

            if (dp[i] != 0)
            {
                // For all multiples of i
                for (int j = 2 * i; j < N; j += i)
                {
                    dp[i] = Math.max(dp[i], 1 + dp[j]);
                    ans = Math.max(ans, dp[i]);
                }
            }
        }

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 3, 4, 6, 8, 10, 18, 21, 24 };

        int n = arr.length;

        // Function call
        System.out.println(maximum_set(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python3 implementation of the above approach

N = 1000005

# Function to find the size of the
# largest divisible subarray
def maximum_set(a, n):
    dp = [0 for i in range(N)]

    # Mark all elements of the array
    for i in a:
        dp[i] = 1

    ans = 1

    # Traverse reverse
    for i in range(N - 1, 0, -1):

        if (dp[i] != 0):

            # For all multiples of i
            for j in range(2 * i, N, i):
                dp[i] = max(dp[i], 1 + dp[j])
                ans = max(ans, dp[i])

    # Return the required answer
    return ans

# Driver code

arr = [3, 4, 6, 8, 10, 18, 21, 24]

n = len(arr)

# Function call
print(maximum_set(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    static int N = 1000005 ;

    // Function to find the size of the
    //largest divisible subarray
    static int maximum_set(int []a, int n)
    {
        int []dp = new int[N] ;

        // Mark all elements of the array
        for (int i = 0; i < n; i++)
            dp[a[i]] = 1;

        int ans = 1;

        // Traverse reverse
        for (int i = N - 1; i >= 1; i--)
        {

            if (dp[i] != 0)
            {
                // For all multiples of i
                for (int j = 2 * i; j < N; j += i)
                {
                    dp[i] = Math.Max(dp[i], 1 + dp[j]);
                    ans = Math.Max(ans, dp[i]);
                }
            }
        }

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 3, 4, 6, 8, 10, 18, 21, 24 };
        int n = arr.Length;

        // Function call
        Console.WriteLine(maximum_set(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

let N = 1000005

// Function to find the size of the
//largest divisible subarray
function maximum_set(a, n) {
    let dp = new Array(N).fill(0);

    // Mark all elements of the array
    for (let i = 0; i < n; i++)
        dp[a[i]] = 1;

    let ans = 1;

    // Traverse reverse
    for (let i = N - 1; i >= 1; i--) {

        if (dp[i] != 0) {
            // For all multiples of i
            for (let j = 2 * i; j < N; j += i) {
                dp[i] = Math.max(dp[i], 1 + dp[j]);
                ans = Math.max(ans, dp[i]);
            }
        }
    }

    // Return the required answer
    return ans;
}

// Driver code

let arr = [3, 4, 6, 8, 10, 18, 21, 24];

let n = arr.length;

// Function call
document.write(maximum_set(arr, n));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(n*sqrt(n))