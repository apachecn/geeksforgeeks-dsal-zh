# 生成 N 长度置换，使得相邻元素之间的绝对差出现在范围[2，4]

内

> 原文:[https://www . geeksforgeeks . org/generate-an-n-length-replacement-这样相邻元素之间的绝对差异就出现在-2-4/](https://www.geeksforgeeks.org/generate-an-n-length-permutation-such-that-absolute-difference-between-adjacent-elements-are-present-in-the-range-2-4/) 范围内

给定一个正整数 **N** ，任务是构造第一个 **N** 自然数 的[排列，使得相邻元素之间的绝对差为 **2** 、 **3** 或 **4** 。如果无法构造这样的排列，则打印**-1”**。](https://www.geeksforgeeks.org/check-if-an-array-is-a-permutation-of-numbers-from-1-to-n/)

**示例:**

> **输入:** N = 4
> **输出:** 3 1 4 2
> **解释:**
> 考虑一个排列{3，1，4，2}。现在，相邻元素之间的绝对差值是{2，3，2}。
> 
> **输入:** N = 9
> **输出:**9 7 5 3 4 2 6 8

**方法:**给定的问题可以通过将连续的奇偶元素组合在一起构造[排列](https://www.geeksforgeeks.org/permutation-coefficient/)来解决。按照以下步骤解决问题:

*   如果 **N** 的值小于 **4** ，则打印 **-1** ，因为不可能根据给定的条件为小于 **4** 的 **N** 构造置换。
*   初始化一个变量，说 **i** 为 **N** ，执行以下步骤:
    *   [如果 **i** 的值为偶数](https://www.geeksforgeeks.org/php-check-number-even-odd/)，则 **i** 的值递减 **1** 。
    *   [迭代直到](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)T2 I 的值至少为 **1** 并打印 **i** 的值，将 **i** 的值递减 **2** 。
    *   打印 **4** 和 **2** 并将 **i** 的值更新为 **6** 。
    *   [在](https://www.geeksforgeeks.org/range-based-loop-c/)**【I，N】**范围内迭代，打印 **i** 的值，并将 **i** 的值增加 **2** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the permutation of
// size N with absolute difference of
// adjacent elements in range [2, 4]
void getPermutation(int N)
{
    // If N is less than 4
    if (N <= 3) {
        cout << -1;
        return;
    }

    int i = N;

    // Check if N is even
    if (N % 2 == 0)
        i--;

    // Traverse through odd integers
    while (i >= 1) {
        cout << i << " ";
        i -= 2;
    }

    cout << 4 << " " << 2 << " ";

    // Update the value of i
    i = 6;

    // Traverse through even integers
    while (i <= N) {
        cout << i << " ";
        i += 2;
    }
}

// Driver Code
int main()
{
    int N = 9;
    getPermutation(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for tha above approach
import java.util.*;

class GFG{

// Function to print the permutation of
// size N with absolute difference of
// adjacent elements in range [2, 4]
static void getPermutation(int N)
{

    // If N is less than 4
    if (N <= 3)
    {
        System.out.print(-1);
        return;
    }

    int i = N;

    // Check if N is even
    if (N % 2 == 0)
        i--;

    // Traverse through odd integers
    while (i >= 1)
    {
        System.out.print(i + " ");
        i -= 2;
    }

    System.out.print(4 + " " + 2 +" ");

    // Update the value of i
    i = 6;

    // Traverse through even integers
    while (i <= N)
    {
        System.out.print(i + " ");
        i += 2;
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 9;

    getPermutation(N);
}   
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print permutation of
# size N with absolute difference of
# adjacent elements in range [2, 4]
def getPermutation(N):

    # If N is less than 4
    if (N <= 3):
        print(-1)
        return

    i = N

    # Check if N is even
    if (N % 2 == 0):
        i -= 1

    # Traverse through odd integers
    while (i >= 1):
        print(i, end = " ")
        i -= 2

    print(4, 2, end = " ")

    # Update the value of i
    i = 6

    # Traverse through even integers
    while (i <= N):
        print( i, end = " ")
        i += 2

# Driver Code
if __name__ == '__main__':
    N = 9
    getPermutation(N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the permutation of
// size N with absolute difference of
// adjacent elements in range [2, 4]
static void getPermutation(int N)
{

    // If N is less than 4
    if (N <= 3)
    {

        Console.Write(-1);
        return;
    }

    int i = N;

    // Check if N is even
    if (N % 2 == 0)
        i--;

    // Traverse through odd integers
    while (i >= 1)
    {
        Console.Write(i + " ");
        i -= 2;
    }

    Console.Write(4 + " " + 2 +" ");

    // Update the value of i
    i = 6;

    // Traverse through even integers
    while (i <= N)
    {
        Console.Write(i +" ");
        i += 2;
    }
}

// Driver Code
public static void Main()
{
    int N = 9;

    getPermutation(N);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print the permutation of
// size N with absolute difference of
// adjacent elements in range [2, 4]
function getPermutation(N)
{

    // If N is less than 4
    if (N <= 3)
    {
        document.write(-1);
        return;
    }

    let i = N;

    // Check if N is even
    if (N % 2 == 0)
        i--;

    // Traverse through odd integers
    while (i >= 1)
    {
        document.write(i + " ");
        i -= 2;
    }

    document.write(4 + " " + 2 + " ");

    // Update the value of i
    i = 6;

    // Traverse through even integers
    while (i <= N)
    {
        document.write(i + " ");
        i += 2;
    }
}

// Driver Code
let N = 9;

getPermutation(N);

// This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
9 7 5 3 1 4 2 6 8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)