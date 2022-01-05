# 查询以给定值将子阵列中的每个元素更新为按位异或

> 原文:[https://www . geeksforgeeks . org/查询-更新-子数组中的每个元素-给定值按位异或/](https://www.geeksforgeeks.org/queries-to-update-each-element-in-subarray-to-bitwise-xor-with-a-given-value/)

给定一个数组 **arr[]** ，并查询形式为 **(l，r，val)** 的 **Q[][]** ，每个查询的任务是用 **val** 将索引**【l–1，r–1】**中的所有元素更新为[逐位异或](https://www.geeksforgeeks.org/find-xor-of-two-number-without-using-xor-operator/)。打印完成所有查询后获得的最终数组。
**示例:**

> **输入** : arr[] = {2，3，6，5，4}，Q[][] = {{1，3，2}，{2，4，4}}
> **输出:** 0 5 0 1 4
> **解释:**
> 1 <sup>st</sup> 查询:关注子数组{2，3，6}在用其与 val(= 2)
> 的异或替换每个元素后，修改为{0，1，4} 5}在将每个元素替换为其与 val 的异或运算后，修改为{5，0，1 }
> 因此，最终数组为{0，5，0，1，4}
> **输入:**arr[= { 1，3，5}，Q[][] = {{1，2，8}，{2，3，3}}
> **输出:** 9 8 6

**天真的方法:**
解决这个问题最简单的方法是遍历每个查询的索引**【l–1，r–1】**，并将**arr【I】**替换为 **arr[i]^val** 。完成所有查询后，打印修改后的数组。
***时间复杂度:**O(N * sizeof(Q))*
***辅助空间:** O(1)*
**方法:**按照以下步骤通过以恒定的时间复杂度处理每个查询来解决问题:

*   用全零初始化数组 **temp[]** 。
*   对于表单 **(l，r，val)** 的每个查询，更新**温度【l–1】**和**温度【r】**，将其各自的**与**值**异或。**
*   对每个查询完成上述步骤后，将 **temp[]** 转换为**前缀异或数组**。
*   最后，通过将第 i <sup>个</sup>元素替换为其**异或**来执行更新 arr[]。

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform XOR in
// the range [lo, hi]
void findxor(int temp[], int N,
             int lo, int hi, int val)
{
    temp[lo] ^= val;
    if (hi != N - 1)
        temp[hi + 1] ^= val;
}

// Function to generate Prefix
// Xor Array
void updateArray(int temp[], int N)
{
    for (int i = 1; i < N; i++)
        temp[i] ^= temp[i - 1];
}

// Function to perform each Query
// and print the final array
void xorQuery(int arr[], int n,
              vector<vector<int> > Q)
{

    int temp[n];
    // initialize temp array to 0
    memset(temp, 0, sizeof(temp));

    // Perform each Query
    for (int i = 0; i < Q.size(); i++) {
        findxor(temp, n, Q[i][0] - 1,
                Q[i][1] - 1, Q[i][2]);
    }

    // Modify the array
    updateArray(temp, n);

    // Print the final array
    for (int i = 0; i < n; ++i) {
        cout << (arr[i] ^ temp[i]) << " ";
    }
}

// Driver Code
int main()
{

    int arr[] = { 2, 3, 6, 5, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    vector<vector<int> > Q = { { 1, 3, 2 },
                               { 2, 4, 4 } };

    xorQuery(arr, n, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to perform XOR in
// the range [lo, hi]
static void findxor(int temp[], int N,
                    int lo, int hi, int val)
{
    temp[lo] ^= val;
    if (hi != N - 1)
        temp[hi + 1] ^= val;
}

// Function to generate Prefix
// Xor Array
static void updateArray(int temp[], int N)
{
    for(int i = 1; i < N; i++)
        temp[i] ^= temp[i - 1];
}

// Function to perform each Query
// and print the final array
static void xorQuery(int arr[], int n,
                     int[][] Q)
{
    int[] temp = new int[n];

    // Perform each Query
    for(int i = 0; i < Q.length; i++)
    {
        findxor(temp, n, Q[i][0] - 1,
                         Q[i][1] - 1,
                         Q[i][2]);
    }

    // Modify the array
    updateArray(temp, n);

    // Print the final array
    for(int i = 0; i < n; ++i)
    {
        System.out.print((arr[i] ^ temp[i]) + " ");
    }
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 2, 3, 6, 5, 4 };
    int n = arr.length;

    int[][] Q = { { 1, 3, 2 },
                  { 2, 4, 4 } };

    xorQuery(arr, n, Q);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to perform XOR in
# the range [lo, hi]
def findxor(temp, N, lo, hi, val):

    temp[lo] ^= val
    if (hi != N - 1):
        temp[hi + 1] ^= val

# Function to generate Prefix
# Xor Array
def updateArray(temp, N):

    for i in range(1, N):
        temp[i] ^= temp[i - 1]

# Function to perform each Query
# and print the final array
def xorQuery(arr, n, Q):

    temp =[0] * n

    # Perform each Query
    for i in range(len(Q)):
        findxor(temp, n, Q[i][0] - 1,
                         Q[i][1] - 1,
                         Q[i][2])

    # Modify the array
    updateArray(temp, n)

    # Print the final array
    for i in range(n):
        print((arr[i] ^ temp[i]), end = " ")

# Driver Code
if __name__ == "__main__":

    arr = [ 2, 3, 6, 5, 4 ]
    n = len(arr)
    Q = [ [ 1, 3, 2 ],
          [ 2, 4, 4 ] ]

    xorQuery(arr, n, Q)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to perform XOR in
// the range [lo, hi]
static void findxor(int []temp, int N,
                    int lo, int hi, int val)
{
    temp[lo] ^= val;

    if (hi != N - 1)
        temp[hi + 1] ^= val;
}

// Function to generate Prefix
// Xor Array
static void updateArray(int []temp, int N)
{
    for(int i = 1; i < N; i++)
        temp[i] ^= temp[i - 1];
}

// Function to perform each Query
// and print the readonly array
static void xorQuery(int []arr, int n,
                     int[,] Q)
{
    int[] temp = new int[n];

    // Perform each Query
    for(int i = 0; i < Q.GetLength(0); i++)
    {
        findxor(temp, n, Q[i, 0] - 1,
                         Q[i, 1] - 1,
                         Q[i, 2]);
    }

    // Modify the array
    updateArray(temp, n);

    // Print the readonly array
    for(int i = 0; i < n; ++i)
    {
        Console.Write((arr[i] ^ temp[i]) + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 3, 6, 5, 4 };
    int n = arr.Length;

    int[,] Q = { { 1, 3, 2 },
                 { 2, 4, 4 } };

    xorQuery(arr, n, Q);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript Program to implement
// the above approach

// Function to perform XOR in
// the range [lo, hi]
function findxor(temp, N, lo, hi, val) {
    temp[lo] ^= val;
    if (hi != N - 1)
        temp[hi + 1] ^= val;
}

// Function to generate Prefix
// Xor Array
function updateArray(temp, N) {
    for (let i = 1; i < N; i++)
        temp[i] ^= temp[i - 1];
}

// Function to perform each Query
// and print the final array
function xorQuery(arr, n, Q) {

    let temp = new Array(n);
    // initialize temp array to 0
    temp.fill(0)

    // Perform each Query
    for (let i = 0; i < Q.length; i++) {
        findxor(temp, n, Q[i][0] - 1,
            Q[i][1] - 1, Q[i][2]);
    }

    // Modify the array
    updateArray(temp, n);

    // Print the final array
    for (let i = 0; i < n; ++i) {
        document.write(`${arr[i] ^ temp[i]} `);
    }
}

// Driver Code

let arr = [2, 3, 6, 5, 4];
let n = arr.length;
let Q = [[1, 3, 2],
[2, 4, 4]];

xorQuery(arr, n, Q);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
0 5 0 1 4
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*