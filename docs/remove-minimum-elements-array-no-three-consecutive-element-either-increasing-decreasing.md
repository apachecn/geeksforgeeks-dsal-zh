# 从数组中移除最小元素，使得没有三个连续的元素增加或减少

> 原文:[https://www . geesforgeks . org/remove-minimum-elements-array-no-三连续-element-要么-递增-递减/](https://www.geeksforgeeks.org/remove-minimum-elements-array-no-three-consecutive-element-either-increasing-decreasing/)

给定一组不同的正整数。任务是找到要移除的元素的最小数量，使得数组中没有三个连续的元素在增加或减少。也就是说，拆除后要么是一个<sub>I–1</sub>T18】a<sub>I</sub>T19】a<sub>I+1</sub>要么是一个<sub>I–1</sub>T20】a<sub>I</sub>T21】a<sub>I+1</sub>。
**举例:**

```
Input : arr[] = {5, 2, 3, 6, 1}
Output : 1
Given arr[] is not in required form 
(2 < 3 < 6). So, after removal of
6 or 3, array will be in required manner.

Input : arr[] = { 4, 2, 6, 3, 10, 1}
Output : 0
```

观察，对于 n < 3, output will be 0 since no element need to be remove.
**方法 1 O(n <sup>2</sup> ):**
如果我们仔细观察，我们可以注意到 arr 中的元素移除后，剩下的是 arr 的之字形子序列。假设新数组是 arr’。那么我们为到达 arr 所执行的删除次数‘就是 arr 的大小–arr 的大小’。我们的目标是最小化这种差异。注意 arr 的大小是固定的，所以我们必须最小化-arr 的大小'或最大化 arr 的大小'。这样问题就简化为寻找[最长的之字形子序列](https://www.geeksforgeeks.org/longest-zig-zag-subsequence/)。
**方法 2 O(n):(棘手)**
要移除的元素是那些 a <sub>i</sub> 使得
a<sub>I-1</sub>T58】a<sub>I</sub>T59】a<sub>I+1</sub>或
a<sub>I-1</sub>T60】a<sub>I</sub>T61】a<sub>I
**这是怎么工作的？**
我们来定义一个 <sub>i</sub> be as，
Peak if 0<I<n–1 和一个<sub>I–1</sub>T64】a<sub>I</sub>T65】a<sub>I+1</sub>。
谷若 0<I<n–1 和 a<sub>I–1</sub>T68】a<sub>I</sub>T69】a<sub>I+1</sub>。
设 P(arr)和 V(arr)分别为峰数和谷数。
观察到，在任何之字形排列中，除端点外的所有元素都是峰或谷，即 n = P(arr) + V(arr) + 2。
现在，我们可以表明任何删除都不会增加任何数组中峰谷的总数:
1。假设我们去掉一个既不是峰也不是谷的元素 a<sub>I【T56:</sub></sub> 

*   如果一个 <sub>i</sub> 是一个端点，那么显然没有峰或谷可以形成。

*   如果 a<sub>I–1</sub><a<sub>I</sub><a<sub>I+1</sub>，那么在移除 a <sub>i</sub> 之后，元素 a<sub>I–1</sub>和 a <sub>i + 1</sub> 将相邻。但是由于 a<sub>I–1</sub><a<sub>I+1</sub>，a<sub>I–1</sub>或 a <sub>i + 1</sub> 的状态不会改变，即如果 a<sub>I–1</sub>或 a <sub>i + 1</sub> 最初是一个峰/谷/两者都不变，那么在移除之后它将保持一个峰/谷/两者都不变，因为它们与其邻居的比较将是相同的。特别是，没有形成新的峰或谷。

*   类似的情况还有一个<sub>I–1</sub>>a<sub>I</sub>>a<sub>I+1</sub>。

2.假设我们去掉一个峰或谷:

*   假设我们去掉一个峰，那么 a<sub>I–1</sub><a<sub>I</sub>T24】a<sub>I+1</sub>。现在有可能一个<sub>I–1</sub>或一个 <sub>i + 1</sub> 会变成一个峰或谷。但是我们可以表明，它们不能同时改变，因为要么一个<sub>I–1</sub><a<sub>I+1</sub>，这意味着一个<sub>I–1</sub>的状态永远不变，要么一个<sub>I–1</sub>>a<sub>I+1</sub>，这意味着一个 <sub>i + 1</sub> 的状态永远不变。因此，将形成一个峰或谷，但是由于我们移除了一个峰，峰/谷的总数不会增加。

*   当我们移除一个山谷，即一个<sub>I–1</sub>>a<sub>I</sub><a<sub>I+1</sub>时，同样的事情也会发生。

因此任何删除都不会改变 P(arr) + V(arr)。
利用这个论点，我们可以说 arr 的最长之字形子序列的长度至多为 P(arr) + V(arr) + 2。
另一方面，arr 具有长度为 P(arr) + V(arr) + 2 的之字形子序列，即 arr 的峰、谷、端点的序列。可以证明这个子序列是之字形的(通过尝试一些例子)，因此最长的之字形子序列的长度至少为 P(arr) + V(arr) + 2。因此，从前面两个论证中，我们可以说最长的之字形子序列的确切长度为 P(arr) + V(arr) + 2。
因此我们的问题的答案是 arr 的大小–P(arr)–V(arr)–2。
**算法:**

```
1\. Initialize count = 0.
2\. For each element arr[i] from index i = 1 to n - 2.
   (i) if (arr[i-1]  arr[i+1])
   (ii) increment count by 1.
3\. return count.
```

## C++

```
// C++ program to find minimum
// elements to be removed so
// that array becomes zig-zag.
#include <bits/stdc++.h>
using namespace std;

int minimumDeletions(int a[],
                     int n)
{
    if (n <= 2)
        return 0;

    // If number of element
    // is greater than 2.
    int count = 0;
    for (int i = 0; i < n - 2; i++)
    {
        // If three element are
        // consecutively increasing
        // or decreasing.
        if ((a[i] < a[i + 1] &&
             a[i + 1] < a[i + 2]) ||
            (a[i] > a[i + 1] &&
             a[i + 1] > a[i + 2]))
            count++;
    }

    return count;
}

// Driver Code
int main()
{
    int a[] = { 5, 2, 3, 6, 1 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << minimumDeletions(a, n)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// elements to be removed so that
// array becomes zig-zag.

class GFG
{
    static int minimumDeletions(int a[],
                                int n)
    {
        if (n <= 2)
            return 0;

        // If number of element
        // is greater than 2.
        int count = 0;
        for (int i = 0; i < n - 2; i++)
        {
            // If three element are
            // consecutively increasing
            // or decreasing.
            if ((a[i] < a[i + 1] &&
                 a[i + 1] < a[i + 2]) ||
                (a[i] > a[i + 1] &&
                 a[i + 1] > a[i + 2]))
                count++;
        }

        return count;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int a[] = { 5, 2, 3, 6, 1 };
        int n = a.length;

        System.out.println(minimumDeletions(a, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find minimum
# elements to be removed so that
# array becomes zig-zag.

def minimumDeletions(a, n):

    if (n <= 2):
        return 0

    # If number of element is
    # greater than 2.
    count = 0
    for i in range(n - 2):

        # If three element are
        # consecutively increasing
        # or decreasing.
        if ((a[i] < a[i + 1] and
             a[i + 1] < a[i + 2]) or
            (a[i] > a[i + 1] and
             a[i + 1] > a[i + 2])):
            count += 1

    return count

# Driver Code
a = [ 5, 2, 3, 6, 1 ]
n = len(a)
print(minimumDeletions(a, n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find minimum
// elements to be removed so
// that array becomes zig-zag.
using System;

class GFG
{
    static int minimumDeletions(int []a,
                                int n)
    {
        if (n <= 2)
            return 0;

        // If number of element is
        // greater than 2.
        int count = 0;
        for (int i = 0; i < n - 2; i++)
        {
            // If three element are
            // consecutively increasing
            // or decreasing.
            if ((a[i] < a[i + 1] &&
                 a[i + 1] < a[i + 2]) ||
                (a[i] > a[i + 1] &&
                 a[i + 1] > a[i + 2]))
                count++;
        }

        return count;
    }

    // Driver Code
    public static void Main ()
    {
        int []a = { 5, 2, 3, 6, 1 };
        int n = a.Length;

        Console.Write(minimumDeletions(a, n));
    }
}

// This code is contributed
// by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// elements to be removed so that
// array becomes zig-zag.

function minimumDeletions($a, $n)
{
    if ($n <= 2)
        return 0;

    // If number of element
    // is greater than 2.
    $count = 0;
    for ($i = 0; $i < $n - 2; $i++)
    {
        // If three element are
        // consecutively increasing
        // or decreasing.
        if (($a[$i] < $a[$i + 1] &&
             $a[$i + 1] < $a[$i + 2]) ||
            ($a[$i] > $a[$i + 1] &&
             $a[$i + 1] > $a[$i + 2]))
            $count++;
    }

    return $count;
}

// Driver Code

{
    $a = array( 5, 2, 3, 6, 1 );
    $n = sizeof($a) / sizeof($a[0]);

    echo minimumDeletions($a, $n) ;

    return 0;
}

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find minimum
// elements to be removed so
// that array becomes zig-zag.

function minimumDeletions(a, n) {
    if (n <= 2)
        return 0;

    // If number of element
    // is greater than 2.
    let count = 0;
    for (let i = 0; i < n - 2; i++) {
        // If three element are
        // consecutively increasing
        // or decreasing.
        if ((a[i] < a[i + 1] &&
            a[i + 1] < a[i + 2]) ||
            (a[i] > a[i + 1] &&
                a[i + 1] > a[i + 2]))
            count++;
    }

    return count;
}

// Driver Code

let a = [5, 2, 3, 6, 1];
let n = a.length;

document.write(minimumDeletions(a, n) + "<br>");

</script>
```

**输出:**

```
1
```

**时间复杂度:** O(n)。
本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。