# GCD 等于 1 的子阵数量

> 原文:[https://www . geeksforgeeks . org/子阵数量-带有-gcd-等于-1/](https://www.geeksforgeeks.org/number-of-subarrays-with-gcd-equal-to-1/)

给定一个数组 **arr[]** ，任务是找到子数组的数量，其中 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 值等于 **1** 。

**示例:**

> **输入:** arr[] = {1，1，1}
> **输出:** 6
> 给定阵列
> 的所有子阵列的 GCD 将等于 1。
> **输入:** arr[] = {2，2，2}
> **输出:** 0

**方法:**关键的观察是，如果子阵列 **arr[l…r]** 的所有元素的 GCD 是已知的，那么子阵列 **arr[l…r+1]** 的所有元素的 GCD 可以通过简单地用 **arr[r + 1]** 取前一个子阵列的 GCD 来获得。
因此，对于每个索引 **i** ，继续向前迭代，计算从索引 **i** 到 **j** 的 GCD，并检查它是否等于 **1** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required count
int cntSubArr(int* arr, int n)
{
    // To store the final answer
    int ans = 0;

    for (int i = 0; i < n; i++) {

        // To store the GCD starting from
        // index 'i'
        int curr_gcd = 0;

        // Loop to find the gcd of each subarray
        // from arr[i] to arr[i...n-1]
        for (int j = i; j < n; j++) {
            curr_gcd = __gcd(curr_gcd, arr[j]);

            // Increment the count if curr_gcd = 1
            ans += (curr_gcd == 1);
        }
    }

    // Return the final answer
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 1 };
    int n = sizeof(arr) / sizeof(int);

    cout << cntSubArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the required count
static int cntSubArr(int []arr, int n)
{
    // To store the final answer
    int ans = 0;

    for (int i = 0; i < n; i++)
    {

        // To store the GCD starting from
        // index 'i'
        int curr_gcd = 0;

        // Loop to find the gcd of each subarray
        // from arr[i] to arr[i...n-1]
        for (int j = i; j < n; j++)
        {
            curr_gcd = __gcd(curr_gcd, arr[j]);

            // Increment the count if curr_gcd = 1
            ans += (curr_gcd == 1) ? 1 : 0;
        }
    }

    // Return the final answer
    return ans;
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);    
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 1, 1, 1 };
    int n = arr.length;

    System.out.println(cntSubArr(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd

# Function to return the required count
def cntSubArr(arr, n) :

    # To store the final answer
    ans = 0;

    for i in range(n) :

        # To store the GCD starting from
        # index 'i'
        curr_gcd = 0;

        # Loop to find the gcd of each subarray
        # from arr[i] to arr[i...n-1]
        for j in range(i, n) :
            curr_gcd = gcd(curr_gcd, arr[j]);

            # Increment the count if curr_gcd = 1
            ans += (curr_gcd == 1);

    # Return the final answer
    return ans;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 1, 1 ];
    n = len(arr);

    print(cntSubArr(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the required count
static int cntSubArr(int []arr, int n)
{
    // To store the final answer
    int ans = 0;

    for (int i = 0; i < n; i++)
    {

        // To store the GCD starting from
        // index 'i'
        int curr_gcd = 0;

        // Loop to find the gcd of each subarray
        // from arr[i] to arr[i...n-1]
        for (int j = i; j < n; j++)
        {
            curr_gcd = __gcd(curr_gcd, arr[j]);

            // Increment the count if curr_gcd = 1
            ans += (curr_gcd == 1) ? 1 : 0;
        }
    }

    // Return the final answer
    return ans;
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);    
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 1, 1 };
    int n = arr.Length;

    Console.WriteLine(cntSubArr(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

function __gcd(a, b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);    
}

// Function to return the required count
function cntSubArr(arr, n)
{
    // To store the final answer
    var ans = 0;

    for (var i = 0; i < n; i++) {

        // To store the GCD starting from
        // index 'i'
        var curr_gcd = 0;

        // Loop to find the gcd of each subarray
        // from arr[i] to arr[i...n-1]
        for (var j = i; j < n; j++) {
            curr_gcd = __gcd(curr_gcd, arr[j]);

            // Increment the count if curr_gcd = 1
            ans += (curr_gcd == 1);
        }
    }

    // Return the final answer
    return ans;
}

// Driver code
var arr = [1, 1, 1];
var n = arr.length;
document.write( cntSubArr(arr, n));

</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(N <sup>2</sup> )