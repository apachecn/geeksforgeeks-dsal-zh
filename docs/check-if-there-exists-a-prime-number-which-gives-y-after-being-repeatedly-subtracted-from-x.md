# 反复从 X 中减去后检查是否存在给出 Y 的素数

> 原文:[https://www . geeksforgeeks . org/check-if-exists-a-prime-number-of-then-y-before-from-x/](https://www.geeksforgeeks.org/check-if-there-exists-a-prime-number-which-gives-y-after-being-repeatedly-subtracted-from-x/)

给定两个整数 **X** 和 **Y** ，其中 **X > Y** ，任务是检查是否存在质数 **P** ，如果 **P** 从 **X** 中重复减去，则给出 **Y** 。

**示例:**

> **输入:** X = 100，Y = 98
> **输出:**是
> (100 –( 2 * 1)= 98)
> **输入:** X = 45，Y = 31
> **输出:**是
> (45 –( 7 * 2))= 31

**天真的方法:**对从 **2** 到 **x** 的每个整数运行一个循环。如果当前数是素数，并且它满足问题中给出的标准，那么它就是所需的数。
**有效方法:**请注意，对于有效素数 **p** ，**x–k * p = y**或**x–y = k * p**。假设， **p = 2** 然后**(x–y)= 2，4，6，…** (均为偶数)。这意味着如果**(x–y)**是偶数，那么答案总是正确的。如果**(x–y)**是除 **1** 以外的奇数，它将总是有一个质因数。要么它本身是素数，要么它是一个较小的素数和一些其他整数的乘积。所以除了 **1** 以外，所有奇数的答案都是真。
如果**(x–y)= 1**，既不是素数，也不是复合数，该怎么办。所以这是唯一一个答案为假的情况。

以下是该方法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if any
// prime number satisfies
// the given conditions
bool isPossible(int x, int y)
{

    // No such prime exists
    if ((x - y) == 1)
        return false;

    return true;
}

// Driver code
int main()
{
    int x = 100, y = 98;

    if (isPossible(x, y))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true if any
// prime number satisfies
// the given conditions
static boolean isPossible(int x, int y)
{

    // No such prime exists
    if ((x - y) == 1)
        return false;

    return true;
}

// Driver code
public static void main(String[] args)
{
    int x = 100, y = 98;

    if (isPossible(x, y))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if any
# prime number satisfies
# the given conditions
def isPossible(x, y):

    # No such prime exists
    if ((x - y) == 1):
        return False

    return True

# Driver code
x = 100
y = 98

if (isPossible(x, y)):
    print("Yes")
else:
    print("No")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if any
// prime number satisfies
// the given conditions
static bool isPossible(int x, int y)
{

    // No such prime exists
    if ((x - y) == 1)
        return false;

    return true;
}

// Driver code
public static void Main(String[] args)
{
    int x = 100, y = 98;

    if (isPossible(x, y))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function that returns true if any
    // prime number satisfies
    // the given conditions
    function isPossible(x , y) {

        // No such prime exists
        if ((x - y) == 1)
            return false;

        return true;
    }

    // Driver code

        var x = 100, y = 98;

        if (isPossible(x, y))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
Yes
```