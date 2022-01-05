# 数组中所有成对连续元素的绝对差值

> 原文:[https://www . geeksforgeeks . org/数组中所有成对连续元素的绝对差值/](https://www.geeksforgeeks.org/absolute-difference-of-all-pairwise-consecutive-elements-in-an-array/)

给定 N 个元素的整数数组。任务是打印所有成对连续元素的绝对差值。
大小为 N 的数组的成对连续对是(a[i]，a[i+1])，所有 I 的范围从 0 到 N-2
**示例:**

```
Input: arr[] = {8, 5, 4, 3, 15, 20}
Output: 3, 1, 1, 12, 5

Input: arr[] = {5, 10, 15, 20}
Output: 5, 5, 5
```

**方法:**解决方法是遍历数组，计算并打印每对的绝对差(arr[i]，arr[i+1])。
以下是上述办法的实施情况:

## C++

```
// C++ program to print the absolute
// difference of the consecutive elements
#include <iostream>
using namespace std;

// Function to print pairwise absolute
// difference of consecutive elements
void pairwiseDifference(int arr[], int n)
{
    int diff;
    for (int i = 0; i < n - 1; i++) {

        // absolute difference between
        // consecutive numbers
        diff = abs(arr[i] - arr[i + 1]);
        cout << diff << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 4, 10, 15, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    pairwiseDifference(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the absolute
// difference of the consecutive elements

class GFG{
// Function to print pairwise absolute
// difference of consecutive elements
static void pairwiseDifference(int arr[], int n)
{
    int diff;
    for (int i = 0; i < n - 1; i++) {

        // absolute difference between
        // consecutive numbers
        diff = Math.abs(arr[i] - arr[i + 1]);
        System.out.print(diff+" ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 10, 15, 5, 6 };
    int n = arr.length;

    pairwiseDifference(arr, n);
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python 3 program to print the absolute
# difference of the consecutive elements

# Function to print pairwise absolute
# difference of consecutive elements
def pairwiseDifference(arr, n):

    for i in range(n - 1) :

        # absolute difference between
        # consecutive numbers
        diff = abs(arr[i] - arr[i + 1])
        print(diff , end = " ")

# Driver Code
if __name__=="__main__":
    arr = [ 4, 10, 15, 5, 6 ]
    n = len(arr)

    pairwiseDifference(arr, n)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to print the absolute
// difference of the consecutive elements
using System;

class GFG{
// Function to print pairwise absolute
// difference of consecutive elements
static void pairwiseDifference(int []arr, int n)
{
    int diff;
    for (int i = 0; i < n - 1; i++) {

        // absolute difference between
        // consecutive numbers
        diff = Math.Abs(arr[i] - arr[i + 1]);
        Console.WriteLine(diff+" ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 4, 10, 15, 5, 6 };
    int n = arr.Length;

    pairwiseDifference(arr, n);
}
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the absolute
// difference of the consecutive elements

// Function to print pairwise absolute
// difference of consecutive elements
function pairwiseDifference($arr, $n)
{
    $diff = 0;
    for ($i = 0; $i < $n - 1; $i++)
    {

        // absolute difference between
        // consecutive numbers
        $diff = abs($arr[$i] - $arr[$i + 1]);
        echo $diff." ";
    }
}

// Driver Code
$arr = array( 4, 10, 15, 5, 6 );
$n = sizeof($arr);

pairwiseDifference($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to print the absolute
// difference of the consecutive elements    
// Function to print pairwise absolute
    // difference of consecutive elements
    function pairwiseDifference(arr , n) {
        var diff;
        for (i = 0; i < n - 1; i++) {

            // absolute difference between
            // consecutive numbers
            diff = Math.abs(arr[i] - arr[i + 1]);
            document.write(diff + " ");
        }
    }

    // Driver Code

        var arr = [ 4, 10, 15, 5, 6 ];
        var n = arr.length;

        pairwiseDifference(arr, n);

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
6 5 10 1
```

**时间复杂度:** O(n)