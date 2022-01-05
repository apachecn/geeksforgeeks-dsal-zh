# 绝对差之和最小的数组元素

> 原文:[https://www . geesforgeks . org/带有最小绝对差和的数组元素/](https://www.geeksforgeeks.org/array-element-with-minimum-sum-of-absolute-differences/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是从数组中找到一个元素 **x** ，使得**| arr[0]–x |+| arr[1]–x |+| arr[2]–x |+…+| arr[N–1]–x |**最小化，然后打印最小化的和。
**举例:**

> **输入:** arr[] = {1，3，9，3，6}
> **输出:** 11
> 最优解是选择 x = 3，这样就产生了和
> | 1–3 |+| 3–3 |+| 9–3 |+| 3–3 |+| 6–3 | = 2+0+6+0+3 = 11
> **输入:** arr[] = {1，2，3，4}
> 【T11

一个**简单的解决方案**是迭代每个元素，检查它是否给出最优解。这个解决方案的时间复杂度是 O(n*n)
一个**有效的方法:**总是选择 **x** 作为数组的中值。如果 **n 为偶数**，有**两个中位**，那么两个中位都是最优选择。该方法的时间复杂度为 **O(n * log(n))** ，因为为了找到中间值，必须对数组进行排序。当找到 x(数组的中间值)时，计算并打印最小和。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimized sum
int minSum(int arr[], int n)
{
    // Sort the array
    sort(arr, arr + n);

    // Median of the array
    int x = arr[n / 2];

    int sum = 0;

    // Calculate the minimized sum
    for (int i = 0; i < n; i++)
        sum += abs(arr[i] - x);

    // Return the required sum
    return sum;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 9, 3, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the minimized sum
static int minSum(int arr[], int n)
{
    // Sort the array
    Arrays.sort(arr);

    // Median of the array
    int x = arr[(int)n / 2];

    int sum = 0;

    // Calculate the minimized sum
    for (int i = 0; i < n; i++)
        sum += Math.abs(arr[i] - x);

    // Return the required sum
    return sum;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 3, 9, 3, 6 };
    int n = arr.length;
    System.out.println(minSum(arr, n));
}
}

// This code is contribute by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimized sum
def minSum(arr, n) :

    # Sort the array
    arr.sort();

    # Median of the array
    x = arr[n // 2];

    sum = 0;

    # Calculate the minimized sum
    for i in range(n) :
        sum += abs(arr[i] - x);

    # Return the required sum
    return sum;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 3, 9, 3, 6 ];
    n = len(arr)
    print(minSum(arr, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimized sum
static int minSum(int []arr, int n)
{
    // Sort the array
    Array.Sort(arr);

    // Median of the array
    int x = arr[(int)(n / 2)];

    int sum = 0;

    // Calculate the minimized sum
    for (int i = 0; i < n; i++)
        sum += Math.Abs(arr[i] - x);

    // Return the required sum
    return sum;
}

// Driver code
static void Main()
{
    int []arr = { 1, 3, 9, 3, 6 };
    int n = arr.Length;
    Console.WriteLine(minSum(arr, n));
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>

//Javascript implementation of the approach

// Function to return the minimized sum
function minSum(arr, n)
{
    // Sort the array
    arr.sort();

    // Median of the array
    let x = arr[Math.floor(n / 2)];

    let sum = 0;

    // Calculate the minimized sum
    for (let i = 0; i < n; i++)
        sum += Math.abs(arr[i] - x);

    // Return the required sum
    return sum;
}

// Driver code
    let arr = [ 1, 3, 9, 3, 6 ];
    let n = arr.length;
    document.write(minSum(arr, n));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
11
```

上述解决方案的时间复杂度为 O(n Log n)。我们可以利用[线性时间算法找到第 k 大元素](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)，进一步优化使其工作在 O(n)中。