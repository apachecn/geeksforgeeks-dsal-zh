# 检查给定数组是否成对排序

> 原文:[https://www . geesforgeks . org/check-给定-数组-成对-排序-非/](https://www.geeksforgeeks.org/check-given-array-pairwise-sorted-not/)

如果每个连续的数字对都是按排序(非递减)顺序排列的，则数组被认为是成对排序的。对于奇数元素，最后一个元素被忽略，结果基于剩余的偶数元素。

**示例:**

```
Input : arr[] = {10, 15, 9, 9, 1, 5};
Output : Yes
Pairs are (10, 15), (9,  9) and (1, 5).
All these pairs are sorted in non-decreasing
order.

Input : arr[] = {10, 15, 8, 9, 10, 5};
Output : No
The last pair (10, 5) is not sorted.
```

想法是从左到右遍历数组。成对比较元素，如果任何一对违反属性，我们返回 false。如果没有对违反属性，我们返回 true。

## C++

```
// CPP program to check if an array is pair wise
// sorted.
#include <bits/stdc++.h>
using namespace std;

// Check whether the array is pairwise sorted
// or not.
bool checkPairWiseSorted(int arr[], int n)
{
    if (n == 0 || n == 1)
        return true;
    for (int i = 0; i < n; i += 2)
        if (arr[i] > arr[i + 1])
            return false;
    return true;
}

// Driver program to test above function
int main()
{
   int arr[] = {2, 5, 3, 7, 9, 11};
   int n = sizeof(arr) / sizeof(arr[0]);  
   if (checkPairWiseSorted(arr, n))
       printf("Yes");
   else
       printf("No");      
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to check if an array
// is pair wise sorted.

import java.io.*;

public class GFG {

    // Check whether the array is
    // pairwise sorted or not.
    static boolean checkPairWiseSorted(
                          int []arr, int n)
    {
        if (n == 0 || n == 1)
            return true;

        for (int i = 0; i < n; i += 2)
            if (arr[i] > arr[i + 1])
                return false;

        return true;
    }

    // Driver program to test above
    // function
    static public void main (String[] args)
    {
        int []arr = {2, 5, 3, 7, 9, 11};
        int n = arr.length;

        if (checkPairWiseSorted(arr, n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by vt_m.
```

## 计算机编程语言

```
# Python code to check whether the array
# is pairwise sorted or not.
def checkPairWiseSorted(a, n):

    if n == 0 or n == 1:
        return True

    for i in range(0, n, 2):
        if a[i] > a[i + 1]:
            return False

    return True

# Driver code
a = [2, 5, 3, 7, 9, 11]
n = len(a)

if checkPairWiseSorted(a, n):
    print "Yes"
else:
    print "No"

# This code is contributed by 'striver'.
```

## C#

```
// C# program to check if an array is
// pair wise sorted.
using System;

public class GFG {

    // Check whether the array is
    // pairwise sorted or not.
    static bool checkPairWiseSorted(
                      int []arr, int n)
    {
        if (n == 0 || n == 1)
            return true;

        for (int i = 0; i < n; i += 2)
            if (arr[i] > arr[i + 1])
                return false;

        return true;
    }

    // Driver program to test above
    // function
    static public void Main ()
    {
        int []arr = {2, 5, 3, 7, 9, 11};
        int n = arr.Length;

        if (checkPairWiseSorted(arr, n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");    
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if an array is
// pair wise sorted.

// Check whether the array is pairwise
// sorted or not.
function checkPairWiseSorted( $arr, $n)
{
    if ($n == 0 or $n == 1)
        return true;
    for ($i = 0; $i < $n; $i += 2)
        if ($arr[$i] > $arr[$i + 1])
            return false;
    return true;
}

// Driver program to test above function
$arr = array(2, 5, 3, 7, 9, 11);
$n = count($arr);

if (checkPairWiseSorted($arr, $n))
    echo "Yes";
else
    echo "No";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// javascript program to check if an array
// is pair wise sorted.

    // Check whether the array is
    // pairwise sorted or not.
    function checkPairWiseSorted(arr , n) {
        if (n == 0 || n == 1)
            return true;

        for (i = 0; i < n; i += 2)
            if (arr[i] > arr[i + 1])
                return false;

        return true;
    }

    // Driver program to test above
    // function
    var arr = [ 2, 5, 3, 7, 9, 11 ];
        var n = arr.length;

        if (checkPairWiseSorted(arr, n))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by umadevi9616
</script>
```

**输出:**

```
Yes
```

**时间复杂度:**O(n)
T3】空间复杂度: O(1)

本文由 [**ASIPU PAWAN KUMAR**](https://auth.geeksforgeeks.org/profile.php?user=Pawan Asipu) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。