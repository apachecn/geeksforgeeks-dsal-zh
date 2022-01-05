# 排列两个数组，使得每对数组的和大于或等于 K

> 原文:[https://www . geesforgeks . org/permute-两个数组-每对求和-大于等于-k/](https://www.geeksforgeeks.org/permute-two-arrays-sum-every-pair-greater-equal-k/)

给定两个大小相等的数组 **n** 和一个整数 **k** 。任务是对两个数组进行置换，使得它们对应元素的和大于或等于 k，即 a[i] + b[i] > = k。如果存在这样的置换，任务是打印“是”，否则打印“否”。
**例:**

```
Input : a[] = {2, 1, 3}, 
        b[] = { 7, 8, 9 }, 
        k = 10\. 
Output : Yes
Permutation  a[] = { 1, 2, 3 } and b[] = { 9, 8, 7 } 
satisfied the condition a[i] + b[i] >= K.

Input : a[] = {1, 2, 2, 1}, 
        b[] = { 3, 3, 3, 4 }, 
        k = 5\. 
Output : No
```

其思想是按升序对一个数组进行排序，按降序对另一个数组进行排序，如果任何索引不满足条件 a[i] + b[i] >= K，则打印“否”，否则打印“是”。
如果排序数组的条件失败，则不存在满足不等式的数组置换。**证明，**
假设 **a <sub>排序</sub> []** 按升序排序 a[]，而 **b <sub>排序</sub> []** 按降序排序 b[]。
让新的置换 b[]通过交换 b 的任意两个索引 I，j 来创建<sub>排序</sub> []，

*   **情况 1:** i < j，b【I】处的元素现在是 b <sub>排序</sub>【j】。
    现在，a <sub>排序</sub>【I】+b<sub>排序</sub>【j】<K，因为 b <sub>排序</sub>【I】>b<sub>排序</sub>【j】作为 b【】是按降序排序的，我们知道 a <sub>排序</sub>【I】+b<sub>排序</sub>【I】<K。
*   **情况 2:** i > j，b【I】处的元素现在是 b <sub>排序</sub>【j】。
    现在，a <sub>排序</sub>【j】+b<sub>排序</sub>【I】<k，因为 a <sub>排序</sub>【I】>a<sub>排序</sub>【j】作为一个[]按照递增顺序排序，我们知道 a <sub>排序</sub>【I】+b<sub>排序</sub>【I】<k。

下面是这个方法的实现:

## C++

```
// C++ program to check whether permutation of two
// arrays satisfy the condition a[i] + b[i] >= k.
#include<bits/stdc++.h>
using namespace std;

// Check whether any permutation exists which
// satisfy the condition.
bool isPossible(int a[], int b[], int n, int k)
{
    // Sort the array a[] in decreasing order.
    sort(a, a + n);

    // Sort the array b[] in increasing order.
    sort(b, b + n, greater<int>());

    // Checking condition on each index.
    for (int i = 0; i < n; i++)
        if (a[i] + b[i] < k)
            return false;

    return true;
}

// Driven Program
int main()
{
    int a[] = { 2, 1, 3 };
    int b[] = { 7, 8, 9 };
    int k = 10;
    int n = sizeof(a)/sizeof(a[0]);

    isPossible(a, b, n, k) ? cout << "Yes" :
                             cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether
// permutation of two arrays satisfy
// the condition a[i] + b[i] >= k.
import java.util.*;

class GFG
{
// Check whether any permutation
// exists which satisfy the condition.
static boolean isPossible(Integer a[], int b[],
                                  int n, int k)
{
    // Sort the array a[] in decreasing order.
    Arrays.sort(a, Collections.reverseOrder());

    // Sort the array b[] in increasing order.
    Arrays.sort(b);

    // Checking condition on each index.
    for (int i = 0; i < n; i++)
    if (a[i] + b[i] < k)
        return false;

    return true;
}

// Driver code
public static void main(String[] args) {
    Integer a[] = {2, 1, 3};
    int b[] = {7, 8, 9};
    int k = 10;
    int n = a.length;

    if (isPossible(a, b, n, k))
    System.out.print("Yes");
    else
    System.out.print("No");
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to check
# whether permutation of two
# arrays satisfy the condition
# a[i] + b[i] >= k.

# Check whether any
# permutation exists which
# satisfy the condition.
def isPossible(a,b,n,k):

    # Sort the array a[]
    # in decreasing order.
    a.sort(reverse=True)

    # Sort the array b[]
    # in increasing order.
    b.sort()

    # Checking condition
    # on each index.
    for i in range(n):
        if (a[i] + b[i] < k):
            return False

    return True

# Driver code

a = [ 2, 1, 3]
b = [7, 8, 9]
k = 10
n =len(a)

if(isPossible(a, b, n, k)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to check whether
// permutation of two arrays satisfy
// the condition a[i] + b[i] >= k.
using System;

class GFG
{
// Check whether any permutation
// exists which satisfy the condition.
static bool isPossible(int []a, int []b,
                       int n, int k)
{
    // Sort the array a[]
    // in decreasing order.
    Array.Sort(a);

    // Sort the array b[]
    // in increasing order.
    Array.Reverse(b);

    // Checking condition on each index.
    for (int i = 0; i < n; i++)
    if (a[i] + b[i] < k)
        return false;

    return true;
}

// Driver code
public static void Main()
{
    int []a = {2, 1, 3};
    int []b = {7, 8, 9};
    int k = 10;
    int n = a.Length;

    if (isPossible(a, b, n, k))
    Console.WriteLine("Yes");
    else
    Console.WriteLine("No");
}
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check whether
// permutation of two arrays satisfy
// the condition a[i] + b[i] >= k.

// Check whether any permutation
// exists which satisfy the condition.
function isPossible( $a, $b, $n, $k)
{

    // Sort the array a[] in
    // decreasing order.
    sort($a);

    // Sort the array b[] in
    // increasing order.
    rsort($b);

    // Checking condition on each
    // index.
    for ( $i = 0; $i < $n; $i++)
        if ($a[$i] + $b[$i] < $k)
            return false;

    return true;
}

// Driven Program
    $a = array( 2, 1, 3 );
    $b = array( 7, 8, 9 );
    $k = 10;
    $n = count($a);

    if(isPossible($a, $b, $n, $k))
        echo "Yes" ;
    else
        echo "No";

// This code is contributed by
// anuj_67.
?>
```

## java 描述语言

```
<script>

    // JavaScript program to check whether
    // permutation of two arrays satisfy
    // the condition a[i] + b[i] >= k.

    // Check whether any permutation
    // exists which satisfy the condition.
    function isPossible(a, b, n, k)
    {
        // Sort the array a[]
        // in decreasing order.
        a.sort(function(a, b){return a - b});

        // Sort the array b[]
        // in increasing order.
        b.reverse();

        // Checking condition on each index.
        for (let i = 0; i < n; i++)
          if (a[i] + b[i] < k)
              return false;

        return true;
    }

    let a = [2, 1, 3];
    let b = [7, 8, 9];
    let k = 10;
    let n = a.length;

    if (isPossible(a, b, n, k))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(n log n)。
本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。