# 当给出(A + B)、(A + C)和(B + C)中的两个时，求 A、B 和 C 的最小可能值

> 原文:[https://www . geeksforgeeks . org/find-a-b-a-c 和 b-c-b-c-中的两个给定时 a-b-b-c 和 c-c-的最小可能值/](https://www.geeksforgeeks.org/find-minimum-possible-values-of-a-b-and-c-when-two-of-the-a-b-a-c-and-b-c-are-given/)

给定两个整数 **X** 和 **Y** 。 **X** 和 **Y** 代表(A + B)、(A + C)和(B + C)中的任意两个值。任务是找到 **A** 、 **B** 和 **C** ，使得 **A + B + C** 最小可能。
**举例:**

> **输入:** X = 3，Y = 4
> T3】输出: 2 1 2
> A = 2，B = 1，C = 2。
> 那么 A + B = 3，A + C = 4。
> A + B + C = 5，这是最小可能值。
> **输入:** X = 123，Y = 13
> **输出:** 1 12 111

**进场:**让**X = A+B****Y = B+C**。如果 **X > Y** 让我们交换一下。注意**A+b+ C = A+b+(Y–B)= A+Y**。这就是为什么最小化 **A** 的值是最佳的。所以 **A** 的值可以一直是 **1** 。然后**B = X–A**和**C = Y–B**。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find A, B and C
void MinimumValue(int x, int y)
{

    // Keep minimum number in x
    if (x > y)
        swap(x, y);

    // Find the numbers
    int a = 1;
    int b = x - 1;
    int c = y - b;

    cout << a << " " << b << " " << c;
}

// Driver code
int main()
{
    int x = 123, y = 13;

    // Function call
    MinimumValue(x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to find A, B and C
static void MinimumValue(int x, int y)
{

    // Keep minimum number in x
    if (x > y)
    {
        int temp = x;
            x = y;
            y = temp;
    }

    // Find the numbers
    int a = 1;
    int b = x - 1;
    int c = y - b;

    System.out.print( a + " " + b + " " + c);
}

// Driver code
public static void main (String[] args)
{
    int x = 123, y = 13;

    // Function call
    MinimumValue(x, y);
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find A, B and C
def MinimumValue(x, y):

    # Keep minimum number in x
    if (x > y):
        x, y = y, x

    # Find the numbers
    a = 1
    b = x - 1
    c = y - b

    print(a, b, c)

# Driver code
x = 123
y = 13

# Function call
MinimumValue(x, y)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find A, B and C
static void MinimumValue(int x, int y)
{

    // Keep minimum number in x
    if (x > y)
    {
        int temp = x;
            x = y;
            y = temp;
    }

    // Find the numbers
    int a = 1;
    int b = x - 1;
    int c = y - b;

    Console.WriteLine( a + " " + b + " " + c);
}

// Driver code
public static void Main ()
{
    int x = 123, y = 13;

    // Function call
    MinimumValue(x, y);
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
// javascript implementation of the approach

// Function to find A, B and C
function MinimumValue(x, y)
{

    // Keep minimum number in x
    if (x > y)
    {
        var temp = x;
            x = y;
            y = temp;
    }

    // Find the numbers
    var a = 1;
    var b = x - 1;
    var c = y - b;

    document.write( a + " " + b + " " + c);
}

// Driver code
    var x = 123, y = 13;

    // Function call
    MinimumValue(x, y);

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
1 12 111
```