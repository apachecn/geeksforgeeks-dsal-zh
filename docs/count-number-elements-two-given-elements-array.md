# 计算数组中两个给定元素之间的元素数量

> 原文:[https://www . geesforgeks . org/count-number-elements-two-given-elements-array/](https://www.geeksforgeeks.org/count-number-elements-two-given-elements-array/)

给定一个由 n 个元素组成的未排序数组，同时给定两个点 num1 和 num2。任务是计算给定点之间出现的元素数量(不包括 num1 和 num2)。
如果 num1 和 num2 出现多次，我们需要考虑 num1 最左边的出现和 num2 最右边的出现。
示例:

```
Input : arr[] = {3 5 7 6 4 9 12 4 8}
        num1 = 5
        num2 = 4
Output : 5
Number of elements between leftmost occurrence
of 5 and rightmost occurrence of 4 is five.

Input : arr[] = {4, 6, 8, 3, 6, 2, 8, 9, 4}
        num1 = 4
        num2 = 4
Output : 7

Input : arr[] = {4, 6, 8, 3, 6, 2, 8, 9, 4}
        num1 = 4
        num2 = 10
Output : 0
```

在所有情况下(当单个或两个元素都不存在时)
解决方案应该只遍历数组一次

想法是从左边遍历数组，找到 num1 的第一个匹配项。如果到达终点，我们返回 0。然后我们从最右边的元素开始遍历，找到 num2。我们只遍历到大于 num1 索引的点。如果到达终点，我们返回 0。如果我们找到了这两个元素，我们使用找到的元素的索引返回计数。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// Program to count number of elements between
// two given elements.
#include <bits/stdc++.h>
using namespace std;

// Function to count number of elements
// occurs between the elements.
int getCount(int arr[], int n, int num1, int num2)
{
    // Find num1
    int i = 0;
    for (i = 0; i < n; i++)
        if (arr[i] == num1)
            break;

    // If num1 is not present or present at end
    if (i >= n-1)
        return 0;

    // Find num2
    int j;
    for (j = n-1; j >= i+1; j--)
        if (arr[j] == num2)
            break;

    // If num2 is not present
    if (j == i)
        return 0;

    // return number of elements between
    // the two elements.
    return (j - i - 1);
}

// Driver Code
int main()
{
    int arr[] = { 3, 5, 7, 6, 4, 9, 12, 4, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int num1 = 5, num2 = 4;
    cout << getCount(arr, n, num1, num2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to count number of elements
// between two given elements.
import java.io.*;

class GFG
{
    // Function to count number of elements
    // occurs between the elements.
    static int getCount(int arr[], int n,
                            int num1, int num2)
    {
        // Find num1
        int i = 0;
        for (i = 0; i < n; i++)
            if (arr[i] == num1)
                break;

        // If num1 is not present
        // or present at end
        if (i >= n - 1)
            return 0;

        // Find num2
        int j;
        for (j = n - 1; j >= i + 1; j--)
            if (arr[j] == num2)
                break;

        // If num2 is not present
        if (j == i)
            return 0;

        // return number of elements
        // between the two elements.
        return (j - i - 1);
    }

    // Driver program
    public static void main (String[] args)
    {
        int arr[] = { 3, 5, 7, 6, 4, 9, 12, 4, 8 };
        int n = arr.length;
        int num1 = 5, num2 = 4;
        System.out.println( getCount(arr, n, num1, num2));

    }
}
// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python Program to count number of elements between
# two given elements.

# Function to count number of elements
# occurs between the elements.
def getCount(arr, n, num1, num2):

    # Find num1
    for i in range(0,n):
        if (arr[i] == num1):
            break

    #If num1 is not present or present at end
    if (i >= n-1):
        return 0

    # Find num2
    for j in range(n-1, i+1, -1):
        if (arr[j] == num2):
            break

    # If num2 is not present
    if (j == i):
        return 0

    # return number of elements between
    # the two elements.
    return (j - i - 1)

# Driver Code
arr= [ 3, 5, 7, 6, 4, 9, 12, 4, 8 ]
n=len(arr)
num1 = 5
num2 = 4
print(getCount(arr, n, num1, num2))

# This code is contributed by SHARIQ_JMI
```

## C#

```
// C# Program to count number of elements
// between two given elements.
using System;

class GFG  {

    // Function to count number of elements
    // occurs between the elements.
    static int getCount(int []arr, int n,
                        int num1, int num2)
    {

        // Find num1
        int i = 0;
        for (i = 0; i < n; i++)
            if (arr[i] == num1)
                break;

        // If num1 is not present
        // or present at end
        if (i >= n - 1)
            return 0;

        // Find num2
        int j;
        for (j = n - 1; j >= i + 1; j--)
            if (arr[j] == num2)
                break;

        // If num2 is not present
        if (j == i)
            return 0;

        // return number of elements
        // between the two elements.
        return (j - i - 1);
    }

    // Driver Code
    public static void Main ()
    {
        int []arr = {3, 5, 7, 6, 4, 9, 12, 4, 8};
        int n = arr.Length;
        int num1 = 5, num2 = 4;
        Console.WriteLine(getCount(arr, n, num1, num2));

    }
}

// This article is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to count number
// of elements between
// two given elements.

// Function to count
// number of elements
// occurs between the
// elements.
function getCount($arr, $n,
                  $num1, $num2)
{

    // Find num1
    $i = 0;
    for ($i = 0; $i < $n; $i++)
        if ($arr[$i] == $num1)
            break;

    // If num1 is not present
    // or present at end
    if ($i >= $n - 1)
        return 0;

    // Find num2
    $j;
    for ($j = $n - 1; $j >= $i + 1; $j--)
        if ($arr[$j] == $num2)
            break;

    // If num2 is not present
    if ($j == $i)
        return 0;

    // return number of elements
    // betweenthe two elements.
    return ($j - $i - 1);
}

// Driver Code
$arr = array(3, 5, 7, 6, 4, 9, 12, 4, 8);
$n = sizeof($arr);
$num1 = 5; $num2 = 4;
echo(getCount($arr, $n, $num1, $num2));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Program to count number of elements between
// two given elements.

// Function to count number of elements
// occurs between the elements.
function getCount( arr, n, num1, num2)
{
    // Find num1
    let i = 0;
    for (i = 0; i < n; i++)
        if (arr[i] == num1)
            break;

    // If num1 is not present or present at end
    if (i >= n-1)
        return 0;

    // Find num2
    let j;
    for (j = n-1; j >= i+1; j--)
        if (arr[j] == num2)
            break;

    // If num2 is not present
    if (j == i)
        return 0;

    // return number of elements between
    // the two elements.
    return (j - i - 1);
}

    // Driver program

    let arr = [ 3, 5, 7, 6, 4, 9, 12, 4, 8 ];
    let n = arr.length;
    let num1 = 5, num2 = 4;
    document.write(getCount(arr, n, num1, num2));

</script>
```

**输出:**

```
5
```

**如何处理多个查询？**
为了处理多个查询，我们可以使用哈希并为数组中的每个元素存储最左边和最右边的索引。一旦我们存储了这些，我们就可以在 O(1)时间内回答所有的查询。
本文由 [**达曼德拉库马尔**](https://auth.geeksforgeeks.org/profile.php?user=dharammnnit&list=practice) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。