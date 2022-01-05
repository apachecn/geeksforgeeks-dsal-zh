# 使用递归检查数组是否回文的程序

> 原文:[https://www . geesforgeks . org/program-to-check-如果数组是回文或不使用递归/](https://www.geeksforgeeks.org/program-to-check-if-an-array-is-palindrome-or-not-using-recursion/)

给定一个数组。任务是使用递归来确定一个数组是否是回文。
**例:**

```
Input: arr[] = {3, 6, 0, 6, 3}
Output: Palindrome

Input: arr[] = {1, 2, 3, 4, 5}
Output: Not Palindrome
```

**进场:**

1.  **基本情况:**如果数组只有一个元素，即 begin == end 则返回 1，同样如果 begin > end 表示数组是回文，则也返回 1。
2.  如果第一个和最后一个元素相等，则再次递归调用该函数，但递增从 1 开始，递减从 1 结束。
3.  如果第一个和最后一个元素不相等，则返回 0。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <iostream>
using namespace std;

// Recursive function that returns 1 if
// palindrome, 0 if not palindrome
int palindrome(int arr[], int begin, int end)
{
    // base case
    if (begin >= end) {
        return 1;
    }
    if (arr[begin] == arr[end]) {
        return palindrome(arr, begin + 1, end - 1);
    }
    else {
        return 0;
    }
}

// Driver code
int main()
{
    int a[] = { 3, 6, 0, 6, 3 };
    int n = sizeof(a) / sizeof(a[0]);

    if (palindrome(a, 0, n - 1) == 1)
        cout << "Palindrome";
    else
        cout << "Not Palindrome";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

import java.io.*;

class GFG {

// Recursive function that returns 1 if
// palindrome, 0 if not palindrome
static int palindrome(int arr[], int begin, int end)
{
    // base case
    if (begin >= end) {
        return 1;
    }
    if (arr[begin] == arr[end]) {
        return palindrome(arr, begin + 1, end - 1);
    }
    else {
        return 0;
    }
}

// Driver code
    public static void main (String[] args) {
    int a[] = { 3, 6, 0, 6, 3 };
    int n = a.length;

    if (palindrome(a, 0, n - 1) == 1)
        System.out.print( "Palindrome");
    else
        System.out.println( "Not Palindrome");
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Recursive function that returns 1 if
# palindrome, 0 if not palindrome
def palindrome(arr, begin, end):

    # base case
    if (begin >= end) :
        return 1

    if (arr[begin] == arr[end]) :
        return palindrome(arr, begin + 1,
                                 end - 1)

    else :
        return 0

# Driver code
if __name__ == "__main__":
    a = [ 3, 6, 0, 6, 3 ]
    n = len(a)

    if (palindrome(a, 0, n - 1) == 1):
        print("Palindrome")
    else:
        print("Not Palindrome")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Recursive function that returns 1
// if palindrome, 0 if not palindrome
static int palindrome(int []arr,
                      int begin, int end)
{
    // base case
    if (begin >= end)
    {
        return 1;
    }
    if (arr[begin] == arr[end])
    {
        return palindrome(arr, begin + 1,
                               end - 1);
    }
    else
    {
        return 0;
    }
}

// Driver code
public static void Main ()
{
    int []a = { 3, 6, 0, 6, 3 };
    int n = a.Length;

    if (palindrome(a, 0, n - 1) == 1)
        Console.WriteLine("Palindrome");
    else
        Console.WriteLine("Not Palindrome");
}
}

// This code is contributed by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Recursive function that returns 1
// if palindrome, 0 if not palindrome
function palindrome($arr, $begin, $end)
{
    // base case
    if ($begin >= $end)
    {
        return 1;
    }
    if ($arr[$begin] == $arr[$end])
    {
        return palindrome($arr, $begin + 1,
                                $end - 1);
    }
    else
    {
        return 0;
    }
}

// Driver code
$a = array( 3, 6, 0, 6, 3 );
$n = count($a);

if (palindrome($a, 0, $n - 1) == 1)
    echo "Palindrome";
else
    echo "Not Palindrome";

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    // Recursive function that returns 1 if
    // palindrome, 0 if not palindrome
    function palindrome(arr, begin, end)
    {
        // base case
        if (begin >= end) {
            return 1;
        }
        if (arr[begin] == arr[end]) {
            return palindrome(arr, begin + 1, end - 1);
        }
        else {
            return 0;
        }
    }

// Driver code
    let a = [ 3, 6, 0, 6, 3 ];
    let n = a.length;

    if (palindrome(a, 0, n - 1) == 1)
        document.write("Palindrome");
    else
        document.write("Not Palindrome");

        // This code is contributed by divyeshrabadiya07.

</script>
```

**Output:** 

```
Palindrome
```