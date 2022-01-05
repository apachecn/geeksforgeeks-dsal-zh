# 数字总和为 n 且可被 10^N 除尽的最小数

> 原文:[https://www . geesforgeks . org/最小-数-和-位数-n-整除-10n/](https://www.geeksforgeeks.org/smallest-number-sum-digits-n-divisible-10n/)

求最小的数，使其位数之和为 N，并可被![10^N  ](img/adb280816f48354ab185fab891861636.png "Rendered by QuickLaTeX.com")整除。
**例:**

```
Input : N = 5
Output : 500000
500000 is the smallest number divisible
by 10^5 and sum of digits as 5.

Input : N = 20
Output : 29900000000000000000000
```

**解释**
要让一个数被![10^N  ](img/adb280816f48354ab185fab891861636.png "Rendered by QuickLaTeX.com")整除，我们至少需要在数的末尾加 N 个零。为了使数字最小，我们在数字的末尾加 N 个零。现在，我们需要保证数字的总和为 n，为此，我们将尽量使数字的长度尽可能小，以得到答案。因此，我们继续在数字中插入 9，直到总和不超过 n。如果我们还有余数，那么我们保持它作为第一个数字(最高有效的一个)，这样得到的数字最小。
该方法适用于所有子任务，但有两种情况:
1。首先，最终的数字可能不适合 C++/Java 中的数据类型。因为我们只需要输出数字，所以我们可以使用字符串来存储答案。
2。唯一一个答案为 0 的角情况是 N = 0。
3。没有不存在答案的情况。

## C++

```
// CPP program to find smallest
// number to find smallest number
// with N as sum of digits and
// divisible by 10^N.
#include <bits/stdc++.h>
using namespace std;

void digitsNum(int N)
{
    // If N = 0 the string will be 0
    if (N == 0)
        cout << "0\n";

    // If n is not perfectly divisible
    // by 9 output the remainder
    if (N % 9 != 0)
        cout << (N % 9);

    // Print 9 N/9 times
    for (int i = 1; i <= (N / 9); ++i)
        cout << "9";

    // Append N zero's to the number so
    // as to make it divisible by 10^N
    for (int i = 1; i <= N; ++i)
        cout << "0";

    cout << "\n";
}

// Driver Code
int main()
{
    int N = 5;
    cout << "The number is : ";
    digitsNum(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest
// number to find smallest number
// with N as sum of digits and
// divisible by 10^N.
import java.io.*;

class GFG
{

static void digitsNum(int N)
{
    // If N = 0 the string will be 0
    if (N == 0)
    System.out.println("0");

    // If n is not perfectly divisible
    // by 9 output the remainder
    if (N % 9 != 0)
        System.out.print((N % 9));

    // Print 9 N/9 times
    for (int i = 1; i <= (N / 9); ++i)
        System.out.print("9");

    // Append N zero's to the number so
    // as to make it divisible by 10^N
    for (int i = 1; i <= N; ++i)
        System.out.print("0");
        System.out.print("" );

}

    // Driver Code
    public static void main (String[] args)
    {
    int N = 5;
    System.out.print("The number is : ");
    digitsNum(N);
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python program to find smallest
# number to find smallest number
# with N as sum of digits and
# divisible by 10^N.

import math
def digitsNum(N):

    # If N = 0 the string will be 0
    if (N == 0) :
        print("0", end = "")

    # If n is not perfectly divisible
    # by 9 output the remainder
    if (N % 9 != 0):
        print (N % 9, end ="")

    # Print 9 N/9 times
    for i in range( 1, int(N / 9) + 1) :
        print("9", end = "")

    # Append N zero's to the number so
    # as to make it divisible by 10^N
    for i in range(1, N + 1) :
        print("0", end = "")

    print()

# Driver Code
N = 5
print("The number is : ",end="")
digitsNum(N)

# This code is contributed by Gitanjali.
```

## C#

```
// C# program to find smallest
// number to find smallest number
// with N as sum of digits and
// divisible by 10^N.
using System;

class GFG
{

static void digitsNum(int N)
{
    // If N = 0 the string will be 0
    if (N == 0)
Console.Write("0");

    // If n is not perfectly divisible
    // by 9 output the remainder
    if (N % 9 != 0)
        Console.Write((N % 9));

    // Print 9 N/9 times
    for (int i = 1; i <= (N / 9); ++i)
        Console.Write("9");

    // Append N zero's to the number so
    // as to make it divisible by 10^N )
    for (int i = 1; i <= N; ++i)
        Console.Write("0");
        Console.WriteLine("" );

}

    // Driver Code
    public static void Main ()
    {
    int N = 5;
    Console.Write("The number is : ");
    digitsNum(N);
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find smallest
// number to find smallest number
// with N as sum of digits and
// divisible by 10^N.

function digitsNum($N)
{
    // If N = 0 the string will be 0
    if ($N == 0)
        echo "0\n";

    // If n is not perfectly divisible
    // by 9 output the remainder
    if ($N % 9 != 0)
        echo ($N % 9);

    // Print 9 N/9 times
    for ( $i = 1; $i <= ($N / 9); ++$i)
        echo "9";

    // Append N zero's to the number so
    // as to make it divisible by 10^N
    for ($i = 1; $i <= $N; ++$i)
        echo "0";

    echo "\n";
}

// Driver Code
$N = 5;
echo "The number is : ";
digitsNum($N);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
      // JavaScript program to find smallest
      // number to find smallest number
      // with N as sum of digits and
      // divisible by 10^N.
      function digitsNum(N)
      {

        // If N = 0 the string will be 0
        if (N == 0) document.write("0\n");

        // If n is not perfectly divisible
        // by 9 output the remainder
        if (N % 9 != 0) document.write(N % 9);

        // Print 9 N/9 times
        for (var i = 1; i <= N / 9; ++i) document.write("9");

        // Append N zero's to the number so
        // as to make it divisible by 10^N
        for (var i = 1; i <= N; ++i) document.write("0");

        document.write("\n");
      }

      // Driver Code

      var N = 5;
      document.write("The number is : ");
      digitsNum(N);

      // This code is contributed by rrrtnx.
    </script>
```

**输出:**

```
The number is : 500000
```

**时间复杂度:** O(N)