# 冰雹号

> 原文:[https://www.geeksforgeeks.org/hailstone-numbers/](https://www.geeksforgeeks.org/hailstone-numbers/)

我们被提供了一个数字 N。我们的任务是从 N 生成所有的冰雹数字，并找到 N 所采取的步骤数

**柯拉茨猜想:**l .柯拉茨在 1937 年提出的一个问题，也叫 3x+1 映射，3n+1 问题。设 N 为整数。根据柯拉茨猜想，如果我们按照如下方式不断迭代 N
N = N/2//对于偶数 N
和 N = 3 * N + 1 //对于奇数 N
我们的数最终会收敛到 1，与 N 的选择无关
**冰雹数:**柯拉茨猜想生成的整数序列称为冰雹数。

**示例:**

```
Input : N = 7
Output : 
Hailstone Numbers: 7, 22, 11, 34, 17,
                   52, 26, 13, 40, 20,
                   10, 5, 16, 8, 4, 2,
                    1
No. of steps Required: 17

Input : N = 9
Output : 
Hailstone Numbers: 9, 28, 14, 7, 22, 11,
                   34, 17, 52, 26, 13, 
                   40, 20, 10, 5, 16, 8,
                   4, 2, 1
No. of steps Required: 20

In the first example, N = 7\. 
The numbers will be calculated as follows:
7
3 * 7 + 1 = 22     // Since 7 is odd.
22 / 2 = 11        // 22 is even.
3 * 11 + 1 = 34    // 11 is odd.
.... and so on upto 1.
```

这个想法很简单，我们递归打印数字，直到我们达到基本大小写。

## C++

```
// C++ program to generate hailstone
// numbers and calculate steps required
// to reduce them to 1
#include <bits/stdc++.h>
using namespace std;

// function to print hailstone numbers
// and to calculate the number of steps
// required
int HailstoneNumbers(int N)
{
    static int c;

    cout << N << " ";

    if (N == 1 && c == 0) {

        // N is initially 1.
        return c;
    }
    else if (N == 1 && c != 0) {

        // N is reduced to 1.
        c++;
        return c;
    }
    else if (N % 2 == 0) {

        // If N is Even.
        c++;
        HailstoneNumbers(N / 2);
    }
    else if (N % 2 != 0) {

        // N is Odd.
        c++;
        HailstoneNumbers(3 * N + 1);
    }
}

// Driver code
int main()
{
    int N = 7;
    int x;

    // Function to generate Hailstone
    // Numbers
    x = HailstoneNumbers(N);

    // Output: Number of Steps
    cout << endl;
    cout << "Number of Steps: " << x;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate hailstone
// numbers and calculate steps required
// to reduce them to 1
import java.util.*;
class GFG {
    static int c;

    // function to print hailstone numbers
    // and to calculate the number of steps
    // required
    static int HailstoneNumbers(int N)
    {
        System.out.print(N + " ");

        if (N == 1 && c == 0) {

            // N is initially 1.
            return c;
        }
        else if (N == 1 && c != 0) {

            // N is reduced to 1.
            c++;
            return c;
        }
        else if (N % 2 == 0) {

            // If N is Even.
            c++;
            HailstoneNumbers(N / 2);
        }
        else if (N % 2 != 0) {

            // N is Odd.
            c++;
            HailstoneNumbers(3 * N + 1);
        }
        return c;
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 7;
        int x;

        // Function to generate Hailstone
        // Numbers
        x = HailstoneNumbers(N);

        // Output: Number of Steps
        System.out.println();
        System.out.println("Number of Steps: " + x);
    }
}
/* This code is contributed by Kriti Shukla */
```

## 计算机编程语言

```
# Python3 program to generate
# hailstone numbers and
# calculate steps required
# to reduce them to 1

# function to print hailstone
# numbers and to calculate
# the number of steps required

def HailstoneNumbers(N, c):
    print(N, end=" ")
    if (N == 1 and c == 0):

        # N is initially 1.
        return c
    elif (N == 1 and c != 0):

        # N is reduced to 1.
        c = c + 1
    elif (N % 2 == 0):

        # If N is Even.
        c = c + 1
        c = HailstoneNumbers(int(N / 2), c)
    elif (N % 2 != 0):

        # N is Odd.
        c = c + 1
        c = HailstoneNumbers(3 * N + 1, c)
    return c

# Driver Code
N = 7

# Function to generate
# Hailstone Numbers
x = HailstoneNumbers(N, 0)

# Output: Number of Steps
print("\nNumber of Steps: ", x)

# This code is contributed
# by mits
```

## C#

```
// C# program to generate hailstone
// numbers and calculate steps required
// to reduce them to 1
using System;

class GFG {
    static int c;

    // function to print hailstone numbers
    // and to calculate the number of steps
    // required
    static int HailstoneNumbers(int N)
    {
        Console.Write(N + " ");

        if (N == 1 && c == 0) {

            // N is initially 1.
            return c;
        }
        else if (N == 1 && c != 0) {

            // N is reduced to 1.
            c++;
            return c;
        }
        else if (N % 2 == 0) {

            // If N is Even.
            c++;
            HailstoneNumbers(N / 2);
        }
        else if (N % 2 != 0) {

            // N is Odd.
            c++;
            HailstoneNumbers(3 * N + 1);
        }
        return c;
    }

    // Driver code
    public static void Main()
    {
        int N = 7;
        int x;

        // Function to generate Hailstone
        // Numbers
        x = HailstoneNumbers(N);

        // Output: Number of Steps
        Console.WriteLine();
        Console.WriteLine("Number of Steps: " + x);
    }
}
// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to generate 
// hailstone numbers and
// calculate steps required
// to reduce them to 1

// function to print hailstone
// numbers and to calculate the
// number of steps required
function HailstoneNumbers($N)
{
    static $c;

    echo $N." ";

    if ($N == 1 && $c == 0)
    {

        // N is initially 1.
        return $c;
    }
    else if ($N == 1 && $c != 0)
    {

        // N is reduced to 1.
        $c++;
        return $c;
    }
    else if ($N % 2 == 0)
    {

        // If N is Even.
        $c++;
        HailstoneNumbers((int)($N / 2));
    }
    else if ($N % 2 != 0)
    {

        // N is Odd.
        $c++;
        HailstoneNumbers(3 * $N + 1);
    }
    return $c;
}

// Driver Code
$N = 7;

// Function to generate
// Hailstone Numbers
$x = HailstoneNumbers($N);

// Output: Number of Steps
echo "\nNumber of Steps: ". $x;

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to generate hailstone
// numbers and calculate steps required
// to reduce them to 1

let c = 0;

    // function to print hailstone numbers
    // and to calculate the number of steps
    // required
    function HailstoneNumbers(N)
    {
        document.write(N + " ");

        if (N == 1 && c == 0) {

            // N is initially 1.
            return c;
        }
        else if (N == 1 && c != 0) {

            // N is reduced to 1.
            c++;
            return c;
        }
        else if (N % 2 == 0) {

            // If N is Even.
            c++;
            HailstoneNumbers(N / 2);
        }
        else if (N % 2 != 0) {

            // N is Odd.
            c++;
            HailstoneNumbers(3 * N + 1);
        }
        return c;
    }     

// Driver Code
        let N = 7;
        let x;

        // Function to generate Hailstone
        // Numbers
        x = HailstoneNumbers(N);

        // Output: Number of Steps
        document.write("<br/>");
        document.write("Number of Steps: " + x);

// This code is contributed by susmitakundugoaldanga.
</script>
```

**Output**

```
7 22 11 34 17 52 26 13 40 20 10 5 16 8 4 2 1 
Number of Steps: 17
```

本文由**vinet Joshi**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。