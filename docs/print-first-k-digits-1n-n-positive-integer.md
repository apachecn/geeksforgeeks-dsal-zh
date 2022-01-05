# 打印 1/n 的前 k 位数字，其中 n 为正整数

> 原文:[https://www . geesforgeks . org/print-first-k-digits-1n-n-正整数/](https://www.geeksforgeeks.org/print-first-k-digits-1n-n-positive-integer/)

给定一个正整数 n，在值 1/n 的点之后打印前 k 个数字。您的程序应该避免溢出和浮点运算。
**例:**

```
Input:   n = 3, k = 3
Output:  333

Input:   n = 50, k = 4
Output:  0200
```

**强烈建议尽量减少浏览器，先自己试试这个。**
我们来考虑一个例子 n = 7，k = 3。1/7 的第一位是‘1’，可以通过做 10/7 的整数值得到。10/7 的余数是 3。下一位是 4，取整数值 30/7 即可。30/7 的余数是 2。接下来的数字是 2，取整数值 20/7
即可

## C++

```
#include <iostream>
using namespace std;

// Function to print first k digits after dot in value
// of 1/n.  n is assumed to be a positive integer.
void print(int n, int k)
{
   int rem = 1; // Initialize remainder

   // Run a loop k times to print k digits
   for (int i = 0; i < k; i++)
   {
         // The next digit can always be obtained as
         // doing (10*rem)/10
         cout << (10 * rem) / n;

         // Update remainder
         rem = (10*rem) % n;
   }
}

// Driver program to test above function
int main()
{
    int n = 7, k = 3;
    print(n, k);
    cout << endl;

    n = 21, k = 4;
    print(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to Print first k
// digits of 1/n where n is a
// positive integer
import java.io.*;

class GFG
{
    // Function to print first
    // k digits after dot in value
    // of 1/n. n is assumed to be
    // a positive integer.
    static void print(int n, int k)
    {
        // Initialize remainder
        int rem = 1;

        // Run a loop k times to print k digits
        for (int i = 0; i < k; i++)
        {
            // The next digit can always be
            // obtained as doing (10*rem)/10
            System.out.print( (10 * rem) / n);

            // Update remainder
            rem = (10 * rem) % n;

        }

    }

    // Driver program
    public static void main(String []args)
    {
        int n = 7, k = 3;
        print(n, k);
        System.out.println();

        n = 21;
        k = 4;
        print(n, k);

    }
}

// This article is contributed by vt_m
```

## 蟒蛇 3

```
# Python code to Print first k
# digits of 1/n where n is a
# positive integer
import math

# Function to print first k digits
# after dot in value of 1/n. n is
# assumed to be a positive integer.
def Print(n, k):
    rem = 1 # Initialize remainder

    # Run a loop k times to print
    # k digits
    for i in range(0, k):
        # The next digit can always
        # be obtained as doing
        # (10*rem)/10
        print(math.floor(((10 * rem)
                       / n)), end="")

        # Update remainder
        rem = (10*rem) % n

# Driver program to test
# above function
n = 7
k = 3
Print(n, k);
print(" ")
n = 21
k = 4
Print(n, k);

# This code is contributed by Sam007.
```

## C#

```
// C# code to Print first k digits of
// 1/n where n is a positive integer
using System;

class GFG {

    // Function to print first
    // k digits after dot in value
    // of 1/n. n is assumed to be
    // a positive integer.
    static void print(int n, int k)
    {

        // Initialize remainder
        int rem = 1;

        // Run a loop k times to
        // print k digits
        for (int i = 0; i < k; i++)
        {

            // The next digit can always be
            // obtained as doing (10*rem)/10
            Console.Write( (10 * rem) / n);

            // Update remainder
            rem = (10 * rem) % n;
        }
    }

    // Driver program
    public static void Main()
    {
        int n = 7, k = 3;
        print(n, k);
        Console.WriteLine();

        n = 21;
        k = 4;
        print(n, k);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Function to print first k digits
// after dot in value of 1/n. n is
// assumed to be a positive integer.

function println($n, $k)
{
    // Initialize remainder
    $rem = 1;

// Run a loop k times
// to print k digits
for ($i = 0; $i < $k; $i++)
{
    // The next digit can always
    // be obtained as doing
    // (10 * rem) / 10
    echo floor((10 * $rem) / $n);

    // Update remainder
    $rem = (10 * $rem) % $n;
}
}

// Driver Code
$n = 7; $k = 3;
println($n, $k);
echo "\n";

$n = 21; $k = 4;
println($n, $k);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Function to print first k digits after dot in value
// of 1/n.  n is assumed to be a positive integer.
function print(n,  k)
{
   let rem = 1; // Initialize remainder
   let ans = '';
   // Run a loop k times to print k digits
   for (let i = 0; i < k; i++)
   {
         // The next digit can always be obtained as
         // doing (10*rem)/10
         ans += Math.floor(((10 * rem) / n));
         // Update remainder
         rem = (10*rem) % n;
   }
   document.write(ans)
}

// Driver program to test above function
let n = 7;
let k = 3;
print(n, k);
document.write("<br>");
n = 21;
k = 4;
print(n, k);

</script>
```

**输出:**

```
142
0476
```

时间复杂度:0(k)

辅助空间:0(1)

**参考:**
[算法与编程:问题与解决方案](http://www.flipkart.com/algorithms-programming-problems-solutions-english-first/p/itmdwjdzydjcdmmp?pid=9780817638474&affid=sandeepgfg)
本文由**沙钦**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。