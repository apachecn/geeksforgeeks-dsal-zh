# 元素在[0，X]范围内或奇数次幂为 2 且和为 N 的集合的最小尺寸

> 原文:[https://www . geeksforgeeks . org/最小尺寸集合具有 0-x 范围内的任一元素或 n 的 2 的奇数次幂/](https://www.geeksforgeeks.org/minimum-size-of-set-having-either-element-in-range-0-x-or-an-odd-power-of-2-with-sum-n/)

给定两个正整数 **N** 和 **X** ，任务是找到最小整数集的大小，使得[集合的所有元素之和](https://www.geeksforgeeks.org/accumulate-and-partial_sum-in-c-stl-numeric-header/)为 **N** ，每个集合元素要么在**【0，X】**的范围内，要么是[为 **2**](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/) 的奇次幂。如果找不到这样的[尺寸的套装](https://www.geeksforgeeks.org/setsize-c-stl/)，则打印**-1”**。

**示例:**

> **输入:** N = 11，X = 2
> **输出:** 3
> **说明:**集合{1，2，8}是元素个数最小的集合，使得元素的和为 11，每个元素或者在范围[0，2](即 1 和 2)内，或者是 2 的奇次幂(即 8 = 2 <sup>3</sup> )。
> 
> **输入:** N = 3，X = 0
> **输出:** -1
> **说明:**不存在有效集合。

**方法:**给定的问题可以通过以下步骤解决:

*   维护一个变量**大小**，它存储一个有效集合的最小可能大小，并用 **0** 初始化它。
*   迭代直到 **N** 的值大于 **X** 并执行以下步骤:
    *   从 **N** 中减去小于或等于 **N** 的 **2** 的最大奇次 **i** 。
    *   将**尺寸**的值增加 **1** 。
*   如果 **N** 的值为正，则将**大小**的值增加 **1** 。
*   完成上述步骤后，打印**尺寸**的值作为所需结果。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the highest odd power
// of 2 in the range [0, N]
int highestPowerof2(int n)
{

    int p = int(log2(n));

    // If P is even, subtract 1
    if(p % 2 == 0)
        p -= 1;

    return int(pow(2, p));
}

// Function to find the minimum operations
// to make N
int minStep(int N, int X)
{

   // If N is odd and X = 0, then no
    // valid set exist
    if(N % 2 and X == 0)
        return -1;

    // Stores the minimum possible size
    // of the valid set
    int size = 0;

    // Loop to subtract highest odd power
    // of 2 while X < N, step 2
    while(X < N){
        N -= highestPowerof2(N);
        size += 1;
     }

    // If N > 0, then increment the value
    // of answer by 1
    if(N)
        size += 1;

    // Return the resultant size of set
    return size;

}

// Driver Code
int main(){
    int N = 11;
    int X = 2;
    cout<<(minStep(N, X));

}

// This code is contributed by ipg2016107.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

// Function to find the highest odd power
// of 2 in the range [0, N]
static int highestPowerof2(int n)
{

    int p = (int)Math.floor(Math.log(n)/Math.log(2.0));

    // If P is even, subtract 1
    if(p % 2 == 0)
        p -= 1;

    int result = (int)(Math.pow(2,p));

        return result;
}

// Function to find the minimum operations
// to make N
static int minStep(int N, int X)
{

   // If N is odd and X = 0, then no
    // valid set exist
    if (N % 2 != 0 && X == 0)
        return -1;

    // Stores the minimum possible size
    // of the valid set
    int size = 0;

    // Loop to subtract highest odd power
    // of 2 while X < N, step 2
    while(X < N){
        N -= highestPowerof2(N);
        size += 1;
     }

    // If N > 0, then increment the value
    // of answer by 1
    if (N != 0)
        size += 1;

    // Return the resultant size of set
    return size;

}

// Driver Code
public static void main (String[] args)
{
    int N = 11;
    int X = 2;
    System.out.println(minStep(N, X));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python program for the above approach
import math

# Function to find the highest odd power
# of 2 in the range [0, N]
def highestPowerof2(n):

    p = int(math.log(n, 2))

    # If P is even, subtract 1
    if p % 2 == 0:
        p -= 1

    return int(pow(2, p))

# Function to find the minimum operations
# to make N
def minStep(N, X):

    # If N is odd and X = 0, then no
    # valid set exist
    if N % 2 and X == 0:
        return -1

    # Stores the minimum possible size
    # of the valid set
    size = 0

    # Loop to subtract highest odd power
    # of 2 while X < N, step 2
    while X < N:
        N -= highestPowerof2(N)
        size += 1

    # If N > 0, then increment the value
    # of answer by 1
    if N:
        size += 1

    # Return the resultant size of set
    return size

# Driver Code
if __name__ == '__main__':
    N = 11
    X = 2
    print(minStep(N, X))
```

## C#

```
// C# program for the above approach
using System;

class GFG {

// Function to find the highest odd power
// of 2 in the range [0, N]
static int highestPowerof2(int n)
{

    int p = (int)Math.Floor(Math.Log(n)/Math.Log(2.0));

    // If P is even, subtract 1
    if(p % 2 == 0)
        p -= 1;

    int result = (int)(Math.Pow(2,p));

        return result;
}

// Function to find the minimum operations
// to make N
static int minStep(int N, int X)
{

// If N is odd and X = 0, then no
    // valid set exist
    if (N % 2 != 0 && X == 0)
        return -1;

    // Stores the minimum possible size
    // of the valid set
    int size = 0;

    // Loop to subtract highest odd power
    // of 2 while X < N, step 2
    while(X < N){
        N -= highestPowerof2(N);
        size += 1;
    }

    // If N > 0, then increment the value
    // of answer by 1
    if (N != 0)
        size += 1;

    // Return the resultant size of set
    return size;

}

// Driver Code
public static void Main (String[] args)
{
    int N = 11;
    int X = 2;
    Console.Write(minStep(N, X));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the highest odd power
// of 2 in the range [0, N]
function highestPowerof2(n)
{
    let p = Math.floor(Math.log2(n));

    // If P is even, subtract 1
    if (p % 2 == 0)
    {
        p -= 1
    }

    return Math.pow(2, p)
}

// Function to find the minimum operations
// to make N
function minStep(N, X)
{

    // If N is odd and X = 0, then no
    // valid set exist
    if (N % 2 != 0 && X == 0)
        return -1

    // Stores the minimum possible size
    // of the valid set
    let size = 0

    // Loop to subtract highest odd power
    // of 2 while X < N, step 2
    while (X < N)
    {
        N -= highestPowerof2(N)
        size += 1
    }

    // If N > 0, then increment the value
    // of answer by 1
    if (N != 0)
        size += 1

    // Return the resultant size of set
    return size;
}

// Driver Code
let N = 11
let X = 2

document.write(minStep(N, X))

// This code is contributed by Potta Lokesh
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*