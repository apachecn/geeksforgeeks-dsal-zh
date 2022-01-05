# 找到几何平均值最大的子集

> 原文:[https://www . geesforgeks . org/find-subset-maximum-geometric-mean/](https://www.geeksforgeeks.org/find-subset-greatest-geometric-mean/)

给定一个正整数数组，我们的任务是找到一个大于 1 且乘积最大的子集。

```
Input  : arr[] = {1, 5, 7, 2, 0};    
Output : 5 7
The subset containing 5 and 7 produces maximum
geometric mean

Input  : arr[] = { 4, 3 , 5 , 9 , 8 };
Output : 8 9
```

一种简单的方法是运行两个循环，逐个检查给出最大几何平均值的数组元素。这个解决方案的时间复杂度是 O(n*n)，这个解决方案也会导致溢出。

一个**有效的解决方案**是基于这样一个事实，即最大的两个元素总是产生最大的平均值，因为问题需要找到一个大于 1 的子集。

## C++

```
// C++ program to find a subset of size 2 or
// greater with greatest geometric mean. This
// program basically find largest two elements.
#include <bits/stdc++.h>
using namespace std;

void findLargestGM(int arr[], int n)
{
    /* There should be atleast two elements */
    if (n < 2)
    {
        printf(" Invalid Input ");
        return;
    }

    int first = INT_MIN, second = INT_MIN;
    for (int i = 0; i < n ; i ++)
    {
        /* If current element is smaller than first
           then update both first and second */
        if (arr[i] > first)
        {
            second = first;
            first = arr[i];
        }

        /* If arr[i] is in between first and second
           then update second  */
        else if (arr[i] > second)
            second = arr[i];
    }

    printf("%d %d", second, first);
}

/* Driver program to test above function */
int main()
{
    int arr[] = {12, 13, 17, 10, 34, 1};
    int n = sizeof(arr)/sizeof(arr[0]);
    findLargestGM(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a subset of size 2 or
// greater with greatest geometric mean. This
// program basically find largest two elements.

class GFG {

    static void findLargestGM(int arr[], int n)
    {

        // There should be atleast two elements
        if (n < 2)
        {
            System.out.print(" Invalid Input ");
        }

        int first = -2147483648, second = -2147483648;

        for (int i = 0; i < n ; i ++)
        {

            /* If current element is smaller than first
            then update both first and second */
            if (arr[i] > first)
            {
                second = first;
                first = arr[i];
            }

            /* If arr[i] is in between first and second
            then update second */
            else if (arr[i] > second)
                second = arr[i];
        }

        System.out.print(second + " " + first);
    }

    // Driver function
    public static void main(String arg[])
    {
        int arr[] = {12, 13, 17, 10, 34, 1};
        int n = arr.length;

        findLargestGM(arr, n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find
# a subset of size 2 or
# greater with greatest
# geometric mean. This
# program basically find
# largest two elements.

import sys
def findLargestGM(arr, n):

        # There should be
        # atleast two elements
    if n < 2:
        print (" Invalid Input ")
        return

    first = -sys.maxsize - 1
    second = -sys.maxsize - 1
    for i in range(0,n):

        # If current element is
        # smaller than first
        # then update both first
        # and second
        if arr[i] > first:
            second = first
            first = arr[i]

        # If arr[i] is in between
        # first and second
        # then update second
        elif arr[i] > second:
            second = arr[i]

    print ("%d %d"%(second, first))

# Driver program to
# test above function
arr = [12, 13, 17, 10, 34, 1]
n = len(arr)

findLargestGM(arr, n)

# This code is contributed
# by Shreyanshi Arun.
```

## C#

```
// C# program to find a subset of size 2 or
// greater with greatest geometric mean. This
// program basically find largest two elements.
using System;

class GFG {

    static void findLargestGM(int []arr, int n)
    {

        // There should be atleast two elements
        if (n < 2)
        {
            Console.Write("Invalid Input");
        }

        int first = -2147483648;
        int second = -2147483648;

        for (int i = 0; i < n ; i ++)
        {

            // If current element is smaller
            // than first then update both
            // first and second
            if (arr[i] > first)
            {
                second = first;
                first = arr[i];
            }

            // If arr[i] is in between first
            // and second then update second
            else if (arr[i] > second)
                second = arr[i];
        }

        Console.Write(second + " " + first);
    }

    // Driver code
    public static void Main()
    {
        int []arr = {12, 13, 17, 10, 34, 1};
        int n = arr.Length;

        findLargestGM(arr, n);
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find a subset of size 2 or
// greater with greatest geometric mean. This
// program basically find largest two elements.

function findLargestGM($arr, $n)
{
    /* There should be atleast two elements */
    if ($n < 2)
    {
        echo(" Invalid Input ");
        return;
    }

    $first = PHP_INT_MIN; $second = PHP_INT_MIN;
    for ($i = 0; $i < $n ; $i++)
    {
        /* If current element is smaller than first
        then update both first and second */
        if ($arr[$i] > $first)
        {
            $second = $first;
            $first = $arr[$i];
        }

        /* If arr[i] is in between first and second
        then update second */
        else if ($arr[$i] > $second)
            $second = $arr[$i];
    }

    echo($second . " " . $first);
}

/* Driver program to test above function */
$arr = array(12, 13, 17, 10, 34, 1);
$n = sizeof($arr);
findLargestGM($arr, $n);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find a subset of size 2 or
// greater with greatest geometric mean. This
// program basically find largest two elements.
function findLargestGM(arr, n)
{

    // There should be atleast two elements
    if (n < 2)
    {
        document.write("Invalid Input");
    }

    let first = -2147483648;
    let second = -2147483648;

    for(let i = 0; i < n ; i ++)
    {

        // If current element is smaller
        // than first then update both
        // first and second
        if (arr[i] > first)
        {
            second = first;
            first = arr[i];
        }

        // If arr[i] is in between first
        // and second then update second
        else if (arr[i] > second)
            second = arr[i];
    }
    document.write(second + " " + first);
}

// Driver code
let arr = [ 12, 13, 17, 10, 34, 1 ];
let n = arr.length;

findLargestGM(arr, n);

// This code is contribute by divyesh072019

</script>
```

输出:

```
17 34
```

时间复杂度:O(n)
空间复杂度:O(1)

本文由**丹麦语 _RAZA** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。