# 一个数组中同素对的数量

> 原文:[https://www . geesforgeks . org/find-number-co-prime-pairs-array/](https://www.geeksforgeeks.org/find-number-co-prime-pairs-array/)

同素或互素对是那些 GCD 为 1 的数对。给定一个大小为 n 的数组，找出数组中同素或互素对的个数。

示例:

```
Input : 1 2 3
Output : 3
Here, Co-prime pairs are ( 1, 2), ( 2, 3), 
 ( 1, 3)  

Input :4 8 3 9
Output :4
Here, Co-prime pairs are  ( 4, 3), ( 8, 3), 
 ( 4, 9 ), ( 8, 9 ) 
```

**方法:**使用两个循环，检查数组中每一个可能的对。如果该对的 Gcd 为 1，递增计数器值，最后显示它。

## C++

```
// C++ program to find
// number of co-prime
// pairs in array
#include <bits/stdc++.h>
using namespace std;

// function to check for gcd
bool coprime(int a, int b)
{  
    return (__gcd(a, b) == 1);
}

// Recursive function to
// return gcd of a and b
int numOfPairs(int arr[], int n)
{

    int count = 0;
    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
            if (coprime(arr[i], arr[j]))
                count++;

    return count;
}

// driver code
int main()
{
    int arr[] = { 1, 2, 5, 4, 8, 3, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << numOfPairs(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// number of co-prime
// pairs in array
import java.io.*;

class GFG {

    // Recursive function to
    // return gcd of a and b
    static int gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0 || b == 0)
        return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return gcd(a-b, b);

        return gcd(a, b-a);
    }

    // function to check for gcd
    static boolean coprime(int a, int b)
    {
        return (gcd(a, b) == 1);
    }

    // Returns count of co-prime
    // pairs present in array
    static int numOfPairs(int arr[], int n)
    {

        int count = 0;
        for (int i = 0; i < n - 1; i++)
            for (int j = i + 1; j < n; j++)
                if (coprime(arr[i], arr[j]))
                    count++;

        return count;
    }

    // driver code
    public static void main(String args[])
                            throws IOException
    {
        int arr[] = { 1, 2, 5, 4, 8, 3, 9 };
        int n = arr.length;

        System.out.println(numOfPairs(arr, n));
    }
}

/* This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program to
# find number of co
# prime pairs in array

# Recursive function to
# return gcd of a and b
def gcd(a, b):

    # Everything divides 0
    if (a == 0 or b == 0):
        return False

    # base case
    if (a == b):
        return a

    # a is greater
    if (a > b):
        return gcd(a-b, b)

    return gcd(a, b-a)

# function to check
# for gcd
def coprime(a, b) :
    return (gcd(a, b) == 1)

# Returns count of
# co-prime pairs
# present in array
def numOfPairs(arr, n) :
    count = 0

    for i in range(0, n-1) :
        for j in range(i+1, n) :

            if (coprime(arr[i], arr[j])) :
                count = count + 1

    return count

# driver code
arr = [1, 2, 5, 4, 8, 3, 9]
n = len(arr)

print(numOfPairs(arr, n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find number of
// co-prime pairs in array
using System;

class GFG {

    // Recursive function to
    // return gcd of a and b
    static int gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0 || b == 0)
        return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return gcd(a-b, b);

        return gcd(a, b-a);
    }

    // function to check for gcd
    static bool coprime(int a, int b)
    {
        return (gcd(a, b) == 1);
    }

    // Returns count of co-prime
    // pairs present in array
    static int numOfPairs(int []arr, int n)
    {

        int count = 0;
        for (int i = 0; i < n - 1; i++)
            for (int j = i + 1; j < n; j++)
                if (coprime(arr[i], arr[j]))
                    count++;

        return count;
    }

    // driver code
    public static void Main()
    {
        int []arr = { 1, 2, 5, 4, 8, 3, 9 };
        int n = arr.Length;

        Console.WriteLine(numOfPairs(arr, n));
    }
}

//This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// number of co-prime
// pairs in array

// Recursive function to
// return gcd of a and b
function __gcd( $a, $b)
{

    // Everything divides 0
    if ($a == 0 or $b == 0)
    return 0;

    // base case
    if ($a == $b)
        return $a;

    // a is greater
    if ($a > $b)
        return __gcd($a - $b, $b);
    return __gcd($a, $b - $a);
}

// function to check for gcd
function coprime($a, $b)
{
    return (__gcd($a, $b) == 1);
}

// Recursive function to
// return gcd of a and b
function numOfPairs($arr, $n)
{

    $count = 0;
    for ( $i = 0; $i < $n - 1; $i++)
        for ($j = $i + 1; $j < $n; $j++)
            if (coprime($arr[$i], $arr[$j]))
                $count++;

    return $count;
}

    // Driver code
    $arr = array(1, 2, 5, 4, 8, 3, 9);
    $n = count($arr);
    echo numOfPairs($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// number of co-prime 
// pairs in array

// Recursive function to
// return gcd of a and b
function gcd(a, b)
{

    // Everything divides 0
    if (a == 0 || b == 0)
        return 0;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);

    return gcd(a, b - a);
}

// Function to check for gcd
function coprime(a, b)
{
    return (gcd(a, b) == 1);
}

// Returns count of co-prime
// pairs present in array
function numOfPairs(arr, n)
{

    let count = 0;
    for(let i = 0; i < n - 1; i++)
        for(let j = i + 1; j < n; j++)
            if (coprime(arr[i], arr[j]))
                count++;

    return count;
}

// Driver code
let arr = [ 1, 2, 5, 4, 8, 3, 9 ];
let n = arr.length;

document.write(numOfPairs(arr, n));

// This code is contributed by susmitakundugoaldanga

</script>
```

输出:

```
17
```

本文由 [**迪本杜·罗伊·乔杜里**](https://auth.geeksforgeeks.org/profile.php?user=Dibyendu Roy Chaudhuri) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。