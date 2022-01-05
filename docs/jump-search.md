# 跳转搜索

> 原文:[https://www.geeksforgeeks.org/jump-search/](https://www.geeksforgeeks.org/jump-search/)

像[二分搜索法](http://geeksquiz.com/binary-search/)一样，跳转搜索是一种排序数组的搜索算法。基本思想是通过向前跳固定步或跳过一些元素代替搜索所有元素来检查更少的元素(比[线性搜索](https://www.geeksforgeeks.org/analysis-of-algorithms-set-2-asymptotic-analysis/))。
例如，假设我们有一个大小为 n 的数组 arr[]和一个大小为 m 的块(待跳转)。然后我们在索引 arr[0]、arr[m]、arr[2m]处搜索…..arr[km]等等。一旦我们找到了区间(arr[km] < x < arr[(k+1)m])，我们就从索引 km 执行线性搜索操作来找到元素 x。
让我们考虑以下数组:(0，1，1，2，3，5，8，13，21，34，55，89，144，233，377，610)。数组的长度是 16。假设要跳转的块大小为 4，跳转搜索将通过以下步骤找到值 55。
STEP 1:从索引 0 跳转到索引 4；
STEP 2:从索引 4 跳转到索引 8；
STEP 3:从指数 8 跳到指数 12；
STEP 4:由于索引 12 处的元素大于 55，我们将跳回到索引 8。
步骤 5:从索引 8 开始进行线性搜索，得到元素 55。
**要跳过的最佳块大小是多少？**
在最坏的情况下，我们必须进行 n/m 次跳转，如果最后一次检查的值大于要搜索的元素，我们会进行更多的 m-1 比较，以进行线性搜索。因此，最坏情况下的比较总数将为((n/m) + m-1)。当 m = √n 时，函数的值((n/m) + m-1)将最小，因此，最佳步长为 m = **√n.**

## C++

```
// C++ program to implement Jump Search

#include <bits/stdc++.h>
using namespace std;

int jumpSearch(int arr[], int x, int n)
{
    // Finding block size to be jumped
    int step = sqrt(n);

    // Finding the block where element is
    // present (if it is present)
    int prev = 0;
    while (arr[min(step, n)-1] < x)
    {
        prev = step;
        step += sqrt(n);
        if (prev >= n)
            return -1;
    }

    // Doing a linear search for x in block
    // beginning with prev.
    while (arr[prev] < x)
    {
        prev++;

        // If we reached next block or end of
        // array, element is not present.
        if (prev == min(step, n))
            return -1;
    }
    // If element is found
    if (arr[prev] == x)
        return prev;

    return -1;
}

// Driver program to test function
int main()
{
    int arr[] = { 0, 1, 1, 2, 3, 5, 8, 13, 21,
                34, 55, 89, 144, 233, 377, 610 };
    int x = 55;
    int n = sizeof(arr) / sizeof(arr[0]);

    // Find the index of 'x' using Jump Search
    int index = jumpSearch(arr, x, n);

    // Print the index where 'x' is located
    cout << "\nNumber " << x << " is at index " << index;
    return 0;
}

// Contributed by nuclode
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement Jump Search.
public class JumpSearch
{
    public static int jumpSearch(int[] arr, int x)
    {
        int n = arr.length;

        // Finding block size to be jumped
        int step = (int)Math.floor(Math.sqrt(n));

        // Finding the block where element is
        // present (if it is present)
        int prev = 0;
        while (arr[Math.min(step, n)-1] < x)
        {
            prev = step;
            step += (int)Math.floor(Math.sqrt(n));
            if (prev >= n)
                return -1;
        }

        // Doing a linear search for x in block
        // beginning with prev.
        while (arr[prev] < x)
        {
            prev++;

            // If we reached next block or end of
            // array, element is not present.
            if (prev == Math.min(step, n))
                return -1;
        }

        // If element is found
        if (arr[prev] == x)
            return prev;

        return -1;
    }

    // Driver program to test function
    public static void main(String [ ] args)
    {
        int arr[] = { 0, 1, 1, 2, 3, 5, 8, 13, 21,
                    34, 55, 89, 144, 233, 377, 610};
        int x = 55;

        // Find the index of 'x' using Jump Search
        int index = jumpSearch(arr, x);

        // Print the index where 'x' is located
        System.out.println("\nNumber " + x +
                            " is at index " + index);
    }
}
```

## 蟒蛇 3

```
# Python3 code to implement Jump Search
import math

def jumpSearch( arr , x , n ):

    # Finding block size to be jumped
    step = math.sqrt(n)

    # Finding the block where element is
    # present (if it is present)
    prev = 0
    while arr[int(min(step, n)-1)] < x:
        prev = step
        step += math.sqrt(n)
        if prev >= n:
            return -1

    # Doing a linear search for x in
    # block beginning with prev.
    while arr[int(prev)] < x:
        prev += 1

        # If we reached next block or end
        # of array, element is not present.
        if prev == min(step, n):
            return -1

    # If element is found
    if arr[int(prev)] == x:
        return prev

    return -1

# Driver code to test function
arr = [ 0, 1, 1, 2, 3, 5, 8, 13, 21,
    34, 55, 89, 144, 233, 377, 610 ]
x = 55
n = len(arr)

# Find the index of 'x' using Jump Search
index = jumpSearch(arr, x, n)

# Print the index where 'x' is located
print("Number" , x, "is at index" ,"%.0f"%index)

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to implement Jump Search.
using System;
public class JumpSearch
{
    public static int jumpSearch(int[] arr, int x)
    {
        int n = arr.Length;

        // Finding block size to be jumped
        int step = (int)Math.Floor(Math.Sqrt(n));

        // Finding the block where element is
        // present (if it is present)
        int prev = 0;
        while (arr[Math.Min(step, n)-1] < x)
        {
            prev = step;
            step += (int)Math.Floor(Math.Sqrt(n));
            if (prev >= n)
                return -1;
        }

        // Doing a linear search for x in block
        // beginning with prev.
        while (arr[prev] < x)
        {
            prev++;

            // If we reached next block or end of
            // array, element is not present.
            if (prev == Math.Min(step, n))
                return -1;
        }

        // If element is found
        if (arr[prev] == x)
            return prev;

        return -1;
    }

    // Driver program to test function
    public static void Main()
    {
        int[] arr = { 0, 1, 1, 2, 3, 5, 8, 13, 21,
                    34, 55, 89, 144, 233, 377, 610};
        int x = 55;

        // Find the index of 'x' using Jump Search
        int index = jumpSearch(arr, x);

        // Print the index where 'x' is located
        Console.Write("Number " + x +
                            " is at index " + index);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement Jump Search

function jumpSearch($arr, $x, $n)
{
    // Finding block size to be jumped
    $step = sqrt($n);

    // Finding the block where element is
    // present (if it is present)
    $prev = 0;
    while ($arr[min($step, $n)-1] < $x)
    {
        $prev = $step;
        $step += sqrt($n);
        if ($prev >= $n)
            return -1;
    }

    // Doing a linear search for x in block
    // beginning with prev.
    while ($arr[$prev] < $x)
    {
        $prev++;

        // If we reached next block or end of
        // array, element is not present.
        if ($prev == min($step, $n))
            return -1;
    }
    // If element is found
    if ($arr[$prev] == $x)
        return $prev;

    return -1;
}

// Driver program to test function
$arr = array( 0, 1, 1, 2, 3, 5, 8, 13, 21,
                34, 55, 89, 144, 233, 377, 610 );
$x = 55;
$n = sizeof($arr) / sizeof($arr[0]);

// Find the index of '$x' using Jump Search
$index = jumpSearch($arr, $x, $n);

// Print the index where '$x' is located
echo "Number ".$x." is at index " .$index;
return 0;
?>
```

## java 描述语言

```
<script>
// Javascript program to implement Jump Search

function jumpSearch(arr, x, n)
{
    // Finding block size to be jumped
    let step = Math.sqrt(n);

    // Finding the block where element is
    // present (if it is present)
    let prev = 0;
    while (arr[Math.min(step, n)-1] < x)
    {
        prev = step;
        step += Math.sqrt(n);
        if (prev >= n)
            return -1;
    }

    // Doing a linear search for x in block
    // beginning with prev.
    while (arr[prev] < x)
    {
        prev++;

        // If we reached next block or end of
        // array, element is not present.
        if (prev == Math.min(step, n))
            return -1;
    }
    // If element is found
    if (arr[prev] == x)
        return prev;

    return -1;
}

// Driver program to test function
let arr = [0, 1, 1, 2, 3, 5, 8, 13, 21,
                34, 55, 89, 144, 233, 377, 610];
let x = 55;
let n = arr.length;

// Find the index of 'x' using Jump Search
let index = jumpSearch(arr, x, n);

// Print the index where 'x' is located
document.write(`Number ${x} is at index ${index}`);

// This code is contributed by _saurabh_jaiswal
</script>
```

输出:

```
Number 55 is at index 10
```

时间复杂度:O(√n)
辅助空间:O(1)
**重要点:**

*   仅适用于排序数组。
*   要跳转的块的最佳大小是(√ n)。这使得跳转搜索的时间复杂度为 O(√ n)。
*   跳跃搜索的时间复杂度介于线性搜索((O(n))和二分搜索法(O (Log n))之间。
*   二分搜索法比跳转搜索更好，但跳转搜索有一个优势，我们只遍历回一次(二分搜索法可能需要多达 O(Log n)次跳转，考虑一种情况，其中要搜索的元素是最小的元素或仅比最小的元素大)。因此，在二分搜索法成本高昂的系统中，我们使用跳转搜索。

**参考文献:**
https://en.wikipedia.org/wiki/Jump_search
本文由 **Harsh Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。