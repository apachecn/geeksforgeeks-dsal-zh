# 生成以 N 和 K 的相邻差开始的双离子阵列

> 原文:[https://www . geesforgeks . org/generate-a-bitonic-array-以 n 和相邻差 k 开头/](https://www.geeksforgeeks.org/generate-a-bitonic-array-starting-with-n-and-adjacent-difference-of-k/)

给定两个整数 **N** 和 **K** ，任务是生成一个双离子数组，其中第一个元素是 N，每个元素都是 K 的差。
**示例:**

> **输入:** N = 10，K = 5
> **输出:** 10 5 0 5 10
> **输入:** N = 16，K = 5
> **输出:** 16 11 6 1 -4 1 6 11 16

**方法:**思路是用[递归](https://www.geeksforgeeks.org/recursion/)来解决这个问题。如问题所述，双离子阵列的第一个元素是 **N** 。因此，将其追加到数组中并求解 n。下面是递归函数定义:

*   **基本情况:**当 N 的值小于等于 0 时，那么返回 1，因为现在值会增加。
*   **递归情况:**如果 N 的值大于，那么追加 N–K，递归调用 N–K，最后追加 N

以下是上述方法的实现:

## C++

```
// C++ implementation to generate a
// Bitonic array where consecutive
// elements are at difference of K

#include <bits/stdc++.h>
using namespace std;

// Recursive function to generate a
// Bitonic array where consecutive
// elements are at the difference of K
int decreseq(int n, int k)
{
    // Recursively call until N > 0
    if (n > 0) {

        // Print decreasing sequence
        cout << n - k << " ";
        decreseq(n - k, k);
    }

    // if N less than 0 then
    // particular function return 1
    if (n <= 0)
        return 1;

    // Print increasing sequence
    cout << n << " ";
    return 1;
}

// Driver Code
int main()
{
    int n = 10, k = 5;
    cout << n << " ";
    decreseq(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to generate a
// Bitonic array where consecutive
// elements are at difference of K
import java.util.*;
class GFG{

// Recursive function to generate a
// Bitonic array where consecutive
// elements are at the difference of K
static int decreseq(int n, int k)
{
    // Recursively call until N > 0
    if (n > 0)
    {

        // Print decreasing sequence
        System.out.print(n - k + " ");
        decreseq(n - k, k);
    }

    // if N less than 0 then
    // particular function return 1
    if (n <= 0)
        return 1;

    // Print increasing sequence
    System.out.print(n + " ");
    return 1;
}

// Driver Code
public static void main(String[] args)
{
    int n = 10, k = 5;
    System.out.print(n+ " ");
    decreseq(n, k);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to generate a
# Bitonic array where consecutive
# elements are at difference of K

# Recursive function to generate a
# Bitonic array where consecutive
# elements are at the difference of K
def decreseq(n, k):

    # Recursively call until N > 0
    if (n > 0):

        # Print decreasing sequence
        print(n - k, end = " ");
        decreseq(n - k, k);

    # if N less than 0 then
    # particular function return 1
    if (n <= 0):
        return 1;

    # Print increasing sequence
    print(n, end = " ");
    return 1;

# Driver Code
n = 10; k = 5;
print(n, end = " ");
decreseq(n, k);

# This code is contributed by Code_Mech
```

## C#

```
// C# implementation to generate a
// Bitonic array where consecutive
// elements are at difference of K
using System;

class GFG{

// Recursive function to generate a
// Bitonic array where consecutive
// elements are at the difference of K
static int decreseq(int n, int k)
{

    // Recursively call until N > 0
    if (n > 0)
    {

        // Print decreasing sequence
        Console.Write(n - k + " ");
        decreseq(n - k, k);
    }

    // If N less than 0 then
    // particular function return 1
    if (n <= 0)
        return 1;

    // Print increasing sequence
    Console.Write(n + " ");
    return 1;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 10, k = 5;

    Console.Write(n + " ");

    decreseq(n, k);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript implementation to generate a
// Bitonic array where consecutive
// elements are at difference of K

// Recursive function to generate a
// Bitonic array where consecutive
// elements are at the difference of K
function decreseq(n, k)
{
    // Recursively call until N > 0
    if (n > 0) {

        // Print decreasing sequence
        document.write( n - k + " ");
        decreseq(n - k, k);
    }

    // if N less than 0 then
    // particular function return 1
    if (n <= 0)
        return 1;

    // Print increasing sequence
    document.write( n + " ");
    return 1;
}

// Driver Code
var n = 10, k = 5;
document.write( n + " ");
decreseq(n, k);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
10 5 0 5 10
```