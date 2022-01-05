# 在所有可能的对之间插入绝对差后计数非重复数组元素

> 原文:[https://www . geesforgeks . org/count-非重复-数组-元素-插入后-所有可能对之间的绝对差异/](https://www.geeksforgeeks.org/count-non-repeating-array-elements-after-inserting-absolute-difference-between-all-possible-pairs/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过重复插入给定数组的所有可能对之间的绝对差来最大化不同数组元素的数量。

**示例:**

> **输入:** arr[] = { 2，4，16 }
> **输出:** 9
> **解释:**
> 插入(arr[2]–arr[1])将 arr[]修改为{ 2，4，12，16 }
> 插入(arr[2]–arr[1])将 arr[]修改为{ 2，4，8，12，16 }
> 插入(arr[2]–arr[1])将 arr[]修改为{ 2，16 } 16 }
> insert(arr[6]–arr[0])将 arr[]修改为{ 2，4，6，8，10，12，14 16 }
> insert(arr[2]–arr[0])将 arr[]修改为{ 2，4，4 6，8，10，12，14 16 }
> insert(arr[2]–arr[1])将 arr[]修改为{ 0，2，4，4，6，8，10，12，14 16
> 
> **输入:** arr[] = { 3，6，5，4 }
> **输出:** 7

**天真法:**解决这个问题最简单的方法是从给定数组中反复选择一对，插入该对的绝对差。最后，检查数组中是否已经存在所有可能对的绝对差。如果发现为真，则将不同元素的计数打印到数组中。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效法:**思路是利用两个数的 GCD 可以通过重复从较大的数中减去较小的数，直到两个元素变得相等的事实。因此，将元素插入到数组中，使得所有相邻元素之间的绝对差必须等于数组的 GCD。按照以下步骤解决问题:

*   [找到阵中最大的元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)说出 **Max** 。
*   [找到阵](https://www.geeksforgeeks.org/gcd-two-array-numbers/)的 GCD，说 **GCDArr** 。
*   最后打印 **((Max / GCDArr) + 1)** 的值。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the gcd of
// the two numbers
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to find distinct elements in the array
// by repeatidely inserting the absolute difference
// of all possible pairs
int DistinctValues(int arr[], int N)
{

    // Stores largest element
    // of the array
    int max_value = INT_MIN;

    // Traverse the array, arr[]
    for (int i = 0; i < N; ++i) {

        // Update max_value
        max_value = max(max_value, arr[i]);
    }

    // Stores GCD of array
    int GCDArr = arr[0];

    // Traverse the array, arr[]
    for (int i = 1; i < N; ++i) {

        // Update GCDArr
        GCDArr = gcd(GCDArr, arr[i]);
    }

    // Stores distinct elements in the array by
    // repeatidely inserting absolute difference
    // of all possible pairs
    int answer = (max_value / GCDArr) + 1;

    return answer;
}

// Driver Code
int main()
{

    // Given array arr[]
    int arr[] = { 4, 12, 16, 24 };

    int N = sizeof(arr) / sizeof(int);

    cout << DistinctValues(arr, N);

    return 0;
}
// This code is contributed by hemanth gadarla
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;
class GFG
{

// Function to find the gcd of
// the two numbers
static int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to find distinct elements in the array
// by repeatidely inserting the absolute difference
// of all possible pairs
static int DistinctValues(int arr[], int N)
{

    // Stores largest element
    // of the array
    int max_value = Integer.MIN_VALUE;

    // Traverse the array, arr[]
    for (int i = 0; i < N; ++i)
    {

        // Update max_value
        max_value = Math.max(max_value, arr[i]);
    }

    // Stores GCD of array
    int GCDArr = arr[0];

    // Traverse the array, arr[]
    for (int i = 1; i < N; ++i)
    {

        // Update GCDArr
        GCDArr = gcd(GCDArr, arr[i]);
    }

    // Stores distinct elements in the array by
    // repeatidely inserting absolute difference
    // of all possible pairs
    int answer = (max_value / GCDArr) + 1;
    return answer;
}

// Driver code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 4, 12, 16, 24 };
    int N = arr.length;
    System.out.println(DistinctValues(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program of the above approach
import sys

# Function to find the gcd of
# the two numbers
def gcd(a, b):

    if a == 0:
        return b

    return gcd(b % a, a)

# Function to find distinct elements in
# the array by repeatidely inserting the
# absolute difference of all possible pairs
def DistinctValues(arr, N):

    # Stores largest element
    # of the array
    max_value = -sys.maxsize - 1

    # Update max_value
    max_value = max(arr)

    # Stores GCD of array
    GCDArr = arr[0]

    # Traverse the array, arr[]
    for i in range(1, N):

        # Update GCDArr
        GCDArr = gcd(GCDArr, arr[i])

     # Stores distinct elements in the array by
     # repeatedely inserting absolute difference
     # of all possible pairs
    answer = max_value // GCDArr

    return answer + 1

# Driver code

# Given array arr[]
arr = [ 4, 12, 16, 24 ]
N = len(arr)

print(DistinctValues(arr, N))

# This code is contributed by hemanth gadarla
```

## C#

```
// C# program of the above approach
using System;
class GFG
{

  // Function to find the gcd of
  // the two numbers
  static int gcd(int a, int b)
  {
    if (a == 0)
      return b;
    return gcd(b % a, a);
  }

  // Function to find distinct elements in the array
  // by repeatidely inserting the absolute difference
  // of all possible pairs
  static int DistinctValues(int[] arr, int N)
  {

    // Stores largest element
    // of the array
    int max_value = Int32.MinValue;

    // Traverse the array, arr[]
    for (int i = 0; i < N; ++i)
    {

      // Update max_value
      max_value = Math.Max(max_value, arr[i]);
    }

    // Stores GCD of array
    int GCDArr = arr[0];

    // Traverse the array, arr[]
    for (int i = 1; i < N; ++i)
    {

      // Update GCDArr
      GCDArr = gcd(GCDArr, arr[i]);
    }

    // Stores distinct elements in the array by
    // repeatidely inserting absolute difference
    // of all possible pairs
    int answer = (max_value / GCDArr) + 1;
    return answer;
  }

  // Driver code
  static void Main()
  {

    // Given array arr[]
    int[] arr = { 4, 12, 16, 24 };
    int N = arr.Length;
    Console.WriteLine(DistinctValues(arr, N));
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>
// javascript program of the above approach

    // Function to find the gcd of
    // the two numbers
    function gcd(a , b) {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Function to find distinct elements in the array
    // by repeatidely inserting the absolute difference
    // of all possible pairs
    function DistinctValues(arr , N) {

        // Stores largest element
        // of the array
        var max_value = Number.MIN_VALUE;

        // Traverse the array, arr
        for (i = 0; i < N; ++i) {

            // Update max_value
            max_value = Math.max(max_value, arr[i]);
        }

        // Stores GCD of array
        var GCDArr = arr[0];

        // Traverse the array, arr
        for (i = 1; i < N; ++i) {

            // Update GCDArr
            GCDArr = gcd(GCDArr, arr[i]);
        }

        // Stores distinct elements in the array by
        // repeatidely inserting absolute difference
        // of all possible pairs
        var answer = (max_value / GCDArr) + 1;
        return answer;
    }

    // Driver code

        // Given array arr
        var arr = [ 4, 12, 16, 24 ];
        var N = arr.length;
        document.write(DistinctValues(arr, N));

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(N * Min)，其中 Min 是数组中最小的元素*
***辅助空间:** O(1)*