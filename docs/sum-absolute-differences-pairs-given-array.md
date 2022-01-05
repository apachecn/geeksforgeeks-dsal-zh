# 给定数组中所有对的绝对差之和

> 原文:[https://www . geesforgeks . org/sum-绝对差-对-给定-数组/](https://www.geeksforgeeks.org/sum-absolute-differences-pairs-given-array/)

给定不同元素的排序数组，任务是找出给定数组中所有对的绝对差的总和。
示例:

```
Input : arr[] = {1, 2, 3, 4}
Output: 10
Sum of |2-1| + |3-1| + |4-1| +
       |3-2| + |4-2| + |4-3| = 10

Input : arr[] = {1, 8, 9, 15, 16}
Output: 74

Input : arr[] = {1, 2, 3, 4, 5, 7, 9, 11, 14}
Output: 188
```

一个**这个问题的简单解决方法**就是一个一个的找每一对，取其差，一起总结。这种方法的时间复杂度为 0(n<sup>2</sup>)。
一个针对这个问题的**高效解决方案**需要简单观察。由于数组是排序的，并且元素是不同的，当我们取对的绝对差的和时，第 I 个位置的每个元素被加上 I 次，减去 n-1-i 次。
例如在{1，2，3，4}中，索引 2 处的元素是 arr[2] = 3，因此所有以 3 为一个元素的对都将是(1，3)、(2，3)和(3，4)，现在当我们对对的绝对差求和时，那么对于所有以 3 为一个元素的对，求和将是= (3-1)+(3-2)+(4-3)。我们可以看到，3 加 i = 2 次，减 n-1-i = (4-1-2) = 1 次。
每个元素的广义表达式为 sum = sum+(I * a[I])–(n-1-I)* a[I]。

## C++

```
// C++ program to find sum of absolutre differences
// in all pairs in a sorted array of distinct numbers
#include<bits/stdc++.h>
using namespace std;

// Function to calculate sum of absolute difference
// of all pairs in array
// arr[]  --> array of elements
int sumPairs(int arr[],int n)
{
    // final result
    int sum = 0;
    for (int i=n-1; i>=0; i--)
        sum += i*arr[i] - (n-1-i)*arr[i];
    return sum;
}

// Driver program to run the case
int main()
{
    int arr[] = {1, 8, 9, 15, 16};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << sumPairs(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of absolutre
// differences in all pairs in a sorted
// array of distinct numbers
class GFG {

    // Function to calculate sum of absolute
    // difference of all pairs in array
    // arr[] --> array of elements
    static int sumPairs(int arr[], int n)
    {

        // final result
        int sum = 0;
        for (int i = n - 1; i >= 0; i--)
            sum += i * arr[i] - (n - 1 - i)
                                  * arr[i];

        return sum;
    }

    // Driver program
    public static void main(String arg[])
    {
        int arr[] = { 1, 8, 9, 15, 16 };
        int n = arr.length;

        System.out.print(sumPairs(arr, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find sum of
# absolutre differences in all pairs
# in a sorted array of distinct numbers

# Function to calculate sum of absolute
# difference of all pairs in array
# arr[] --> array of elements
def sumPairs(arr, n):

    # final result
    sum = 0
    for i in range(n - 1, -1, -1):
        sum += i*arr[i] - (n-1-i) * arr[i]
    return sum

# Driver program
arr = [1, 8, 9, 15, 16]
n = len(arr)
print(sumPairs(arr, n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find sum of absolutre
// differences in all pairs in a sorted
// array of distinct numbers
using System;
class GFG {

    // Function to calculate sum of absolute
    // difference of all pairs in array
    // arr[] --> array of elements
    static int sumPairs(int []arr, int n)
    {

        // final result
        int sum = 0;
        for (int i = n - 1; i >= 0; i--)
            sum += i * arr[i] - (n - 1 - i)
                                  * arr[i];

        return sum;
    }

    // Driver program
    public static void Main()
    {
        int []arr = { 1, 8, 9, 15, 16 };
        int n = arr.Length;

        Console.Write(sumPairs(arr, n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP program to find sum of absolutre differences
// in all pairs in a sorted array of distinct numbers

// Function to calculate sum of absolute difference
// of all pairs in array
// arr[] --> array of elements
function sumPairs($arr,$n)
{
    // final result
    $sum = 0;
    for ($i=$n-1; $i>=0; $i--)
        $sum =  $sum + $i*$arr[$i] - ($n-1-$i)*$arr[$i];
    return $sum;
}

// Driver program to run the case
$arr = array(1, 8, 9, 15, 16);
    $n = sizeof($arr)/sizeof($arr[0]);
    echo sumPairs($arr, $n);
?>
```

## java 描述语言

```
<script>

// JavaScript program to find
// sum of absolutre differences
// in all pairs in a sorted array
// of distinct numbers

// Function to calculate sum of absolute difference
// of all pairs in array
// arr[]  --> array of elements
function sumPairs( arr, n)
{
    // final result
    let sum = 0;
    for (let i=n-1; i>=0; i--)
        sum += i*arr[i] - (n-1-i)*arr[i];
    return sum;
}

// Driver program to run the case
let arr = [ 1, 8, 9, 15, 16 ];
let n = arr.length;
document.write(sumPairs(arr, n));

</script>
```

**输出:**

```
74
```

时间复杂度:O(n)
辅助空间:O(1)e
**如果数组没有排序怎么办？**
对于数组未排序的情况，高效的解决方案也更好。我们可以先在 O(n Log n)时间内对数组进行排序，然后在 O(n)中找到需要的值。所以整体时间复杂度为 O(n Log n)仍然优于 O(n <sup>2</sup> )
本文由[**Shashank Mishra(Gulu)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。