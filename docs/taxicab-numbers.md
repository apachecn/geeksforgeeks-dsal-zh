# 出租车号码

> 原文:[https://www.geeksforgeeks.org/taxicab-numbers/](https://www.geeksforgeeks.org/taxicab-numbers/)

第 n 个 Taxicab 编号 Taxicab(n)，也称为第 n 个 **Hardy-Ramanujan 编号**，定义为可以用 n 种不同方式表示为两个正立方数之和的最小数。
最著名的出租车号是 1729 =出租车(2) = (1 ^ 3) + (12 ^ 3) = (9 ^ 3) + (10 ^ 3)。
给定一个数字 N，打印前 N 个出租车(2)号。
**例:**

```
Input: N = 1
Output: 1729
Explanation: 1729 = (1 ^ 3) + (12 ^ 3) 
                  = (9 ^ 3) + (10 ^ 3)

Input: N = 2
Output: 1729 4104
Explanation: 1729 = (1 ^ 3) + (12 ^ 3) 
                   = (9 ^ 3) + (10 ^ 3)
              4104 = (16 ^ 3) + (2 ^ 3) 
                   = (15 ^ 3) + (9 ^ 3)
```

我们逐一尝试所有号码，并检查是否是出租车号码。为了检查一个数字是否是出租车，我们使用两个嵌套循环:
在外循环中，我们计算一个数字的立方根。
在内部循环中，我们检查是否有产生结果的立方根。

## C++

```
// C++ implementation to print first N Taxicab(2)
// numbers :
#include<bits/stdc++.h>
using namespace std;

void printTaxicab2(int N)
{
    // Starting from 1, check every number if
    // it is Taxicab until count reaches N.
    int i = 1, count = 0;
    while (count < N)
    {
       int int_count = 0;

       // Try all possible pairs (j, k) whose cube
       // sums can be i.
       for (int j = 1; j <= pow(i, 1.0/3); j++)
          for (int k = j + 1; k <= pow(i, 1.0/3); k++)
              if (j*j*j + k*k*k == i)
                  int_count++;

       // Taxicab(2) found
       if (int_count == 2)
       {
          count++;
          cout << count << " " << i << endl; 
       }

       i++;
    }
}

// Driver code
int main()
{
    int N = 5;
    printTaxicab2(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Taxicab Numbers
import java.util.*;

class GFG {

    public static void printTaxicab2(int N)
    {
        // Starting from 1, check every number if
        // it is Taxicab until count reaches N.
        int i = 1, count = 0;
        while (count < N)
        {
           int int_count = 0;

           // Try all possible pairs (j, k) whose 
           // cube sums can be i.
           for (int j = 1; j <= Math.pow(i, 1.0/3); j++)
              for (int k = j + 1; k <= Math.pow(i, 1.0/3);
                                                   k++)
                  if (j * j * j + k * k * k == i)
                      int_count++;

           // Taxicab(2) found
           if (int_count == 2)
           {
              count++;
              System.out.println(count + " " + i); 
           }

           i++;
        }
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int N = 5;
        printTaxicab2(N);

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 implementation to print
# first N Taxicab(2) numbers
import math

def printTaxicab2(N):

    # Starting from 1, check every number if
    # it is Taxicab until count reaches N.
    i, count = 1, 0
    while (count < N):

        int_count = 0

        # Try all possible pairs (j, k)
        # whose cube sums can be i.
        for j in range(1, math.ceil(\
                   pow(i, 1.0 / 3)) + 1):

            for k in range(j + 1,\
              math.ceil(pow(i, 1.0 / 3)) + 1):
                if (j * j * j + k * k * k == i):
                    int_count += 1

        # Taxicab(2) found
        if (int_count == 2):

            count += 1
            print(count, " ", i)

        i += 1

# Driver code
N = 5
printTaxicab2(N)

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# Code for Taxicab Numbers
using System;

class GFG {

    public static void printTaxicab2(int N)
    {
        // Starting from 1, check every number if
        // it is Taxicab until count reaches N.
        int i = 1, count = 0;
        while (count < N)
        {
            int int_count = 0;

            // Try all possible pairs (j, k) whose
            // cube sums can be i.
            for (int j = 1; j <= Math.Pow(i, 1.0/3); j++)
                for (int k = j + 1; k <= Math.Pow(i, 1.0/3);
                                                    k++)
                    if (j * j * j + k * k * k == i)
                        int_count++;

            // Taxicab(2) found
            if (int_count == 2)
            {
                count++;
                Console.WriteLine(count + " " + i);
            }

            i++;
        }
    }

    // Driver program
    public static void Main()
    {
        int N = 5;
        printTaxicab2(N);

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to print first
// N Taxicab(2) numbers :

function printTaxicab2($N)
{

    // Starting from 1, check every
    // number if it is Taxicab until
    // count reaches N.
    $i = 1; $count = 0;
    while ($count < $N)
    {
        $int_count = 0;

        // Try all possible pairs (j, k)
        // whose cube sums can be i.
        for ($j = 1; $j <= pow($i, 1.0/3); $j++)
            for ( $k = $j + 1; $k <= pow($i, 1.0/3); $k++)
                if ($j * $j * $j + $k * $k * $k == $i)
                    $int_count++;

        // Taxicab(2) found
        if ($int_count == 2)
        {
            $count++;
            echo $count, " ", $i, "\n";
        }

        $i++;
    }
}

// Driver code

    $N = 5;
    printTaxicab2($N);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
// Javascript implementation to print first
// N Taxicab(2) numbers :
function printTaxicab2(N)
{

    // Starting from 1, check every
    // number if it is Taxicab until
    // count reaches N.
    let i = 1; count = 0;
    while (count < N)
    {
        let int_count = 0;

        // Try all possible pairs (j, k)
        // whose cube sums can be i.
        for (let j = 1; j <= Math.pow(i, 1.0/3); j++)
            for (let k = j + 1; k <= Math.pow(i, 1.0/3); k++)
                if (j * j * j + k * k * k == i)
                    int_count++;

        // Taxicab(2) found
        if (int_count == 2)
        {
            count++;
            document.write(count + " " + i + "<br>");
        }

        i++;
    }
}

// Driver code
    let N = 5;
    printTaxicab2(N);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output**

```
1 1729
2 4104
3 13832
4 20683
5 32832
```

本文由 **Rohit Thapliyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。