# 查找最大子集的大小，按位“与”大于它们的按位“异或”

> 原文:[https://www . geeksforgeeks . org/find-最大子集大小按位异或/](https://www.geeksforgeeks.org/find-size-of-largest-subset-with-bitwise-and-greater-than-their-bitwise-xor/)

给定 N 个整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到最大子集的大小，使得子集的所有元素的[按位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)大于子集的所有元素的[按位“异或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 2
> **解释:**子集{2，3}所有元素的按位“与”为 2，而所有元素的按位“异或”为 1。因此，按位“与”>按位“异或”。因此，子集所需的大小是 2，这是最大可能的大小。另一个有效子集的例子是{4，5}。
> 
> **输入:** arr[] = {24，20，18，17，16 }
> T3】输出: 4

**方法:**给定的问题可以通过[使用](https://www.geeksforgeeks.org/print-subsets-given-size-set/)[递归方法](https://www.geeksforgeeks.org/recursion/)生成给定集合的所有可能的子集并保持每个子集的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)和[位“异或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的值来解决。所需的答案将是子集的最大大小，以便按位“与”>按位“异或”。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to iterate over all
// the subsets of the given array and return
// the maximum size of subset such that the
// bitwise AND > bitwise OR of all elements
int maxSizeSubset(
    int* arr, int N, int bitwiseXOR,
    int bitwiseAND, int i, int len = 0)
{
    // Stores the maximum length of subset
    int ans = INT_MIN;

    // Update ans
    if (bitwiseAND > bitwiseXOR) {
        ans = len;
    }

    // Base Case
    if (i == N) {
        return ans;
    }

    // Recursive call excluding the
    // ith element of the given array
    ans = max(ans, maxSizeSubset(
                       arr, N, bitwiseXOR,
                       bitwiseAND, i + 1, len));

    // Recursive call including the ith element
    // of the given array
    ans = max(ans,
              maxSizeSubset(
                  arr, N,
                  (arr[i] ^ bitwiseXOR),
                  (arr[i] & bitwiseAND), i + 1,
                  len + 1));

    // Return Answer
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 24, 20, 18, 17, 16 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxSizeSubset(
        arr, N, 0,
        pow(2, 10) - 1, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG {

// Recursive function to iterate over all
// the subsets of the given array and return
// the maximum size of subset such that the
// bitwise AND > bitwise OR of all elements
static int maxSizeSubset(
    int[] arr, int N, int bitwiseXOR,
    int bitwiseAND, int i, int len)
{

    // Stores the maximum length of subset
    int ans = Integer.MIN_VALUE;

    // Update ans
    if (bitwiseAND > bitwiseXOR) {
        ans = len;
    }

    // Base Case
    if (i == N) {
        return ans;
    }

    // Recursive call excluding the
    // ith element of the given array
    ans = Math.max(ans, maxSizeSubset(
                       arr, N, bitwiseXOR,
                       bitwiseAND, i + 1, len));

    // Recursive call including the ith element
    // of the given array
    ans = Math.max(ans,
              maxSizeSubset(
                  arr, N,
                  (arr[i] ^ bitwiseXOR),
                  (arr[i] & bitwiseAND), i + 1,
                  len + 1));

    // Return Answer
    return ans;
}

// Driver Code
public static void main (String[] args) {

    int arr[] = { 24, 20, 18, 17, 16 };
    int N = arr.length;

    System.out.println(maxSizeSubset(arr, N, 0, (int)Math.pow(2, 10) - 1, 0, 0));
}
}

// This code is contributed by target_2.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach
import sys

# Recursive function to iterate over all
# the subsets of the given array and return
# the maximum size of subset such that the
# bitwise AND > bitwise OR of all elements
def maxSizeSubset(arr, N, bitwiseXOR,
                    bitwiseAND, i, len) :

    # Stores the maximum length of subset
    ans = -sys.maxsize - 1

    # Update ans
    if (bitwiseAND > bitwiseXOR) :
        ans = len

    # Base Case
    if (i == N) :
        return ans

    # Recursive call excluding the
    # ith element of the given array
    ans = max(ans, maxSizeSubset(
                       arr, N, bitwiseXOR,
                       bitwiseAND, i + 1, len))

    # Recursive call including the ith element
    # of the given array
    ans = max(ans,
              maxSizeSubset(
                  arr, N,
                  (arr[i] ^ bitwiseXOR),
                  (arr[i] & bitwiseAND), i + 1,
                  len + 1))

    # Return Answer
    return ans

# Driver Code

arr = [ 24, 20, 18, 17, 16 ]
N = len(arr)

print(maxSizeSubset(arr, N, 0,
            pow(2, 10) - 1, 0, 0))

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

// Recursive function to iterate over all
// the subsets of the given array and return
// the maximum size of subset such that the
// bitwise AND > bitwise OR of all elements
static int maxSizeSubset(
    int []arr, int N, int bitwiseXOR,
    int bitwiseAND, int i, int len)
{

    // Stores the maximum length of subset
    int ans = Int32.MinValue;

    // Update ans
    if (bitwiseAND > bitwiseXOR) {
        ans = len;
    }

    // Base Case
    if (i == N) {
        return ans;
    }

    // Recursive call excluding the
    // ith element of the given array
    ans = Math.Max(ans, maxSizeSubset(
                       arr, N, bitwiseXOR,
                       bitwiseAND, i + 1, len));

    // Recursive call including the ith element
    // of the given array
    ans = Math.Max(ans,
              maxSizeSubset(
                  arr, N,
                  (arr[i] ^ bitwiseXOR),
                  (arr[i] & bitwiseAND), i + 1,
                  len + 1));

    // Return Answer
    return ans;
}

// Driver Code
public static void Main () {

    int []arr = { 24, 20, 18, 17, 16 };
    int N = arr.Length;

    Console.Write(maxSizeSubset(arr, N, 0, (int)Math.Pow(2, 10) - 1, 0, 0));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach

       // Recursive function to iterate over all
       // the subsets of the given array and return
       // the maximum size of subset such that the
       // bitwise AND > bitwise OR of all elements
       function maxSizeSubset(
           arr, N, bitwiseXOR,
           bitwiseAND, i, len = 0)
      {
           // Stores the maximum length of subset
           let ans = Number.MIN_VALUE;

           // Update ans
           if (bitwiseAND > bitwiseXOR) {
               ans = len;
           }

           // Base Case
           if (i == N) {
               return ans;
           }

           // Recursive call excluding the
           // ith element of the given array
           ans = Math.max(ans, maxSizeSubset(
               arr, N, bitwiseXOR,
               bitwiseAND, i + 1, len));

           // Recursive call including the ith element
           // of the given array
           ans = Math.max(ans,
               maxSizeSubset(
                   arr, N,
                   (arr[i] ^ bitwiseXOR),
                   (arr[i] & bitwiseAND), i + 1,
                   len + 1));

           // Return Answer
           return ans;
       }

       // Driver Code
       let arr = [24, 20, 18, 17, 16];
       let N = arr.length;

       document.write(maxSizeSubset(
           arr, N, 0,
           Math.pow(2, 10) - 1, 0))

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
4
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*