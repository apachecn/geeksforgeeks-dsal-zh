# 选择 k 个数组元素，使得最大值和最小值的差值最小

> 原文:[https://www . geesforgeks . org/k-numbers-difference-maximum-minimum-k-number-minimum/](https://www.geeksforgeeks.org/k-numbers-difference-maximum-minimum-k-number-minimized/)

给定一组 **n 个**整数和一个正数 **k 个**。我们可以从给定的数组中取任意 k 个整数。任务是找到 K 个数的最大值和最小值之差的最小可能值。

**示例:**

```
Input : arr[] = {10, 100, 300, 200, 1000, 20, 30}
        k = 3
Output : 20
20 is the minimum possible difference between any
maximum and minimum of any k numbers.
Given k = 3, we get the result 20 by selecting 
integers {10, 20, 30}.
max(10, 20, 30) - min(10, 20, 30) = 30 - 10 = 20.

Input : arr[] = {1, 2, 3, 4, 10, 20, 30, 40, 
                                   100, 200}.
        k = 4      
Output : 3
```

思路是对数组排序，选择 k 个连续整数。为什么连续？假设所选的 k 个整数是 arr[0]，arr[1]，…arr[r]，arr[r+x]…，arr[k-1]，它们都是递增的，但在排序的数组中不是连续的。这意味着存在一个介于 arr[r]和 arr[r+x]之间的整数 p。因此，如果包含 p，并且 arr[0]被移除，那么新的差异将是 arr[r]–arr[1]，而旧的差异是 arr[r]–arr[0]。我们知道 arr[0] ≤ arr[1] ≤ … ≤ arr[k-1],所以最小差减小或保持不变。如果我们对其他类似 p 的数字执行相同的过程，我们会得到最小的差异。
解决问题的算法:

1.  对数组进行排序。
2.  计算每组 k 个连续整数的最大值(k 个数)–最小值(k 个数)。
3.  返回在步骤 2 中获得的所有值的最小值。

以下是上述思路的实现:

## C++

```
// C++ program to find minimum difference of maximum
// and minimum of K number.
#include<bits/stdc++.h>
using namespace std;

// Return minimum difference of maximum and minimum
// of k elements of arr[0..n-1].
int minDiff(int arr[], int n, int k)
{
    int result = INT_MAX;

    // Sorting the array.
    sort(arr, arr + n);

    // Find minimum value among all K size subarray.
    for (int i=0; i<=n-k; i++)
        result = min(result, arr[i+k-1] - arr[i]);

    return result;
}

// Driven Program
int main()
{
    int arr[] = {10, 100, 300, 200, 1000, 20, 30};
    int n = sizeof(arr)/sizeof(arr[0]);
    int k = 3;

    cout << minDiff(arr, n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum difference
// of maximum and minimum of K number.
import java.util.*;

class GFG {

// Return minimum difference of
// maximum and minimum of k
// elements of arr[0..n-1].
static int minDiff(int arr[], int n, int k) {
    int result = Integer.MAX_VALUE;

    // Sorting the array.
    Arrays.sort(arr);

    // Find minimum value among
    // all K size subarray.
    for (int i = 0; i <= n - k; i++)
    result = Math.min(result, arr[i + k - 1] - arr[i]);

    return result;
}

// Driver code
public static void main(String[] args) {
    int arr[] = {10, 100, 300, 200, 1000, 20, 30};
    int n = arr.length;
    int k = 3;

    System.out.println(minDiff(arr, n, k));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find minimum
# difference of maximum
# and minimum of K number.

# Return minimum difference
# of maximum and minimum
# of k elements of arr[0..n-1].
def minDiff(arr,n,k):
    result = +2147483647

    # Sorting the array.
    arr.sort()

    # Find minimum value among
    # all K size subarray.
    for i in range(n-k+1):
        result = int(min(result, arr[i+k-1] - arr[i]))

    return result

# Driver code

arr= [10, 100, 300, 200, 1000, 20, 30]
n =len(arr)
k = 3

print(minDiff(arr, n, k))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find minimum
// difference of maximum and
// minimum of K number.
using System;

class GFG {

// Return minimum difference of
// maximum and minimum of k
// elements of arr[0..n - 1].
static int minDiff(int []arr, int n,
                   int k)
{
    int result = int.MaxValue;

    // Sorting the array.
    Array.Sort(arr);

    // Find minimum value among
    // all K size subarray.
    for (int i = 0; i <= n - k; i++)
    result = Math.Min(result, arr[i + k - 1] - arr[i]);

    return result;
}

// Driver code
public static void Main() {
    int []arr = {10, 100, 300, 200, 1000, 20, 30};
    int n = arr.Length;
    int k = 3;

    Console.WriteLine(minDiff(arr, n, k));
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// difference of maximum and
// minimum of K number.

// Return minimum difference
// of maximum and minimum
// of k elements of arr[0..n-1].
function minDiff($arr, $n, $k)
{
    $INT_MAX = 2147483647;
    $result = $INT_MAX ;

    // Sorting the array.
    sort($arr , $n);
    sort($arr);

    // Find minimum value among
    // all K size subarray.
    for ($i = 0; $i <= $n - $k; $i++)
        $result = min($result, $arr[$i + $k - 1] -
                                       $arr[$i]);
    return $result;
}

    // Driver Code
    $arr = array(10, 100, 300, 200, 1000, 20, 30);
    $n = sizeof($arr);
    $k = 3;
    echo minDiff($arr, $n, $k);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// javascript program to find minimum difference
// of maximum and minimum of K number.

    // Return minimum difference of
    // maximum and minimum of k
    // elements of arr[0..n-1].
    function minDiff(arr , n , k) {
        var result = Number.MAX_VALUE;

        // Sorting the array.
        arr.sort((a,b)=>a-b);

        // Find minimum value among
        // all K size subarray.
        for (i = 0; i <= n - k; i++)
            result = Math.min(result, arr[i + k - 1] - arr[i]);

        return result;
    }

    // Driver code

        var arr = [ 10, 100, 300, 200, 1000, 20, 30 ];
        var n = arr.length;
        var k = 3;

        document.write(minDiff(arr, n, k));

// This code contributed by gauravrajput1
</script>
```

输出:

```
20
```

**时间复杂度:** O(nlogn)。
本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。