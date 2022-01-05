# 求前 N 个自然数排列中子数组的个数，使其中值为 M

> 原文:[https://www . geeksforgeeks . org/find-第一个 n 个自然数排列中的子数组数-这样它们的中值为-m/](https://www.geeksforgeeks.org/find-the-number-of-sub-arrays-in-the-permutation-of-first-n-natural-numbers-such-that-their-median-is-m/)

给定一个数组 **arr[]** ，该数组包含第一个 **N** 自然数和一个整数 **M ≤ N** 的排列。任务是找到子阵列的数量，使得序列的中值为 m。
序列的中值是以非递减顺序排序后位于序列中间的元素的值。如果序列的长度是偶数，则使用中间两个元素的左边。

**示例:**

> **输入:** a[] = { 2，4，5，3，1}，M = 4
> **输出:** 4
> 所需的子阵列为{ 2，4，5}、{4}、{4，5}和{4，5，3}。
> 
> **输入:** a[] = { 1，2，3，4，5}，M = 5
> T3】输出: 1

**方法:**分段 p[l..r]具有等于 M 的中值，当且仅当 M 属于它并且**小于** = **大于**或**小于** = **大于**–1，其中**小于**是 p[l]中的元素数量..r]严格小于 M 而**大于**的是 p[l]中的一些元素..这里我们使用了一个事实，p 是一个置换(在 p[l..r]正好有一个 M 的出现)。
换句话说，M 属于 p[l..r]，值**大于–小于**等于 0 或 1。
计算前缀和的总和[0..n]，其中 sum[i]是长度 I 的前缀上的值**大于-小于**(即子阵列 p[0..i-1])。对于固定值 r，很容易计算出 l 的个数，因此 p[l..r]是合适的。首先，检查 M 是否在[0..r]。有效值 l 是这样的索引:0 上没有 M..l-1]和 sum[l]=sum[r]或 sum[r]=sum[l]+1。
让我们为每个值保留 M 左边的多个前缀和总和[i]。我们可以用一个映射 c，其中 c[s]是一些指数 l，和[l]=s 和 l 在 m 的左边
所以，对于每个 r，p[0..r]包含 m do ans+= c[sum]+c[sum–1]，其中 sum 为当前值**大于-小于**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of sub-arrays
// in the given permutation of first n natural
// numbers such that their median is m
int segments(int n, int p[], int m)
{
    map<int, int> c;
    c[0] = 1;
    bool has = false;
    int sum = 0;
    long long ans = 0;
    for (int r = 0; r < n; r++) {

        // If element is less than m
        if (p[r] < m)
            sum--;

        // If element greater than m
        else if (p[r] > m)
            sum++;

        // If m is found
        if (p[r] == m)
            has = true;

        // Count the answer
        if (has)
            ans += c[sum] + c[sum - 1];

        // Increment sum
        else
            c[sum]++;
    }

    return ans;
}

