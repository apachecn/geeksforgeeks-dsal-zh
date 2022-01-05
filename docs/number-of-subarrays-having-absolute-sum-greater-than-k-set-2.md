# 绝对和大于 K 的子阵数量|集合-2

> 原文:[https://www . geeksforgeeks . org/子阵数量-具有大于 k 的绝对和-set-2/](https://www.geeksforgeeks.org/number-of-subarrays-having-absolute-sum-greater-than-k-set-2/)

给定一个长度为 **N** 的整数数组 **arr[]** ，由正整数和负整数组成，任务是找出和的绝对值大于给定正数 **K** 的子数组的个数。

**示例:**

> **输入:** arr[] = {-1，0，1}，K = 0
> **输出:** 4
> 所有可能的子阵列，并且有总和:
> {-1 } =-1
> { 0 } = 0
> { 1 } = 1
> {-1，0} = -1
> {0，1} = 1
> {-1，0，1} = 0
> 因此，4 个子阵列有绝对值
> 
> **输入:** arr[] = {2，3，4}，K = 4
> **输出:** 3

**方法:**这里[讨论了一个在正整数数组上工作的类似方法](https://www.geeksforgeeks.org/number-subarrays-sum-less-k/)。
在本文中，我们将研究一种算法，可以同时解决正整数和负整数的这个问题。

1.  创建给定数组的前缀和数组。
2.  对前缀和数组进行排序。
3.  创建变量 **ans** ，查找前缀和数组中值小于 **-K** 或大于 **K** 的元素个数，并用该值初始化 **ans** 。
4.  现在，迭代排序的前缀和数组，对于每个索引 **i** ，找到第一个元素的索引，其值大于 **arr[i] + K** 。假设这个指数是 **j** 。

那么 ans 可以更新为**ans+= N–j**，因为前缀和数组中的元素数量大于 **arr[i]+K** 的值将等于**N–j**。
要找到索引 **j** ，对前缀和数组进行二进制搜索。具体来说，在**前缀-和[i] + k** 的值上找到[上限](https://www.geeksforgeeks.org/lower-and-upper-bound-theory/)。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
#define maxLen 30
using namespace std;

// Function to find required value
int findCnt(int arr[], int n, int k)
{
    // Variable to store final answer
    int ans = 0;

    // Loop to find prefix-sum
    for (int i = 1; i < n; i++) {
        arr[i] += arr[i - 1];
        if (arr[i] > k or arr[i] < -1 * k)
            ans++;
    }

    if (arr[0] > k || arr[0] < -1 * k)
        ans++;

    // Sorting prefix-sum array
    sort(arr, arr + n);

    // Loop to find upper_bound
    // for each element
    for (int i = 0; i < n; i++)
        ans += n -
       (upper_bound(arr, arr + n, arr[i] + k) - arr);

    // Returning final answer
    return ans;
}

// Driver code
int main()
{
    int arr[] = { -1, 4, -5, 6 };
    int n = sizeof(arr) / sizeof(int);
    int k = 0;

    // Function to find required value
    cout << findCnt(arr, n, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int maxLen = 30;

// Function to find required value
static int findCnt(int arr[], int n, int k)
{
    // Variable to store final answer
    int ans = 0;

    // Loop to find prefix-sum
    for (int i = 1; i < n; i++)
    {
        arr[i] += arr[i - 1];
        if (arr[i] > k || arr[i] < -1 * k)
            ans++;
    }

    if (arr[0] > k || arr[0] < -1 * k)
        ans++;

    // Sorting prefix-sum array
    Arrays.sort(arr);

    // Loop to find upper_bound
    // for each element
    for (int i = 0; i < n; i++)
        ans += n - upper_bound(arr, 0, n, arr[i] + k);

    // Returning final answer
    return ans;
}

static int upper_bound(int[] a, int low,
                    int high, int element)
{
    while(low < high)
    {
        int middle = low + (high - low)/2;
        if(a[middle] > element)
            high = middle;
        else
            low = middle + 1;
    }
    return low;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { -1, 4, -5, 6 };
    int n = arr.length;
    int k = 0;

    // Function to find required value
    System.out.println(findCnt(arr, n, k));
}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to find required value
    static int findCnt(int []arr, int n, int k)
    {
        // Variable to store final answer
        int ans = 0;

        // Loop to find prefix-sum
        for (int i = 1; i < n; i++)
        {
            arr[i] += arr[i - 1];
            if (arr[i] > k || arr[i] < -1 * k)
                ans++;
        }

        if (arr[0] > k || arr[0] < -1 * k)
            ans++;

        // Sorting prefix-sum array
        Array.Sort(arr);

        // Loop to find upper_bound
        // for each element
        for (int i = 0; i < n; i++)
            ans += n - upper_bound(arr, 0, n, arr[i] + k);

        // Returning final answer
        return ans;
    }

    static int upper_bound(int[] a, int low,
                        int high, int element)
    {
        while(low < high)
        {
            int middle = low + (high - low)/2;
            if(a[middle] > element)
                high = middle;
            else
                low = middle + 1;
        }
        return low;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { -1, 4, -5, 6 };
        int n = arr.Length;
        int k = 0;

        // Function to find required value
        Console.WriteLine(findCnt(arr, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
from bisect import bisect as upper_bound

maxLen=30

# Function to find required value
def findCnt(arr, n, k):

    # Variable to store final answer
    ans = 0

    # Loop to find prefix-sum
    for i in range(1,n):
        arr[i] += arr[i - 1]
        if (arr[i] > k or arr[i] < -1 * k):
            ans+=1

    if (arr[0] > k or arr[0] < -1 * k):
        ans+=1

    # Sorting prefix-sum array
    arr=sorted(arr)

    # Loop to find upper_bound
    # for each element
    for i in range(n):
        ans += n - upper_bound(arr,arr[i] + k)

    # Returning final answer
    return ans

# Driver code

arr = [-1, 4, -5, 6]
n = len(arr)
k = 0

# Function to find required value
print(findCnt(arr, n, k))

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach
var maxLen = 30;

function upper_bound(a, low, high, element)
    {
        while(low < high)
        {
            var middle = low + parseInt((high - low)/2);
            if(a[middle] > element)
                high = middle;
            else
                low = middle + 1;
        }
        return low;
    }

// Function to find required value
function findCnt(arr, n, k)
{
    // Variable to store final answer
    var ans = 0;

    // Loop to find prefix-sum
    for (var i = 1; i < n; i++) {
        arr[i] += arr[i - 1];
        if (arr[i] > k || arr[i] < -1 * k)
            ans++;
    }

    if (arr[0] > k || arr[0] < -1 * k)
        ans++;

    // Sorting prefix-sum array
    arr.sort((a,b)=>a-b)

    // Loop to find upper_bound
    // for each element
    for (var i = 0; i < n; i++)
        ans += (n - upper_bound(arr, 0, n, arr[i] + k));

    // Returning final answer
    return ans;
}

// Driver code
var arr = [ -1, 4, -5, 6 ];
var n = arr.length;
var k = 0;
// Function to find required value
document.write( findCnt(arr, n, k));

</script>
```

**Output:** 

```
10
```

**时间复杂度:** O(Nlog(N))