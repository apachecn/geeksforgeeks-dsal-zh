# 从 n 个缺少一个的和方程中找出 n 个变量

> 原文:[https://www . geesforgeks . org/find-n-variables-n-sum-equations-one-missing/](https://www.geeksforgeeks.org/find-n-variables-n-sum-equations-one-missing/)

给你一个 n 值数组 a[]作为 a[1]，a[2]…a[n]，它们是 n-变量中 n-方程的一部分，其中方程如下:
方程 n1 = > X2 + X3 +…..+Xn = a1
Eqn2 = > X1 + X3 +…..+Xn = a2
Eqni =>X1+X2+…+X<sub>I-1</sub>+X<sub>I+1</sub>..+Xn = ai
Eqnn = > X1 + X2 +…..+X <sub>n-1</sub> = an
因为你在 n 个变量中有 n 个方程，所以找出所有变量(X1，X2…Xn)的值。
**举例:**

```
Input : a[] = {4, 4, 4, 4, 4}
Output : X1 = 1
         X2 = 1
         X3 = 1
         X4 = 1
         X5 = 1

Input : a[] = {2, 5, 6, 4, 8}
Output : X1 = 4.25
         X2 = 1.25
         X3 = 0.25
         X4 = 2.25
         X5 = -1.75
```

**进场** :
Let，X1+X2+X3+…。Xn= SUM
使用值 SUM，我们的方程为

```
SUM - X1 = a1 -----(1)
SUM - X2 = a2  -----(2)
SUM - Xi = ai  -----(i)
SUM - Xn = an -------(n)
---------------------------------------------------------------
Now, if we add all these equation we will have an equation as :
n*SUM -(X1+X2+...Xn) = a1 + a2 + ...an
n*SUM - SUM = a1 + a2 + ...an
SUM = (a1+a2+...an)/(n-1)

Calculate SUM from above equation.
putting value of SUM in (i), (ii).... we have
X1 = SUM - a1
X2 = SUM - a2
```

**解决方案:**

```
X1 = SUM - a1
X2 = SUM - a2
Xi = SUM - ai
Xn = SUM - an
```

## C++

```
// CPP program to find n-variables
#include <bits/stdc++.h>
using namespace std;

// function to print n-variable values
void findVar(int a[], int n)
{   
    // calculate value of array SUM
    float SUM = 0;
    for (int i = 0; i < n; i++)
        SUM += a[i];

    // Every variable contributes n-1
    // times to sum. So dividing by
    // n-1 to get sum of all.
    SUM /= (n - 1);

    // print the values of n-variables
    for (int i = 0; i < n; i++)
        cout << "X" << (i + 1)
             << " = " << SUM - a[i] << endl;
}

// driver program
int main()
{
    int a[] = { 2, 5, 6, 4, 8 };
    int n = sizeof(a) / sizeof(a[0]);
    findVar(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to
// find n-variables
import java.io.*;

class GFG
{
    // function to print
    // n-variable values
    static void findVar(int []a,
                        int n)
    {
        // calculate value+
        // of array SUM
        float SUM = 0;
        for (int i = 0; i < n; i++)
            SUM += a[i];

        // Every variable contributes
        // n-1 times to sum. So dividing
        // by n-1 to get sum of all.
        SUM /= (n - 1);

        // print the values
        // of n-variables
        for (int i = 0; i < n; i++)
            System.out.print("X" + (i + 1) +
                             " = " + (SUM -
                             a[i]) + "\n");
    }

    // Driver Code
    public static void main(String args[])
    {
        int []a = new int[]{2, 5, 6, 4, 8};
        int n = a.length;
        findVar(a, n);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to
# find n-variables

# function to print
# n-variable values
def findVar(a, n):

    # calculate value of
    # array SUM
    SUM = 0;
    for i in range(n):
        SUM += a[i];

    # Every variable contributes
    # n-1 times to sum. So 
    # dividing by n-1 to get sum
    # of all.
    SUM = SUM / (n - 1);

    # print the values
    # of n-variables
    for i in range(n):
        print("X" , (i + 1),
              " = ", SUM - a[i]);

# Driver Code
a = [2, 5, 6, 4, 8];
n = len(a);
findVar(a, n);

# This code is contributed
# by mits
```

## C#

```
// C# program to find n-variables
using System;
using System.Linq;
using System.Collections.Generic;

class GFG
{
    // function to print
    // n-variable values
    static void findVar(int []a,
                        int n)
    {
        // calculate value+
        // of array SUM
        float SUM = 0;
        for (int i = 0; i < n; i++)
            SUM += a[i];

        // Every variable contributes
        // n-1 times to sum. So dividing
        // by n-1 to get sum of all.
        SUM /= (n - 1);

        // print the values
        // of n-variables
        for (int i = 0; i < n; i++)
            Console.Write("X" + (i + 1) +
                   " = " + (SUM - a[i]) + "\n");
    }

    // Driver Code
    static void Main()
    {
        int []a = { 2, 5, 6, 4, 8 };
        int n = a.Length;
        findVar(a, n);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to
// find n-variables

// function to print
// n-variable values
function findVar($a, $n)
{

    // calculate value of
    // array SUM
    $SUM = 0;
    for ($i = 0; $i < $n; $i++)
        $SUM += $a[$i];

    // Every variable contributes n-1
    // times to sum. So dividing by
    // n-1 to get sum of all.
    $SUM /= ($n - 1);

    // print the values
    // of n-variables
    for ( $i = 0; $i < $n; $i++)
        echo "\nX" , ($i + 1)
            , " = " , $SUM - $a[$i];
}

    // Driver Code
    $a = array(2, 5, 6, 4, 8);
    $n = count($a);
    findVar($a, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// function to print
// n-variable values
function findVar(a,n)
{

    // calculate value+
    // of array SUM
    let SUM = 0;
    for (let i = 0; i < n; i++)
        SUM += a[i];

    // Every variable contributes
    // n-1 times to sum. So dividing
    // by n-1 to get sum of all.
    SUM /= (n - 1);

    // print the values
    // of n-variables
    for (let i = 0; i < n; i++)
        document.write("X" + (i + 1) + " = " + (SUM - a[i]) + "<br>");
}

let a = [2, 5, 6, 4, 8 ];
let n = a.length;
findVar(a, n);

// This code is contributed by mohit kumar 29.

</script>
```

**Output :** 

```
X1 = 4.25
X2 = 1.25
X3 = 0.25
X4 = 2.25
X5 = -1.75
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)