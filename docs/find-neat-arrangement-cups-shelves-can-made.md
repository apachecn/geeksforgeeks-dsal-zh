# 看看能不能把杯子和架子排列整齐

> 原文:[https://www . geesforgeks . org/find-整齐-排列-杯子-架子-罐头-制造/](https://www.geeksforgeeks.org/find-neat-arrangement-cups-shelves-can-made/)

给定三种不同类型的杯子(a[])和茶托(b[])，以及 n 个架子，看看杯子和架子是否能排列整齐。
遵循以下规则，杯碟排列整齐:

*   没有架子能同时放杯子和茶碟
*   任何架子上最多只能有 5 个杯子
*   任何架子上最多只能有 10 个调味酱

示例:

```
Input : a[] = {3, 2, 6}
        b[] = {4, 8, 9}
        n = 10
Output : Yes
Explanation :  
Total cups = 11, shelves required = 3
Total saucers = 21, shelves required = 3
Total required shelves = 3 + 3 = 6, 
which is less than given number of 
shelves n. So, output is Yes.

Input : a[] = {4, 7, 4}
        b[] = {3, 9, 10}
        n = 2
Output : No
```

**进场:**整理杯子和茶托，找出杯子总数![a  ](img/c30e654d88f33e45c5463a428b007bce.png "Rendered by QuickLaTeX.com")和茶托总数![b  ](img/5a3a9480cd4e66896d3cc12d182fefab.png "Rendered by QuickLaTeX.com")。因为同一个架子上不能超过 5 个杯子，所以通过公式![\frac{a+5-1}{5}  ](img/efb1e7e756263cd7012adc34b22e44de.png "Rendered by QuickLaTeX.com")找出杯子需要的最大架子数，通过公式![\frac{b+10-1}{10}  ](img/4b9dba61dade0dc5617e8c3e594501f1.png "Rendered by QuickLaTeX.com")找出茶碟需要的最大架子数。如果这两个值之和等于或小于![n  ](img/31d70d7c99878a33c601d487c9b6eb43.png "Rendered by QuickLaTeX.com")，则这种安排是可能的，否则是不可能的。
以下是上述方法的实施:

## C++

```
// C++ code to find if neat
// arrangement of cups and
// shelves can be made
#include<bits/stdc++.h>
using namespace std;

// Function to check arrangement
void canArrange(int a[], int b[], int n)
{
    int suma = 0, sumb = 0;

    // Calculating total number
    // of cups
    for(int i = 0; i < 3; i++)
        suma += a[i];

    // Calculating total number
    // of saucers
    for(int i = 0; i < 3; i++)
        sumb += b[i];

    // Adding 5 and 10 so that if the
    // total sum is less than 5 and
    // 10 then we can get 1 as the
    // answer and not 0
    int na = (suma + 5 - 1) / 5;
    int nb = (sumb + 10 - 1) / 10;

    if(na + nb <= n)
        cout << "Yes";
    else
        cout << "No";
}

// Driver code
int main()
{
    // Number of cups of each type
    int a[] = {3, 2, 6};

    // Number of saucers of each type
    int b[] = {4, 8, 9};

    // Number of shelves
    int n = 10;

    // Calling function
    canArrange(a, b, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find if neat
// arrangement of cups and
// shelves can be made
import java.io.*;

class Gfg
{
    // Function to check arrangement
    public static void canArrange(int a[], int b[],
                                           int n)
    {
        int suma = 0, sumb = 0;

        // Calculating total number
        // of cups
        for(int i = 0; i < 3; i++)
            suma += a[i];

        // Calculating total number
        // of saucers
        for(int i = 0; i < 3; i++)
            sumb += b[i];

        // Adding 5 and 10 so that if
        // the total sum is less than
        // 5 and 10 then we can get 1
        // as the answer and not 0
        int na = (suma + 5 - 1) / 5;
        int nb = (sumb + 10 - 1) / 10;

        if(na + nb <= n)
            System.out.println("Yes");
        else
            System.out.println("No");
    }

    // Driver function
    public static void main(String args[])
    {
        // Number of cups of each type
        int a[] = {3, 2, 6};

        // Number of saucers of each type
        int b[] = {4, 8, 9};

        // Number of shelves
        int n = 10;

        // Calling function
        canArrange(a, b, n);
    }
}
```

## 蟒蛇 3

```
# Python code to find if neat
# arrangement of cups and
# shelves can be made

import math

# Function to check arrangement
def canArrange( a, b, n):
        suma = 0
        sumb = 0

        # Calculating total number
        # of cups
        for i in range(0, len(a)):
            suma += a[i]

        # Calculating total number
        # of saucers
        for i in range(0,len(b)):
            sumb += b[i]

        # Adding 5 and 10 so that if
        # the total sum is less than
        # 5 and 10 then we can get 1
        # as the answer and not 0
        na = (suma + 5 - 1) / 5
        nb = (sumb + 10 - 1) / 10

        if(na + nb <= n):
            print("Yes")
        else:
            print("No")

# driver function

#Number of cups of each type
a = [3, 2, 6]

# Number of saucers of each type
b = [4, 8, 9]

# Number of shelves
n = 10

#Calling function
canArrange(a ,b ,n)

# This code is contributed by Gitanjali.
```

## C#

```
// C# code to find if neat
// arrangement of cups and
// shelves can be made
using System;

class Gfg {

    // Function to check arrangement
    public static void canArrange(int []a, int []b,
                                        int n)
    {

        int suma = 0, sumb = 0;

        // Calculating total number
        // of cups
        for(int i = 0; i < 3; i++)
            suma += a[i];

        // Calculating total number
        // of saucers
        for(int i = 0; i < 3; i++)
            sumb += b[i];

        // Adding 5 and 10 so that if
        // the total sum is less than
        // 5 and 10 then we can get 1
        // as the answer and not 0
        int na = (suma + 5 - 1) / 5;
        int nb = (sumb + 10 - 1) / 10;

        if(na + nb <= n)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }

    // Driver function
    public static void Main()
    {

        // Number of cups of each type
        int []a = {3, 2, 6};

        // Number of saucers of each type
        int []b = {4, 8, 9};

        // Number of shelves
        int n = 10;

        // Calling function
        canArrange(a, b, n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find if neat
// arrangement of cups and
// shelves can be made

// Function to check arrangement
function canArrange($a, $b, $n)
{
    $suma = 0; $sumb = 0;

    // Calculating total number
    // of cups
    for( $i = 0; $i < 3; $i++)
        $suma += $a[$i];

    // Calculating total number
    // of saucers
    for( $i = 0; $i < 3; $i++)
        $sumb += $b[$i];

    // Adding 5 and 10 so that if the
    // total sum is less than 5 and
    // 10 then we can get 1 as the
    // answer and not 0
    $na = ($suma + 5 - 1) / 5;
    $nb = ($sumb + 10 - 1) / 10;

    if($na + $nb <= $n)
        echo "Yes";
    else
        echo "No";
}

    // Driver code

    // Number of cups of each type
    $a = array(3, 2, 6);

    // Number of saucers of each type
    $b = array(4, 8, 9);

    // Number of shelves
    $n = 10;

    // Calling function
    canArrange($a, $b, $n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// Javascript code to find if neat
// arrangement of cups and
// shelves can be made

// Function to check arrangement
function canArrange( a, b, n)
{
    let suma = 0, sumb = 0;

    // Calculating total number
    // of cups
    for(let i = 0; i < 3; i++)
        suma += a[i];

    // Calculating total number
    // of saucers
    for(let i = 0; i < 3; i++)
        sumb += b[i];

    // Adding 5 and 10 so that if the
    // total sum is less than 5 and
    // 10 then we can get 1 as the
    // answer and not 0
    let na = Math.floor((suma + 5 - 1)/5);
    let nb = Math.floor((sumb + 10 - 1)/10);

    if(na + nb <= n)
        document.write("Yes");
    else
        document.write("No");
}

    // driver code

    // Number of cups of each type
    let a = [3, 2, 6];

    // Number of saucers of each type
    let b = [4, 8, 9];

    // Number of shelves
    let n = 10;

    // Calling function
    canArrange(a, b, n);

</script>
```

输出:

```
Yes
```