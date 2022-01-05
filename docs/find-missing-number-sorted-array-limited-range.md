# 在有限范围的排序数组中找到缺失的数字

> 原文:[https://www . geesforgeks . org/find-missing-number-sorted-array-limited-range/](https://www.geeksforgeeks.org/find-missing-number-sorted-array-limited-range/)

给定一个大小为 n 的排序数组，并且给定从 1 到 n+1 的数字中有一个缺失，那么将找到缺失的数字。可以假设数组有不同的元素。
**例:**

```
Input : 1 3 4 5 6
Output : 2

Input  : 1 2 3 4 5 7 8 9 10
Output  : 6
```

我们遍历所有元素。对于每个元素 a[i]，我们检查它是否等于 i+1。如果没有，我们返回(i+1)。

## C++

```
// C++ program to find missing Number in
// a sorted array of size n and distinct
// elements.
#include<bits/stdc++.h>
using namespace std;

// Function to find missing number
int getMissingNo(int a[], int n)
{
    for (int i=0; i<n; i++)       
        if (a[i] != (i+1))
            return (i+1);

    // If all numbers from 1 to n
    // are present
    return n+1;
}

// Driver code
int main()
{
    int a[] = {1, 2, 4, 5, 6};
    int n = sizeof(a) / sizeof(a[0]);
    cout << getMissingNo(a, n);
    return 0;
}

// This code is contributed by Sachin Bisht
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find missing Number in
// a sorted array of size n and distinct
// elements.
class Main
{
    // Function to find missing number
    static int getMissingNo(int a[])
    {
        int n = a.length;
        for (int i=0; i<n; i++)       
            if (a[i] != (i+1))
                return (i+1);

        // If all numbers from 1 to n
        // are present
        return n+1;
    }

    /* program to test above function */
    public static void main(String args[])
    {
        int a[] = {1, 2, 4, 5, 6};
        System.out.println(getMissingNo(a));
    }
}
```

## 计算机编程语言

```
# Python program to find missing Number in
# a sorted array of size n and distinct
# elements.

# function to find missing number
def getMissingNo(a):
    n = len(a)

    for i in range(n):
        if(a[i] != i + 1):
            return i + 1

    # If all numbers from 1 to n
    # are present
    return n+1

# Driver code
a = [1, 2, 4, 5, 6]
print(getMissingNo(a))

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to find missing Number
// in a sorted array of size n and
// distinct elements.
using System;

class GFG
{

// Function to find missing number
static int getMissingNo(int []a, int n)
{
    for (int i = 0; i < n; i++)
        if (a[i] != (i + 1))
            return (i + 1);

    // If all numbers from
    // 1 to n are present
    return n + 1;
}

// Driver code
public static void Main()
{
    int []a = {1, 2, 4, 5, 6};
    int n = a.Length;
    Console.WriteLine(getMissingNo(a, n));
}
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find missing Number
// in a sorted array of size n and
// distinct elements.

// Function to find missing number
function getMissingNo($a, $n)
{
    for ($i = 0; $i < $n; $i++)
        if ($a[$i] != ($i + 1))
            return ($i + 1);

    // If all numbers from
    // 1 to n are present
    return $n + 1;
}

// Driver code
$a = array(1, 2, 4, 5, 6);
$n = sizeof($a);
echo getMissingNo($a, $n);

// This code is contributed
// by ihritik
?>
```

## java 描述语言

```
<script>
// javascript program to find missing Number
// in a sorted array of size n and
// distinct elements.

// Function to find missing number
function getMissingNo(a,n)
{
    for (let i = 0; i < n; i++)
        if (a[i] != (i + 1))
            return (i + 1);

    // If all numbers from
    // 1 to n are present
    return n + 1;
}

// Driver code
let a = [1, 2, 4, 5, 6]
let n = a.length;
document.write(getMissingNo(a, n));

// This code is contributed by mohit kumar 29.
</script>
```

**输出:**

```
3
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*
本文由**巴拉古鲁**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。