# 计算“向前移动”对数组进行排序的最小移动次数

> 原文:[https://www . geesforgeks . org/count-最小数量-移动-前置-移动-排序-数组/](https://www.geeksforgeeks.org/count-minimum-number-move-front-moves-sort-array/)

给定一个大小为 n 的数组，使数组元素在 1 到 n 的范围内。任务是计算将项目排列为{1，2，3，… n}的移动到前面的操作数。**移至前方**操作是拾取任何物品并将其放置在第一位置。
这个问题也可以看作是一堆物品，唯一可用的移动是从堆中拉出一个物品并将其放在堆的顶部。
**示例:**

```
Input: arr[] = {3, 2, 1, 4}.
Output: 2
First, we pull out 2 and places it on top, 
so the array becomes (2, 3, 1, 4). After that, 
pull out 1 and becomes (1, 2, 3, 4).

Input:  arr[] = {5, 7, 4, 3, 2, 6, 1}
Output:  6
We pull elements in following order
7, 6, 5, 4, 3 and 2

Input: arr[] = {4, 3, 2, 1}.
Output: 3
```

想法是从头到尾遍历数组。我们期望最后是 n，所以我们将 expectedItem 初始化为 n。所有在 expectedItem 的实际位置和当前位置之间的项目都必须移动到前面。所以我们计算当前项目和预期项目之间的项目数。一旦找到 expectedItem，我们就通过将 expectedItem 减少 1 来寻找下一个 expectedITem。
以下是最小移动次数的算法:

```
1\. Initialize expected number at current position as n 
2\. Start from the last element of array.
     a) If the current item is same as expected item, 
           decrease expected item by 1.
3\. Return expected item.
```

下面是这个方法的实现。

## C++

```
// C++ program to find minimum number of move-to-front
// moves to arrange items in sorted order.
#include <bits/stdc++.h>
using namespace std;

// Calculate minimum number of moves to arrange array
// in increasing order.
int minMoves(int arr[], int n)
{
    // Since we traverse array from end, extected item
    // is initially  n
    int expectedItem = n;

    // Traverse array from end
    for (int i=n-1; i >= 0; i--)
    {
        // If current item is at its correct position,
        // decrement the expectedItem (which also means
        // decrement in minimum number of moves)
        if (arr[i] == expectedItem)
            expectedItem--;
    }

    return expectedItem;
}

// Driver Program
int main()
{
    int arr[] = {4, 3, 2, 1};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << minMoves(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find minimum
// number of move-to-front moves
// to arrange items in sorted order.
import java.io.*;

class GFG
{
    // Calculate minimum number of moves
    // to arrange array in increasing order.
    static int minMoves(int arr[], int n)
    {
        // Since we traverse array from end,
        // extected item is initially n
        int expectedItem = n;

        // Traverse array from end
        for (int i = n - 1; i >= 0; i--)
        {
            // If current item is at its correct position,
            // decrement the expectedItem (which also means
            // decrement in minimum number of moves)
            if (arr[i] == expectedItem)
                expectedItem--;
        }

        return expectedItem;
    }

    // Driver Program
    public static void main (String[] args)
    {
        int arr[] = {4, 3, 2, 1};
        int n = arr.length;
        System.out.println( minMoves(arr, n));

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python 3 program to find minimum
# number of move-to-front moves
# to arrange items in sorted order.

# Calculate minimum number of moves
# to arrange array in increasing order.
def minMoves(arr, n):

    # Since we traverse array from end,
    # expected item is initially n
    expectedItem = n

    # Traverse array from end
    for i in range(n - 1, -1, -1):

        # If current item is at its
        # correct position, decrement
        # the expectedItem (which also
        # means decrement in minimum
        # number of moves)
        if (arr[i] == expectedItem):
            expectedItem -= 1
    return expectedItem

# Driver Code
arr = [4, 3, 2, 1]
n = len(arr)
print(minMoves(arr, n))

# This code is contributed 29AjayKumar
```

## C#

```
// C# program to find minimum
// number of move-to-front moves
// to arrange items in sorted order.
using System;

class GFG {

    // Calculate minimum number of moves
    // to arrange array in increasing order.
    static int minMoves(int []arr, int n)
    {
        // Since we traverse array from end,
        // extected item is initially n
        int expectedItem = n;

        // Traverse array from end
        for (int i = n - 1; i >= 0; i--)
        {
            // If current item is at its
            // correct position, decrement
            // the expectedItem (which also
            // means decrement in minimum
            // number of moves)
            if (arr[i] == expectedItem)
                expectedItem--;
        }

        return expectedItem;
    }

    // Driver Program
    public static void Main ()
    {
        int []arr = {4, 3, 2, 1};
        int n = arr.Length;
        Console.Write( minMoves(arr, n));

    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// number of move-to-front moves
// to arrange items in sorted order.

// Calculate minimum number of
// moves to arrange array
// in increasing order.
function minMoves($arr, $n)
{
    // Since we traverse array
    // from end, extected item
    // is initially n
    $expectedItem = $n;

    // Traverse array from end
    for ($i = $n - 1; $i >= 0; $i--)
    {
        // If current item is at its
        // correct position, decrement
        // the expectedItem (which also
        // means decrement in minimum
        // number of moves)
        if ($arr[$i] == $expectedItem)
            $expectedItem--;
    }

    return $expectedItem;
}

// Driver Code
$arr = array(4, 3, 2, 1);
$n = count($arr);
echo minMoves($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find minimum
    // number of move-to-front moves
    // to arrange items in sorted order.

    // Calculate minimum number of moves
    // to arrange array in increasing order.
    function minMoves(arr, n)
    {
        // Since we traverse array from end,
        // extected item is initially n
        let expectedItem = n;

        // Traverse array from end
        for (let i = n - 1; i >= 0; i--)
        {
            // If current item is at its
            // correct position, decrement
            // the expectedItem (which also
            // means decrement in minimum
            // number of moves)
            if (arr[i] == expectedItem)
                expectedItem--;
        }

        return expectedItem;
    }

    let arr = [4, 3, 2, 1];
    let n = arr.length;
    document.write( minMoves(arr, n));

</script>
```

**输出:**

```
3
```

**时间复杂度:** O(n)
本文由[**Anuj Chauhan(Anuj 0503)**](https://web.facebook.com/anuj0503)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。