// Driver code
int main()
{
    int a[] = { 2, 4, 5, 3, 1 };
    int n = sizeof(a) / sizeof(a[0]);
    int m = 4;
    cout << segments(n, a, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.HashMap;

class GFG
{

    // Function to return the count of sub-arrays
    // in the given permutation of first n natural
    // numbers such that their median is m
    public static int segments(int n, int[] p, int m)
    {
        HashMap<Integer, Integer> c = new HashMap<>();
        c.put(0, 1);
        boolean has = false;
        int sum = 0;
        int ans = 0;
        for (int r = 0; r < n; r++)
        {

            // If element is less than m
            if (p[r] < m)
                sum--;

            // If element greater than m
            else if (p[r] > m)
                sum++;

            // If m is found
            if (p[r] == m)
                has = true;

            // Count the answer
            if (has)
                ans += (c.get(sum) == null ? 0 :
                        c.get(sum)) +
                       (c.get(sum - 1) == null ? 0 :
                        c.get(sum - 1));

            // Increment sum
            else
                c.put(sum, c.get(sum) == null ? 1 :
                           c.get(sum) + 1);
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] a = { 2, 4, 5, 3, 1 };
        int n = a.length;
        int m = 4;
        System.out.println(segments(n, a, m));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of sub-arrays
# in the given permutation of first n natural
# numbers such that their median is m
def segments(n, p, m):

    c = dict()

    c[0] = 1

    has = False

    Sum = 0

    ans = 0

    for r in range(n):

        # If element is less than m
        if (p[r] < m):
            Sum -= 1

        # If element greater than m
        elif (p[r] > m):
            Sum += 1

        # If m is found
        if (p[r] == m):
            has = True

        # Count the answer
        if (has):
            if(Sum in c.keys()):
                ans += c[Sum]
            if Sum-1 in c.keys():
                ans += c[Sum - 1]

        # Increment Sum
        else:
            c[Sum] = c.get(Sum, 0) + 1

    return ans

# Driver code
a = [2, 4, 5, 3, 1]
n = len(a)
m = 4
print(segments(n, a, m))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;            

class GFG
{

    // Function to return the count of sub-arrays
    // in the given permutation of first n natural
    // numbers such that their median is m
    public static int segments(int n, int[] p, int m)
    {
        Dictionary<int, int> c = new Dictionary<int, int>();
        c.Add(0, 1);
        bool has = false;
        int sum = 0;
        int ans = 0;
        for (int r = 0; r < n; r++)
        {

            // If element is less than m
            if (p[r] < m)
                sum--;

            // If element greater than m
            else if (p[r] > m)
                sum++;

            // If m is found
            if (p[r] == m)
                has = true;

            // Count the answer
            if (has)
                ans += (!c.ContainsKey(sum) ? 0 :
                         c[sum]) +
                    (!c.ContainsKey(sum - 1) ? 0 :
                      c[sum - 1]);

            // Increment sum
            else
                c.Add(sum, !c.ContainsKey(sum) ? 1 :
                            c[sum] + 1);
        }
        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] a = { 2, 4, 5, 3, 1 };
        int n = a.Length;
        int m = 4;
        Console.WriteLine(segments(n, a, m));
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of sub-arrays
// in the given permutation of first n natural
// numbers such that their median is m
function segments($n, $p, $m)
{
    $c = array();
    $c[0] = 1;

    $has = false;
    $sum = 0;
    $ans = 0;

    for ($r = 0; $r < $n; $r++)
    {

        // If element is less than m
        if ($p[$r] < $m)
            $sum--;

        // If element greater than m
        else if ($p[$r] > $m)
            $sum++;

        // If m is found
        if ($p[$r] == $m)
            $has = true;

        // Count the answer
        if ($has)
            $ans += $c[$sum] + $c[$sum - 1];

        // Increment sum
        else
            $c[$sum]++;
    }

    return $ans;
}

// Driver code
$a = array( 2, 4, 5, 3, 1 );
$n = count($a);
$m = 4;

echo segments($n, $a, $m);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function to return the count of sub-arrays
// in the given permutation of first n natural
// numbers such that their median is m
function segments(n, p, m)
{
    var c = new Map();
    c.set(0,1);
    var hs = false;
    var sum = 0;
    var ans = 0;
    var r;
    for (r = 0; r < n; r++) {

        // If element is less than m
        if (p[r] < m)
            sum--;

        // If element greater than m
        else if (p[r] > m)
            sum++;

        // If m is found
        if (p[r] == m)
            hs = true;

        // Count the answer
        if (hs){
            if(c.has(sum) && c.has(sum-1))
              ans += c.get(sum) + c.get(sum - 1);
            else if(c.has(sum))
              ans += c.get(sum);
            else if(c.has(sum-1))
             ans += c.get(sum-1);
        }

        // Increment sum
        else{
            if(c.has(sum))
             c.set(sum,c.get(sum)+1);
            else
              c.set(sum,1);
        }
    }

    return ans;
}

// Driver code

    var a = [2, 4, 5, 3, 1];
    var n = a.length;
    var m = 4;
    document.write(segments(n, a, m));

</script>
```

**Output:** 

```
4
```