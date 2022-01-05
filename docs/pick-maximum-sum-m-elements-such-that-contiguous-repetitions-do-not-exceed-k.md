# 选择 M 个元素的最大和，使得连续重复不超过 K

> 原文:[https://www . geesforgeks . org/pick-maximum-sum-m-elements-so-to-contined-repeats-do-not-over-k/](https://www.geeksforgeeks.org/pick-maximum-sum-m-elements-such-that-contiguous-repetitions-do-not-exceed-k/)

给定不同元素和两个整数的数组**arr[]****M**和 **K** ，任务是从给定的数组元素(元素可以在生成的数组中重复)生成数组，使得生成的数组的大小为 **M** ，并且具有所有相同元素的任何子数组的长度不得超过 **K** 。打印所有可能生成的数组中元素的最大总和。
**举例:**

> **输入:** arr[] = {1，3，6，7，4，5}，M = 9，K = 2
> **输出:** 60
> 最大和排列是 7 7 6 7 6 7 7 7 6 7 6。请注意，没有大小超过 2 的子阵列包含所有相同的元素。
> **输入:** arr[] = {8，13，9，17，4，12}，M = 5，K = 1
> **输出:** 77
> 最大和排列为 17，13，17，13，17

**方法:**如果我们想要最大和，我们必须从数组中获取**最大值**值，但是我们最多可以重复这个最大值 K 次，所以我们必须用**第二个最大值**值将其分开一次，然后我们再次获取第一个最大值，直到 K 次，这个循环一直持续到我们获取总的 **M** 值。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum required sum
long int maxSum(int arr[], int n, int m, int k)
{

    int max1 = -1, max2 = -1;

    // All the elements in the array are distinct
    // Finding the maximum and the second maximum
    // element from the array
    for (int i = 0; i < n; i++) {
        if (arr[i] > max1) {
            max2 = max1;
            max1 = arr[i];
        }
        else if (arr[i] > max2)
            max2 = arr[i];
    }

    // Total times the second maximum element
    // will appear in the generated array
    int counter = m / (k + 1);

    long int sum = counter * max2 + (m - counter) * max1;

    // Return the required sum
    return sum;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 6, 7, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int m = 9, k = 2;
    cout << maxSum(arr, n, m, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the maximum required sum
static int maxSum(int arr[], int n, int m, int k)
{

    int max1 = -1, max2 = -1;

    // All the elements in the array are distinct
    // Finding the maximum and the second maximum
    // element from the array
    for (int i = 0; i < n; i++)
    {
        if (arr[i] > max1)
        {
            max2 = max1;
            max1 = arr[i];
        }
        else if (arr[i] > max2)
            max2 = arr[i];
    }

    // Total times the second maximum element
    // will appear in the generated array
    int counter = m / (k + 1);

    int sum = counter * max2 + (m - counter) * max1;

    // Return the required sum
    return sum;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 3, 6, 7, 4, 5 };
    int n = arr.length;
    int m = 9, k = 2;
    System.out.println(maxSum(arr, n, m, k));
}
}

// This code is contributed by
// Surendra Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
def maxSum(arr, n, m, k):

    max1 = -1
    max2 = -1

    # All the elements in the array are distinct
    # Finding the maximum and the second maximum
    # element from the array
    for i in range(0, n):
        if(arr[i] > max1):
            max2 = max1
            max1 = arr[i]
        elif(arr[i] > max2):
            max2 = arr[i]

    # Total times the second maximum element
    # will appear in the generated array
    counter = int(m / (k + 1))

    sum = counter * max2 + (m - counter) * max1

    # Return the required sum
    return int(sum)

# Driver code
arr = [1, 3, 6, 7, 4, 5]
n = len(arr)
m = 9
k = 2

print(maxSum(arr, n, m, k))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum required sum
static int maxSum(int []arr, int n, int m, int k)
{

    int max1 = -1, max2 = -1;

    // All the elements in the array are distinct
    // Finding the maximum and the second maximum
    // element from the array
    for (int i = 0; i < n; i++)
    {
        if (arr[i] > max1)
        {
            max2 = max1;
            max1 = arr[i];
        }
        else if (arr[i] > max2)
            max2 = arr[i];
    }

    // Total times the second maximum element
    // will appear in the generated array
    int counter = m / (k + 1);

    int sum = counter * max2 + (m - counter) * max1;

    // Return the required sum
    return sum;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 3, 6, 7, 4, 5 };
    int n = arr.Length;
    int m = 9, k = 2;
    Console.WriteLine(maxSum(arr, n, m, k));
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the maximum required sum
function maxSum(arr, n, m, k)
{

    var max1 = -1, max2 = -1;

    // All the elements in the array are distinct
    // Finding the maximum and the second maximum
    // element from the array
    for (var i = 0; i < n; i++) {
        if (arr[i] > max1) {
            max2 = max1;
            max1 = arr[i];
        }
        else if (arr[i] > max2)
            max2 = arr[i];
    }

    // Total times the second maximum element
    // will appear in the generated array
    var counter = m / (k + 1);

    var sum = counter * max2 + (m - counter) * max1;

    // Return the required sum
    return sum;
}

// Driver code
var arr = [1, 3, 6, 7, 4, 5];
var n = arr.length;
var m = 9, k = 2;
document.write( maxSum(arr, n, m, k));

</script>
```

**Output:** 

```
60
```