# 寻找第 n 个奇斐波那契数的程序

> 原文:[https://www . geesforgeks . org/program-to-find-n-奇数-fibonacci-number/](https://www.geeksforgeeks.org/program-to-find-nth-odd-fibonacci-number/)

给定一个整数 N，任务是找到第 N<sup>个奇数斐波那契数。
奇数斐波那契数列为:</sup> 

> 1, 1, 3, 5, 13, 21, 55, 89, 233, 377, 987, 1597………….等等。
> **注**:在上面的数列中，我们从一般的[斐波那契数列](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)中省略了偶数项。

**例:**

```
Input: N = 3
Output: 3

Input: N = 4
Output: 5
```

**进场:**
仔细观察可以推断，每三个斐波那契数中就有一个是偶数，所以第 N 个<sup>的</sup>奇数斐波那契数就是一般斐波那契数列中的 **{(3*N+1)/2} <sup>第</sup>个**项。
以下是上述方法的实施:

## C++

```
// C++ program for Nth odd fibonacci number

#include <bits/stdc++.h>
using namespace std;

// Function to find nth odd fibonacci number
int oddFib(int n)
{
    n = (3 * n + 1) / 2;
    int a = -1, b = 1, c, i;
    for (i = 1; i <= n; i++) {
        c = a + b;
        a = b;
        b = c;
    }
    return c;
}

// Driver Code
int main()
{
    int n = 4;

    cout << oddFib(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Nth odd fibonacci number
class GFG
{

    // Function to find nth odd fibonacci number
    static int oddFib(int n)
    {
        n = (3 * n + 1) / 2;

        int a = -1, b = 1, c = 0, i;

        for (i = 1; i <= n; i++)
        {
            c = a + b;
            a = b;
            b = c;
        }
        return c;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 4;

        System.out.println(oddFib(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program for Nth odd fibonacci number

# Function to find nth odd fibonacci number
def oddFib(n):
    n = (3 * n + 1) // 2

    a = -1
    b = 1
    c = 0
    for i in range(1, n + 1):
        c = a + b
        a = b
        b = c

    return c

# Driver Code
n = 4

print(oddFib(n))

# This code is contributed by mohit kumar
```

## C#

```
// C# program for Nth odd fibonacci number
using System;

class GFG
{

    // Function to find nth odd fibonacci number
    static int oddFib(int n)
    {
        n = (3 * n + 1) / 2;

        int a = -1, b = 1, c = 0, i;

        for (i = 1; i <= n; i++)
        {
            c = a + b;
            a = b;
            b = c;
        }
        return c;
    }

    // Driver Code
    public static void Main (String[] args)
    {
        int n = 4;

        Console.WriteLine(oddFib(n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for Nth odd fibonacci number

// Function to find nth odd fibonacci number
function oddFib(n)
{
    n = (3 * n + 1) / 2;
    var a = -1, b = 1, c, i;
    for (i = 1; i <= n; i++) {
        c = a + b;
        a = b;
        b = c;
    }
    return c;
}

// Driver Code
var n = 4;
document.write(oddFib(n));

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N)