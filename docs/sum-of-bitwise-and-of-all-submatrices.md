# 所有子矩阵的按位“与”的和

> 原文:[https://www . geeksforgeeks . org/所有子矩阵的按位求和/](https://www.geeksforgeeks.org/sum-of-bitwise-and-of-all-submatrices/)

给定一个 **NxN** 矩阵，任务是找到其所有矩形子矩阵的逐位“与”的和。

**示例:**

```
Input : arr[][] = {{1, 1, 1},
                   {1, 1, 1},
                   {1, 1, 1}}
Output : 36
Explanation: All the possible submatrices will have AND value 1.
Since, there are 36 submatrices in total, ans = 36

Input : arr[][] = {{9, 7, 4},
                   {8, 9, 2},
                   {11, 11, 5}}
Output : 135 
```

**先决条件** : [全为 1 的二进制矩阵的矩形子矩阵数](https://www.geeksforgeeks.org/number-of-submatrices-with-all-1s/)。
**朴素解法:**一个简单的解法是生成所有的子矩阵，并为每个子矩阵找到所需的 and。这种方法的时间复杂度为 0(N<sup>6</sup>)。

**高效方法:**为了更好的理解，我们假设一个元素的任意一位用变量‘I’表示，变量‘sum’用来存储最终的和。
这里的想法是，我们将尝试使用第 i <sup>个</sup>位集来查找 AND 值的数量(具有逐位 and( &)的子矩阵)。让我们假设，设置了第 i <sup>个</sup>位的子矩阵有“S <sub>i</sub> 个。对于 i <sup>第</sup>位，该和可以更新为**和+=(2<sup>I</sup>* S<sub>I</sub>)**。
对于每个位“I”，创建一个布尔矩阵 **set_bit** ，如果设置了 arr[R][C]的 I<sup>位，则在索引(R，C)处存储“1”。否则，它存储“0”。然后，对于这个布尔数组，我们尝试寻找全为 1 的矩形子矩阵的个数(S <sub>i</sub> )。对于第<sup>位，最终总和将更新为:</sup></sup>

```
sum += 2i * Si
```

下面是上述方法的实现:

## C++

```
// C++ program to find sum of Bit-wise AND
// of all submatrices

#include <iostream>
#include <stack>

using namespace std;

#define n 3

// Function to find prefix-count for each row
// from right to left
void findPrefixCount(int p_arr[][n], bool set_bit[][n])
{
    for (int i = 0; i < n; i++) {
        for (int j = n - 1; j >= 0; j--) {
            if (!set_bit[i][j])
                continue;

            if (j != n - 1)
                p_arr[i][j] += p_arr[i][j + 1];

            p_arr[i][j] += (int)set_bit[i][j];
        }
    }
}

// Function to find the number of submatrices
// with all 1s
int matrixAllOne(bool set_bit[][n])
{
    // Array to store required prefix count of 1s from
    // right to left for boolean array
    int p_arr[n][n] = { 0 };

    findPrefixCount(p_arr, set_bit);

    // Variable to store the final answer
    int ans = 0;

    // For each index of a column, determine the number
    // of sub-matrices starting from that index
    // and has all 1s
    for (int j = 0; j < n; j++) {
        int i = n - 1;

        // Stack to store elements and the count
        // of the numbers they popped
        // First part of pair is value of inserted element
        // Second part is count of the number of elements
        // pushed before with a greater value
        stack<pair<int, int> > q;

        // variable to store the number of submatrices
        // with all 1s
        int to_sum = 0;

        while (i >= 0) {
            int c = 0;
            while (q.size() != 0 and q.top().first > p_arr[i][j]) {
                to_sum -= (q.top().second + 1) * (q.top().first - p_arr[i][j]);
                c += q.top().second + 1;
                q.pop();
            }

            to_sum += p_arr[i][j];
            ans += to_sum;

            q.push({ p_arr[i][j], c });
            i--;
        }
    }

    return ans;
}

// Function to find the sum of Bitwise-AND
// of all submatrices
int sumAndMatrix(int arr[][n])
{
    int sum = 0;

    int mul = 1;

    for (int i = 0; i < 30; i++) {
        // matrix to store the status
        // of ith bit of each element
        // of matrix arr
        bool set_bit[n][n];

        for (int R = 0; R < n; R++)
            for (int C = 0; C < n; C++)
                set_bit[R][C] = ((arr[R][C] & (1 << i)) != 0);

        sum += (mul * matrixAllOne(set_bit));

        mul *= 2;
    }

    return sum;
}

// Driver Code
int main()
{
    int arr[][n] = { { 9, 7, 4 },
                     { 8, 9, 2 },
                     { 11, 11, 5 } };

    cout << sumAndMatrix(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of Bit-wise AND
// of all submatrices
import java.util.*;

class GFG
{

static int n = 3;

// Function to find prefix-count for 
// each row from right to left
static void findPrefixCount(int p_arr[][],
                            boolean set_bit[][])
{
    for (int i = 0; i < n; i++)
    {
        for (int j = n - 1; j >= 0; j--)
        {
            if (!set_bit[i][j])
                continue;

            if (j != n - 1)
                p_arr[i][j] += p_arr[i][j + 1];

            p_arr[i][j] += (set_bit[i][j]) ? 1 : 0;
        }
    }
}
static class pair
{
    int first,second;
    pair(){}

    pair(int a, int b)
    {
        first = a;
        second = b;
    }
}

// Function to find the number of
// submatrices with all 1s
static int matrixAllOne(boolean set_bit[][])
{
    // Array to store required prefix count of 1s from
    // right to left for boolean array
    int p_arr[][] = new int[n][n];

    for(int i = 0; i < n; i++)
        for(int j = 0; j < n;j++)
            p_arr[i][j] = 0;

    findPrefixCount(p_arr, set_bit);

    // Variable to store the final answer
    int ans = 0;

    // For each index of a column, determine the number
    // of sub-matrices starting from that index
    // and has all 1s
    for (int j = 0; j < n; j++)
    {
        int i = n - 1;

        // Stack to store elements and the count
        // of the numbers they popped
        // First part of pair is value of inserted element
        // Second part is count of the number of elements
        // pushed before with a greater value
        Stack<pair > q = new Stack<pair >();

        // variable to store the number of submatrices
        // with all 1s
        int to_sum = 0;

        while (i >= 0)
        {
            int c = 0;
            while (q.size() != 0 &&
                    q.peek().first > p_arr[i][j])
            {
                to_sum -= (q.peek().second + 1) *
                            (q.peek().first - p_arr[i][j]);
                c += q.peek().second + 1;
                q.pop();
            }

            to_sum += p_arr[i][j];
            ans += to_sum;

            q.push(new pair( p_arr[i][j], c ));
            i--;
        }
    }
    return ans;
}

// Function to find sum of Bitwise-OR of
// all submatrices
static int sumAndMatrix(int arr[][])
{
    int sum = 0;

    int mul = 1;

    for (int i = 0; i < 30; i++)
    {
        // matrix to store the status
        // of ith bit of each element
        // of matrix arr
        boolean set_bit[][] = new boolean[n][n];

        for (int R = 0; R < n; R++)
            for (int C = 0; C < n; C++)
                set_bit[R][C] = ((arr[R][C] & (1 << i)) != 0);

        sum += (mul * matrixAllOne(set_bit));

        mul *= 2;
    }
    return sum;
}

// Driver Code
public static void main(String args[])
{
    int arr[][] = { { 9, 7, 4 },
                    { 8, 9, 2 },
                    { 11, 11, 5 } };

    System.out.println( sumAndMatrix(arr));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find sum of
# Bitwise-AND of all submatrices

# Function to find prefix-count for
# each row from right to left
def findPrefixCount(p_arr, set_bit):

    for i in range(0, n):
        for j in range(n - 1, -1, -1):

            if not set_bit[i][j]:
                continue
            if j != n - 1:
                p_arr[i][j] += p_arr[i][j + 1]

            p_arr[i][j] += int(set_bit[i][j])

# Function to create a boolean matrix
# set_bit which stores ‘1’ at an index
# (R, C) if ith bit of arr[R][C] is set.
def matrixAllOne(set_bit):

    # Array to store prefix count of zeros
    # from right to left for boolean array
    p_arr = [[0 for i in range(n)]
                for j in range(n)]

    findPrefixCount(p_arr, set_bit)

    # Variable to store the final answer
    ans = 0

    # For each index of a column we
    # will try to determine the number
    # of sub-matrices starting from
    # that index and has all 1s
    for j in range(0, n):

        i = n - 1

        # stack to store elements and the
        # count of the numbers they popped

        # First part of pair will be the
        # value of inserted element.
        # Second part will be the count
        # of the number of elements pushed
        # before with a greater value
        q = []

        # Variable to store the number
        # of submatrices with all 0s
        to_sum = 0

        while i >= 0:

            c = 0
            while (len(q) != 0 and
                   q[-1][0] > p_arr[i][j]):

                to_sum -= ((q[-1][1] + 1) *
                           (q[-1][0] - p_arr[i][j]))

                c += q.pop()[1] + 1

            to_sum += p_arr[i][j]
            ans += to_sum

            q.append((p_arr[i][j], c))
            i -= 1

    # Return the final answer
    return ans

# Function to find sum of
# Bitwise-AND of all submatrices
def sumAndMatrix(arr):

    Sum, mul = 0, 1
    for i in range(0, 30):

        # matrix to store the status
        # of ith bit of each element
        # of matrix arr
        set_bit = [[False for i in range(n)]
                          for j in range(n)]

        for R in range(0, n):
            for C in range(0, n):
                set_bit[R][C] = ((arr[R][C] &
                                 (1 << i)) != 0)

        Sum += (mul * matrixAllOne(set_bit))
        mul *= 2

    return Sum

# Driver Code
if __name__ == "__main__":

    n = 3
    arr = [[9, 7, 4],
        [8, 9, 2],
        [11, 11, 5]]

    print(sumAndMatrix(arr))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find sum of Bit-wise AND
// of all submatrices
using System;
using System.Collections.Generic;

class GFG
{

static int n = 3;

// Function to find prefix-count for
// each row from right to left
static void findPrefixCount(int [,]p_arr,
                            bool [,]set_bit)
{
    for (int i = 0; i < n; i++)
    {
        for (int j = n - 1; j >= 0; j--)
        {
            if (!set_bit[i, j])
                continue;

            if (j != n - 1)
                p_arr[i, j] += p_arr[i, j + 1];

            p_arr[i, j] += (set_bit[i, j]) ? 1 : 0;
        }
    }
}
public class pair
{
    public int first,second;
    public pair(){}

    public pair(int a, int b)
    {
        first = a;
        second = b;
    }
}

// Function to find the number of
// submatrices with all 1s
static int matrixAllOne(bool [,]set_bit)
{
    // Array to store required prefix count of 1s from
    // right to left for boolean array
    int [,]p_arr = new int[n, n];

    for(int i = 0; i < n; i++)
        for(int j = 0; j < n;j++)
            p_arr[i, j] = 0;

    findPrefixCount(p_arr, set_bit);

    // Variable to store the final answer
    int ans = 0;

    // For each index of a column, determine the number
    // of sub-matrices starting from that index
    // and has all 1s
    for (int j = 0; j < n; j++)
    {
        int i = n - 1;

        // Stack to store elements and the count
        // of the numbers they popped
        // First part of pair is value of inserted element
        // Second part is count of the number of elements
        // pushed before with a greater value
        Stack<pair > q = new Stack<pair >();

        // variable to store the number of submatrices
        // with all 1s
        int to_sum = 0;

        while (i >= 0)
        {
            int c = 0;
            while (q.Count != 0 &&
                    q.Peek().first > p_arr[i,j])
            {
                to_sum -= (q.Peek().second + 1) *
                            (q.Peek().first - p_arr[i,j]);
                c += q.Peek().second + 1;
                q.Pop();
            }

            to_sum += p_arr[i,j];
            ans += to_sum;

            q.Push(new pair( p_arr[i,j], c ));
            i--;
        }
    }
    return ans;
}

// Function to find sum of Bitwise-OR of
// all submatrices
static int sumAndMatrix(int [,]arr)
{
    int sum = 0;

    int mul = 1;

    for (int i = 0; i < 30; i++)
    {
        // matrix to store the status
        // of ith bit of each element
        // of matrix arr
        bool [,]set_bit = new bool[n,n];

        for (int R = 0; R < n; R++)
            for (int C = 0; C < n; C++)
                set_bit[R, C] = ((arr[R, C] & (1 << i)) != 0);

        sum += (mul * matrixAllOne(set_bit));

        mul *= 2;
    }
    return sum;
}

// Driver Code
public static void Main(String []args)
{
    int [,]arr = { { 9, 7, 4 },
                    { 8, 9, 2 },
                    { 11, 11, 5 } };

    Console.WriteLine(sumAndMatrix(arr));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find sum of Bit-wise AND
// of all submatrices

var n = 3;

// Function to find prefix-count for each row
// from right to left
function findPrefixCount(p_arr, set_bit)
{
    for (var i = 0; i < n; i++) {
        for (var j = n - 1; j >= 0; j--) {
            if (!set_bit[i][j])
                continue;

            if (j != n - 1)
                p_arr[i][j] += p_arr[i][j + 1];

            p_arr[i][j] += set_bit[i][j];
        }
    }
}

// Function to find the number of submatrices
// with all 1s
function matrixAllOne(set_bit)
{
    // Array to store required prefix count of 1s from
    // right to left for boolean array
    var p_arr = Array.from(Array(n), ()=> Array(n).fill(0));

    findPrefixCount(p_arr, set_bit);

    // Variable to store the final answer
    var ans = 0;

    // For each index of a column, determine the number
    // of sub-matrices starting from that index
    // and has all 1s
    for (var j = 0; j < n; j++) {
        var i = n - 1;

        // Stack to store elements and the count
        // of the numbers they popped
        // First part of pair is value of inserted element
        // Second part is count of the number of elements
        // pushed before with a greater value
        var q = [];

        // variable to store the number of submatrices
        // with all 1s
        var to_sum = 0;

        while (i >= 0) {
            var c = 0;
            while (q.length != 0 && q[q.length - 1][0] > p_arr[i][j]) {
                to_sum -= (q[q.length - 1][1] + 1) * (q[q.length - 1][0] - p_arr[i][j]);
                c += q[q.length - 1][1] + 1;
                q.pop();
            }

            to_sum += p_arr[i][j];
            ans += to_sum;

            q.push([p_arr[i][j], c ]);
            i--;
        }
    }

    return ans;
}

// Function to find the sum of Bitwise-AND
// of all submatrices
function sumAndMatrix(arr)
{
    var sum = 0;

    var mul = 1;

    for (var i = 0; i < 30; i++) {
        // matrix to store the status
        // of ith bit of each element
        // of matrix arr
        var set_bit = Array.from(Array(n), ()=> Array(n));

        for (var R = 0; R < n; R++)
            for (var C = 0; C < n; C++)
                set_bit[R][C] = ((arr[R][C] & (1 << i)) != 0);

        sum += (mul * matrixAllOne(set_bit));

        mul *= 2;
    }

    return sum;
}

// Driver Code
var arr = [ [ 9, 7, 4 ],
                 [ 8, 9, 2 ],
                 [ 11, 11, 5 ] ];
document.write( sumAndMatrix(arr));

</script>
```

**Output:** 

```
135
```

**时间复杂度** : O(N <sup>2</sup> )。