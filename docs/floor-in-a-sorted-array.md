# 排序数组中的楼层

> 原文:[https://www.geeksforgeeks.org/floor-in-a-sorted-array/](https://www.geeksforgeeks.org/floor-in-a-sorted-array/)

给定一个排序数组和一个值 x，x 的 floor 是数组中小于或等于 x 的最大元素，写高效函数求 x 的 floor
**例:**

```
Input : arr[] = {1, 2, 8, 10, 10, 12, 19}, x = 5
Output : 2
2 is the largest element in 
arr[] smaller than 5.

Input : arr[] = {1, 2, 8, 10, 10, 12, 19}, x = 20
Output : 19
19 is the largest element in
arr[] smaller than 20.

Input : arr[] = {1, 2, 8, 10, 10, 12, 19}, x = 0
Output : -1
Since floor doesn't exist,
output is -1.
```

**<u>简单方法</u>**
**方法:**思路很简单，遍历数组找到第一个大于 x 的元素，找到的元素之前的元素就是 x 的楼层
**算法:**

1.  从头到尾遍历数组。
2.  如果当前元素大于 x，打印前一个数字并中断循环。
3.  如果没有大于 x 的数字，则打印最后一个元素
4.  如果第一个数字大于 x，则打印-1

## C++

```
// C++ program to find floor of a given number
// in a sorted array
#include <iostream>
using namespace std;

/* An inefficient function to get
index of floor of x in arr[0..n-1] */
int floorSearch(int arr[], int n, int x)
{
    // If last element is smaller than x
    if (x >= arr[n - 1])
        return n - 1;

    // If first element is greater than x
    if (x < arr[0])
        return -1;

    // Linearly search for the first element
    // greater than x
    for (int i = 1; i < n; i++)
        if (arr[i] > x)
            return (i - 1);

    return -1;
}

/* Driver program to check above functions */
int main()
{
    int arr[] = { 1, 2, 4, 6, 10, 12, 14 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 7;
    int index = floorSearch(arr, n - 1, x);
    if (index == -1)
        cout<<"Floor of "<<x <<" doesn't exist in array ";
    else
        cout<<"Floor of "<< x <<" is " << arr[index];
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C/C++ program to find floor of a given number
// in a sorted array
#include <stdio.h>

/* An inefficient function to get
index of floor of x in arr[0..n-1] */
int floorSearch(int arr[], int n, int x)
{
    // If last element is smaller than x
    if (x >= arr[n - 1])
        return n - 1;

    // If first element is greater than x
    if (x < arr[0])
        return -1;

    // Linearly search for the first element
    // greater than x
    for (int i = 1; i < n; i++)
        if (arr[i] > x)
            return (i - 1);

    return -1;
}

/* Driver program to check above functions */
int main()
{
    int arr[] = { 1, 2, 4, 6, 10, 12, 14 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 7;
    int index = floorSearch(arr, n - 1, x);
    if (index == -1)
        printf("Floor of %d doesn't exist in array ", x);
    else
        printf("Floor of %d is %d", x, arr[index]);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find floor of
// a given number in a sorted array
import java.io.*;
import java.util.*;
import java.lang.*;

class GFG {

    /* An inefficient function to get index of floor
of x in arr[0..n-1] */
    static int floorSearch(
        int arr[], int n, int x)
    {
        // If last element is smaller than x
        if (x >= arr[n - 1])
            return n - 1;

        // If first element is greater than x
        if (x < arr[0])
            return -1;

        // Linearly search for the first element
        // greater than x
        for (int i = 1; i < n; i++)
            if (arr[i] > x)
                return (i - 1);

        return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 4, 6, 10, 12, 14 };
        int n = arr.length;
        int x = 7;
        int index = floorSearch(arr, n - 1, x);
        if (index == -1)
            System.out.print(
                "Floor of " + x
                + " doesn't exist in array ");
        else
            System.out.print(
                "Floor of " + x + " is "
                + arr[index]);
    }
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# Python3 program to find floor of a
# given number in a sorted array

# Function to get index of floor
# of x in arr[low..high]
def floorSearch(arr, low, high, x):

    # If low and high cross each other
    if (low > high):
        return -1

    # If last element is smaller than x
    if (x >= arr[high]):
        return high

    # Find the middle point
    mid = int((low + high) / 2)

    # If middle point is floor.
    if (arr[mid] == x):
        return mid

    # If x lies between mid-1 and mid
    if (mid > 0 and arr[mid-1] <= x
                and x < arr[mid]):
        return mid - 1

    # If x is smaller than mid,
    # floor must be in left half.
    if (x < arr[mid]):
        return floorSearch(arr, low, mid-1, x)

    # If mid-1 is not floor and x is greater than
    # arr[mid],
    return floorSearch(arr, mid + 1, high, x)

# Driver Code
arr = [1, 2, 4, 6, 10, 12, 14]
n = len(arr)
x = 7
index = floorSearch(arr, 0, n-1, x)

if (index == -1):
    print("Floor of", x, "doesn't exist \
                    in array ", end = "")
else:
    print("Floor of", x, "is", arr[index])

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# program to find floor of a given number
// in a sorted array
using System;

class GFG {

    /* An inefficient function to get index of floor
of x in arr[0..n-1] */
    static int floorSearch(int[] arr, int n, int x)
    {
        // If last element is smaller than x
        if (x >= arr[n - 1])
            return n - 1;

        // If first element is greater than x
        if (x < arr[0])
            return -1;

        // Linearly search for the first element
        // greater than x
        for (int i = 1; i < n; i++)
            if (arr[i] > x)
                return (i - 1);

        return -1;
    }

    // Driver Code
    static void Main()
    {
        int[] arr = { 1, 2, 4, 6, 10, 12, 14 };
        int n = arr.Length;
        int x = 7;
        int index = floorSearch(arr, n - 1, x);
        if (index == -1)
            Console.WriteLine("Floor of " + x + " doesn't exist in array ");
        else
            Console.WriteLine("Floor of " + x + " is " + arr[index]);
    }
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find floor of
// a given number in a sorted array

/* An inefficient function
   to get index of floor
   of x in arr[0..n-1] */

function floorSearch($arr, $n, $x)
{
    // If last element is smaller
    // than x
    if ($x >= $arr[$n - 1])
        return $n - 1;

    // If first element is greater
    // than x
    if ($x < $arr[0])
        return -1;

    // Linearly search for the
    // first element greater than x
    for ($i = 1; $i < $n; $i++)
    if ($arr[$i] > $x)
        return ($i - 1);

    return -1;
}

// Driver Code
$arr = array (1, 2, 4, 6, 10, 12, 14);
$n = sizeof($arr);
$x = 7;
$index = floorSearch($arr, $n - 1, $x);
if ($index == -1)
    echo "Floor of ", $x,
         "doesn't exist in array ";
else
    echo "Floor of ", $x,
         " is ", $arr[$index];

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to find floor of
// a given number in a sorted array

    /* An inefficient function to get index of floor
of x in arr[0..n-1] */
    function floorSearch(arr, n, x)
    {
        // If last element is smaller than x
        if (x >= arr[n - 1])
            return n - 1;

        // If first element is greater than x
        if (x < arr[0])
            return -1;

        // Linearly search for the first element
        // greater than x
        for (let i = 1; i < n; i++)
            if (arr[i] > x)
                return (i - 1);

        return -1;
    }

// Driver Code

        let arr = [ 1, 2, 4, 6, 10, 12, 14 ];
        let n = arr.length;
        let x = 7;
        let index = floorSearch(arr, n - 1, x);
        if (index == -1)
             document.write(
                "Floor of " + x
                + " doesn't exist in array ");
        else
             document.write(
                "Floor of " + x + " is "
                + arr[index]);

</script>
```

**输出:**

```
Floor of 7 is 6.
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    遍历一个数组只需要一个循环，因此时间复杂度为 O(n)。
*   **空间复杂度:** O(1)。
    不需要额外的空间，所以空间复杂度是恒定的

**<u>高效法</u>**
**进场:**问题有蹊跷，给定数组排序。其思想是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)通过将一个数字 *x* 与中间元素进行比较，并将搜索空间分成两半，从而在排序后的数组中找到该数字的楼层。
**算法:**

1.  该算法可以递归实现，也可以通过迭代实现，但基本思想保持不变。
2.  有一些基本案件需要处理。
    1.  如果没有大于 x 的数字，则打印最后一个元素
    2.  如果第一个数字大于 x，则打印-1
3.  创建三个变量 *low = 0* ，mid 和 *high = n-1* 和另一个变量来存储答案
4.  运行循环或递归，直到且除非 low 小于或等于 high。
5.  检查中间(*(低+高)/2* )元素是否小于 x，如果是则更新低，即*低=中间+ 1* ，用中间元素更新答案。在这一步中，我们将搜索空间减少到一半。
6.  否则更新低，即*高=中-1*
7.  打印答案。

## C++

```
// A C/C++ program to find floor
// of a given number in a sorted array
#include <iostream>
using namespace std;

/* Function to get index of floor of x in
   arr[low..high] */
int floorSearch(int arr[], int low,
                int high, int x)
{
    // If low and high cross each other
    if (low > high)
        return -1;

    // If last element is smaller than x
    if (x >= arr[high])
        return high;

    // Find the middle point
    int mid = (low + high) / 2;

    // If middle point is floor.
    if (arr[mid] == x)
        return mid;

    // If x lies between mid-1 and mid
    if (mid > 0 && arr[mid - 1] <= x
        && x < arr[mid])
        return mid - 1;

    // If x is smaller than mid, floor
    // must be in left half.
    if (x < arr[mid])
        return floorSearch(
            arr, low, mid - 1, x);

    // If mid-1 is not floor and x is
    // greater than arr[mid],
    return floorSearch(arr, mid + 1, high, x);
}

/* Driver program to check above functions */
int main()
{
    int arr[] = { 1, 2, 4, 6, 10, 12, 14 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 7;
    int index = floorSearch(arr, 0, n - 1, x);
    if (index == -1)
        cout<< "Floor of " <<x <<" doesn't exist in array ";
    else
        cout<<"Floor of "<< x <<" is " << arr[index];
    return 0;
}

// this code is contributed by shivanisinghss2110
```

## C

```
// A C/C++ program to find floor
// of a given number in a sorted array
#include <stdio.h>

/* Function to get index of floor of x in
   arr[low..high] */
int floorSearch(int arr[], int low,
                int high, int x)
{
    // If low and high cross each other
    if (low > high)
        return -1;

    // If last element is smaller than x
    if (x >= arr[high])
        return high;

    // Find the middle point
    int mid = (low + high) / 2;

    // If middle point is floor.
    if (arr[mid] == x)
        return mid;

    // If x lies between mid-1 and mid
    if (mid > 0 && arr[mid - 1] <= x
        && x < arr[mid])
        return mid - 1;

    // If x is smaller than mid, floor
    // must be in left half.
    if (x < arr[mid])
        return floorSearch(
            arr, low, mid - 1, x);

    // If mid-1 is not floor and x is
    // greater than arr[mid],
    return floorSearch(arr, mid + 1, high, x);
}

/* Driver program to check above functions */
int main()
{
    int arr[] = { 1, 2, 4, 6, 10, 12, 14 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 7;
    int index = floorSearch(arr, 0, n - 1, x);
    if (index == -1)
        printf(
            "Floor of %d doesn't exist in array ", x);
    else
        printf(
            "Floor of %d is %d", x, arr[index]);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find floor of
// a given number in a sorted array
import java.io.*;

class GFG {

    /* Function to get index of floor of x in
    arr[low..high] */
    static int floorSearch(
        int arr[], int low,
        int high, int x)
    {
        // If low and high cross each other
        if (low > high)
            return -1;

        // If last element is smaller than x
        if (x >= arr[high])
            return high;

        // Find the middle point
        int mid = (low + high) / 2;

        // If middle point is floor.
        if (arr[mid] == x)
            return mid;

        // If x lies between mid-1 and mid
        if (
            mid > 0 && arr[mid - 1] <= x && x < arr[mid])
            return mid - 1;

        // If x is smaller than mid, floor
        // must be in left half.
        if (x < arr[mid])
            return floorSearch(
                arr, low,
                mid - 1, x);

        // If mid-1 is not floor and x is
        // greater than arr[mid],
        return floorSearch(
            arr, mid + 1, high,
            x);
    }

    /* Driver program to check above functions */
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 4, 6, 10, 12, 14 };
        int n = arr.length;
        int x = 7;
        int index = floorSearch(
            arr, 0, n - 1,
            x);
        if (index == -1)
            System.out.println(
                "Floor of " + x + " dosen't exist in array ");
        else
            System.out.println(
                "Floor of " + x + " is " + arr[index]);
    }
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 program to find floor of a 
# given number in a sorted array

# Function to get index of floor
# of x in arr[low..high]
def floorSearch(arr, low, high, x):

    # If low and high cross each other
    if (low > high):
        return -1

    # If last element is smaller than x
    if (x >= arr[high]):
        return high

    # Find the middle point
    mid = int((low + high) / 2)

    # If middle point is floor.
    if (arr[mid] == x):
        return mid

    # If x lies between mid-1 and mid
    if (mid > 0 and arr[mid-1] <= x
                and x < arr[mid]):
        return mid - 1

    # If x is smaller than mid, 
    # floor must be in left half.
    if (x < arr[mid]):
        return floorSearch(arr, low, mid-1, x)

    # If mid-1 is not floor and x is greater than
    # arr[mid],
    return floorSearch(arr, mid + 1, high, x)

# Driver Code
arr = [1, 2, 4, 6, 10, 12, 14]
n = len(arr)
x = 7
index = floorSearch(arr, 0, n-1, x)

if (index == -1):
    print("Floor of", x, "doesn't exist\
                    in array ", end = "")
else:
    print("Floor of", x, "is", arr[index])

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# program to find floor of
// a given number in a sorted array
using System;

class GFG {

    /* Function to get index of floor of x in
    arr[low..high] */
    static int floorSearch(
        int[] arr, int low,
        int high, int x)
    {

        // If low and high cross each other
        if (low > high)
            return -1;

        // If last element is smaller than x
        if (x >= arr[high])
            return high;

        // Find the middle point
        int mid = (low + high) / 2;

        // If middle point is floor.
        if (arr[mid] == x)
            return mid;

        // If x lies between mid-1 and mid
        if (mid > 0 && arr[mid - 1] <= x && x < arr[mid])
            return mid - 1;

        // If x is smaller than mid, floor
        // must be in left half.
        if (x < arr[mid])
            return floorSearch(arr, low,
                               mid - 1, x);

        // If mid-1 is not floor and x is
        // greater than arr[mid],
        return floorSearch(arr, mid + 1, high,
                           x);
    }

    /* Driver program to check above functions */
    public static void Main()
    {
        int[] arr = { 1, 2, 4, 6, 10, 12, 14 };
        int n = arr.Length;
        int x = 7;
        int index = floorSearch(arr, 0, n - 1,
                                x);
        if (index == -1)
            Console.Write("Floor of " + x + " dosen't exist in array ");
        else
            Console.Write("Floor of " + x + " is " + arr[index]);
    }
}

// This code is contributed by nitin mittal.
```

## java 描述语言

```
<script>

// javascript program to find floor of
// a given number in a sorted array

/* Function to get index of floor of x in
arr[low..high] */
function floorSearch(
    arr , low,
    high , x)
{
    // If low and high cross each other
    if (low > high)
        return -1;

    // If last element is smaller than x
    if (x >= arr[high])
        return high;

    // Find the middle point
    var mid = (low + high) / 2;

    // If middle point is floor.
    if (arr[mid] == x)
        return mid;

    // If x lies between mid-1 and mid
    if (
        mid > 0 && arr[mid - 1] <= x && x < arr[mid])
        return mid - 1;

    // If x is smaller than mid, floor
    // must be in left half.
    if (x < arr[mid])
        return floorSearch(
            arr, low,
            mid - 1, x);

    // If mid-1 is not floor and x is
    // greater than arr[mid],
    return floorSearch(
        arr, mid + 1, high,
        x);
}

/* Driver program to check above functions */
var arr = [ 1, 2, 4, 6, 10, 12, 14 ];
var n = arr.length;
var x = 7;
var index = floorSearch(
    arr, 0, n - 1,
    x);
if (index == -1)
    document.write(
        "Floor of " + x + " dosen't exist in array ");
else
    document.write(
        "Floor of " + x + " is " + arr[index]);

// This code is contributed by Amit Katiyar
</script>
```

**输出:**

```
Floor of 7 is 6.
```

**复杂度分析:**

*   **时间复杂度:** O(log n)。
    要运行二分搜索法，所需的时间复杂度为 0(对数 n)。
*   **空间复杂度:** O(1)。
    由于不需要额外的空间，所以空间复杂度不变。

本文由 **Mayank Agrawal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。