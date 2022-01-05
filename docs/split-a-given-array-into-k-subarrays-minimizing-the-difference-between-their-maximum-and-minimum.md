# 将给定的阵列分割成 K 个子阵列，最小化它们的最大值和最小值之间的差异

> 原文:[https://www . geeksforgeeks . org/将给定数组拆分成 k 个子数组-最小化它们的最大值和最小值之差/](https://www.geeksforgeeks.org/split-a-given-array-into-k-subarrays-minimizing-the-difference-between-their-maximum-and-minimum/)

给定一个排序后的 **N** 整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个整数 **K** ，任务是将数组拆分为 **K** 子数组，使得每个子数组的最大和最小元素之差之和最小。

**示例:**

> **输入:** arr[] = {1，3，3，7}，K = 4
> **输出:** 0
> **解释:**
> 给定的阵列可以拆分为{1}、{3}、{3}和{7}四个子阵列。
> 每个子阵列的最小值和最大值之差为:
> 1。{1}，差值= 1–1 = 0
> 2。{3}，差值= 3–3 = 0
> 3。{3}，差值= 3–3 = 0
> 4。{7}，差值= 7–7 = 0
> 因此，所有差值之和为 0，最小化。
> 
> **输入:** arr[] = {4，8，15，16，23，42}，K = 3
> **输出:** 12
> **解释:**
> 给定的阵列可以拆分为{4，8，15，16}、{23}和{ 42 } 3 个子阵列。
> 每个子阵列的最小值和最大值之差为:
> 1。{4，8，15，16}，差= 16–4 = 12
> 2。{23}，差值= 23–23 = 0
> 3。{42}，差值= 42–42 = 0
> 因此，所有差值之和为 12，最小。

**方法:**要在给定条件下将给定数组拆分为 **K** 子数组，思路是在元素**arr【I+1】**和**arr【I】**之间差异最大的索引处(比如说 **i** 处)进行拆分。下面是实现这种方法的步骤:

1.  将给定数组中连续元素对之间的差异存储到另一个数组中(比如说 **temp[]** )。
2.  [按升序排列](https://www.geeksforgeeks.org/sorting-algorithms/)数组**温度[]** 。
3.  将总差值(比如 **diff** )初始化为给定数组的第一个和最后一个元素的差值 **arr[]** 。
4.  将数组**温度[]** 中的第一个**K–1**值加到上述差值上。
5.  存储在 **diff** 中的值是 **K** 子阵列的最大和最小元素之差的最小和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the subarray
int find(int a[], int n, int k)
{
    vector<int> v;

    // Add the difference to vectors
    for (int i = 1; i < n; ++i) {
        v.push_back(a[i - 1] - a[i]);
    }

    // Sort vector to find minimum k
    sort(v.begin(), v.end());

    // Initialize result
    int res = a[n - 1] - a[0];

    // Adding first k-1 values
    for (int i = 0; i < k - 1; ++i) {
        res += v[i];
    }

// Return the minimized sum
    return res;
}

// Driver Code
int main()
{
// Given array arr[]
    int arr[] = { 4, 8, 15, 16, 23, 42 };

    int N = sizeof(arr) / sizeof(int);

// Given K
int K = 3;

// Function Call
    cout << find(arr, N, K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the subarray
static int find(int a[], int n, int k)
{
    Vector<Integer> v = new Vector<Integer>();

    // Add the difference to vectors
    for(int i = 1; i < n; ++i)
    {
       v.add(a[i - 1] - a[i]);
    }

    // Sort vector to find minimum k
    Collections.sort(v);

    // Initialize result
    int res = a[n - 1] - a[0];

    // Adding first k-1 values
    for(int i = 0; i < k - 1; ++i)
    {
       res += v.get(i);
    }

    // Return the minimized sum
    return res;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 4, 8, 15, 16, 23, 42 };

    int N = arr.length;

    // Given K
    int K = 3;

    // Function Call
    System.out.print(find(arr, N, K) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the subarray
def find(a, n, k):

    v = []

    # Add the difference to vectors
    for i in range(1, n):
        v.append(a[i - 1] - a[i])

    # Sort vector to find minimum k
    v.sort()

    # Initialize result
    res = a[n - 1] - a[0]

    # Adding first k-1 values
    for i in range(k - 1):
        res += v[i]

    # Return the minimized sum
    return res

# Driver code
arr = [ 4, 8, 15, 16, 23, 42 ]

# Length of array
N = len(arr)

K = 3

# Function Call
print(find(arr, N, K))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the subarray
static int find(int []a, int n, int k)
{
    List<int> v = new List<int>();

    // Add the difference to vectors
    for(int i = 1; i < n; ++i)
    {
       v.Add(a[i - 1] - a[i]);
    }

    // Sort vector to find minimum k
    v.Sort();

    // Initialize result
    int res = a[n - 1] - a[0];

    // Adding first k-1 values
    for(int i = 0; i < k - 1; ++i)
    {
       res += v[i];
    }

    // Return the minimized sum
    return res;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 4, 8, 15, 16, 23, 42 };
    int N = arr.Length;

    // Given K
    int K = 3;

    // Function Call
    Console.Write(find(arr, N, K) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to find the subarray
    function find(a , n , k) {
        var v = [];

        // Add the difference to vectors
        for (i = 1; i < n; ++i) {
            v.push(a[i - 1] - a[i]);
        }

        // Sort vector to find minimum k
        v.sort((a,b)=>a-b);

        // Initialize result
        var res = a[n - 1] - a[0];

        // Adding first k-1 values
        for (i = 0; i < k - 1; ++i) {
            res += v[i];
        }

        // Return the minimized sum
        return res;
    }

    // Driver Code

        // Given array arr
        var arr = [ 4, 8, 15, 16, 23, 42 ];

        var N = arr.length;

        // Given K
        var K = 3;

        // Function Call
        document.write(find(arr, N, K) + "\n");

// This code contributed by aashish1995
</script>
```

**Output:** 

```
12
```

**时间复杂度:** *O(N)* ，其中 N 为数组中元素的个数。
**辅助空间:** *O(N)* ，其中 N 为数组中的元素个数。