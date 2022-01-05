# 检查矩阵是否是两个的乘积的弗赖瓦德算法

> 原文:[https://www.geeksforgeeks.org/freivalds-algorithm/](https://www.geeksforgeeks.org/freivalds-algorithm/)

给定三个矩阵 A、B 和 C，求 C 是否是 A 和 B 的乘积。
**例:**

```
Input : A = 1 1
            1 1
        B = 1 1
            1 1
        C = 2  2
             2 2
Output : Yes
C = A x B

Input : A = 1 1 1
            1 1 1
            1 1 1
        B = 1 1 1
            1 1 1
            1 1 1
        C = 3 3 3
            3 1 2
            3 3 3 
Output : No
```

A **简单的解决方法**就是找到 A 和 B 的乘积，然后检查乘积是否等于 C。该方法的一个可能的时间复杂度是使用[斯特雷森矩阵乘法](https://www.geeksforgeeks.org/strassens-matrix-multiplication/)的 0(n<sup>2.8874</sup>)。
[**Freivalds 的算法**](https://en.wikipedia.org/wiki/Freivalds%27_algorithm) 是一种概率随机化算法，在时间上以高概率工作 **O(n <sup>2</sup> )** 。在 **O(kn <sup>2</sup> )** 时间内，算法可以验证故障概率小于 **2 <sup>-k</sup>** 的矩阵乘积。由于输出并不总是正确的，所以它是[蒙特卡罗随机算法](https://www.geeksforgeeks.org/randomized-algorithms-set-2-classification-and-applications/)。
**步骤:**

1.  生成一个 **n × 1** 随机 0/1 向量 **r⃗** 。
2.  计算**p⃗= a×(br)⃗-cr⃗**。
3.  如果 **P⃗ = ( 0，0，…，0 ) <sup>T</sup>** 返回真，否则返回假。

这个想法是基于这样一个事实，如果 c 实际上是一个乘积，那么 a×(br)⃗-cr⃗)的值将总是 0。如果值非零，那么 C 就不能是乘积。错误条件是，即使 C 不是乘积，该值也可能为 0。
下面是上述方法的实现:

## C++

```
// CPP code to implement Freivald’s Algorithm
#include <bits/stdc++.h>
using namespace std;

#define N 2

// Function to check if ABx = Cx
int freivald(int a[][N], int b[][N], int c[][N])
{
    // Generate a random vector
    bool r[N];
    for (int i = 0; i < N; i++)
        r[i] = random() % 2;

    // Now comput B*r for evaluating
    // expression A * (B*r) - (C*r)
    int br[N] = { 0 };
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            br[i] = br[i] + b[i][j] * r[j];

    // Now comput C*r for evaluating
    // expression A * (B*r) - (C*r)
    int cr[N] = { 0 };
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            cr[i] = cr[i] + c[i][j] * r[j];

    // Now comput A* (B*r) for evaluating
    // expression A * (B*r) - (C*r)
    int axbr[N] = { 0 };
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            axbr[i] = axbr[i] + a[i][j] * br[j];

    // Finally check if value of expression
    // A * (B*r) - (C*r) is 0 or not
    for (int i = 0; i < N; i++)
        if (axbr[i] - cr[i] != 0)
            false;

    return true;
}

// Runs k iterations Freivald. The value
// of k determines accuracy. Higher value
// means higher accuracy.
bool isProduct(int a[][N], int b[][N],
               int c[][N], int k)
{
    for (int i=0; i<k; i++)
        if (freivald(a, b, c) == false)
            return false;
    return true;
}

// Driver code
int main()
{
    int a[N][N] = { { 1, 1 }, { 1, 1 } };
    int b[N][N] = { { 1, 1 }, { 1, 1 } };
    int c[N][N] = { { 2, 2 }, { 2, 2 } };
    int k = 2;
    if (isProduct(a, b, c, k))
        printf("Yes");
    else
        printf("No");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement
// Freivald's Algorithm
import java.io.*;
import java.util.*;
import java.math.*;

class GFG {
    static int N = 2;

    // Function to check if ABx = Cx
    static boolean freivald(int a[][], int b[][],
                                       int c[][])
    {
        // Generate a random vector
        int r[] = new int[N];
        for (int i = 0; i < N; i++)
        r[i] = (int)(Math.random()) % 2;

        // Now comput B*r for evaluating
        // expression A * (B*r) - (C*r)
        int br[] = new int[N];
        Arrays.fill(br, 0);
        for (int i = 0; i < N; i++)
            for (int j = 0; j < N; j++)
                br[i] = br[i] + b[i][j] * r[j];

        // Now comput C*r for evaluating
        // expression A * (B*r) - (C*r)
        int cr[] = new int[N];
        Arrays.fill(cr, 0);
        for (int i = 0; i < N; i++)
            for (int j = 0; j < N; j++)
                cr[i] = cr[i] + c[i][j] * r[j];

        // Now comput A* (B*r) for evaluating
        // expression A * (B*r) - (C*r)
        int axbr[] = new int[N];
        Arrays.fill(axbr, 0);
        for (int i = 0; i < N; i++)
            for (int j = 0; j < N; j++)
                axbr[i] = axbr[i] + a[i][j] * br[j];

        // Finally check if value of expression
        // A * (B*r) - (C*r) is 0 or not
        for (int i = 0; i < N; i++)
            if (axbr[i] - cr[i] != 0)
                return false;

        return true;
    }

    // Runs k iterations Freivald. The value
    // of k determines accuracy. Higher value
    // means higher accuracy.
    static boolean isProduct(int a[][], int b[][],
                                 int c[][], int k)
    {
        for (int i = 0; i < k; i++)
            if (freivald(a, b, c) == false)
                return false;
        return true;
    }

    // Driver code
    public static void main(String args[])
    {
        int a[][] = { { 1, 1 }, { 1, 1 } };
        int b[][] = { { 1, 1 }, { 1, 1 } };
        int c[][] = { { 2, 2 }, { 2, 2 } };
        int k = 2;
        if (isProduct(a, b, c, k))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python3 code to implement Freivald’s Algorithm
import random
N = 2

# Function to check if ABx = Cx
def freivald(a, b, c) :

    # Generate a random vector
    r = [0] * N

    for i in range(0, N) :
        r[i] = (int)(random.randrange(509090009) % 2)

    # Now comput B*r for evaluating
    # expression A * (B*r) - (C*r)
    br = [0] * N

    for i in range(0, N) :
        for j in range(0, N) :
            br[i] = br[i] + b[i][j] * r[j]

    # Now comput C*r for evaluating
    # expression A * (B*r) - (C*r)
    cr = [0] * N
    for i in range(0, N) :
        for j in range(0, N) :
            cr[i] = cr[i] + c[i][j] * r[j]

    # Now comput A* (B*r) for evaluating
    # expression A * (B*r) - (C*r)
    axbr = [0] * N
    for i in range(0, N) :
        for j in range(0, N) :
            axbr[i] = axbr[i] + a[i][j] * br[j]

    # Finally check if value of expression
    # A * (B*r) - (C*r) is 0 or not
    for i in range(0, N) :
        if (axbr[i] - cr[i] != 0) :
            return False

    return True

# Runs k iterations Freivald. The value
# of k determines accuracy. Higher value
# means higher accuracy.
def isProduct(a, b, c, k) :

    for i in range(0, k) :
        if (freivald(a, b, c) == False) :
            return False
    return True

# Driver code
a = [ [ 1, 1 ], [ 1, 1 ] ]
b = [ [ 1, 1 ], [ 1, 1 ] ]
c = [ [ 2, 2 ], [ 2, 2 ] ]
k = 2

if (isProduct(a, b, c, k)) :
    print("Yes")
else :
    print("No")

# This code is contributed by Nikita Tiwari
```

## C#

```
// C# code to implement
// Freivald's Algorithm
using System;

class GFG
{
    static int N = 2;

    // Function to check
    // if ABx = Cx
    static bool freivald(int [,]a,
                         int [,]b,
                         int [,]c)
    {
        // Generate a
        // random vector
        Random rand = new Random();
        int []r = new int[N];

        for (int i = 0; i < N; i++)
        r[i] = (int)(rand.Next()) % 2;

        // Now compute B*r for
        // evaluating expression
        // A * (B*r) - (C*r)
        int []br = new int[N];

        for (int i = 0; i < N; i++)
            for (int j = 0; j < N; j++)
                br[i] = br[i] +
                        b[i, j] * r[j];

        // Now compute C*r for
        // evaluating expression
        // A * (B*r) - (C*r)
        int []cr = new int[N];

        for (int i = 0; i < N; i++)
            for (int j = 0; j < N; j++)
                cr[i] = cr[i] +
                        c[i, j] * r[j];

        // Now compute A* (B*r) for
        // evaluating expression
        // A * (B*r) - (C*r)
        int []axbr = new int[N];

        for (int i = 0; i < N; i++)
            for (int j = 0; j < N; j++)
                axbr[i] = axbr[i] +
                          a[i, j] * br[j];

        // Finally check if value
        // of expression A * (B*r) -
        // (C*r) is 0 or not
        for (int i = 0; i < N; i++)
            if (axbr[i] - cr[i] != 0)
                return false;

        return true;
    }

    // Runs k iterations Freivald.
    // The value of k determines
    // accuracy. Higher value
    // means higher accuracy.
    static bool isProduct(int [,]a, int [,]b,
                          int [,]c, int k)
    {
        for (int i = 0; i < k; i++)
            if (freivald(a, b, c) == false)
                return false;
        return true;
    }

    // Driver code
    static void Main()
    {
        int [,]a = new int[,]{ { 1, 1 },
                               { 1, 1 }};
        int [,]b = new int[,]{ { 1, 1 },
                               { 1, 1 }};
        int [,]c = new int[,]{ { 2, 2 },
                               { 2, 2 }};
        int k = 2;
        if (isProduct(a, b, c, k))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}
// This code is contributed
// by Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to implement
// Freivald’s Algorithm
$N = 2;

// Function to check
// if ABx = Cx
function freivald($a, $b, $c)
{
    global $N;

    // Generate a
    // random vector
    $r = array();
    $br = array();
    $cr = array();
    $axbr = array();

    for ($i = 0; $i < $N; $i++)
    {
        $r[$i] = mt_rand() % 2;
        $br[$i] = 0;
        $cr[$i] = 0;
        $axbr[$i] = 0;
    }

    // Now comput B*r for
    // evaluating expression
    // A * (B*r) - (C*r)
    for ($i = 0; $i < $N; $i++)
    {
        for ($j = 0; $j < $N; $j++)
            $br[$i] = $br[$i] +
                      $b[$i][$j] *
                      $r[$j];
    }

    // Now comput C*r for
    // evaluating expression
    // A * (B*r) - (C*r)
    for ($i = 0; $i < $N; $i++)
    {
        for ($j = 0; $j < $N; $j++)
            $cr[$i] = $cr[$i] +
                      $c[$i][$j] *
                      $r[$j];
    }

    // Now comput A* (B*r) for
    // evaluating expression
    // A * (B*r) - (C*r)
    for ($i = 0; $i < $N; $i++)
    {
        for ($j = 0; $j < $N; $j++)
            $axbr[$i] = $axbr[$i] +
                        $a[$i][$j] *
                        $br[$j];
    }

    // Finally check if value
    // of expression A * (B*r) -
    // (C*r) is 0 or not
    for ($i = 0; $i < $N; $i++)
        if ($axbr[$i] - $cr[$i] != 0)
            return false;

    return true;
}

// Runs k iterations Freivald.
// The value of k determines
// accuracy. Higher value
// means higher accuracy.
function isProduct($a, $b, $c, $k)
{
    for ($i = 0; $i < $k; $i++)
        if (freivald($a,
                     $b, $c) == false)
            return false;
    return true;
}

// Driver code
$a = array(array(1, 1),
           array(1, 1));
$b = array(array(1, 1),
           array(1, 1));
$c = array(array(2, 2),
           array(2, 2));
$k = 2;
if (isProduct($a, $b,
              $c, $k))
    echo ("Yes");
else
    echo ("No");

// This code is contributed
// by Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

    // JavaScript code to implement Freivald’s Algorithm
    let N = 2;

    // Function to check if ABx = Cx
    function freivald(a,b,c)
    {
        // Generate a random vector
        let r = new Array(N);
        for (let i = 0; i < N; i++)
            r[i] = Math.random() % 2;

        // Now comput B*r for evaluating
        // expression A * (B*r) - (C*r)
        let br = new Array(N);
        br.fill(0);
        for (let i = 0; i < N; i++)
            for (let j = 0; j < N; j++)
                br[i] = br[i] + b[i][j] * r[j];

        // Now comput C*r for evaluating
        // expression A * (B*r) - (C*r)
        let cr = new Array(N);
        cr.fill(0);
        for (let i = 0; i < N; i++)
            for (let j = 0; j < N; j++)
                cr[i] = cr[i] + c[i][j] * r[j];

        // Now comput A* (B*r) for evaluating
        // expression A * (B*r) - (C*r)
        let axbr = new Array(N);
        axbr.fill(0);
        for (let i = 0; i < N; i++)
            for (let j = 0; j < N; j++)
                axbr[i] = axbr[i] + a[i][j] * br[j];

        // Finally check if value of expression
        // A * (B*r) - (C*r) is 0 or not
        for (let i = 0; i < N; i++)
            if (axbr[i] - cr[i] != 0)
                false;

        return true;
    }

    // Runs k iterations Freivald. The value
    // of k determines accuracy. Higher value
    // means higher accuracy.
    function isProduct(a,b,c,k)
    {
        for (let i=0; i<k; i++)
            if (freivald(a, b, c) == false)
                return false;
        return true;
    }

    // Driver code
    let a = [[ 1, 1 ], [ 1, 1 ]];
    let b = [[ 1, 1 ], [ 1, 1 ]];
    let c = [[ 2, 2 ], [ 2, 2 ]];
    let k = 2;
    if (isProduct(a, b, c, k))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(北^ 2)
T3】辅助空间: O(北^ 2)