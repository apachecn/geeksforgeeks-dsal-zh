# 求数列 14，28，20，40 的第 n 项，…..

> 原文:[https://www . geesforgeks . org/find-the-n-term-of-series-14-28-20-40/](https://www.geeksforgeeks.org/find-the-nth-term-of-the-series-14-28-20-40/)

给定一个数字![N  ](img/05447a6f3ec73065b361522074101320.png "Rendered by QuickLaTeX.com")。任务是在以下系列中找到第 N 个术语:

> **14，28，20，40，32，64…..**

**例:**

```
Input : N = 5
Output : 32

Input : N = 6
Output : 64
```

**进场:**

1.  用 14 初始化第一个数字。
2.  运行从 **i = 2 到 N** 的循环，并执行以下步骤:
    *   对我来说，是上学期的两倍。例如，如果 i = 2，当前项将是 2 *(I = 1 时的项)，即 2*14 = 28。
    *   对于奇数 I，从上一项减去 8。
    *   退出循环并打印最终数字。

以下是上述方法的实现:

## C++

```
// CPP program to find the Nth term of
// the series 14, 28, 20, 40, …..

#include <iostream>
using namespace std;

// Function to find the N-th term
int findNth(int N)
{
    // initializing the 1st number
    int b = 14;

    int i;

    // loop from 2nd term to nth term
    for (i = 2; i <= N; i++) {
        // if i is even, double the
        // previous number
        if (i % 2 == 0)
            b = b * 2;
        // if i is odd, subtract 8 from
        // previous number
        else
            b = b - 8;
    }

    return b;
}

// Driver Code
int main()
{
    int N = 6;

    cout << findNth(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Nth term of
// the series 14, 28, 20, 40,

import java.io.*;

class GFG {

// Function to find the N-th term
 static int findNth(int N)
{
    // initializing the 1st number
    int b = 14;

    int i;

    // loop from 2nd term to nth term
    for (i = 2; i <= N; i++) {
        // if i is even, double the
        // previous number
        if (i % 2 == 0)
            b = b * 2;
        // if i is odd, subtract 8 from
        // previous number
        else
            b = b - 8;
    }

    return b;
}

// Driver Code

    public static void main (String[] args) {
        int N = 6;

    System.out.print(findNth(N));
    }
}
// This code is contributed by shs
```

## 蟒蛇 3

```
# Python 3 program to find the Nth term
# of the series 14, 28, 20, 40, …..

# Function to find the N-th term
def findNth(N):

    # initializing the 1st number
    b = 14

    # loop from 2nd term to nth term
    for i in range (2, N + 1):

        # if i is even, double the
        # previous number
        if (i % 2 == 0):
            b = b * 2

        # if i is odd, subtract 8 from
        # previous number
        else:
            b = b - 8

    return b

# Driver Code
N = 6

print(findNth(N))

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# program to find the Nth term of
// the series 14, 28, 20, 40,

using System;

public class GFG{
    // Function to find the N-th term
static int findNth(int N)
{
    // initializing the 1st number
    int b = 14;

    int i;

    // loop from 2nd term to nth term
    for (i = 2; i <= N; i++) {
        // if i is even, double the
        // previous number
        if (i % 2 == 0)
            b = b * 2;
        // if i is odd, subtract 8 from
        // previous number
        else
            b = b - 8;
    }

    return b;
}

// Driver Code

    static public void Main (){
    int N = 6;
    Console.WriteLine(findNth(N));
    }
}
// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the Nth term of
// the series 14, 28, 20, 40, …..

// Function to find the N-th term
function findNth($N)
{
    // initializing the 1st number
    $b = 14;

    // loop from 2nd term to nth term
    for ($i = 2; $i <= $N; $i++)
    {
        // if i is even, double the
        // previous number
        if ($i % 2 == 0)
            $b = $b * 2;

        // if i is odd, subtract 8 from
        // previous number
        else
            $b = $b - 8;
    }
    return $b;
}

// Driver Code
$N = 6;
echo findNth($N);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>

// java script program to find the Nth term of
// the series 14, 28, 20, 40, …..

// Function to find the N-th term
function findNth(N)
{
    // initializing the 1st number
    let b = 14;

    // loop from 2nd term to nth term
    for (let i = 2; i <= N; i++)
    {
        // if i is even, double the
        // previous number
        if (i % 2 == 0)
            b = b * 2;

        // if i is odd, subtract 8 from
        // previous number
        else
            b = b - 8;
    }
    return b;
}

// Driver Code
N = 6;
document.write(findNth(N));

// This code is contributed
// by pulamolu mohan pavan cse
</script>
```

**Output:** 

```
64
```