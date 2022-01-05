# 检查是否可以通过给定的步骤

从(1，0)到达(X，Y)

> 原文:[https://www . geeksforgeeks . org/check-如果有可能-x-y-from-1-0-按给定步骤/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-reach-x-y-from-1-0-by-given-steps/)

给定两个正整数 **X** 和 **Y** ，任务是检查是否有可能通过给定的步骤从 **(1，0)** 到达 **(X，Y)** 。在每一步中，来自任何单元格 **(a，b)** 的可能移动是 **(a，b + a)** 或 **(a + b，b)** 。如有可能，打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** X = 2，Y = 7
> **输出:**是
> **说明:**到达(2，7)的招式顺序为:(1，0) - > (1，1) - > (2，1) - > (2，3) - > (2，5) - > (2，7)。
> 
> **输入:** X = 30，Y = 24
> T3】输出:否

**天真方法:**最简单的方法是尝试通过使用操作**(X–Y，Y)** 或 **(X，Y–X)**递归地从点 **(X，Y)** 移动到 **(1，0)** ，直到它等于 **(1，0)** 。如果**X**-坐标小于 **1** 或**Y**-坐标小于 **0** ，则不可能达到 **(1，0)** 。因此，打印**“否”**。否则，如果达到 **(1，0)** ，则打印**“是”**。

***时间复杂度:** O(2 <sup>log (min(X，Y))</sup>)*
*T8】辅助空间: O(1)*

**有效方法:**想法是观察以下特性:

*   试着以相反的顺序解决问题，即可以从 **(X，Y)** 移至 **(1，0)** 通过隐遁移至点**(X–Y，Y)** 或 **(X，Y–X)**。
*   上述属性可以表示如下:

> **GCD(X，Y) = GCD(X，Y–X)或 GCD(X–Y，Y)**
> 其中，
> 基本情况为 **GCD(X，0) = X**
> 现在，注意 1 和 0 的 GCD，即 gcd(1，0)为 1。
> 因此，X 和 Y 的 gcd 也必须是 1 才能达到(1，0)。

因此，从上面的观察来看，如果 **GCD(X，Y) = 1** ，从 **(1，0)** 到 **(X，Y)** 的路径总是存在的。如果给定的两个数字的 [GCD 为 **1** ，则打印“是”。否则，打印**“否”**。](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to find the GCD of two
// numbers a and b
int GCD(int a, int b)
{
    // Base Case
    if (b == 0)
        return a;

    // Recursively find the GCD
    else
        return GCD(b, a % b);
}

// Function to check if (x, y) can be
// reached from (1, 0) from given moves
void check(int x, int y)
{
    // If GCD is 1, then print "Yes"
    if (GCD(x, y) == 1) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    // Given X and Y
    int X = 2, Y = 7;

    // Function call
    check(X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to find the
// GCD of two numbers a
// and b
static int GCD(int a,
               int b)
{
  // Base Case
  if (b == 0)
    return a;

  // Recursively find
  // the GCD
  else
    return GCD(b, a % b);
}

// Function to check if
// (x, y) can be reached
// from (1, 0) from given
// moves
static void check(int x,
                  int y)
{
  // If GCD is 1, then
  // print "Yes"
  if (GCD(x, y) == 1)
  {
    System.out.print("Yes");
  }
  else
  {
    System.out.print("No");
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given X and Y
  int X = 2, Y = 7;

  // Function call
  check(X, Y);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the GCD of two
# numbers a and b
def GCD(a, b):

    # Base Case
    if (b == 0):
        return a

    # Recursively find the GCD
    else:
        return GCD(b, a % b)

# Function to check if (x, y) can be
# reached from (1, 0) from given moves
def check(x, y):

    # If GCD is 1, then pr"Yes"
    if (GCD(x, y) == 1):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    # Given X and Y
    X = 2
    Y = 7

    # Function call
    check(X, Y)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;

class GFG{

// Function to find the
// GCD of two numbers a
// and b
static int GCD(int a, int b)
{

  // Base Case
  if (b == 0)
    return a;

  // Recursively find
  // the GCD
  else
    return GCD(b, a % b);
}

// Function to check if
// (x, y) can be reached
// from (1, 0) from given
// moves
static void check(int x, int y)
{

  // If GCD is 1, then
  // print "Yes"
  if (GCD(x, y) == 1)
  {
    Console.WriteLine("Yes");
  }
  else
  {
    Console.WriteLine("No");
  }
}

// Driver Code
public static void Main()
{

  // Given X and Y
  int X = 2, Y = 7;

  // Function call
  check(X, Y);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find the GCD of two
// numbers a and b
function GCD(a, b)
{

    // Base Case
    if (b == 0)
        return a;

    // Recursively find the GCD
    else
        return GCD(b, a % b);
}

// Function to check if (x, y) can be
// reached from (1, 0) from given moves
function check(x, y)
{

    // If GCD is 1, then print "Yes"
    if (GCD(x, y) == 1) {
        document.write("Yes");
    }
    else {
        document.write("No");
    }
}

// Driver Code

    // Given X and Y
    let X = 2, Y = 7;

    // Function call
    check(X, Y);

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(log(min(X，Y))*
***辅助空间:** O(1)*