# 首先连续增加然后减少的阵列元素的总和

> 原文:[https://www . geesforgeks . org/sum-array-elements-first-continuous-递增-递减/](https://www.geeksforgeeks.org/sum-array-elements-first-continuously-increasing-decreasing/)

给定一个数组，其中元素首先连续增加，然后再次达到其连续减少的第一个单位数。我们想添加数组的元素。我们可以假设总和没有溢出。
示例:

```
Input  : arr[] = {5, 6, 7, 6, 5}.
Output : 29 

Input  : arr[] = {10, 11, 12, 13, 12, 11, 10}
Output : 79
```

一个**简单的解决方案**就是遍历 n，加上数组的元素。

## C++

```
// Simple C++ method to find sum of the
// elements of array.
#include <iostream>
using namespace std;
int arraySum(int arr[], int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum = sum + arr[i];
    return sum;
}

// Driver code
int main()
{
    int arr[] = {10, 11, 12, 13, 12, 11, 10};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << arraySum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Sum of array elements
// that is first continuously increasing
// then decreasing
class GFG {

    public static int arraySum(int arr[], int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum = sum + arr[i];
        return sum;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = {10, 11, 12, 13, 12, 11, 10};
        int n = arr.length;
        System.out.print(arraySum(arr, n));

    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Simple python method to find sum of the
# elements of array.
def arraySum( arr, n):
    _sum = 0
    for i in range(n):
        _sum = _sum + arr[i]
    return _sum

# Driver code
arr = [10, 11, 12, 13, 12, 11, 10]
n = len(arr)
print(arraySum(arr, n))

# This code is contributedc by "Abhishek Sharma 44"
```

## C#

```
// C# Code for Sum of array elements
// that is first continuously increasing
// then decreasing
using System;

class GFG {

    public static int arraySum(int []arr, int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum = sum + arr[i];
        return sum;
    }

    // Driver program
    public static void Main()
    {
        int []arr = {10, 11, 12, 13, 12, 11, 10};
        int n = arr.Length;
        Console.WriteLine(arraySum(arr, n));

    }
}
// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP method
// to find sum of the
// elements of array.
function arraySum($arr, $n)
{
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum = $sum + $arr[$i];
    return $sum;
}

// Driver code
$arr = array(10, 11, 12, 13,
             12, 11, 10);
$n = sizeof($arr);
echo(arraySum($arr, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
    // Simple Javascript method
// to find sum of the
// elements of array.
function arraySum(arr, n)
{
    let sum = 0;
    for (let i = 0; i < n; i++)
        sum = sum + arr[i];
    return sum;
}

// Driver code
let arr = [10, 11, 12, 13,
             12, 11, 10];
let n = arr.length;
document.write(arraySum(arr, n));

// This code is contributed by _saurabh_jaiswal.
</script>
```

输出:

```
79
```

一个**有效的解决方案**是应用下面的公式。

```
*sum = (arr[0] - 1)*n + ⌈n/2⌉<sup>2</sup>*

How does it work? 
If we take a closer look, we can notice that the
sum can be written as.

(arr[0] - 1)*n + (1 + 2 + .. x + (x -1) + (x-2) + ..1)
Let us understand above result with example {10, 11,
12, 13, 12, 11, 10}.  If we subtract 9 (arr[0]-1) from
this array, we get {1, 2, 3, 2, 1}.

Where x = ceil(n/2)  [Half of array size]

As we know that 1 + 2 + 3 + . . . + x = x * (x + 1)/2.
And we have given
    = 1 + 2 + 3 + . . . + x + (x - 1) + . . . + 3 + 2 + 1
    = (1 + 2 + 3 + . . . + x) + ((x - 1) + . . . + 3 + 2 + 1)
    = (x * (x + 1))/2 + ((x - 1) * x)/2
    = (x2 + x)/2 + (n2 - x)/2
    = (2 * x2)/2
    = x2
```

## C++

```
// Efficient C++ method to find sum of the
// elements of array that is halfway increasing
// and then halfway decreassing
#include <iostream>
using namespace std;

int arraySum(int arr[], int n)
{
    int x = (n+1)/2;
    return (arr[0] - 1)*n + x*x;
}

// Driver code
int main()
{
    int arr[] = {10, 11, 12, 13, 12, 11, 10};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << arraySum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Sum of array elements
// that is first continuously increasing
// then decreasing
class GFG {

    public static int arraySum(int arr[], int n)
    {
        int x = (n + 1) / 2;
        return (arr[0] - 1) * n + x * x;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = {10, 11, 12, 13, 12, 11, 10};
        int n = arr.length;
        System.out.print(arraySum(arr, n));  
    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Efficient python method to find sum of the
# elements of array that is halfway increasing
# and then halfway decreassing
def arraySum( arr, n):
    x = (n + 1)/2
    return (arr[0] - 1)*n + x * x

# Driver code
arr = [10, 11, 12, 13, 12, 11, 10]
n = len(arr)
print(arraySum(arr, n))

# This code is contributedc by "Abhishek Sharma 44"
```

## C#

```
// C# Code for Sum of array elements
// that is first continuously increasing
// then decreasing
using System;

class GFG {

    public static int arraySum(int []arr, int n)
    {
        int x = (n + 1) / 2;
        return (arr[0] - 1) * n + x * x;
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int []arr = {10, 11, 12, 13, 12, 11, 10};
        int n = arr.Length;
        Console.WriteLine(arraySum(arr, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP method to
// find sum of the elements
// of array that is halfway
// increasing and then halfway
// decreassing

function arraySum($arr, $n)
{
    $x = ($n + 1) / 2;
    return ($arr[0] - 1) *
            $n + $x * $x;
}

// Driver code
$arr = array(10, 11, 12, 13,
                12, 11, 10);
$n = sizeof($arr);
echo(arraySum($arr, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
// Efficient Javascript method to
// find sum of the elements
// of array that is halfway
// increasing and then halfway
// decreassing

function arraySum(arr, n)
{
    let x = (n + 1) / 2;
    return (arr[0] - 1) *
            n + x * x;
}

// Driver code
let arr = [10, 11, 12, 13,
                12, 11, 10];
let n = arr.length;
document.write(arraySum(arr, n));

// This code is contributed by _saurabh_jaiswal.
```

输出:

```
79
```

本文由**达曼德拉·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。