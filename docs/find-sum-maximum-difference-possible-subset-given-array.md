# 求给定数组所有子集的最大可能差值之和。

> 原文:[https://www . geesforgeks . org/find-sum-最大差值-可能子集-给定-数组/](https://www.geeksforgeeks.org/find-sum-maximum-difference-possible-subset-given-array/)

给我们一个 n 个非负整数的数组 arr[](允许重复元素)，从给定数组的所有子集中找出最大可能差的和。
假设最大值代表任何子集的最大值，而最小值代表集合的最小值。我们需要找到所有可能子集的最大(s)-最小(s)之和。

**示例:**

```
Input : arr[] = {1, 2, 3}
Output : result = 6

Explanation : 
All possible subset and for each subset s,
max(s)-min(s) are as :
SUBSET    |  max(s) | min(s) | max(s)-min(s)
{1, 2}    |  2      |  1     |   1
{1, 3}    |  3      |  1     |   2
{2, 3}    |  3      |  2     |   1
{1, 2, 3} |  3      |  1     |   2
Total Difference sum = 6
Note : max(s) - min(s) for all subset with 
single element must be zero.

Input : arr[] = {1, 2, 2}
Output : result = 3

Explanation : 
All possible subset and for each subset s,
max(s)-min(s) are as :
  SUBSET  |  max(s) | min(s)| max(s)-min(s)
  {1, 2}  |  2      |  1    |   1
  {1, 2}  |  2      |  1    |   1
  {2, 2}  |  2      |  2    |   0
{1, 2, 2} |  2      |  1    |   1
Total Difference sum = 3
```

**基本做法:**分别计算每个子集的最大元素之和，以及每个子集的最小元素之和，然后从最大值中减去最小和，得到答案。通过迭代每个子集的元素，可以很容易地计算出每个子集的最大/最小元素之和。但是由于我们必须迭代所有子集，这种方法的时间复杂度是指数 O(n2^n).
**高效方法:**
由于我们要分别计算每个子集的最大元素之和，以及每个子集的最小元素之和，这里是执行这种计算的有效方法。
**所有子集的最小元素之和:**
假设 arr[]的元素按非递减顺序为{a1，a2，…，an}。现在，我们可以将 arr[]的子集划分为以下类别:

*   包含元素 a1 的子集:这些子集可以通过取{a2，a3，…，an}的任意子集，然后将 a1 加入其中得到。这样的子集的数量将是 2 <sup>n-1</sup> ，并且它们都有 a1 作为它们的最小元素。
*   不包含元素 a1，但包含 a2 的子集:这些子集可以通过取{a3，a4，…，an}的任意子集，然后将 a2 加入其中得到。这样的子集的数量将是 2 <sup>n-2</sup> ，并且它们都有 a2 作为它们的最小元素。
*   …..
*   不包含元素 a1，a2，…，ai-1 但包含 ai 的子集:这些子集可以通过取{ai+1，ai+2，…，an}的任意子集，然后加入 ai 得到。这样的子集的数量将是 2 <sup>n-i</sup> ，并且它们都有 ai 作为它们的最小元素。

可以看出，上述迭代是完整的，即它只考虑每个子集一次。因此，所有子集的最小元素之和将为:
min _ sum = a1 * 2<sup>n-1</sup>+a2 * 2<sup>n-2</sup>+…+an * 2<sup>0</sup>
借助[霍纳法](https://en.wikipedia.org/wiki/Horner%27s_method) …
可以在线性时间内轻松计算出该和。同样，我们可以计算出 arr[]的所有子集的最大元素之和。唯一的区别是我们需要以非递增的顺序迭代 arr[]的元素。
**注:**我们可能有一个大的答案，所以我们要用 mod 10^9 +7 来计算答案。

## C++

```
// CPP for finding max min difference
// from all subset of given set
#include <bits/stdc++.h>
using namespace std;

const long long int MOD = 1000000007;

// function for sum of max min difference 
int maxMin (int arr[], int n) 
{
    // sort all numbers
    sort(arr, arr + n);

    // iterate over array and with help of 
    // horner's rule calc max_sum and min_sum
    long long int min_sum = 0, max_sum = 0;
    for (int i = 0; i < n; i++)
    {
        max_sum = 2 * max_sum + arr[n-1-i];
        max_sum %= MOD;
        min_sum = 2 * min_sum + arr[i];
        min_sum %= MOD;
    }

    return (max_sum - min_sum + MOD) % MOD;
}

// Driver Code
int main()
{
    int arr[] = {1, 2, 3, 4};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxMin(arr,n);
    return 0;
} 
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Find the sum of maximum 
// difference possible from all subset 
// of a given array.
import java.util.*;

class GFG {

    public static int MOD = 1000000007;

    // function for sum of max min difference 
    public static long maxMin (int arr[], int n) 
    {
        // sort all numbers
        Arrays.sort(arr);

        // iterate over array and with help of 
        // horner's rule calc max_sum and min_sum
        long min_sum = 0, max_sum = 0;
        for (int i = 0; i < n; i++)
        {
            max_sum = 2 * max_sum + arr[n - 1 - i];
            max_sum %= MOD;
            min_sum = 2 * min_sum + arr[i];
            min_sum %= MOD;
        }

        return (max_sum - min_sum + MOD)%MOD;
    }

    // Driver Code
    public static void main(String[] args) 
    {
            int arr[] = {1, 2, 3, 4};
            int n = arr.length;
            System.out.println(maxMin(arr, n));
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# python for finding max min difference
#from all subset of given set

MOD = 1000000007;

# function for sum of max min difference 
def maxMin (arr,n):

    # sort all numbers
    arr.sort()

    # iterate over array and with help of 
    # horner's rule calc max_sum and min_sum
    min_sum = 0
    max_sum = 0
    for i in range(0,n):

        max_sum = 2 * max_sum + arr[n-1-i];
        max_sum %= MOD;
        min_sum = 2 * min_sum + arr[i];
        min_sum %= MOD;

    return (max_sum - min_sum + MOD) % MOD;

# Driver Code
arr = [1, 2, 3, 4]
n = len(arr)
print( maxMin(arr, n))

# This code is contributed by Sam007.
```

## C#

```

// C# Code to Find the sum of maximum 
// difference possible from all subset 
// of a given array.
using System;

class GFG {

    public static int MOD = 1000000007;

    // function for sum of max min difference 
    public static long maxMin (int []arr, int n) 
    {
        // sort all numbers
        Array.Sort(arr);

        // iterate over array and with help of 
        // horner's rule calc max_sum and min_sum
        long min_sum = 0, max_sum = 0;
        for (int i = 0; i < n; i++)
        {
            max_sum = 2 * max_sum + arr[n - 1 - i];
            max_sum %= MOD;
            min_sum = 2 * min_sum + arr[i];
            min_sum %= MOD;
        }

        return (max_sum - min_sum + MOD) % MOD;
    }

    // Driver Code
    public static void Main() 
    {
            int []arr = {1, 2, 3, 4};
            int n = arr.Length;
            Console.Write(maxMin(arr, n));    
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP for finding max min difference
// from all subset of given set
$MOD = 1000000007;

// function for sum of 
// max min difference 
function maxMin ($arr, $n) 
{
    global $MOD;

    // sort all numbers
    sort($arr);

    // iterate over array 
    // and with help of 
    // horner's rule calc 
    // max_sum and min_sum
    $min_sum = 0; $max_sum = 0;

    for ($i = 0; $i < $n;$i++)
    {
        $max_sum = 2 * $max_sum + 
                       $arr[$n - 1 - $i];
        $max_sum %= $MOD;
        $min_sum = 2 * $min_sum + $arr[$i];
        $min_sum %= $MOD;
    }

    return ($max_sum - $min_sum + $MOD) % $MOD;
}

// Driver Code
$arr = array(1, 2, 3, 4);
$n = count($arr);
echo maxMin($arr, $n);

// This code is contributed by vt_m. 
?>
```

## java 描述语言

```
<script>

// Javascript for finding max min difference
// from all subset of given set

var MOD = 1000000007;

// function for sum of max min difference 
function maxMin (arr, n) 
{
    // sort all numbers
    arr.sort((a,b)=> a-b);

    // iterate over array and with help of 
    // horner's rule calc max_sum and min_sum
    var min_sum = 0, max_sum = 0;
    for (var i = 0; i < n; i++)
    {
        max_sum = 2 * max_sum + arr[n-1-i];
        max_sum %= MOD;
        min_sum = 2 * min_sum + arr[i];
        min_sum %= MOD;
    }

    return (max_sum - min_sum + MOD) % MOD;
}

// Driver Code
var arr = [1, 2, 3, 4];
var n = arr.length;
document.write( maxMin(arr,n));

</script>
```

**输出:**

```
23
```

本文由[**Shivam Pradhan(anuj _ charm)**](http://www.facebook.com/ma5ter6it)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。