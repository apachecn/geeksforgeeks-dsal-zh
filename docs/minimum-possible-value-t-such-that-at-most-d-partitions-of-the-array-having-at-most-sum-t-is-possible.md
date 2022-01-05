# 最小可能值 T，使得最多 D 个具有最多和 T 的数组分区是可能的

> 原文:[https://www . geesforgeks . org/最小可能值-t-这样最多 d 个分区的阵列最多有 t 个可能的总和/](https://www.geeksforgeeks.org/minimum-possible-value-t-such-that-at-most-d-partitions-of-the-array-having-at-most-sum-t-is-possible/)

给定一个由 **N** 整数和一个整数 **D** 组成的数组**arr【】**，任务是找到最小的整数 **T** ，这样整个数组最多可以从给定的数组中分割成 **D** 个子数组，并且有总和 **T** 。

**示例:**

> **输入:** D = 5，arr[] = {1，2，3，4，5，6，7，8，9，10}
> **输出:** 15
> **解释:**
> 如果 T = 15，那么 5 个子阵列{{1，2，3，4，5}，{6，7}，{8}，{9}，{10}
> 
> **输入:** D = 2，arr[] = {1，1，1，1}
> **输出:** 3
> **解释:**
> 如果 T = 3，那么这 2 个分区为{{1，1，1}，{1，1}}

**天真法:**思路是检查 **T** 在**【max(元素)、sum(元素)】**范围内所有可能的值是否最多可以有 D 个分区。

***时间复杂度:** O( N*R )*
***辅助空间:** O(1)*

**高效途径:**思路是利用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)对上述途径进行优化。按照以下步骤解决问题:

*   考虑 **R =【最大(元素)，和(元素)】**范围内的 **T** 。
*   如果中位数 **T** 最多只能生成 **D** 分区，那么检查中位数是否小于 **T** 。
*   否则，检查中间值是否大于当前中间值 **T** 。
*   最后返回 **T** 的可能值。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the array
// can be partitioned into atmost d
// subarray with sum atmost T
bool possible(int T, int arr[], int n, int d)
{
    // Initial partition
    int partition = 1;

    // Current sum
    int total = 0;

    for (int i = 0; i < n; i++) {

        total = total + arr[i];

        // If current sum exceeds T
        if (total > T) {

            // Create a new partition
            partition = partition + 1;
            total = arr[i];

            // If count of partitions
            // exceed d
            if (partition > d) {
                return false;
            }
        }
    }

    return true;
}

// Function to find the minimum
// possible value of T
void calcT(int n, int d, int arr[])
{
    // Stores the maximum and
    // total sum of elements
    int mx = -1, sum = 0;

    for (int i = 0; i < n; i++) {

        // Maximum element
        mx = max(mx, arr[i]);

        // Sum of all elements
        sum = sum + arr[i];
    }

    int lb = mx;
    int ub = sum;

    while (lb < ub) {

        // Calculate median  T
        int T_mid = lb + (ub - lb) / 2;

        // If atmost D partitions possible
        if (possible(T_mid, arr, n, d) == true) {

            // Check for smaller T
            ub = T_mid;
        }

        // Otherwise
        else {

            // Check for larger T
            lb = T_mid + 1;
        }
    }

    // Print the minimum T required
    cout << lb << endl;
}

// Driver Code
int main()
{
    int d = 2;
    int arr[] = { 1, 1, 1, 1, 1 };

    int n = sizeof arr / sizeof arr[0];
    // Function call
    calcT(n, d, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.io.*;

class GFG{

// Function to check if the array
// can be partitioned into atmost d
// subarray with sum atmost T
public static boolean possible(int T, int arr[],
                               int n, int d)
{

    // Initial partition
    int partition = 1;

    // Current sum
    int total = 0;

    for(int i = 0; i < n; i++)
    {
        total = total + arr[i];

        // If current sum exceeds T
        if (total > T)
        {

            // Create a new partition
            partition = partition + 1;
            total = arr[i];

            // If count of partitions
            // exceed d
            if (partition > d)
            {
                return false;
            }
        }
    }
    return true;
}

// Function to find the minimum
// possible value of T
public static void calcT(int n, int d,
                         int arr[])
{

    // Stores the maximum and
    // total sum of elements
    int mx = -1, sum = 0;

    for(int i = 0; i < n; i++)
    {

        // Maximum element
        mx = Math.max(mx, arr[i]);

        // Sum of all elements
        sum = sum + arr[i];
    }

    int lb = mx;
    int ub = sum;

    while (lb < ub)
    {

        // Calculate median T
        int T_mid = lb + (ub - lb) / 2;

        // If atmost D partitions possible
        if (possible(T_mid, arr, n, d) == true)
        {

            // Check for smaller T
            ub = T_mid;
        }

        // Otherwise
        else
        {

            // Check for larger T
            lb = T_mid + 1;
        }
    }

    // Print the minimum T required
    System.out.println(lb);
}

// Driver code
public static void main(String args[])
{
    int d = 2;
    int arr[] = { 1, 1, 1, 1, 1 };

    int n = arr.length;

    // Function call
    calcT(n, d, arr);
}
}

// This code is contributed by decoding
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the array
# can be partitioned into atmost d
# subarray with sum atmost T
def possible(T, arr, n, d):

    # Initial partition
    partition = 1;

    # Current sum
    total = 0;

    for i in range(n):
        total = total + arr[i];

        # If current sum exceeds T
        if (total > T):

            # Create a new partition
            partition = partition + 1;
            total = arr[i];

            # If count of partitions
            # exceed d
            if (partition > d):
                return False;

    return True;

# Function to find the minimum
# possible value of T
def calcT(n, d, arr):

    # Stores the maximum and
    # total sum of elements
    mx = -1; sum = 0;

    for i in range(n):

        # Maximum element
        mx = max(mx, arr[i]);

        # Sum of all elements
        sum = sum + arr[i];

    lb = mx;
    ub = sum;

    while (lb < ub):

        # Calculate median T
        T_mid = lb + (ub - lb) // 2;

        # If atmost D partitions possible
        if (possible(T_mid, arr, n, d) == True):

            # Check for smaller T
            ub = T_mid;

        # Otherwise
        else:

            # Check for larger T
            lb = T_mid + 1;

    # Print the minimum T required
    print(lb);

# Driver code
if __name__ == '__main__':

    d = 2;
    arr = [ 1, 1, 1, 1, 1 ];

    n = len(arr);

    # Function call
    calcT(n, d, arr);

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the array
// can be partitioned into atmost d
// subarray with sum atmost T
public static bool possible(int T, int []arr,
                            int n, int d)
{

    // Initial partition
    int partition = 1;

    // Current sum
    int total = 0;

    for(int i = 0; i < n; i++)
    {
        total = total + arr[i];

        // If current sum exceeds T
        if (total > T)
        {

            // Create a new partition
            partition = partition + 1;
            total = arr[i];

            // If count of partitions
            // exceed d
            if (partition > d)
            {
                return false;
            }
        }
    }
    return true;
}

// Function to find the minimum
// possible value of T
public static void calcT(int n, int d,
                         int []arr)
{

    // Stores the maximum and
    // total sum of elements
    int mx = -1, sum = 0;

    for(int i = 0; i < n; i++)
    {

        // Maximum element
        mx = Math.Max(mx, arr[i]);

        // Sum of all elements
        sum = sum + arr[i];
    }

    int lb = mx;
    int ub = sum;

    while (lb < ub)
    {

        // Calculate median T
        int T_mid = lb + (ub - lb) / 2;

        // If atmost D partitions possible
        if (possible(T_mid, arr, n, d) == true)
        {

            // Check for smaller T
            ub = T_mid;
        }

        // Otherwise
        else
        {

            // Check for larger T
            lb = T_mid + 1;
        }
    }

    // Print the minimum T required
    Console.WriteLine(lb);
}

// Driver code
public static void Main(String []args)
{
    int d = 2;
    int []arr = { 1, 1, 1, 1, 1 };

    int n = arr.Length;

    // Function call
    calcT(n, d, arr);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JavaScript program for the
// above approach

// Function to check if the array
// can be partitioned into atmost d
// subarray with sum atmost T
function possible(T, arr,
                               n, d)
{

    // Initial partition
    let partition = 1;

    // Current sum
    let total = 0;

    for(let i = 0; i < n; i++)
    {
        total = total + arr[i];

        // If current sum exceeds T
        if (total > T)
        {

            // Create a new partition
            partition = partition + 1;
            total = arr[i];

            // If count of partitions
            // exceed d
            if (partition > d)
            {
                return false;
            }
        }
    }
    return true;
}

// Function to find the minimum
// possible value of T
function calcT(n, d, arr)
{

    // Stores the maximum and
    // total sum of elements
    let mx = -1, sum = 0;

    for(let i = 0; i < n; i++)
    {

        // Maximum element
        mx = Math.max(mx, arr[i]);

        // Sum of all elements
        sum = sum + arr[i];
    }

    let lb = mx;
    let ub = sum;

    while (lb < ub)
    {

        // Calculate median T
        let T_mid = lb + (ub - lb) / 2;

        // If atmost D partitions possible
        if (possible(T_mid, arr, n, d) == true)
        {

            // Check for smaller T
            ub = T_mid;
        }

        // Otherwise
        else
        {

            // Check for larger T
            lb = T_mid + 1;
        }
    }

    // Print the minimum T required
    document.write(lb);
}

// Driver Code

    let d = 2;
    let arr = [ 1, 1, 1, 1, 1 ];

    let n = arr.length;

    // Function call
    calcT(n, d, arr);

</script>
```

**Output**

```
3
```

***时间复杂度:**O(N * log(sum))*
***辅助空间:** O(1)*