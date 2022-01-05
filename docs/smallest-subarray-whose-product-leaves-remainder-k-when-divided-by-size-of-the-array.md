# 最小子阵列，其乘积除以阵列大小后剩下余数 K

> 原文:[https://www . geesforgeks . org/minist-subarray-then-product-leaks-余数-k-当除以数组大小/](https://www.geeksforgeeks.org/smallest-subarray-whose-product-leaves-remainder-k-when-divided-by-size-of-the-array/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出最小子阵列的长度，该子阵列的乘积除以 **N** 得到余数 **K** 。如果不存在这样的子阵列，打印**-1”**。

**示例:**

> **输入:** N = 3，arr = {2，2，6}，K = 1
> **输出:** 2
> **解释:**
> 所有可能的子阵为:
> { 2 }->2(mod 3)= 2
> { 2 }->2(mod 3)= 2
> { 6 }->6(mod 3)= 0
> { 2，2} - >
> 因此，最小子阵列的长度为 2。
> 
> **输入:** N = 4，arr = {2，2，3，3}，K = 1
> **输出:** 2
> **说明:**
> 只有子阵{3，3}满足性质，因此最小子阵的长度为 2。

**方法:**
想法是[生成给定阵列的所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)并打印最小子阵列的长度，当除以 **N** 时，其所有元素的乘积给出余数 **K** 。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the subarray of
// minimum length
int findsubArray(int arr[], int N, int K)
{

    // Initialize the minimum
    // subarray size to N + 1
    int res = N + 1;

    // Generate all possible subarray
    for (int i = 0; i < N; i++) {

        // Initialize the product
        int curr_prod = 1;

        for (int j = i; j < N; j++) {

            // Find the product
            curr_prod = curr_prod * arr[j];

            if (curr_prod % N == K
                && res > (j - i + 1)) {

                res = min(res, j - i + 1);
                break;
            }
        }
    }

    // Return the minimum size of subarray
    return (res == N + 1) ? 0 : res;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 2, 2, 3 };

    int N = sizeof(arr)
            / sizeof(arr[0]);

    int K = 1;

    int answer = findsubArray(arr, N, K);

    if (answer != 0)
        cout << answer;
    else
        cout << "-1";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// above approach
import java.util.*;

class GFG{

// Function to find the subarray of
// minimum length
static int findsubArray(int arr[],
                        int N, int K)
{

    // Initialize the minimum
    // subarray size to N + 1
    int res = N + 1;

    // Generate all possible subarray
    for(int i = 0; i < N; i++)
    {

        // Initialize the product
        int curr_prod = 1;

        for(int j = i; j < N; j++)
        {

            // Find the product
            curr_prod = curr_prod * arr[j];

            if (curr_prod % N == K &&
                 res > (j - i + 1))
            {
                res = Math.min(res, j - i + 1);
                break;
            }
        }
    }

    // Return the minimum size of subarray
    return (res == N + 1) ? 0 : res;
}

// Driver code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 2, 2, 3 };

    int N = arr.length;
    int K = 1;

    int answer = findsubArray(arr, N, K);

    if (answer != 0)
        System.out.println(answer);
    else
        System.out.println("-1");
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the subarray of
# minimum length
def findsubArray(arr, N, K):

    # Initialize the minimum
    # subarray size to N + 1
    res = N + 1

    # Generate all possible subarray
    for i in range(0, N):

        # Initialize the product
        curr_prad = 1

        for j in range(i, N):

            # Find the product
            curr_prad = curr_prad * arr[j]

            if (curr_prad % N == K and
                res > (j - i + 1)):
                res = min(res, j - i + 1)
                break

    # Return the minimum size of subarray
    if res == N + 1:
        return 0
    else:
        return res

# Driver code
if __name__ == '__main__':

    # Given array
    arr = [ 2, 2, 3 ]
    N = len(arr)
    K = 1

    answer = findsubArray(arr, N, K)

    if (answer != 0):
        print(answer)
    else:
        print(-1)

# This code is contributed by virusbuddah_
```

## C#

```
// C# program to implement the
// above approach
using System;

class GFG{

// Function to find the subarray of
// minimum length
static int findsubArray(int []arr,
                        int N, int K)
{

    // Initialize the minimum
    // subarray size to N + 1
    int res = N + 1;

    // Generate all possible subarray
    for(int i = 0; i < N; i++)
    {

        // Initialize the product
        int curr_prod = 1;

        for(int j = i; j < N; j++)
        {

            // Find the product
            curr_prod = curr_prod * arr[j];

            if (curr_prod % N == K &&
                res > (j - i + 1))
            {
                res = Math.Min(res, j - i + 1);
                break;
            }
        }
    }

    // Return the minimum size of subarray
    return (res == N + 1) ? 0 : res;
}

// Driver code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 2, 2, 3 };

    int N = arr.Length;
    int K = 1;

    int answer = findsubArray(arr, N, K);

    if (answer != 0)
        Console.WriteLine(answer);
    else
        Console.WriteLine("-1");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program to implement the
// above approach

// Function to find the subarray of
// minimum length
function findsubArray(arr, N, K)
{

    // Initialize the minimum
    // subarray size to N + 1
    var res = N + 1;

    // Generate all possible subarray
    for(i = 0; i < N; i++)
    {

        // Initialize the product
        var curr_prod = 1;

        for(j = i; j < N; j++)
        {

            // Find the product
            curr_prod = curr_prod * arr[j];

            if (curr_prod % N == K &&
                 res > (j - i + 1))
            {
                res = Math.min(res, j - i + 1);
                break;
            }
        }
    }

    // Return the minimum size of subarray
    return (res == N + 1) ? 0 : res;
}

// Driver code

// Given array
var arr = [ 2, 2, 3 ];

var N = arr.length;
var K = 1;

var answer = findsubArray(arr, N, K);

if (answer != 0)
    document.write(answer);
else
    document.write("-1");

// This code is contributed by umadevi9616

</script>
```

**输出:**

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*