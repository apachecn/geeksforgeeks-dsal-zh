# 以 0 为数字计数

> 原文:[https://www.geeksforgeeks.org/count-numbers-0-digit/](https://www.geeksforgeeks.org/count-numbers-0-digit/)

计算从 1 到 N 有多少整数包含 0 作为数字。
示例:

```
Input:  n = 9
Output: 0

Input: n = 107
Output: 17
The numbers having 0 are 10, 20,..90, 100, 101..107

Input: n = 155
Output: 24
The numbers having 0 are 10, 20,..90, 100, 101..110,
120, ..150.
```

其思想是遍历从 1 到 n 的所有数字。对于每个遍历的数字，遍历其数字，如果任何数字为 0，递增计数。以下是上述思路的实现:

## C++

```
// C++ program to count numbers from 1 to n with
// 0 as a digit
#include<bits/stdc++.h>
using namespace std;

// Returns 1 if x has 0, else 0
int has0(int x)
{
    // Traverse through all digits of
    // x to check if it has 0.
    while (x)
    {
        // If current digit is 0, return true
        if (x % 10 == 0)
          return 1;

        x /= 10;
    }

    return 0;
}

// Returns count of numbers from 1 to n with 0 as digit
int getCount(int n)
{
    // Initialize count of numbers having 0 as digit
    int count = 0;

    // Traverse through all numbers and for every number
    // check if it has 0.
    for (int i=1; i<=n; i++)
        count += has0(i);

    return count;
}

// Driver program
int main()
{
    int n = 107;
    cout << "Count of numbers from 1" << " to "
         << n << " is " << getCount(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count numbers
// from 1 to n with 0 as a digit
import java.io.*;

class GFG {

    // Returns 1 if x has 0, else 0
    static int has0(int x)
    {
        // Traverse through all digits
        // of x to check if it has 0.
        while (x != 0)
        {
            // If current digit is 0,
            // return true
            if (x % 10 == 0)
            return 1;

            x /= 10;
        }

        return 0;
    }

    // Returns count of numbers
    // from 1 to n with 0 as digit
    static int getCount(int n)
    {
        // Initialize count of
        // numbers having 0 as digit
        int count = 0;

        // Traverse through all numbers
        // and for every number
        // check if it has 0.
        for (int i = 1; i <= n; i++)
            count += has0(i);

        return count;
    }

// Driver program
public static void main(String args[])
{
  int n = 107;
  System.out.println("Count of numbers from 1"
            + " to " +n + " is " + getCount(n));
}
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python3 program to count numbers
# from 1 to n with 0 as a digit

# Returns 1 if x has 0, else 0
def has0(x) :

    # Traverse through all digits
    # of x to check if it has 0.
    while (x != 0) :

        # If current digit is 0,
        # return true
        if (x % 10 == 0) :
            return 1

        x = x // 10

    return 0

# Returns count of numbers
# from 1 to n with 0 as digit
def getCount(n) :

    # Initialize count of numbers
    # having 0 as digit.
    count = 0

    # Traverse through all numbers
    # and for every number check
    # if it has 0.
    for i in range(1, n + 1) :
        count = count + has0(i)

    return count

# Driver program
n = 107
print("Count of numbers from 1", " to ",
                n , " is " , getCount(n))

# This code is contributed by Nikita tiwari.
```

## C#

```
// C# program to count numbers
// from 1 to n with 0 as a digit
using System;

class GFG
{

    // Returns 1 if x has 0, else 0
    static int has0(int x)
    {
        // Traverse through all digits
        // of x to check if it has 0.
        while (x != 0)
        {
            // If current digit is 0,
            // return true
            if (x % 10 == 0)
            return 1;

            x /= 10;
        }

        return 0;
    }

    // Returns count of numbers
    // from 1 to n with 0 as digit
    static int getCount(int n)
    {
        // Initialize count of
        // numbers having 0 as digit
        int count = 0;

        // Traverse through all numbers
        // and for every number
        // check if it has 0.
        for (int i = 1; i <= n; i++)
            count += has0(i);

        return count;
    }

// Driver Code
public static void Main()
{

    int n = 107;
    Console.WriteLine("Count of numbers from 1"
                        + " to " +n + " is " + getCount(n));
}
}

// This code is contributed by Sam007
```

## java 描述语言

```
<script>

// JavaScript program to count numbers from 1 to n with
// 0 as a digit

// Returns 1 if x has 0, else 0
function has0(x)
{
    // Traverse through all digits of
    // x to check if it has 0.
    while (x)
    {
        // If current digit is 0, return true
        if (x % 10 == 0)
        return 1;

        x = Math.floor(x / 10);
    }

    return 0;
}

// Returns count of numbers from 1 to n with 0 as digit
function getCount(n)
{
    // Initialize count of numbers having 0 as digit
    let count = 0;

    // Traverse through all numbers and for every number
    // check if it has 0.
    for (let i=1; i<=n; i++)
        count += has0(i);

    return count;
}

// Driver program

    let n = 107;
    document.write("Count of numbers from 1" + " to "
        + n + " is " + getCount(n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
Count of numbers from 1 to 107 is 17
```

关于优化的解决方案，请参考下面的帖子。
[以 0 为数字计数](https://www.geeksforgeeks.org/count-numbers-having-0-as-a-digit/)
本文由戴拉杰·古普塔供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息