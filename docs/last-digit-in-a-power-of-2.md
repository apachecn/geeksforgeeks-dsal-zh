# 2 次方的最后一位数字

> 原文:[https://www.geeksforgeeks.org/last-digit-in-a-power-of-2/](https://www.geeksforgeeks.org/last-digit-in-a-power-of-2/)

给定一个数字 n，我们需要找到 2<sup>n</sup>T2 的最后一位数字

> 输入:n = 4
> 输出:6
> 2^4 = 16 的最后一位是 6
> 输入:n = 11
> 输出:8
> 2^11 = 2048 的最后一位是 8

一个**天真的解决方案**是首先计算幂=幂(2，n)，然后用幂% 10 找到幂的最后一位数字。这个解决方案是低效的，并且对于稍大的 n 也有一个整数算术问题。
一个**高效的解决方案**是基于这样的事实:如果我们离开 2^0，最后的数字以 4 为周期重复，即 1。2 的幂(从 2^1 开始)是 2、4、8、16、32、64、128、256、512、1024、2048、…
我们可以注意到最后的数字是 2、4、8、6、2、4、8、6、2、4、8、…
1)我们计算 rem = n % 4。请注意，最后一个 rem 的值将从 0 到 3。
2)我们根据余数的值返回最后一位数字。

```
Remainder   Last Digit
  1            2
  2            4
  3            8
  0            6
```

图解:设 n = 11，rem = n % 4 = 3。2^3 的最后一位数字是 8，与 2^11.的最后一位数字相同

## C++

```
// C++ program to find last digit in a power of 2.
#include <bits/stdc++.h>
using namespace std;

int lastDigit2PowerN(int n)
{

    // Corner case
    if (n == 0)
        return 1;

    // Find the shift in current cycle
    // and return value accordingly
    else if (n % 4 == 1)
        return 2;
    else if (n % 4 == 2)
        return 4;
    else if (n % 4 == 3)
        return 8;
    else
        return 6; // When n % 4 == 0
}

// Driver code
int main()
{
    for (int n = 0; n < 20; n++)
        cout << lastDigit2PowerN(n) << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find last
// digit in a power of 2.
import java.io.*;
import java.util.*;

class GFG{

static int lastDigit2PowerN(int n)
{

    // Corner case
    if (n == 0)
        return 1;

    // Find the shift in current cycle
    // and return value accordingly
    else if (n % 4 == 1)
        return 2;
    else if (n % 4 == 2)
        return 4;
    else if (n % 4 == 3)
        return 8;
    else
        return 6; // When n % 4 == 0
}

// Driver code
public static void main(String[] args)
{
    for (int n = 0; n < 20; n++)
    System.out.print(lastDigit2PowerN(n) + " ");
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 program to find last
# digit in a power of 2.
def lastDigit2PowerN(n):

    # Corner case
    if n == 0:
        return 1

    # Find the shift in current cycle
    # and return value accordingly
    elif n % 4 == 1:
        return 2
    elif n % 4 == 2:
        return 4
    elif n % 4 == 3:
        return 8
    else:
        return 6 # When n % 4 == 0

# Driver code
for n in range(20):
    print(lastDigit2PowerN(n), end = " ")

# This code is contributed by divyeshrabadiya07   
```

## C#

```
// C# program to find last
// digit in a power of 2.
using System;
class GFG{

static int lastDigit2PowerN(int n)
{

    // Corner case
    if (n == 0)
        return 1;

    // Find the shift in current cycle
    // and return value accordingly
    else if (n % 4 == 1)
        return 2;
    else if (n % 4 == 2)
        return 4;
    else if (n % 4 == 3)
        return 8;
    else
        return 6; // When n % 4 == 0
}

// Driver code
public static void Main(string[] args)
{
    for (int n = 0; n < 20; n++)
    {
        Console.Write(lastDigit2PowerN(n) + " ");
    }
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

      // JavaScript program to find
      // last digit in a power of 2.

      function lastDigit2PowerN(n)
      {
        // Corner case
        if (n == 0)
        return 1;

        // Find the shift in current cycle
        // and return value accordingly
        else if (n % 4 == 1)
        return 2;
        else if (n % 4 == 2)
        return 4;
        else if (n % 4 == 3)
        return 8;
        else
        return 6; // When n % 4 == 0
      }

      // Driver code
      for (var n = 0; n < 20; n++)
      document.write(lastDigit2PowerN(n) + " ");

    </script>
```

**Output:** 

```
1 2 4 8 6 2 4 8 6 2 4 8 6 2 4 8 6 2 4 8
```

时间复杂度:O(1)
辅助空间:O(1)
我们能把它推广到任何输入数吗？大数请参考[查找 a^b 最后一位数字](https://www.geeksforgeeks.org/find-last-digit-of-ab-for-large-numbers/)T4】