# 打印几何级数的程序

> 原文:[https://www . geesforgeks . org/program-to-print-gp-geometric-progression/](https://www.geeksforgeeks.org/program-to-print-gp-geometric-progression/)

给定几何级数的第一项(a)、公比(r)和整数 n，任务是打印级数的第 n 项。
示例:

```
Input : a = 2 r = 2, n = 4
Output : 2 4 8 16
```

**进场:**

> 我们知道几何级数就像= 2，4，8，16，32 ……。
> 在本系列中，2 是该系列的起始术语。
> 公比= 4 / 2 = 2(系列中的公比)。
> 所以我们可以把级数写成:
> t1 = a1
> T2 = a1 * r<sup>(2-1)</sup>
> T3 = a1 * r<sup>(3-1)</sup>
> T4 = a1 * r<sup>(4-1)</sup>
> 。
> 。
> 。
> 。
> tN = a1 * r <sup>(n-1)</sup>

要打印几何级数，我们使用简单的公式。

```
TN = a1 * r(n-1)
```

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to print GP.
#include <bits/stdc++.h>
using namespace std;

void printGP(int a, int r, int n)
{
    int curr_term;
    for (int i = 0; i < n; i++) {
        curr_term = a * pow(r, i);
        cout << curr_term << " ";
    }
}

// Driver code
int main()
{
    int a = 2; // starting number
    int r = 3; // Common ratio
    int n = 5; // N th term to be find
    printGP(a, r, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print GP.
class GFG {
    static void printGP(int a, int r, int n)
    {
        int curr_term;
        for (int i = 0; i < n; i++) {
            curr_term = a * (int)Math.pow(r, i);
            System.out.print(curr_term + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int a = 2; // starting number
        int r = 3; // Common ratio
        int n = 5; // N th term to be find
        printGP(a, r, n);
    }
}
// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python 3 program to print GP.

def printGP(a, r, n):
    for i in range(0, n):
        curr_term = a * pow(r, i)
        print(curr_term, end =" ")

# Driver code

a = 2 # starting number
r = 3 # Common ratio
n = 5 # N th term to be find

printGP(a, r, n)

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to print GP.
using System;

class GFG {

    static void printGP(int a, int r, int n)
    {

        int curr_term;

        for (int i = 0; i < n; i++) {
            curr_term = a * (int)Math.Pow(r, i);
            Console.Write(curr_term + " ");
        }
    }

    // Driver code
    public static void Main()
    {

        int a = 2; // starting number
        int r = 3; // Common ratio
        int n = 5; // N th term to be find

        printGP(a, r, n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print GP.

// function to print GP
function printGP($a, $r, $n)
{
    for ($i = 0; $i < $n; $i++)
    {
        $curr_term = $a * pow($r, $i);
        echo $curr_term, " ";
    }
}

    // Driver Code

    // starting number
    $a = 2;

    // Common ratio
    $r = 3;

    // N th term to be find
    $n = 5;
    printGP($a, $r, $n);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to print GP.

function printGP(a, r, n)
{
    let curr_term;
    for (let i = 0; i < n; i++) {
        curr_term = a * Math.pow(r, i);
        document.write(curr_term + " ");
    }
}

// Driver code

    let a = 2; // starting number
    let r = 3; // Common ratio
    let n = 5; // N th term to be find
    printGP(a, r, n);

// This code is contributed by Surbhi Tyagi

</script>
```

**Output:** 

```
2 6 18 54 162
```