# 可被 90 整除的最大数字，可以用 0 和 5 来表示

> 原文:[https://www . geeksforgeeks . org/最大数字可被 90 整除-使用 0 和 5/](https://www.geeksforgeeks.org/largest-number-divisible-by-90-that-can-be-made-using-0-and-5/)

给定一个包含 N 个元素的数组。每个元素不是 0 就是 5。找到最大的可被 90 整除的数，这个数可以用这个数组的任意数量的元素组成，并以任何方式排列它们。

**示例**:

```
Input : arr[] = {5, 5, 5, 5, 5, 5, 5, 5, 0, 5, 5}
Output : 5555555550

Input : arr[] = {5, 0}
Output : 0 
```

因为我们可以选择和置换任意数量的元素，所以只有数组中 0 和 5s 的数量是重要的。让我们将计数分别存储为 c0 和 c5。
这个数字必须是 90 的 9*10 的倍数。因此，数字必须是 9 和 10 的倍数。
可分性规则如下:

*   一个数要能被 10 整除，就应该以 0 结尾。
*   一个数要能被 9 整除，数字的总和应该能被 9 整除。因为唯一允许使用的非零数字是 5，所以我们使用 5 的次数必须是 9 的倍数，这样总和将是 45 的倍数，即可以被 9 整除。

有 3 种可能:

*   c0=0。这意味着没有一个数能被 10 整除。
*   c5=0。这意味着唯一能被 90 整除的数字是 0。
*   如果以上两个条件都为假。让我们把 5s 的数量分成 9 组。将会有完全填满的地板(c5/9)组，我们可以使用所有组的所有 5s 来获得 9 的倍数，这也使得数字和是 9 的倍数。因为增加零的数量不会影响整除性，所以我们可以使用所有的零。

以下是上述方法的实现:

## C++

```
// CPP program to find largest number
// divisible by 90 that can be made
// using 0 and 5

#include <bits/stdc++.h>
using namespace std;

// Function to find largest number
// divisible by 90 that can be made
// using 0 and 5
void printLargestDivisible(int n, int a[])
{
    // Count of 0s and 5s
    int i, c0 = 0, c5 = 0;
    for (i = 0; i < n; i++) {
        if (a[i] == 0)
            c0++;
        else
            c5++;
    }

    // The number of 5s that can be used
    c5 = floor(c5 / 9) * 9;
    if (c0 == 0) // The number can't be
        cout << -1; // made multiple of 10
    else if (c5 == 0) // The only multiple of 90
        cout << 0; // that can be made is 0
    else {
        for (i = 0; i < c5; i++)
            cout << 5;
        for (i = 0; i < c0; i++)
            cout << 0;
    }
}

// Driver Code
int main()
{
    int a[] = { 5, 5, 5, 5, 5, 5, 5, 5, 0, 5, 5 };

    int n = sizeof(a) / sizeof(a[0]);

    printLargestDivisible(n, a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find largest number
// divisible by 90 that can be made
// using 0 and 5

import java.io.*;

class GFG {

// Function to find largest number
// divisible by 90 that can be made
// using 0 and 5
static void printLargestDivisible(int n, int a[])
{
    // Count of 0s and 5s
    int i, c0 = 0, c5 = 0;
    for (i = 0; i < n; i++) {
        if (a[i] == 0)
            c0++;
        else
            c5++;
    }

    // The number of 5s that can be used
    c5 = (int)Math.floor(c5 / 9) * 9;
    if (c0 == 0) // The number can't be
        System.out.print(-1); // made multiple of 10
    else if (c5 == 0) // The only multiple of 90
        System.out.println(0); // that can be made is 0
    else {
        for (i = 0; i < c5; i++)
            System.out.print(5);
        for (i = 0; i < c0; i++)
            System.out.print(0);
    }
}

// Driver Code

    public static void main (String[] args) {
        int a[] = { 5, 5, 5, 5, 5, 5, 5, 5, 0, 5, 5 };

    int n = a.length;

    printLargestDivisible(n, a);
    }
}
// This code is contributed
// by shs
```

## 蟒蛇 3

```
# Python3 program to find largest number
# divisible by 90 that can be made
# using 0 and 5

# from math import every methods
from math import *

# Function to find largest number
# divisible by 90 that can be made
# using 0 and 5
def printLargestDivisible(n, a) :

    # Count of 0s and 5s
    c0, c5 = 0, 0

    for i in range(n) :

        if a[i] == 0 :
            c0 += 1
        else :
            c5 += 1

    # The number of 5s that can be used
    c5 = floor(c5 / 9) * 9

    if c0 == 0 : # The number can't be
        print(-1,end = "") # made multiple of 10

    elif c5 == 0 : # The only multiple of 90
        print(0,end = "") # that can be made is 0

    else :

        for i in range(c5) :
            print(5,end = "")
        for i in range(c0) :
            print(0, end = "")

# Driver code
if __name__ == "__main__" :

    a = [ 5, 5, 5, 5, 5, 5, 5, 5, 0, 5, 5]
    n = len(a)

    # Function calling
    printLargestDivisible(n, a)

# This code is contributed by
# ANKITRAI1
```

## C#

```
// C# program to find largest number
// divisible by 90 that can be made
// using 0 and 5
using System;

class GFG {

// Function to find largest number
// divisible by 90 that can be made
// using 0 and 5
public static void printLargestDivisible(int n,
                                       int[] a)
{

    // Count of 0s and 5s
    int i, c0 = 0, c5 = 0;
    for (i = 0; i < n; i++)
    {
        if (a[i] == 0)
        {
            c0++;
        }
        else
        {
            c5++;
        }
    }

    // The number of 5s that can be used
    c5 = (c5 / 9) * 9;

    // The number can't be
    if (c0 == 0)
    {

        // made multiple of 10
        Console.Write(-1);
    }

    // The only multiple of 90
    else if (c5 == 0)
    {

        // that can be made is 0
        Console.WriteLine(0);
    }
    else
    {
        for (i = 0; i < c5; i++)
        {
            Console.Write(5);
        }
        for (i = 0; i < c0; i++)
        {
            Console.Write(0);
        }
    }
}

    // Driver Code
    public static void Main(string[] args)
    {
        int[] a = new int[] {5, 5, 5, 5, 5,
                         5, 5, 5, 0, 5, 5};
        int n = a.Length;
        printLargestDivisible(n, a);
    }
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find largest number
// divisible by 90 that can be made
// using 0 and 5

// Function to find largest number
// divisible by 90 that can be made
// using 0 and 5
function printLargestDivisible($n, $a)
{
    // Count of 0s and 5s
    $i;
    $c0 = 0;
    $c5 = 0;
    for ($i = 0; $i < $n; $i++)
    {
        if ($a[$i] == 0)
            $c0++;
        else
            $c5++;
    }

    // The number of 5s that can be used
    $c5 = floor($c5 / 9) * 9;
    if ($c0 == 0) // The number can't be
        echo -1;  // made multiple of 10
    else if ($c5 == 0) // The only multiple of 90
        echo 0;        // that can be made is 0
    else
    {
        for ($i = 0; $i < $c5; $i++)
            echo 5;
        for ($i = 0; $i < $c0; $i++)
            echo 0;
    }
}

// Driver Code
$a = array( 5, 5, 5, 5, 5, 5,
            5, 5, 0, 5, 5 );

$n = sizeof($a);

printLargestDivisible($n, $a);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to find largest number
    // divisible by 90 that can be made
    // using 0 and 5

    // Function to find largest number
    // divisible by 90 that can be made
    // using 0 and 5
    function printLargestDivisible(n, a)
    {

        // Count of 0s and 5s
        let i, c0 = 0, c5 = 0;
        for (i = 0; i < n; i++)
        {
            if (a[i] == 0)
            {
                c0++;
            }
            else
            {
                c5++;
            }
        }

        // The number of 5s that can be used
        c5 = parseInt(c5 / 9, 10) * 9;

        // The number can't be
        if (c0 == 0)
        {

            // made multiple of 10
            document.write(-1);
        }

        // The only multiple of 90
        else if (c5 == 0)
        {

            // that can be made is 0
            document.write(0 + "</br>");
        }
        else
        {
            for (i = 0; i < c5; i++)
            {
                document.write(5);
            }
            for (i = 0; i < c0; i++)
            {
                document.write(0);
            }
        }
    }

    let a = [5, 5, 5, 5, 5, 5, 5, 5, 0, 5, 5];
    let n = a.length;
    printLargestDivisible(n, a);

</script>
```

**Output:** 

```
5555555550
```

**时间复杂度:** O(N)，其中 N 为数组中的元素个数。