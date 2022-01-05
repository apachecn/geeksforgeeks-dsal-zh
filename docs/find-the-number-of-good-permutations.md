# 找出好排列的数量

> 原文:[https://www . geeksforgeeks . org/find-好排列的数量/](https://www.geeksforgeeks.org/find-the-number-of-good-permutations/)

给定两个整数 **N** 和 **K** 。任务是找到第一个 **N** 自然数的好排列的数量。如果至少存在**N–K**索引 **i** (1 ≤ i ≤ N)，使得 **P <sub>i</sub> = i** ，则该排列被称为良好。

**示例:**

> **输入:** N = 4，K = 1
> **输出:** 1
> {1，2，3，4}是唯一可能的好排列。
> 
> **输入:** N = 5，K = 2
> T3】输出: 11

**方法:**我们来迭代一下 **m** ，这是指数的个数，使得**P<sub>I</sub>T7】不等于 **i** 。显然， **0 ≤ m ≤ k** 。
为了计算固定的 **m** 的排列数，我们需要选择具有属性 **P <sub>i</sub>** 不等于**I**–有**<sup>n</sup>C<sub>m</sub>**的索引，然后我们需要为选择的索引构造一个排列 **Q** ，使得对于每个选择的索引**Q**具有此属性的排列称为[排列](https://www.geeksforgeeks.org/count-derangements-permutation-such-that-no-element-appears-in-its-original-position/)，固定大小的排列数量可以通过对 **m ≤ 4** 的穷举搜索来计算。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of good permutations
int Permutations(int n, int k)
{
    // For m = 0, ans is 1
    int ans = 1;

    // If k is greater than 1
    if (k >= 2)
        ans += (n) * (n - 1) / 2;

    // If k is greater than 2
    if (k >= 3)
        ans += (n) * (n - 1) * (n - 2) * 2 / 6;

    // If k is greater than 3
    if (k >= 4)
        ans += (n) * (n - 1) * (n - 2) * (n - 3) * 9 / 24;

    return ans;
}

// Driver code
int main()
{
    int n = 5, k = 2;
    cout << Permutations(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of good permutations
static int Permutations(int n, int k)
{
    // For m = 0, ans is 1
    int ans = 1;

    // If k is greater than 1
    if (k >= 2)
        ans += (n) * (n - 1) / 2;

    // If k is greater than 2
    if (k >= 3)
        ans += (n) * (n - 1) * (n - 2) * 2 / 6;

    // If k is greater than 3
    if (k >= 4)
        ans += (n) * (n - 1) * (n - 2) * (n - 3) * 9 / 24;

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int n = 5, k = 2;
    System.out.println(Permutations(n, k));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of good permutations
def Permutations(n, k):

    # For m = 0, ans is 1
    ans = 1

    # If k is greater than 1
    if k >= 2:
        ans += (n) * (n - 1) // 2

    # If k is greater than 2
    if k >= 3:
        ans += ((n) * (n - 1) *
                (n - 2) * 2 // 6)

    # If k is greater than 3
    if k >= 4:
        ans += ((n) * (n - 1) * (n - 2) *
                      (n - 3) * 9 // 24)

    return ans

# Driver code
if __name__ == "__main__":

    n, k = 5, 2
    print(Permutations(n, k))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the above approach.
using System;

class GFG
{

// Function to return the count of good permutations
static int Permutations(int n, int k)
{
    // For m = 0, ans is 1
    int ans = 1;

    // If k is greater than 1
    if (k >= 2)
        ans += (n) * (n - 1) / 2;

    // If k is greater than 2
    if (k >= 3)
        ans += (n) * (n - 1) * (n - 2) * 2 / 6;

    // If k is greater than 3
    if (k >= 4)
        ans += (n) * (n - 1) * (n - 2) * (n - 3) * 9 / 24;

    return ans;
}

// Driver code
public static void Main()
{
    int n = 5, k = 2;
    Console.WriteLine(Permutations(n, k));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count
// of good permutations
function Permutations($n, $k)
{
    // For m = 0, ans is 1
    $ans = 1;

    // If k is greater than 1
    if ($k >= 2)
        $ans += ($n) * ($n - 1) / 2;

    // If k is greater than 2
    if ($k >= 3)
        $ans += ($n) * ($n - 1) *
                       ($n - 2) * 2 / 6;

    // If k is greater than 3
    if ($k >= 4)
        $ans += ($n) * ($n - 1) * ($n - 2) *
                       ($n - 3) * 9 / 24;

    return $ans;
}

// Driver code
$n = 5; $k = 2;
echo(Permutations($n, $k));

// This code contributed by Code_Mech.
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the count of good permutations
function Permutations(n, k)
{

    // For m = 0, ans is 1
    var ans = 1;

    // If k is greater than 1
    if (k >= 2)
        ans += (n) * (n - 1) / 2;

    // If k is greater than 2
    if (k >= 3)
        ans += (n) * (n - 1) *
           (n - 2) * 2 / 6;

    // If k is greater than 3
    if (k >= 4)
        ans += (n) * (n - 1) * (n - 2) *
                     (n - 3) * 9 / 24;

    return ans;
}

// Driver Code
var n = 5, k = 2;
document.write(Permutations(n, k));

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
11
```