# 重复除以 2 后留下奇数余数的第一个数字

> 原文:[https://www . geesforgeks . org/先数后留余数重复除以 2/](https://www.geeksforgeeks.org/first-number-to-leave-an-odd-remainder-after-repetitive-division-by-2/)

给定两个整数 **A** 和 **B** ，任务是打印这两个整数中的一个整数，该整数将被较小的 2 分频数转换为奇数。如果两个数字在相同的操作次数后都被转换成奇数，则打印-1。

**示例:**

> **输入:** A = 10，B = 8
> **输出:** 10
> **解释:**
> 第一步:A/2 = 5，B/2 = 4
> 因此，A 是第一个要转换为奇数的数字。
> 
> **输入:** A = 20，B = 12
> **输出:** -1
> **解释:**
> 第一步:A/2 = 10，B/2 = 6
> 第二步:A/2 = 5，B/2 = 3
> 因此，A 和 B 同时转换为奇数。

**天真的方法:**
解决问题最简单的方法如下:

*   检查两个给定的数字是偶数还是奇数。如果其中一个是奇数，打印那个数字。
*   如果两者都是奇数，打印-1。
*   否则，在每一步继续将两者除以 2，并检查它们中是否有任何一个被转换为奇数。如果其中一个被转换，打印该数字的初始值。如果两者同时转换，打印-1。

下面是上述方法的实现:

## C++

```
// C++ program to find the first
// number to be converted to an odd
// integer by repetitive division by 2
#include <bits/stdc++.h>
using namespace std;

// Function to return the first number
// to to be converted to an odd value
int odd_first(int a, int b)
{

    // Initial values
    int true_a = a;
    int true_b = b;

    // Perform repetitive divisions by 2
    while(a % 2 != 1 && b % 2 != 1)
    {
        a = a / 2;
        b = b / 2;
    }

    // If both become odd at same step
    if (a % 2 == 1 && b % 2 == 1)
        return -1;

    // If a is first to become odd
    else if (a % 2 == 1)
        return true_a;

    // If b is first to become odd
    else
        return true_b;
}

// Driver code
int main()
{
    int a = 10;
    int b = 8;

    cout << odd_first(a, b);
}

// This code is contributed by code_hunt
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the first
// number to be converted to an odd
// integer by repetitive division by 2
import java.util.*;
import java.lang.Math;
import java.io.*;

class GFG{

// Function to return the first number
// to to be converted to an odd value
static int odd_first(int a, int b)
{

    // Initial values
    int true_a = a;
    int true_b = b;

    // Perform repetitive divisions by 2
    while(a % 2 != 1 && b % 2 != 1)
    {
        a = a / 2;
        b = b / 2;
    }

    // If both become odd at same step
    if (a % 2 == 1 && b % 2 == 1)
        return -1;

    // If a is first to become odd
    else if (a % 2 == 1)
        return true_a;

    // If b is first to become odd
    else
        return true_b;
}

// Driver code
public static void main(String[] args)
{
    int a = 10;
    int b = 8;

    System.out.print(odd_first(a, b));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program to find the first
# number to be converted to an odd
# integer by repetitive division by 2

# Function to return the first number
# to to be converted to an odd value
def odd_first(a, b):

  # Initial values
  true_a = a
  true_b = b

  # Perform repetitive divisions by 2
  while(a % 2 != 1 and b % 2 != 1):
    a = a//2
    b = b//2

  # If both become odd at same step
  if a % 2 == 1 and b % 2 == 1:
    return -1

  # If a is first to become odd
  elif a % 2 == 1:
    return true_a

  # If b is first to become odd
  else:
    return true_b

# Driver Code
a, b = 10, 8
print(odd_first(a, b))
```

## C#

```
// C# program to find the first
// number to be converted to an odd
// integer by repetitive division by 2
using System;

class GFG{

// Function to return the first number
// to to be converted to an odd value
static int odd_first(int a, int b)
{

    // Initial values
    int true_a = a;
    int true_b = b;

    // Perform repetitive divisions by 2
    while(a % 2 != 1 && b % 2 != 1)
    {
        a = a / 2;
        b = b / 2;
    }

    // If both become odd at same step
    if (a % 2 == 1 && b % 2 == 1)
        return -1;

    // If a is first to become odd
    else if (a % 2 == 1)
        return true_a;

    // If b is first to become odd
    else
        return true_b;
}

// Driver code
public static void Main()
{
    int a = 10;
    int b = 8;

    Console.Write(odd_first(a, b));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to find the first
// number to be converted to an odd
// integer by repetitive division by 2

// Function to return the first number
// to to be converted to an odd value
function odd_first(a, b)
{

    // Initial values
    var true_a = a;
    var true_b = b;

    // Perform repetitive divisions by 2
    while(a % 2 != 1 && b % 2 != 1)
    {
        a = a / 2;
        b = b / 2;
    }

    // If both become odd at same step
    if (a % 2 == 1 && b % 2 == 1)
        return -1;

    // If a is first to become odd
    else if (a % 2 == 1)
        return true_a;

    // If b is first to become odd
    else
        return true_b;
}

// Driver code
var a = 10, b = 8;

document.write(odd_first(a, b));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
10
```

***时间复杂度:** O(log(min(a，b))*
***辅助空间:** O(1)*

**高效方法:**
按照以下步骤优化上述方法:

*   将一个数除以 2 相当于对该数执行右移。
*   因此，两者中最低有效位的数将首先被转换为奇数。

下面是上述方法的实现。

## C++

```
// C++ Program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the position
// least significant set bit
int getFirstSetBitPos(int n)
{
    return log2(n & -n) + 1;
}

// Function return the first number
// to be converted to an odd integer
int oddFirst(int a, int b)
{

    // Stores the positions of the
    // first set bit
    int steps_a = getFirstSetBitPos(a);
    int steps_b = getFirstSetBitPos(b);

    // If both are same
    if (steps_a == steps_b) {
        return -1;
    }

    // If A has the least significant
    // set bit
    if (steps_a > steps_b) {
        return b;
    }

    // Otherwise
    if (steps_a < steps_b) {
        return a;
    }
}

// Driver code
int main()
{
    int a = 10;
    int b = 8;

    cout << oddFirst(a, b);
} 
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program implementation
// of the approach
import java.util.*;
import java.lang.Math;
import java.io.*;

class GFG{

// Function to return the position
// least significant set bit
static int getFirstSetBitPos(int n)
{
    return (int)(Math.log(n & -n) /
                 Math.log(2));
}

// Function return the first number
// to be converted to an odd integer
static int oddFirst(int a, int b)
{

    // Stores the positions of the
    // first set bit
    int steps_a = getFirstSetBitPos(a);
    int steps_b = getFirstSetBitPos(b);

    // If both are same
    if (steps_a == steps_b)
    {
        return -1;
    }

    // If A has the least significant
    // set bit
    else if (steps_a > steps_b)
    {
        return b;
    }

    // Otherwise
    else
    {
        return a;
    }
}

// Driver code
public static void main(String[] args)
{
    int a = 10;
    int b = 8;

    System.out.print(oddFirst(a, b));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach
from math import log

# Function to return the position
# least significant set bit
def getFirstSetBitPos(n):
    return log(n & -n, 2) + 1

# Function return the first number
# to be converted to an odd integer
def oddFirst(a, b):

    # Stores the positions of the
    # first set bit
    steps_a = getFirstSetBitPos(a)
    steps_b = getFirstSetBitPos(b)

    # If both are same
    if (steps_a == steps_b):
        return -1

    # If A has the least significant
    # set bit
    if (steps_a > steps_b):
        return b

    # Otherwise
    if (steps_a < steps_b):
        return a

# Driver code
if __name__ == '__main__':

    a = 10
    b = 8

    print(oddFirst(a, b))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program implementation
// of the approach
using System;

class GFG{

// Function to return the position
// least significant set bit
static int getFirstSetBitPos(int n)
{
    return (int)(Math.Log(n & -n) /
                 Math.Log(2));
}

// Function return the first number
// to be converted to an odd integer
static int oddFirst(int a, int b)
{

    // Stores the positions of the
    // first set bit
    int steps_a = getFirstSetBitPos(a);
    int steps_b = getFirstSetBitPos(b);

    // If both are same
    if (steps_a == steps_b)
    {
        return -1;
    }

    // If A has the least significant
    // set bit
    else if (steps_a > steps_b)
    {
        return b;
    }

    // Otherwise
    else
    {
        return a;
    }
}

// Driver code
public static void Main()
{
    int a = 10;
    int b = 8;

    Console.Write(oddFirst(a, b));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program implementation
// of the approach

// Function to return the position
// least significant set bit
function getFirstSetBitPos(n)
{
    return (Math.log(n & -n) /
                 Math.log(2));
}

// Function return the first number
// to be converted to an odd integer
function oddFirst(a, b)
{

    // Stores the positions of the
    // first set bit
    let steps_a = getFirstSetBitPos(a);
    let steps_b = getFirstSetBitPos(b);

    // If both are same
    if (steps_a == steps_b)
    {
        return -1;
    }

    // If A has the least significant
    // set bit
    else if (steps_a > steps_b)
    {
        return b;
    }

    // Otherwise
    else
    {
        return a;
    }
}

// Driver Code

       let a = 10;
    let b = 8;

    document.write(oddFirst(a, b));

</script>
```

**Output:** 

```
10
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*