# 从较大的元素中减去较小的元素后的数组元素的最小和

> 原文:[https://www . geeksforgeeks . org/从较大数组中减去较小元素后的最小元素总和/](https://www.geeksforgeeks.org/minimum-sum-of-the-elements-of-an-array-after-subtracting-smaller-elements-from-larger/)

给定一个数组 **arr** ，任务是在应用以下操作后找到数组元素的最小和:
对于数组中的任何一对，如果 **a[i] > a[j]** 那么**a[I]= a[I]–a[j]**。

**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 3
> 修改后的数组将为{1，1，1}
> 
> **输入:** a = {2，4，6 }
> T3】输出: 6
> 修改阵将为{2，2，2}

**进场:**这里观察，每次操作后，所有元素的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 保持不变。所以，最后，在应用给定的操作之后，每个元素都将等于数组中所有元素的 gcd。
那么，最终答案将是 **(n * gcd)** 。

下面是上述方法的实现:

## C++

```
// CPP program to Find the minimum sum
// of given array after applying given operation.
#include <bits/stdc++.h>
using namespace std;

// Function to Find the minimum sum
// of given array after applying given operation.
int MinSum(int a[], int n)
{
    // to store final gcd value
    int gcd = a[0];

    // get gcd of the whole array
    for (int i = 1; i < n; i++)
        gcd = __gcd(a[i], gcd);

    return n * gcd;
}

// Driver code
int main()
{

    int a[] = { 20, 14, 6, 8, 15 };

    int n = sizeof(a) / sizeof(a[0]);

    // function call
    cout << MinSum(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Find the minimum sum
// of given array after applying given operation.

import java.io.*;

class GFG {

// Recursive function to return gcd of a and b
static int __gcd(int a, int b)
{
    // Everything divides 0 
    if (a == 0)
       return b;
    if (b == 0)
       return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a-b, b);
    return __gcd(a, b-a);
}
// Function to Find the minimum sum
// of given array after applying given operation.
static int MinSum(int []a, int n)
{
    // to store final gcd value
    int gcd = a[0];

    // get gcd of the whole array
    for (int i = 1; i < n; i++)
        gcd = __gcd(a[i], gcd);

    return n * gcd;
}

// Driver code

    public static void main (String[] args) {
            int a[] = { 20, 14, 6, 8, 15 };

    int n = a.length;

    // function call
    System.out.println(MinSum(a, n));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 program to Find the minimum
# sum of given array after applying
# given operation.
import math

# Function to Find the minimum sum
# of given array after applying
# given operation.
def MinSum(a, n):

    # to store final gcd value
    gcd = a[0]

    # get gcd of the whole array
    for i in range(1, n):
        gcd = math.gcd(a[i], gcd)

    return n * gcd

# Driver code
if __name__ == "__main__":

    a = [20, 14, 6, 8, 15 ]

    n = len(a)

    # function call
    print(MinSum(a, n))

# This code is contributed by ita_c
```

## C#

```
// C# program to Find the minimum sum
// of given array after applying given operation.

using System;
class GFG {

    // Recursive function to return gcd of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0 
        if (a == 0)
           return b;
        if (b == 0)
           return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a-b, b);
        return __gcd(a, b-a);
    }

    // Function to Find the minimum sum
    // of given array after applying given operation.
    static int MinSum(int []a, int n)
    {
        // to store final gcd value
        int gcd = a[0];

        // get gcd of the whole array
        for (int i = 1; i < n; i++)
            gcd = __gcd(a[i], gcd);

        return n * gcd;
    }

    // Driver Program to test above function
    static void Main()
    {
        int []a = { 20, 14, 6, 8, 15 };
        int n = a.Length;
        Console.WriteLine(MinSum(a, n));
    }

    // This code is contributed by Ryuga.
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Find the minimum sum of
// given array after applying given operation.

// Function to Find the minimum sum
// of given array after applying
// given operation.
function gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return gcd($b, $a % $b);

}

function MinSum($a, $n)
{
    // to store final gcd value
    $gcdd = $a[0];

    // get gcd of the whole array
    for ($i = 1; $i < $n; $i++)
        $gcdd = gcd($a[$i], $gcdd);

    return $n * $gcdd;
}

// Driver code
$a = array( 20, 14, 6, 8, 15 );

$n = count($a);

// function call
echo MinSum($a, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to Find the minimum sum
// of given array after applying given operation.

// Recursive function to return gcd of a and b
function __gcd(a, b)
{

    // Everything divides 0 
    if (a == 0)
       return b;
    if (b == 0)
       return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return __gcd(a - b, b);
    return __gcd(a, b - a);
}

// Function to Find the minimum sum
// of given array after applying
// given operation.
function MinSum(a, n)
{

    // To store final gcd value
    var gcd = a[0];

    // Get gcd of the whole array
    for(var i = 1; i < n; i++)
        gcd = __gcd(a[i], gcd);

    return n * gcd;
}

// Driver code
var a = [ 20, 14, 6, 8, 15 ];
var n = a.length;

// Function call
document.write( MinSum(a, n));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
5
```