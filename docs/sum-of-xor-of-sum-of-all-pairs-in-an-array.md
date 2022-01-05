# 数组中所有对之和的异或之和

> 原文:[https://www . geesforgeks . org/数组中所有对的和的异或和/](https://www.geeksforgeeks.org/sum-of-xor-of-sum-of-all-pairs-in-an-array/)

给定一个数组，求数组中所有对之和的异或。
**例:**

```
Input  : arr[] = {1, 2, 3}
Output : 0
(1 + 1) ^ (1 + 2) ^ (1 + 3) ^ (2 + 1) ^ (2 + 2) ^ 
(2 + 3) ^ (3 + 1) ^ (3 + 2) ^ (3 + 3) = 0

Input  : arr[] = {1, 2, 3, 4}
Output : 8
```

一种**天真的做法**是把所有的对一个个考虑，一个个计算它们的异或。

## C++

```
// CPP program to find XOR of pair
// sums.
#include <bits/stdc++.h>

using namespace std;

int xorPairSum(int ar[], int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            sum = sum ^ (ar[i] + ar[j]);
    return sum;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3 };
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << xorPairSum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find XOR of pair sums.
import java.io.*;

class GFG {

// method to find XOR of pair sums
static int xorPairSum(int ar[], int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            sum = sum ^ (ar[i] + ar[j]);
    return sum;
}

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = {1, 2, 3};
        int n = arr.length;
        System.out.print( xorPairSum(arr, n));
    }
}

// This code is contributed by chandan_jnu.
```

## 蟒蛇 3

```
# Python program to find
# XOR of pair sums.

def xor_pair_sum(ar, n):
    total = 0
    for i in range(n):
        for j in range(n):
            total = total ^ (ar[i] + ar[j])

    return total

# Driver program to test the above function
if __name__ == "__main__":
    data = [1, 2, 3]
    print(xor_pair_sum(data, len(data)))

# This code is contributed
# by Kanav Malhotra
```

## C#

```
// C# program to find
// XOR of pair sums.
using System;

class GFG
{
static int xorPairSum(int []ar,
                    int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            sum = sum ^ (ar[i] + ar[j]);
    return sum;
}

// Driver code
static public void Main(String []args)
{
    int []arr = { 1, 2, 3 };
    int n = arr.Length;
    Console.WriteLine(xorPairSum(arr, n));
}
}

// This code is contributed
// by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// XOR of pair sums.

function xorPairSum($ar, $n)
{
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum = $sum ^ ($ar[$i] +
                       $ar[$j]);
    return $sum;
}

// Driver code
$arr = array( 1, 2, 3 );
$n = count($arr);
echo xorPairSum($arr, $n);

// This code is contributed
// by Subhadeep
?>
```

## java 描述语言

```
<script>

// JavaScript program to find XOR of pair
// sums.

function xorPairSum(ar, n)
{
    let sum = 0;
    for (let i = 0; i < n; i++)
        for (let j = 0; j < n; j++)
            sum = sum ^ (ar[i] + ar[j]);
    return sum;
}

// Driver code

    let arr = [ 1, 2, 3 ];
    let n = arr.length;
    document.write(xorPairSum(arr, n));

// This code is contributed by Surbhi Tyagi

</script>
```

**Output:** 

```
0
```