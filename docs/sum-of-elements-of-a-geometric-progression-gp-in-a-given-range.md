# 给定范围内几何级数的元素之和

> 原文:[https://www . geeksforgeeks . org/给定范围内几何级数的元素总和/gp/](https://www.geeksforgeeks.org/sum-of-elements-of-a-geometric-progression-gp-in-a-given-range/)

给定**arr【】**和 **Q** 中的几何级数，以**【L，R】**的形式查询，其中 **L** 是范围的左边界， **R** 是右边界。任务是[找到给定范围内几何级数](https://www.geeksforgeeks.org/program-sum-geometric-series/)元素的和。

**注:**范围为 1-索引， **1 ≤ L，R ≤ N** ，其中 **N** 为 arr 的大小。
**示例:**

> **输入:** arr[] = {2，4，8，16，32，64，128，256}，Q = [[2，4]，[2，6]，[5，8]]
> **输出:**
> 28
> 124
> 480
> **说明:**
> 范围 1: arr = {4，8，16}。因此总和= 28
> 范围 2: arr = {4，8，16，32，64}。因此总和= 124
> 范围 3: arr = {32，64，128，256}。因此总和= 480
> 
> **输入:** arr[] = {7，7，7，7，7，7}，Q = [[1，6]，[2，4]，[3，3]]
> **输出:**
> 42
> 21
> 7
> **说明:**
> 范围 1: arr = {7，7，7，7，7，7，7}。因此总和= 42
> 范围 2: arr = {7，7，7}。因此总和= 21
> 范围 3: arr = {7}。因此总和= 7

**逼近**:由于给定的序列是一个[几何级数](https://www.geeksforgeeks.org/geometric-progression/)，所以可以很容易地分两步高效地求出和:

1.  获取范围的第一个元素。
2.  如果 **d = 1，**则乘以 **d*k** 到它，否则乘以**(d<sup>k</sup>–1)/(d–1)**到它，其中 **d** 是 GP 的公比， **k** 是范围内的元素数。

**例如:**
假设 a[i]是范围的第一个元素， **d** 是 GP 的公比， **k** 是给定范围内的元素个数。
那么范围的总和将是

> = a[i] + a[i+1] + a[i+2] + …..+a[I+k-1]
> = a[I]+(a[I]* d)+(a[I]* d * d)+…。+(a[I]* d<sup>k)</sup>
> = a[I]*(1+d+…+d<sup>k</sup>)
> = a[I]*(d<sup>k</sup>–1)/(d–1)

下面是上述方法的实现:

## C++

```
// C++ program to find the sum
// of elements of an GP in the
// given range
#include <bits/stdc++.h>
using namespace std;

// Function to find sum in the given range
int findSum(int arr[], int n,
            int left, int right)
{

    // Find the value of k
    int k = right - left + 1;

    // Find the common difference
    int d = arr[1] / arr[0];

    // Find the sum
    int ans = arr[left - 1];

    if (d == 1)
        ans = ans * d * k;
    else
        ans = ans * ((int)pow(d, k) - 1 /
                                 (d - 1));

    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 8, 16, 32,
                  64, 128, 256 };
    int queries = 3;
    int q[][2] = { { 2, 4 }, { 2, 6 },
                   { 5, 8 } };

    int n = sizeof(arr) / sizeof(arr[0]);

    for(int i = 0; i < queries; i++)
        cout << (findSum(arr, n, q[i][0], q[i][1]))
             << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum
// of elements of an GP in the
// given range
import java.io.*;
import java.util.*;

class GFG{

// Function to find sum in the given range
static int findSum(int[] arr, int n,
                int left, int right)
{

    // Find the value of k
    int k = right - left + 1;

    // Find the common difference
    int d = arr[1] / arr[0];

    // Find the sum
    int ans = arr[left - 1];

    if (d == 1)
        ans = ans * d * k;
    else
        ans = ans * ((int)Math.pow(d, k) - 1 /
                                (d - 1));

    return ans;
}

// Driver Code
public static void main(String args[])
{
    int[] arr = { 2, 4, 8, 16, 32,
                64, 128, 256 };
    int queries = 3;
    int[][] q = { { 2, 4 }, { 2, 6 }, { 5, 8 } };

    int n = arr.length;

    for(int i = 0; i < queries; i++)
        System.out.println(findSum(arr, n, q[i][0],
                                        q[i][1]));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to
# find the sum of elements
# of an GP in the given range

# Function to find sum in the given range
def findSum(arr, n, left, right):

    # Find the value of k
    k = right - left + 1

    # Find the common difference
    d = arr[1] // arr[0]

    # Find the sum
    ans = arr[left - 1]
    if d == 1:
        ans = ans * d * k
    else:
        ans = ans * (d ** k - 1) // (d -1)
    return ans

# Driver code
if __name__ == '__main__':
    arr = [ 2, 4, 8, 16, 32, 64, 128, 256 ]
    queries = 3
    q = [[ 2, 4 ], [ 2, 6 ], [ 5, 8 ]]
    n = len(arr)

    for i in range(queries):
        print(findSum(arr, n, q[i][0], q[i][1]))
```

## C#

```
// C# program to find the sum
// of elements of an GP in the
// given range
using System;

class GFG{

// Function to find sum in the given range
static int findSum(int[] arr, int n,
                   int left, int right)
{

    // Find the value of k
    int k = right - left + 1;

    // Find the common difference
    int d = arr[1] / arr[0];

    // Find the sum
    int ans = arr[left - 1];

    if (d == 1)
        ans = ans * d * k;
    else
        ans = ans * ((int)Math.Pow(d, k) - 1 /
                                      (d - 1));

    return ans;
}

// Driver Code
public static void Main(string []args)
{
    int[] arr = { 2, 4, 8, 16, 32,
                  64, 128, 256 };

    int queries = 3;
    int[,] q = { { 2, 4 }, { 2, 6 }, { 5, 8 } };

    int n = arr.Length;

    for(int i = 0; i < queries; i++)
        Console.Write(findSum(arr, n, q[i, 0],
                                      q[i, 1]) + "\n");
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// JavaScript program to find the sum
// of elements of an GP in the
// given range

// Function to find sum in the given range
function findSum(arr, n, left, right) {

    // Find the value of k
    let k = right - left + 1;

    // Find the common difference
    let d = arr[1] / arr[0];

    // Find the sum
    let ans = arr[left - 1];

    if (d == 1)
        ans = ans * d * k;
    else
        ans = ans * (Math.pow(d, k) - 1 / (d - 1));

    return ans;
}

// Driver Code
let arr = [2, 4, 8, 16, 32,
    64, 128, 256];

let queries = 3;

let q = [[2, 4], [2, 6],
[5, 8]];

let n = arr.length;

for (let i = 0; i < queries; i++)
    document.write(findSum(arr, n, q[i][0], q[i][1]));

// This code is contributed by blalverma92

</script>
```

**Output:** 

```
28
124
480
```

*   ***时间复杂度:** O(Q)*
*   ***空间复杂度:** O(1)*