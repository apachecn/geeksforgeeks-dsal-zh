# 偶宇称数组中元素的和

> 原文:[https://www . geeksforgeeks . org/从具有偶数奇偶校验的数组中提取元素的总和/](https://www.geeksforgeeks.org/sum-of-elements-from-an-array-having-even-parity/)

给定一个数组 **arr[]** ，任务是使用**逐位运算符**计算给定数组中具有**偶校验**的元素之和，即设置的位数为**偶**。

**示例:**

> **输入:** arr[] = {2，4，3，5，9}
> **输出:** 17
> 只有 3(0011)、5(0101)和 9(1001)有偶宇称
> 所以 3 + 5 + 9 = 17
> 
> **输入:** arr[] = {1，5，4，16，10 }
> T3】输出: 15

**方法:**初始化一个变量**和= 0** 并遍历数组从 **0** 到**n–1**，同时使用[布莱恩·克尼根算法](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)计算**arr【I】**中的设置位数。如果**计数**为**偶数**，则更新**总和=总和+ arr[i]** 。最后打印**和**。

下面是上述方法的实现:

## C++

```
// C++ program to find the sum of the elements
// from an array which have even parity
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if x has even parity
bool checkEvenParity(int x)
{
    // We basically count set bits
    // https://www.geeksforgeeks.org/count-set-bits-in-an-integer/
    int parity = 0;
    while (x != 0) {
        x = x & (x - 1);
        parity++;
    }

    if (parity % 2 == 0)
        return true;
    else
        return false;
}

// Function to return the sum of the elements
// from an array which have even parity
long sumlist(int a[], int n)
{
    long sum = 0;

    for (int i = 0; i < n; i++) {

        // If a[i] has even parity
        if (checkEvenParity(a[i]))
            sum += a[i];
    }
    return sum;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 3, 5, 9 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << sumlist(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of the elements
// from an array which have even parity

import java.io.*;

class GFG {

// Function that returns true if x has even parity
static boolean checkEvenParity(int x)
{
    // We basically count set bits
    // https://www.geeksforgeeks.org/count-set-bits-in-an-integer/
    int parity = 0;
    while (x != 0) {
        x = x & (x - 1);
        parity++;
    }

    if (parity % 2 == 0)
        return true;
    else
        return false;
}

// Function to return the sum of the elements
// from an array which have even parity
static long sumlist(int a[], int n)
{
    long sum = 0;

    for (int i = 0; i < n; i++) {

        // If a[i] has even parity
        if (checkEvenParity(a[i]))
            sum += a[i];
    }
    return sum;
}

// Driver code

    public static void main (String[] args) {
            int arr[] = { 2, 4, 3, 5, 9 };

    int n =arr.length;

    System.out.println(sumlist(arr, n));
    }
}
// This code is contributed by  inder_verma..
```

## 蟒蛇 3

```
# Python3 program to find the sum of the elements
# from an array which have even parity

# Function that returns true if x
# has even parity
def checkEvenParity(x):

    # We basically count set bits
    # https://www.geeksforgeeks.org/count-set-bits-in-an-integer/
    parity = 0
    while (x != 0):
        x = x & (x - 1)
        parity += 1

    if (parity % 2 == 0):
        return True
    else:
        return False

# Function to return the sum of the elements
# from an array which have even parity
def sumlist(a, n):
    sum = 0
    for i in range(n):

        # If a[i] has even parity
        if (checkEvenParity(a[i])):
            sum += a[i]
    return sum

# Driver code
if __name__ == '__main__':
    arr = [ 2, 4, 3, 5, 9 ]
    n = len(arr)
    print(sumlist(arr, n))

# This code is contributed by 29AjayKumar.
```

## C#

```
// C# program to find the sum of the elements
// from an array which have even parity

using System ;

class GFG {

// Function that returns true if x has even parity
static bool checkEvenParity(int x)
{
    // We basically count set bits
    // https://www.geeksforgeeks.org/count-set-bits-in-an-integer/
    int parity = 0;
    while (x != 0) {
        x = x & (x - 1);
        parity++;
    }

    if (parity % 2 == 0)
        return true;
    else
        return false;
}

// Function to return the sum of the elements
// from an array which have even parity
static long sumlist(int []a, int n)
{
    long sum = 0;

    for (int i = 0; i < n; i++) {

        // If a[i] has even parity
        if (checkEvenParity(a[i]))
            sum += a[i];
    }
    return sum;
}

// Driver code

    public static void Main () {
            int []arr = { 2, 4, 3, 5, 9 };

    int n =arr.Length;

    Console.WriteLine(sumlist(arr, n));
    }
    // This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum of the
// elements from an array which have
// even parity

// Function that returns true
// if x has even parity
function checkEvenParity($x)
{
    // We basically count set bits
    // https://www.geeksforgeeks.org/count-set-bits-in-an-integer/
    $parity = 0;
    while ($x != 0)
    {
        $x = ($x & ($x - 1));
        $parity++;
    }

    if ($parity % 2 == 0)
        return true;
    else
        return false;
}

// Function to return the sum of the elements
// from an array which have even parity
function sumlist($a, $n)
{
    $sum = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // If a[i] has even parity
        if (checkEvenParity($a[$i]))
            $sum += $a[$i];
    }
    return $sum;
}

// Driver code
$arr = array( 2, 4, 3, 5, 9 );
$n = sizeof($arr);
echo sumlist($arr, $n);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find the sum of the elements
// from an array which have even parity

// Function that returns true if x has even parity
function checkEvenParity(x)
{

    // We basically count set bits
    // https://www.geeksforgeeks.org/count-set-bits-in-an-integer/
    let parity = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        parity++;
    }

    if (parity % 2 == 0)
        return true;
    else
        return false;
}

// Function to return the sum of the elements
// from an array which have even parity
function sumlist(a, n)
{
    let sum = 0;

    for(let i = 0; i < n; i++)
    {

        // If a[i] has even parity
        if (checkEvenParity(a[i]))
            sum += a[i];
    }
    return sum;
}

// Driver code
let arr = [ 2, 4, 3, 5, 9 ];
let n = arr.length;

document.write(sumlist(arr, n));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
17
```