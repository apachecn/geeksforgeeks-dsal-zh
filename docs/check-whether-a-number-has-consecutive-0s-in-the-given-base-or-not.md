# 检查一个数字在给定的基数内是否有连续的 0

> 原文:[https://www . geesforgeks . org/check-一个数字在给定的基数上是否有连续的 0/](https://www.geeksforgeeks.org/check-whether-a-number-has-consecutive-0s-in-the-given-base-or-not/)

给定一个十进制数 N，任务是在将一个数转换为基于 K 的符号后，检查该数是否有连续的零。

**示例:**

> 输入:N = 4，K = 2
> 输出:否
> 2 中的 4 是 100，因为有连续的 2，所以答案是否
> 
> 输入:N = 15，K = 8
> 输出:是
> 8 基数中的 15 为 17，由于没有连续的 0，所以答案为是。

**逼近**:先把数字 N 转换成基数 K，然后简单检查这个数字是否有连续的零。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to convert N into base K
int toK(int N, int K)
{

// Weight of each digit
    int w = 1;
    int s = 0;
    while (N != 0)
     {
        int r = N % K;
        N = N/K;
        s = r * w + s;
        w *= 10;
     }
    return s;

}

// Function to check for consecutive 0
bool check(int N)
{

// Flag to check if there are consecutive
    // zero or not
    bool fl = false;
    while (N != 0)
    {

        int r = N % 10;
        N = N/10;

        // If there are two consecutive zero
        // then returning False
        if (fl == true and r == 0)
            return false;
        if (r > 0)
            {
            fl = false;
            continue;
            }
        fl = true;

    }
     return true;

}

// We first convert to given base, then
// check if the converted number has two
// consecutive 0s or not
void hasConsecutiveZeroes(int N, int K)
{
    int z = toK(N, K);
    if (check(z))
       cout<<"Yes"<<endl;
    else
      cout<<"No"<<endl;
}

// Driver code
int main()
{
int N = 15;
int K = 8;
hasConsecutiveZeroes(N, K);

}
// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

// Function to convert N into base K
static int toK(int N, int K)
{

    // Weight of each digit
    int w = 1;
    int s = 0;
    while (N != 0)
    {
        int r = N % K;
        N = N / K;
        s = r * w + s;
        w *= 10;
    }
    return s;

}

// Function to check for consecutive 0
static boolean check(int N)
{

    // Flag to check if there are consecutive
    // zero or not
    boolean fl = false;
    while (N != 0)
    {

        int r = N % 10;
        N = N / 10;

        // If there are two consecutive zero
        // then returning False
        if (fl == true && r == 0)
            return false;
        if (r > 0)
        {
            fl = false;
            continue;
        }
        fl = true;
    }
    return true;
}

// We first convert to given base, then
// check if the converted number has two
// consecutive 0s or not
static void hasConsecutiveZeroes(int N, int K)
{
    int z = toK(N, K);
    if (check(z))
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver code
public static void main(String[] args)
{
    int N = 15;
    int K = 8;
    hasConsecutiveZeroes(N, K);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python implementation of the above approach

# We first convert to given base, then
# check if the converted number has two
# consecutive 0s or not
def hasConsecutiveZeroes(N, K):
    z = toK(N, K)
    if (check(z)):
        print("Yes")
    else:
        print("No")

# Function to convert N into base K
def toK(N, K):

    # Weight of each digit
    w = 1
    s = 0
    while (N != 0):
        r = N % K
        N = N//K
        s = r * w + s
        w* = 10
    return s

# Function to check for consecutive 0
def check(N):

    # Flag to check if there are consecutive
    # zero or not
    fl = False
    while (N != 0):
        r = N % 10
        N = N//10

        # If there are two consecutive zero
        # then returning False
        if (fl == True and r == 0):
            return False
        if (r > 0):
            fl = False
            continue
        fl = True
    return True

# Driver code
N, K = 15, 8
hasConsecutiveZeroes(N, K)
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to convert N into base K
static int toK(int N, int K)
{

    // Weight of each digit
    int w = 1;
    int s = 0;
    while (N != 0)
    {
        int r = N % K;
        N = N / K;
        s = r * w + s;
        w *= 10;
    }
    return s;
}

// Function to check for consecutive 0
static Boolean check(int N)
{

    // Flag to check if there are consecutive
    // zero or not
    Boolean fl = false;
    while (N != 0)
    {

        int r = N % 10;
        N = N / 10;

        // If there are two consecutive zero
        // then returning False
        if (fl == true && r == 0)
            return false;
        if (r > 0)
        {
            fl = false;
            continue;
        }
        fl = true;
    }
    return true;
}

// We first convert to given base, then
// check if the converted number has two
// consecutive 0s or not
static void hasConsecutiveZeroes(int N, int K)
{
    int z = toK(N, K);
    if (check(z))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}

// Driver code
public static void Main(String[] args)
{
    int N = 15;
    int K = 8;
    hasConsecutiveZeroes(N, K);
}
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// We first convert to given base,
// then check if the converted number
// has two consecutive 0s or not
function hasConsecutiveZeroes($N, $K)
{
    $z = toK($N, $K);
    if (check($z))
        print("Yes");
    else
        print("No");
}

// Function to convert N into base K
function toK($N, $K)
{
    // Weight of each digit
    $w = 1;
    $s = 0;
    while ($N != 0)
    {
        $r = $N % $K;
        $N = (int)($N / $K);
        $s = $r * $w + $s;
        $w *= 10;
    }
    return $s;
}

// Function to check for consecutive 0
function check($N)
{
    // Flag to check if there are
    // consecutive zero or not
    $fl = false;
    while ($N != 0)
    {
        $r = $N % 10;
        $N = (int)($N / 10);

        // If there are two consecutive
        // zero then returning false
        if ($fl == true and $r == 0)
            return false;
        if ($r > 0)
        {
            $fl = false;
            continue;
        }
        $fl = true;
    }
    return true;
}

// Driver code
$N = 15;
$K = 8;
hasConsecutiveZeroes($N, $K);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to convert N into base K
function toK(N, K)
{

    // Weight of each digit
    let w = 1;
    let s = 0;

    while (N != 0)
    {
        let r = N % K;
        N = parseInt(N / K);
        s = r * w + s;
        w *= 10;
    }
    return s;
}

// Function to check for consecutive 0
function check(N)
{

    // Flag to check if there are consecutive
    // zero or not
    let fl = false;

    while (N != 0)
    {
        let r = N % 10;
        N = parseInt(N/10);

        // If there are two consecutive zero
        // then returning False
        if (fl == true && r == 0)
            return false;
        if (r > 0)
        {
            fl = false;
            continue;
        }
        fl = true;
    }
     return true;
}

// We first convert to given base, then
// check if the converted number has two
// consecutive 0s or not
function hasConsecutiveZeroes(N, K)
{
    let z = toK(N, K);
    if (check(z))
       document.write("Yes");
    else
      document.write("No");
}

// Driver code
let N = 15;
let K = 8;

hasConsecutiveZeroes(N, K);

// This code is contributed by souravmahato348

</script>
```

**Output:** 

```
Yes
```