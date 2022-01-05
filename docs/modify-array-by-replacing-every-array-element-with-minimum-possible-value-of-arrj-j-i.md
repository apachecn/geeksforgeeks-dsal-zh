# 通过用 arr[j]+| j–I |

的最小可能值替换每个数组元素来修改数组

> 原文:[https://www . geeksforgeeks . org/通过用 arrj-j-i 的最小可能值替换每个数组元素来修改数组/](https://www.geeksforgeeks.org/modify-array-by-replacing-every-array-element-with-minimum-possible-value-of-arrj-j-i/)

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是为每个索引找到一个值，使得索引 **i** 处的值为**arr[j]+| j–I |**，其中 **1 ≤ j ≤ N** ，任务是为从 **1 到 N** 的每个索引找到最小值。

**示例:**

> **输入:** N = 5，arr[] = {1，4，2，5，3}
> **输出:** {1，2，2，3，3}
> **解释:**
> arr[0]= arr[0]+| 0-0 | = 1
> arr[1]= arr[0]+| 0-1 | = 2
> arr[2]= arr[2]+| 2-2 | = 2
> arr[3]=
> 
> **输入:** N = 4，arr[] = {1，2，3，4}
> 输出: {1，2，3，4}

**天真方法:**想法是使用两个嵌套的 for 循环来遍历数组和每个**I<sup>th</sup>T7】索引，找到并打印**arr【j】+| I-j |**的最小值。**

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**思路是从左右数组遍历中使用[前缀求和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)技术，找到每个索引的最小值。按照以下步骤解决问题:

1.  取两个辅助阵**dp1【】**和**dp2【】**，其中**dp1【】**存储左右遍历的答案，**dp2【】**存储左右遍历的答案。
2.  从 **i = 2** 到 **N-1** 遍历数组 **arr[]** ，计算 **min(arr[i]，dp1[i-1] + 1)** 。
3.  遍历数组 **arr[]** 从 **i = N-1** 到 **1** 并计算 **min(arr[i]，dp2[i+1] + 1)** 。
4.  再次遍历数组从 **1** 到 **N** 并在每次迭代时打印 **min(dp1[i]，dp2[i])** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum value of
// arr[j] + |j - i| for every array index
void minAtEachIndex(int n, int arr[])
{
    // Stores minimum of a[j] + |i - j|
    // upto position i
    int dp1[n];

    // Stores minimum of a[j] + |i-j|
    // upto position i from the end
    int dp2[n];

    int i;

    dp1[0] = arr[0];

    // Traversing and storing minimum
    // of a[j]+|i-j| upto i
    for (i = 1; i < n; i++)
        dp1[i] = min(arr[i], dp1[i - 1] + 1);

    dp2[n - 1] = arr[n - 1];

    // Traversing and storing minimum
    // of a[j]+|i-j| upto i from the end
    for (i = n - 2; i >= 0; i--)
        dp2[i] = min(arr[i], dp2[i + 1] + 1);

    vector<int> v;

    // Traversing from [0, N] and storing minimum
    // of a[j] + |i - j| from starting and end
    for (i = 0; i < n; i++)
        v.push_back(min(dp1[i], dp2[i]));

    // Print the required array
    for (auto x : v)
        cout << x << " ";
}

// Driver code
int main()
{

    // Given array arr[]
    int arr[] = { 1, 4, 2, 5, 3 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    minAtEachIndex(N, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.util.ArrayList;
import java.util.List;

class GFG{

// Function to find minimum value of
// arr[j] + |j - i| for every array index
static void minAtEachIndex(int n, int arr[])
{

    // Stores minimum of a[j] + |i - j|
    // upto position i
    int dp1[] = new int[n];

    // Stores minimum of a[j] + |i-j|
    // upto position i from the end
    int dp2[] = new int[n];

    int i;

    dp1[0] = arr[0];

    // Traversing and storing minimum
    // of a[j]+|i-j| upto i
    for(i = 1; i < n; i++)
        dp1[i] = Math.min(arr[i], dp1[i - 1] + 1);

    dp2[n - 1] = arr[n - 1];

    // Traversing and storing minimum
    // of a[j]+|i-j| upto i from the end
    for(i = n - 2; i >= 0; i--)
        dp2[i] = Math.min(arr[i], dp2[i + 1] + 1);

    ArrayList<Integer> v = new ArrayList<Integer>();

    // Traversing from [0, N] and storing minimum
    // of a[j] + |i - j| from starting and end
    for(i = 0; i < n; i++)
        v.add(Math.min(dp1[i], dp2[i]));

    // Print the required array
    for(int x : v)
        System.out.print(x + " ");
}

// Driver code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 1, 4, 2, 5, 3 };

    // Size of the array
    int N = arr.length;

    // Function Call
    minAtEachIndex(N, arr);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find minimum value of
# arr[j] + |j - i| for every array index
def minAtEachIndex(n, arr):

    # Stores minimum of a[j] + |i - j|
    # upto position i
    dp1 = [0] * n

    # Stores minimum of a[j] + |i-j|
    # upto position i from the end
    dp2 = [0] * n

    i = 0

    dp1[0] = arr[0]

    # Traversing and storing minimum
    # of a[j]+|i-j| upto i
    for i in range(1, n):
        dp1[i] = min(arr[i], dp1[i - 1] + 1)

    dp2[n - 1] = arr[n - 1]

    # Traversing and storing minimum
    # of a[j]+|i-j| upto i from the end
    for i in range(n - 2, -1, -1):
        dp2[i] = min(arr[i], dp2[i + 1] + 1)

    v = []

    # Traversing from [0, N] and storing minimum
    # of a[j] + |i - j| from starting and end
    for i in range(0, n):
        v.append(min(dp1[i], dp2[i]))

    # Print the required array
    for x in v:
        print(x, end = " ")

# Driver code
if __name__ == '__main__':

    # Given array arr
    arr = [ 1, 4, 2, 5, 3 ]

    # Size of the array
    N = len(arr)

    # Function Call
    minAtEachIndex(N, arr)

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find minimum value of
// arr[j] + |j - i| for every array index
static void minAtEachIndex(int n, int []arr)
{

    // Stores minimum of a[j] + |i - j|
    // upto position i
    int []dp1 = new int[n];

    // Stores minimum of a[j] + |i-j|
    // upto position i from the end
    int []dp2 = new int[n];
    int i;
    dp1[0] = arr[0];

    // Traversing and storing minimum
    // of a[j]+|i-j| upto i
    for(i = 1; i < n; i++)
        dp1[i] = Math.Min(arr[i], dp1[i - 1] + 1);
    dp2[n - 1] = arr[n - 1];

    // Traversing and storing minimum
    // of a[j]+|i-j| upto i from the end
    for(i = n - 2; i >= 0; i--)
        dp2[i] = Math.Min(arr[i], dp2[i + 1] + 1);
    List<int> v = new List<int>();

    // Traversing from [0, N] and storing minimum
    // of a[j] + |i - j| from starting and end
    for(i = 0; i < n; i++)
        v.Add(Math.Min(dp1[i], dp2[i]));

    // Print the required array
    foreach(int x in v)
        Console.Write(x + " ");
}

// Driver code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 1, 4, 2, 5, 3 };

    // Size of the array
    int N = arr.Length;

    // Function Call
    minAtEachIndex(N, arr);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find minimum value of
// arr[j] + |j - i| for every array index
function minAtEachIndex(n, arr)
{
    // Stores minimum of a[j] + |i - j|
    // upto position i
    var dp1 = Array(n);

    // Stores minimum of a[j] + |i-j|
    // upto position i from the end
    var dp2 = Array(n);

    var i;

    dp1[0] = arr[0];

    // Traversing and storing minimum
    // of a[j]+|i-j| upto i
    for (i = 1; i < n; i++)
        dp1[i] = Math.min(arr[i], dp1[i - 1] + 1);

    dp2[n - 1] = arr[n - 1];

    // Traversing and storing minimum
    // of a[j]+|i-j| upto i from the end
    for (i = n - 2; i >= 0; i--)
        dp2[i] = Math.min(arr[i], dp2[i + 1] + 1);

    var v = [];

    // Traversing from [0, N] and storing minimum
    // of a[j] + |i - j| from starting and end
    for (i = 0; i < n; i++)
        v.push(Math.min(dp1[i], dp2[i]));

    // Print the required array
    v.forEach(x => {
        document.write(x + " ");
    });

}

// Driver code

// Given array arr[]
var arr = [1, 4, 2, 5, 3];

// Size of the array
var N = arr.length;

// Function Call
minAtEachIndex(N, arr);

</script>
```

**Output:** 

```
1 2 2 3 3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)