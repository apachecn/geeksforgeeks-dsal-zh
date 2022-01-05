# 选择一个整数的方法的数量，使得在给定的数组中正好有 K 个大于它的元素

> 原文:[https://www . geeksforgeeks . org/选择整数的方法数，以便在给定数组中有恰好大于它的 k 个元素/](https://www.geeksforgeeks.org/number-of-ways-to-choose-an-integer-such-that-there-are-exactly-k-elements-greater-than-it-in-the-given-array/)

给定一个由 **N** 元素和一个整数 **K** 组成的数组**arr【】**，任务是找到选择整数 **X** 的方法数量，使得数组中正好有大于 **X** 的 **K** 元素。
**示例:**

> **输入:** arr[] = {1，3，4，6，8}，K = 2
> **输出:** 2
> X 可以选择为 4 或 5
> **输入:** arr[] = {1，1，1}，K = 2
> **输出:** 0
> 无论您选择哪个整数作为 X，它在给定数组中永远不会有恰好 2 个大于它的元素。

**方法:**
我们计算数组中不同元素的总数。如果不同元素的计数小于或等于 k，那么 0 置换是可能的。否则计数等于不同元素的数量减去 k。
下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to returns the required count of integers
int countWays(int n, int arr[], int k)
{

    if (k <= 0 || k >= n)
        return 0;

    unordered_set<int> s(arr, arr+n);
    if (s.size() <= k)
       return 0;

    // Return the required count
    return s.size() - k;
}

// Driver code
int main()
{
    int arr[] = { 100, 200, 400, 50 };
    int k = 3;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countWays(n, arr, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to returns the
// required count of integers
static int countWays(int n, int arr[], int k)
{

    if (k <= 0 || k >= n)
        return 0;
    Set<Integer> s = new HashSet<Integer>();
    for(int i = 0; i < n; i++)
        s.add(arr[i]);

    if (s.size() <= k)
        return 0;

    // Return the required count
    return s.size() - k;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 100, 200, 400, 50 };
    int k = 3;
    int n = arr.length;
    System.out.println(countWays(n, arr, k));
}
}

// This code id contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to returns the required count of integers
def countWays(n, arr, k) :

    if (k <= 0 or k >= n) :
        return 0

    s = set()
    for element in arr :
        s.add(element)

    if (len(s) <= k) :
        return 0;

    # Return the required count
    return len(s) - k;

# Driver code
if __name__ == "__main__" :

    arr = [ 100, 200, 400, 50 ]
    k = 3;
    n = len(arr) ;
    print(countWays(n, arr, k))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to returns the
    // required count of integers
    static int countWays(int n, int []arr, int k)
    {

        if (k <= 0 || k >= n)
            return 0;
        HashSet<int> s = new HashSet<int>();
        for(int i = 0; i < n; i++)
            s.Add(arr[i]);

        if (s.Count <= k)
            return 0;

        // Return the required count
        return s.Count - k;
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = { 100, 200, 400, 50 };
        int k = 3;
        int n = arr.Length;
        Console.WriteLine(countWays(n, arr, k));
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to returns the required
// count of integers
function countWays($n, $arr, $k)
{
    if ($k <= 0 || $k >= $n)
        return 0;

    $s = array();
    foreach ($arr as $value)
        array_push($s, $value);
    $s = array_unique($s);

    if (count($s) <= $k)
        return 0;

    // Return the required count
    return count($s) - $k;
}

// Driver code
$arr = array(100, 200, 400, 50);
$k = 3;
$n = count($arr);
print(countWays($n, $arr, $k));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

// Function to returns the
// required count of integers
function countWays(n, arr, k)
{

    if (k <= 0 || k >= n)
        return 0;
    let s = new Set();
    for(let i = 0; i < n; i++)
        s.add(arr[i]);

    if (s.size <= k)
        return 0;

    // Return the required count
    return s.size - k;
}

// Driver Code

    let arr = [ 100, 200, 400, 50 ];
    let k = 3;
    let n = arr.length;
    document.write(countWays(n, arr, k));

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(N * log(N))