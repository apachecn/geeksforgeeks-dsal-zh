# 检查数组是否是从 1 到 N 的数字排列

> 原文:[https://www . geeksforgeeks . org/check-if-a-array-a-numbers-从 1 到 n 的排列/](https://www.geeksforgeeks.org/check-if-an-array-is-a-permutation-of-numbers-from-1-to-n/)

给定一个包含正整数 **N** 的数组 **arr** ，任务是检查给定的数组 arr 是否代表一个排列。

> 一个 N 个整数的序列，如果它包含从 1 到 N 的所有整数恰好一次，就叫做置换。

**例:**

> **输入:** arr[] = {1，2，5，3，2}
> **输出:**否
> **说明:**
> 给定的数组不是 1 到 N 的数字排列，因为它包含 2 两次，数组中缺少 4 表示长度为 5 的排列。
> **输入:** arr[] = {1，2，5，3，4}
> **输出:**是
> **说明:**
> 给定数组包含 1 到 5 的所有整数正好一次。因此，它代表长度为 5 的排列。

**天真方法:**显然，给定的数组将只表示长度为 N 的排列，其中 N 是数组的长度。所以我们必须在给定的数组中搜索从 1 到 N 的每个元素。如果所有的元素都找到了，那么这个数组就代表了一个置换，否则就不存在了。
***时间复杂度:** O(N <sup>2</sup> )*
**高效方法:**
上述方法可以使用[集合数据结构](https://www.geeksforgeeks.org/set-in-cpp-stl/)进行优化。

1.  遍历给定的数组，并在集合数据结构中插入每个元素。
2.  还有，[求数组中最大的元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)。这个最大元素将是代表集合大小的 N 值。
3.  遍历数组后，检查集合的大小是否等于 n。
4.  如果集合的大小等于 N，那么这个数组代表一个置换，否则它不代表。

**以下是上述方法的实施:**

## C++

```
// C++ Program to decide if an
// array represents a permutation or not

#include <bits/stdc++.h>
using namespace std;

// Function to check if an
// array represents a permutation or not
bool permutation(int arr[], int n)
{
    // Set to check the count
    // of non-repeating elements
    set<int> hash;

    int maxEle = 0;

    for (int i = 0; i < n; i++) {

        // Insert all elements in the set
        hash.insert(arr[i]);

        // Calculating the max element
        maxEle = max(maxEle, arr[i]);
    }

    if (maxEle != n)
        return false;

    // Check if set size is equal to n
    if (hash.size() == n)
        return true;

    return false;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 5, 3, 2 };
    int n = sizeof(arr) / sizeof(int);

    if (permutation(arr, n))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to decide if an
// array represents a permutation or not
import java.util.*;

class GFG{

// Function to check if an
// array represents a permutation or not
static boolean permutation(int []arr, int n)
{
    // Set to check the count
    // of non-repeating elements
    Set<Integer> hash = new HashSet<Integer>();

    int maxEle = 0;

    for (int i = 0; i < n; i++) {

        // Insert all elements in the set
        hash.add(arr[i]);

        // Calculating the max element
        maxEle = Math.max(maxEle, arr[i]);
    }

    if (maxEle != n)
        return false;

    // Check if set size is equal to n
    if (hash.size() == n)
        return true;

    return false;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 2, 5, 3, 2 };
    int n = arr.length;

    if (permutation(arr, n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 Program to decide if an
# array represents a permutation or not

# Function to check if an
# array represents a permutation or not
def permutation(arr, n):

        # Set to check the count
    # of non-repeating elements
    s = set()

    maxEle = 0;

    for i in range(n):

        # Insert all elements in the set
        s.add(arr[i]);

        # Calculating the max element
        maxEle = max(maxEle, arr[i]);

    if (maxEle != n):
        return False

    # Check if set size is equal to n
    if (len(s) == n):
        return True;

    return False;

# Driver code
if __name__=='__main__':

    arr = [ 1, 2, 5, 3, 2 ]
    n = len(arr)

    if (permutation(arr, n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by Princi Singh
```

## C#

```
// C# Program to decide if an
// array represents a permutation or not
using System;
using System.Collections.Generic;

class GFG{

// Function to check if an
// array represents a permutation or not
static bool permutation(int []arr, int n)
{
    // Set to check the count
    // of non-repeating elements
    HashSet<int> hash = new HashSet<int>();

    int maxEle = 0;

    for (int i = 0; i < n; i++) {

        // Insert all elements in the set
        hash.Add(arr[i]);

        // Calculating the max element
        maxEle = Math.Max(maxEle, arr[i]);
    }

    if (maxEle != n)
        return false;

    // Check if set size is equal to n
    if (hash.Count == n)
        return true;

    return false;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 2, 5, 3, 2 };
    int n = arr.Length;

    if (permutation(arr, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript Program to decide if an
// array represents a permutation or not

// Function to check if an
// array represents a permutation or not
function permutation(arr, n)
{
    // Set to check the count
    // of non-repeating elements
    let hash =  new Set();

    let maxEle = 0;

    for (let i = 0; i < n; i++) {

        // Insert all elements in the set
        hash.add(arr[i]);

        // Calculating the max element
        maxEle = Math.max(maxEle, arr[i]);
    }

    if (maxEle != n)
        return false;

    // Check if set size is equal to n
    if (hash.length == n)
        return true;

    return false;
}

// Driver Code

    let arr = [ 1, 2, 5, 3, 2 ];
    let n = arr.length;

    if (permutation(arr, n))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
No
```

时间复杂度:0(N)

辅助空间:O(N)