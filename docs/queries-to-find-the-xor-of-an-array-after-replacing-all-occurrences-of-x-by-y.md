# 用 Y 替换所有出现的 X 后，查询寻找数组的异或

> 原文:[https://www . geeksforgeeks . org/query-to-find-of-x-by-y 替换所有出现的数组后的异或运算/](https://www.geeksforgeeks.org/queries-to-find-the-xor-of-an-array-after-replacing-all-occurrences-of-x-by-y/)

给定一个由 **N** 不同整数组成的数组 **arr[]** 和类型为 **{X，Y}** 的查询 **Q[][]** ，每个查询的任务是在数组中用 **Y** 替换 **X** 后，找到所有数组元素的**位异或**。

**示例:**

> **输入:** arr[] = {1，2，3，4，5} Q = {(1，4) (3，6) (2，3)}
> **输出:** 4 1 0
> **解释:**
> 查询 1:数组修改为{4，2，3，4，5}和 XOR = 4
> 查询 2:数组修改为{4，2，6，4，5}和 XOR = 1
> 查询 3:数组修改为{4 5}和 XOR = 0
> **输入:** arr[] = {5，7，8，9，} Q = {(5，6) (8，1)}
> **输出:** 0 9
> **解释:**
> 查询 1:数组修改为{6，7，8，9}和 XOR = 0
> 查询 2:数组修改为{6，7，1，9}和 XOR = 9

**方法:**
方法是使用**按位异或**属性:

*   假设有三个元素 **A，B** ，**和**以及 **X** ，它们的异或为， *total_xor = A ^ B ^ X* 。
*   要从 *total_xor* 中移除 **X** 的贡献，请执行 **total_xor ^ X** 。从 **A ^ B ^ X ^ X = A ^ B** (一个元素与其自身的异或为 0)这一事实可以验证。
*   要在 *total_xor* 中添加 **Y** 的贡献，只需执行 **total_xor ^ Y** 。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the bitwise XOR
// of array elements
int total_xor;

// Function to find the total xor
void initialize_xor(int arr[], int n)
{
    // Loop to find the xor
    // of all the elements
    for (int i = 0; i < n; i++) {
        total_xor = total_xor ^ arr[i];
    }
}

// Function to find the XOR
// after replacing all occurrences
// of X by Y for Q queries
void find_xor(int X, int Y)
{
    // Remove contribution of
    // X from total_xor
    total_xor = total_xor ^ X;

    // Adding contribution of
    // Y to total_xor
    total_xor = total_xor ^ Y;

    // Print total_xor
    cout << total_xor << "\n";
}

// Driver Code
int main()
{
    int arr[] = { 5, 7, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    initialize_xor(arr, n);

    vector<vector<int> > Q = { { 5, 6 }, { 8, 1 } };

    for (int i = 0; i < Q.size(); i++) {
        find_xor(Q[i][0], Q[i][1]);
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Stores the bitwise XOR
// of array elements
static int total_xor;

// Function to find the total xor
static void initialize_xor(int arr[],
                           int n)
{
    // Loop to find the xor
    // of all the elements
    for (int i = 0; i < n; i++)
    {
        total_xor = total_xor ^ arr[i];
    }
}

// Function to find the XOR
// after replacing all occurrences
// of X by Y for Q queries
static void find_xor(int X, int Y)
{
    // Remove contribution of
    // X from total_xor
    total_xor = total_xor ^ X;

    // Adding contribution of
    // Y to total_xor
    total_xor = total_xor ^ Y;

    // Print total_xor
    System.out.print(total_xor + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, 7, 8, 9 };
    int n = arr.length;

    initialize_xor(arr, n);

    int [][]Q = { { 5, 6 }, { 8, 1 } };

    for (int i = 0; i < Q.length; i++)
    {
        find_xor(Q[i][0], Q[i][1]);
    }
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Stores the bitwise XOR
# of array elements
global total_xor
total_xor = 0

# Function to find the total xor
def initialize_xor(arr, n):

    global total_xor

    # Loop to find the xor
    # of all the elements
    for i in range(n):
        total_xor = total_xor ^ arr[i]

# Function to find the XOR
# after replacing all occurrences
# of X by Y for Q queries
def find_xor(X, Y):

    global total_xor

    # Remove contribution of
    # X from total_xor
    total_xor = total_xor ^ X

    # Adding contribution of
    # Y to total_xor
    total_xor = total_xor ^ Y

    # Print total_xor
    print(total_xor)

# Driver Code
if __name__ == '__main__':

    arr = [ 5, 7, 8, 9 ]
    n = len(arr)

    initialize_xor(arr, n)

    Q = [ [ 5, 6 ], [ 8, 1 ] ]

    # Function call
    for i in range(len(Q)):
        find_xor(Q[i][0], Q[i][1])

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Stores the bitwise XOR
// of array elements
static int total_xor;

// Function to find the total xor
static void initialize_xor(int []arr,
                           int n)
{

    // Loop to find the xor
    // of all the elements
    for(int i = 0; i < n; i++)
    {
        total_xor = total_xor ^ arr[i];
    }
}

// Function to find the XOR
// after replacing all occurrences
// of X by Y for Q queries
static void find_xor(int X, int Y)
{

    // Remove contribution of
    // X from total_xor
    total_xor = total_xor ^ X;

    // Adding contribution of
    // Y to total_xor
    total_xor = total_xor ^ Y;

    // Print total_xor
    Console.Write(total_xor + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 5, 7, 8, 9 };
    int n = arr.Length;

    initialize_xor(arr, n);

    int [,]Q = { { 5, 6 }, { 8, 1 } };

    for(int i = 0; i < Q.GetLength(0); i++)
    {
        find_xor(Q[i, 0], Q[i, 1]);
    }
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Stores the bitwise XOR
// of array elements
let total_xor;

// Function to find the total xor
function initialize_xor(arr, n)
{
    // Loop to find the xor
    // of all the elements
    for (let i = 0; i < n; i++)
    {
        total_xor = total_xor ^ arr[i];
    }
}

// Function to find the XOR
// after replacing all occurrences
// of X by Y for Q queries
function find_xor(X, Y)
{
    // Remove contribution of
    // X from total_xor
    total_xor = total_xor ^ X;

    // Adding contribution of
    // Y to total_xor
    total_xor = total_xor ^ Y;

    // Print total_xor
    document.write(total_xor + "<br/>");
}

// Driver Code

    let arr = [ 5, 7, 8, 9 ];
    let n = arr.length;

    initialize_xor(arr, n);

    let Q = [[ 5, 6 ], [ 8, 1]];

    for (let i = 0; i < Q.length; i++)
    {
        find_xor(Q[i][0], Q[i][1]);
    }

</script>
```

**Output:** 

```
0
9
```

***时间复杂度:**O(N+sizeof(Q))*
***辅助空间:** O(1)*