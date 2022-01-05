# 计算一个数组中 K 位不同的所有对

> 原文:[https://www . geesforgeks . org/count-所有 k 位不同的数组对/](https://www.geeksforgeeks.org/count-all-pairs-of-an-array-which-differ-in-k-bits/)

给定一个大小为 n 和整数 K 的数组，计算数组中两个数的二进制表示的正好 K 位不同的所有对。
输入数组中的元素值很小，重复次数可能很多。
**例:**

```
Input: arr[] = {2, 4, 1, 3, 1}
       k = 2       
Output: 5
Explanation:
There are only 4 pairs which differs in 
exactly 2 bits of binary representation:
(2, 4), (1, 2) [Two times] and (4, 1)
[Two times]

Input  : arr[] = {2, 1, 2, 1}
         k = 2
Output :  4
```

We strongly recommend that you click here and practice it, before moving on to the solution.

**天真的方法**

一个蛮力是运行两个循环，一个在另一个内部，然后逐个选择对，并对两个元素进行 XOR。XORed 值的结果包含一组在两个元素中不同的位。现在，我们只需要对总集比特进行计数，以便将其与值 k 进行比较。下面是上述方法的实现:

## C++

```
// C++ program to count all pairs with bit difference
// as k
#include<bits/stdc++.h>
using namespace std;

// Utility function to count total ones in a number
int bitCount(int n)
{
    int count = 0;
    while (n)
    {
        if (n & 1)
            ++count;
        n >>= 1;
    }
    return count;
}

// Function to count pairs of K different bits
long long countPairsWithKDiff(int arr[], int n, int k)
{
    long long ans = 0; // initialize final answer

    for (int i = 0; i < n-1; ++i)
    {
        for (int j = i + 1; j < n; ++j)
        {
            int xoredNum = arr[i] ^ arr[j];

            // Check for K differ bit
            if (k == bitCount(xoredNum))
                ++ans;
        }
    }
    return ans;
}

// Driver code
int main()
{
    int k = 2;
    int arr[] = {2, 4, 1, 3, 1};
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << "Total pairs for k = " << k << " are "
         << countPairsWithKDiff(arr, n, k) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all pairs with bit difference
// as k

import java.io.*;

class GFG {

// Utility function to count total ones in a number
static int bitCount(int n)
{
    int count = 0;
    while (n>0)
    {
        if ((n & 1)>0)
            ++count;
        n >>= 1;
    }
    return count;
}

// Function to count pairs of K different bits
static long countPairsWithKDiff(int arr[], int n, int k)
{
    long  ans = 0; // initialize final answer

    for (int i = 0; i < n-1; ++i)
    {
        for (int j = i + 1; j < n; ++j)
        {
            int xoredNum = arr[i] ^ arr[j];

            // Check for K differ bit
            if (k == bitCount(xoredNum))
                ++ans;
        }
    }
    return ans;
}

// Driver code

    public static void main (String[] args) {
            int k = 2;
    int arr[] = {2, 4, 1, 3, 1};
    int n =arr.length;

    System.out.println( "Total pairs for k = " + k + " are "
        + countPairsWithKDiff(arr, n, k) + "\n");
    }
}
// This code is contributed by shs..
```

## 蟒蛇 3

```
# Python 3 program to count all pairs
# with bit difference as k

# Utility function to count total
# ones in a number
def bitCount(n):
    count = 0
    while (n):
        if (n & 1):
            count += 1
        n >>= 1

    return count

# Function to count pairs of K different bits
def countPairsWithKDiff(arr, n, k):
    ans = 0

    # initialize final answer
    for i in range(0, n - 1, 1):
        for j in range(i + 1, n, 1):
            xoredNum = arr[i] ^ arr[j]

            # Check for K differ bit
            if (k == bitCount(xoredNum)):
                ans += 1

    return ans

# Driver code
if __name__ == '__main__':
    k = 2
    arr = [2, 4, 1, 3, 1]
    n = len(arr)

    print("Total pairs for k =", k, "are",
           countPairsWithKDiff(arr, n, k))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to count all pairs
// with bit difference as k
using System;

class GFG
{

// Utility function to count
// total ones in a number
static int bitCount(int n)
{
    int count = 0;
    while (n > 0)
    {
        if ((n & 1) > 0)
            ++count;
        n >>= 1;
    }
    return count;
}

// Function to count pairs of K different bits
static long countPairsWithKDiff(int []arr,
                                int n, int k)
{
    long ans = 0; // initialize final answer

    for (int i = 0; i < n-1; ++i)
    {
        for (int j = i + 1; j < n; ++j)
        {
            int xoredNum = arr[i] ^ arr[j];

            // Check for K differ bit
            if (k == bitCount(xoredNum))
                ++ans;
        }
    }
    return ans;
}

// Driver code
public static void Main ()
{
    int k = 2;
    int []arr = {2, 4, 1, 3, 1};
    int n = arr.Length;

    Console.WriteLine( "Total pairs for k = " +
                                  k + " are " +
        countPairsWithKDiff(arr, n, k) + "\n");
}
}

// This code is contributed by shs..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count all
// pairs with bit difference
// as k

// Utility function to count
// total ones in a number
function bitCount($n)
{
    $count = 0;
    while ($n)
    {
        if ($n & 1)
            ++$count;
        $n >>= 1;
    }
    return $count;
}

// Function to count pairs
// of K different bits
function countPairsWithKDiff($arr, $n, $k)
{

    // initialize final answer
    $ans = 0;

    for ($i = 0; $i < $n-1; ++$i)
    {
        for ($j = $i + 1; $j < $n; ++$j)
        {
            $xoredNum = $arr[$i] ^ $arr[$j];

            // Check for K differ bit
            if ($k == bitCount($xoredNum))
                ++$ans;
        }
    }
    return $ans;
}

    // Driver code
    $k = 2;
    $arr = array(2, 4, 1, 3, 1);
    $n = count($arr);

    echo "Total pairs for k = " , $k , " are "
        , countPairsWithKDiff($arr, $n, $k) , "\n";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to count all pairs with bit difference
// as k

// Utility function to count total ones in a number
function bitCount(n)
{
    let count = 0;
    while (n>0)
    {
        if ((n & 1)>0)
            ++count;
        n >>= 1;
    }
    return count;
}

// Function to count pairs of K different bits
function countPairsWithKDiff(arr, n, k)
{
    let  ans = 0; // initialize final answer

    for (let i = 0; i < n-1; ++i)
    {
        for (let j = i + 1; j < n; ++j)
        {
            let xoredNum = arr[i] ^ arr[j];

            // Check for K differ bit
            if (k == bitCount(xoredNum))
                ++ans;
        }
    }
    return ans;
}

// Driver Code
    let k = 2;
    let arr = [2, 4, 1, 3, 1];
    let n = arr.length;

    document.write( "Total pairs for k = " + k + " are "
        + countPairsWithKDiff(arr, n, k) + "\n");

</script>
```

**输出:**

```
Total pairs for k = 2 are 5
```

**时间复杂度:** O(N <sup>2</sup> * log MAX)，其中 MAX 为输入数组中最大元素。
**辅助空间:** O(1)

**高效方法**

这种方法对于输入数组有小元素和可能有很多重复的情况是有效的。想法是从 0 迭代到 max(arr[i])，对于每一对(I，j)，检查(i ^ j)中的设置位数，并将其与 k 进行比较。我们可以使用 gcc 的内置函数(_builtin_popcount)或预先计算这样的数组，以使检查更快。如果 i ^ j 中的 1 的数目等于 k，那么我们将把 I 和 j 的总数相加

## C++

```
// Below is C++ approach of finding total k bit
// difference pairs
#include<bits/stdc++.h>
using namespace std;

// Function to calculate K bit different pairs in array
long long kBitDifferencePairs(int arr[], int n, int k)
{
    // Get the maximum value among all array elements
    int MAX = *max_element(arr, arr+n);

    // Set the count array to 0, count[] stores the
    // total frequency of array elements
    long long count[MAX+1];
    memset(count, 0, sizeof(count));

    for (int i=0; i < n; ++i)
        ++count[arr[i]];

    // Initialize result
    long long ans = 0;

    // For 0 bit answer will be total count of same number
    if (k == 0)
    {
        for (int i = 0; i <= MAX; ++i)
            ans += (count[i] * (count[i] - 1)) / 2;

        return ans;
    }

    for (int i = 0; i <= MAX; ++i)
    {
        // if count[i] is 0, skip the next loop as it
        // will not contribute the answer
        if (!count[i])
           continue;

        for (int j = i + 1; j <= MAX; ++j)
        {
            //Update answer if k differ bit found
            if ( __builtin_popcount(i ^ j) == k)
                ans += count[i] * count[j];
        }
    }
    return ans;
}

// Driver code
int main()
{
    int k = 2;
    int arr[] = {2, 4, 1, 3, 1};
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << "Total pairs for k = " << k << " are = "
         << kBitDifferencePairs(arr, n, k) << "\n";

    k = 3;
    cout << "Total pairs for k = " << k << " are = "
         << kBitDifferencePairs(arr, n, k) ;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Below is Java approach of finding total k bit
// difference pairs
import java.util.*;

class GFG
{

// Function to calculate K bit
// different pairs in array
static long kBitDifferencePairs(int arr[],
                                int n, int k)
{
    // Get the maximum value among all array elements
    int MAX = Arrays.stream(arr).max().getAsInt();

    // Set the count array to 0,
    // count[] stores the total
    // frequency of array elements
    long []count = new long[MAX + 1];
    Arrays.fill(count, 0);

    for (int i = 0; i < n; ++i)
        ++count[arr[i]];

    // Initialize result
    long ans = 0;

    // For 0 bit answer will be total
    // count of same number
    if (k == 0)
    {
        for (int i = 0; i <= MAX; ++i)
            ans += (count[i] * (count[i] - 1)) / 2;

        return ans;
    }

    for (int i = 0; i <= MAX; ++i)
    {
        // if count[i] is 0, skip the next loop
        // as it will not contribute the answer
        if (count[i] == 0)
        continue;

        for (int j = i + 1; j <= MAX; ++j)
        {
            // Update answer if k differ bit found
            if ( Integer.bitCount(i ^ j) == k)
                ans += count[i] * count[j];
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int k = 2;
    int arr[] = {2, 4, 1, 3, 1};
    int n = arr.length;

    System.out.println("Total pairs for k = " +
                                k + " are = " +
                        kBitDifferencePairs(arr, n, k));

    k = 3;
    System.out.println("Total pairs for k = " +
                                k + " are = " +
                        kBitDifferencePairs(arr, n, k));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Below is Python3 approach of finding
# total k bit difference pairs

# Function to calculate K bit different
# pairs in array
def kBitDifferencePairs(arr, n, k):

    # Get the maximum value among
    # all array elements
    MAX = max(arr)

    # Set the count array to 0, count[] stores
    # the total frequency of array elements
    count = [0 for i in range(MAX + 1)]

    for i in range(n):
        count[arr[i]] += 1

    # Initialize result
    ans = 0

    # For 0 bit answer will be total
    # count of same number
    if (k == 0):
        for i in range(MAX + 1):
            ans += (count[i] * (count[i] - 1)) // 2

        return ans

    for i in range(MAX + 1):

        # if count[i] is 0, skip the next loop
        # as it will not contribute the answer
        if (count[i] == 0):
            continue

        for j in range(i + 1, MAX + 1):

            # Update answer if k differ bit found
            if (bin(i ^ j).count('1') == k):
                ans += count[i] * count[j]

    return ans

# Driver code
k = 2
arr = [2, 4, 1, 3, 1]
n = len(arr)

print("Total pairs for k =", k, "are",
       kBitDifferencePairs(arr, n, k))

k = 3
print("Total pairs for k =", k, "are",
       kBitDifferencePairs(arr, n, k))

# This code is contributed by mohit kumar
```

## C#

```
// Below is C# approach of finding
// total k bit difference pairs
using System;
using System.Linq;

class GFG
{

// Function to calculate K bit
// different pairs in array
static long kBitDifferencePairs(int []arr,
                                int n, int k)
{
    // Get the maximum value among
    // all array elements
    int MAX = arr.Max();

    // Set the count array to 0,
    // count[] stores the total
    // frequency of array elements
    long []count = new long[MAX + 1];

    for (int i = 0; i < n; ++i)
        ++count[arr[i]];

    // Initialize result
    long ans = 0;

    // For 0 bit answer will be total
    // count of same number
    if (k == 0)
    {
        for (int i = 0; i <= MAX; ++i)
            ans += (count[i] * 
                   (count[i] - 1)) / 2;

        return ans;
    }

    for (int i = 0; i <= MAX; ++i)
    {
        // if count[i] is 0, skip the next loop
        // as it will not contribute the answer
        if (count[i] == 0)
        continue;

        for (int j = i + 1; j <= MAX; ++j)
        {
            // Update answer if k differ bit found
            if (BitCount(i ^ j) == k)
                ans += count[i] * count[j];
        }
    }
    return ans;
}

static int BitCount(int n)
{
    int count = 0;
    while (n > 0)
    {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Driver code
public static void Main(String[] args)
{
    int k = 2;
    int []arr = {2, 4, 1, 3, 1};
    int n = arr.Length;

    Console.WriteLine("Total pairs for k = " +
                               k + " are = " +
                       kBitDifferencePairs(arr, n, k));

    k = 3;
    Console.WriteLine("Total pairs for k = " +
                               k + " are = " +
                       kBitDifferencePairs(arr, n, k));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Below is Javascript approach
// of finding total k bit
// difference pairs

// Function to calculate K bit
// different pairs in array
function kBitDifferencePairs(arr, n, k)
{
    // Get the maximum value among
    // all array elements
    let MAX = Math.max(...arr);

    // Set the count array to 0, count[] stores the
    // total frequency of array elements
    let count = new Array(MAX+1).fill(0);

    for (let i=0; i < n; ++i)
        ++count[arr[i]];

    // Initialize result
    let ans = 0;

    // For 0 bit answer will be total
    // count of same number
    if (k == 0)
    {
        for (let i = 0; i <= MAX; ++i)
            ans += parseInt((count[i] *
            (count[i] - 1)) / 2);

        return ans;
    }

    for (let i = 0; i <= MAX; ++i)
    {
        // if count[i] is 0, skip
        // the next loop as it
        // will not contribute the answer
        if (!count[i])
           continue;

        for (let j = i + 1; j <= MAX; ++j)
        {
            //Update answer if k differ bit found
            if ( BitCount(i ^ j) == k)
                ans += count[i] * count[j];
        }
    }
    return ans;
}

function BitCount(n)
{
    let count = 0;
    while (n > 0)
    {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Driver code
    let k = 2;
    let arr = [2, 4, 1, 3, 1];
    let n = arr.length;

    document.write("Total pairs for k = " + k + " are = "
         + kBitDifferencePairs(arr, n, k) + "<br>");

    k = 3;
    document.write("Total pairs for k = " + k + " are = "
         + kBitDifferencePairs(arr, n, k) + "<br>");

</script>
```

**输出:**

```
Total pairs for k = 2 are = 5
```

**时间复杂度:** O(MAX <sup>2</sup> )，其中 MAX 为输入数组中的最大元素。
**辅助空间:** O(MAX)
本文由 [Shubham Bansal](https://www.facebook.com/banalshubham) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。