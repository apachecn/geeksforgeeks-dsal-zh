# 找出两个数的适当分数中的第 n 个数字

> 原文:[https://www . geeksforgeeks . org/find-第 n 位数字的二分之一/](https://www.geeksforgeeks.org/find-the-nth-digit-in-the-proper-fraction-of-two-numbers/)

给定三个整数 **P** 、 **Q** 和 **N** ，其中 **P < Q** ，任务是计算 **P / Q** 的分数值，并找到小数点后的 **N <sup>th</sup>** 位。
**例**

> **输入:** P = 1，Q = 2，N = 1
> **输出:** 5
> (1 / 2) = 0.5，5 为小数点后第一位数字。
> **输入:** P = 5，Q = 6，N = 5
> **输出:**3
> (5/6)= 0.833333333……

**方法:**初始化一个整数变量 **res** ，它存储结果的第 n 个数字。现在，当 **N > 0** 执行以下操作:

1.  将 **N** 减少 **1** 。
2.  要计算数字，更新数值 **P = P * 10** 。
3.  计算 **res = P / Q** 并更新 **P = P % Q** 。

最后，打印 res.
下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the Nth digit
// in the fraction (p / q)
int findNthDigit(int p, int q, int N)
{
    // To store the resultant digit
    int res;

    // While N > 0 compute the Nth digit
    // by dividing p and q and store the
    // result into variable res
    // and go to next digit
    while (N > 0) {
        N--;
        p *= 10;
        res = p / q;
        p %= q;
    }
    return res;
}

// Driver code
int main()
{
    int p = 1, q = 2, N = 1;

    cout << findNthDigit(p, q, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to print the Nth digit
    // in the fraction (p / q)
    static int findNthDigit(int p,
                            int q, int N)
    {
        // To store the resultant digit
        int res = 0;

        // While N > 0 compute the Nth digit
        // by dividing p and q and store the
        // result into variable res
        // and go to next digit
        while (N > 0)
        {
            N--;
            p *= 10;
            res = p / q;
            p %= q;
        }
        return res;
    }

    // Driver code
    public static void main(String args[])
    {
        int p = 1, q = 2, N = 1;

        System.out.println(findNthDigit(p, q, N));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the Nth digit
# in the fraction (p / q)
def findNthDigit(p, q, N) :

    # While N > 0 compute the Nth digit
    # by dividing p and q and store the
    # result into variable res
    # and go to next digit
    while (N > 0) :
        N -= 1;
        p *= 10;
        res = p // q;
        p %= q;

    return res;

# Driver code
if __name__ == "__main__" :

    p = 1; q = 2; N = 1;
    print(findNthDigit(p, q, N));

# This code is contributed by kanugargng
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to print the Nth digit
    // in the fraction (p / q)
    static int findNthDigit(int p, int q, int N)
    {
        // To store the resultant digit
        int res = 0;

        // While N > 0 compute the Nth digit
        // by dividing p and q and store the
        // result into variable res
        // and go to next digit
        while (N > 0)
        {
            N--;
            p *= 10;
            res = p / q;
            p %= q;
        }
        return res;
    }

    // Driver code
    public static void Main()
    {
        int p = 1, q = 2, N = 1;

        Console.WriteLine(findNthDigit(p, q, N));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach

      // Function to print the Nth digit
      // in the fraction (p / q)
      function findNthDigit(p, q, N)
      {

        // To store the resultant digit
        var res;

        // While N > 0 compute the Nth digit
        // by dividing p and q and store the
        // result into variable res
        // and go to next digit
        while (N > 0)
        {
          N--;
          p *= 10;
          res = parseInt(p / q);
          p %= q;
        }
        return res;
      }

      // Driver code
      var p = 1,
        q = 2,
        N = 1;
      document.write(findNthDigit(p, q, N));

      // This code is contributed by rdtank.
    </script>
```

**Output**

```
5
```

**时间复杂度:** O(N)

**辅助空间** : O(1)