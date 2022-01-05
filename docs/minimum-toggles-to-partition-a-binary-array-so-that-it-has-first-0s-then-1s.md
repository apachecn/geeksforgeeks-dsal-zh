# 最小切换来分割一个二进制数组，使其首先为 0，然后为 1

> 原文:[https://www . geesforgeks . org/minimum-toggles-to-partition-a-binary-array-so-it-first-0s-then-1s/](https://www.geeksforgeeks.org/minimum-toggles-to-partition-a-binary-array-so-that-it-has-first-0s-then-1s/)

给定一个只包含 0 和 1 的 n 个整数的数组。找到阵列分区所需的最小切换次数(从 0 切换到 1，反之亦然)，即它的前 0 比 1 多。开头至少要有一个 0，结尾可以有零个或多个 1。

```
Input: arr[] = {1, 0, 1, 1, 0}
Output: 2
Toggle the first and last element i.e.,
1 -> 0
0 -> 1
Final array will become:
arr[] = {0 0 1 1 1}
Since first two consecutive elements are all 0s
and rest three consecutive elements are all 1s.
Therefore minimum two toggles are required.

Input: arr[] = {0, 1, 0, 0, 1, 1, 1}
Output: 1

Input: arr[] = {1, 1}
Output: 1
There should be at least one 0.

Input: arr[] = {0, 0}
Output: 0
There can zero 1s. 
```

如果我们观察这个问题，那么我们会发现从 0 到 n-1 肯定会存在一个点，在这个点上剩下的所有元素应该包含所有的 0，点的右边应该包含所有的 1。那些不遵守这个定律的指数将不得不被移除。想法是从左到右计算所有 0。

```
Let zero[i] denotes the number of 0's till ith
index, then for each i, minimum number of
toggles required can be written as: i - zero[i]
 + zero[n] - zero[i] . The part i - zero[i]
indicates number of 1's to be toggled and the 
part zero[n] - zero[i] indicates number of 0's
to be toggled.

After that we just need to take minimum of 
all to get the final answer. 
```

## C++

```
// C++ program to find minimum toggle required
#include <bits/stdc++.h>
using namespace std;

// Function to calculate minimum toggling
// required by using Dynamic programming
int minToggle(int arr[], int n)
{
    int zero[n + 1];
    zero[0] = 0;

    // Fill entries in zero[] such that zero[i]
    // stores count of zeroes to the left of i
    // (exl
    for (int i = 1; i <= n; ++i) {
        // If zero found update zero[] array
        if (arr[i - 1] == 0)
            zero[i] = zero[i - 1] + 1;
        else
            zero[i] = zero[i - 1];
    }

    // Finding the minimum toggle required from
    // every index(0 to n-1)
    int ans = n;
    for (int i = 1; i <= n; ++i)
        ans = min(ans, i - zero[i] + zero[n] - zero[i]);

    return ans;
}

// Driver Program
int main()
{
    int arr[] = { 1, 0, 1, 1, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minToggle(arr, n) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// toggle required
import java.io.*;

class GFG {

    // Function to calculate minimum toggling
    // required by using Dynamic programming
    static int minToggle(int arr[], int n)
    {
        int zero[] = new int[n + 1];
        zero[0] = 0;

        // Fill entries in zero[] such that
        // zero[i] stores count of zeroes
        // to the left of i (exl
        for (int i = 1; i <= n; ++i) {
            // If zero found update zero[] array
            if (arr[i - 1] == 0)
                zero[i] = zero[i - 1] + 1;
            else
                zero[i] = zero[i - 1];
        }

        // Finding the minimum toggle required
        // from every index(0 to n-1)
        int ans = n;
        for (int i = 1; i <= n; ++i)
            ans = Math.min(ans, i - zero[i] + zero[n]
                                    - zero[i]);

        return ans;
    }

    // Driver Program
    public static void main(String[] args)
    {
        int arr[] = { 1, 0, 1, 1, 0 };
        int n = arr.length;
        System.out.println(minToggle(arr, n));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python program to find
# minimum toggle required

# Function to calculate
# minimum toggling
# required by using
# Dynamic programming
def minToggle(arr, n):

    zero =[0 for i in range(n + 1+1)]
    zero[0] = 0

    # Fill entries in zero[]
    # such that zero[i]
    # stores count of zeroes
    # to the left of i
    # (exl
    for i in range(1, n + 1):

        # If zero found
        # update zero[] array
        if (arr[i-1] == 0):
            zero[i] = zero[i-1] + 1
        else:
            zero[i] = zero[i-1]

    # Finding the minimum
    # toggle required from
    # every index(0 to n-1)
    ans = n
    for i in range(1, n + 1):
        ans = min(ans, i - zero[i] + zero[n] - zero[i])

    return ans

# Driver Program

arr = [1, 0, 1, 1, 0]
n = len(arr)

print(minToggle(arr, n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find minimum
// toggle required
using System;

class GFG {

    // Function to calculate minimum toggling
    // required by using Dynamic programming
    static int minToggle(int[] arr, int n)
    {

        int[] zero = new int[n + 1];
        zero[0] = 0;

        // Fill entries in zero[] such that
        // zero[i] stores count of zeroes
        // to the left of i (exl
        for (int i = 1; i <= n; ++i) {

            // If zero found update zero[]
            // array
            if (arr[i - 1] == 0)
                zero[i] = zero[i - 1] + 1;
            else
                zero[i] = zero[i - 1];
        }

        // Finding the minimum toggle required
        // from every index(0 to n-1)
        int ans = n;

        for (int i = 1; i <= n; ++i)
            ans = Math.Min(ans, i - zero[i] +
                            zero[n] - zero[i]);

        return ans;
    }

    // Driver Program
    public static void Main()
    {
        int[] arr = { 1, 0, 1, 1, 0 };
        int n = arr.Length;

        Console.WriteLine(minToggle(arr, n));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to find minimum toggle required

// Function to calculate minimum toggling
// required by using Dynamic programming
function minToggle($arr, $n)
{
    $zero[0] = 0;
    $zero[$n + 1]=0;

    // Fill entries in zero[] such that zero[i]
    // stores count of zeroes to the left of i
    // (exl
    for ($i = 1; $i <= $n; ++$i) {

        // If zero found update zero[] array
        if ($arr[$i - 1] == 0)
            $zero[$i] = $zero[$i - 1] + 1;
        else
            $zero[$i] = $zero[$i - 1];
    }

    // Finding the minimum toggle required from
    // every index(0 to n-1)
    $ans = $n;

    for ($i = 1; $i <= $n; ++$i)
        $ans = min($ans, $i - $zero[$i]
                      + $zero[$n] - $zero[$i]);

    return $ans;
}

// Driver Program
    $arr = array( 1, 0, 1, 1, 0 );
    $n = sizeof($arr);

    echo minToggle($arr, $n) , "\n";

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find minimum
    // toggle required

    // Function to calculate minimum toggling
    // required by using Dynamic programming
    function minToggle(arr, n)
    {

        let zero = new Array(n + 1);
        zero[0] = 0;

        // Fill entries in zero[] such that
        // zero[i] stores count of zeroes
        // to the left of i (exl
        for (let i = 1; i <= n; ++i) {

            // If zero found update zero[]
            // array
            if (arr[i - 1] == 0)
                zero[i] = zero[i - 1] + 1;
            else
                zero[i] = zero[i - 1];
        }

        // Finding the minimum toggle required
        // from every index(0 to n-1)
        let ans = n;

        for (let i = 1; i <= n; ++i)
            ans = Math.min(ans, i - zero[i] + zero[n] - zero[i]);

        return ans;
    }

    let arr = [ 1, 0, 1, 1, 0 ];
    let n = arr.length;

    document.write(minToggle(arr, n));

</script>
```

**输出:**

```
2
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)

本文由 [Shubham Bansal](https://www.facebook.com/banalshubham) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。