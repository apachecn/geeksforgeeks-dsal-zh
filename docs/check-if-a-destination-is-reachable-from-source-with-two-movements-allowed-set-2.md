# 通过允许的两次移动检查目的地是否可从源到达|设置 2

> 原文:[https://www . geeksforgeeks . org/check-如果一个目的地可以通过两次移动从源到达-允许-set-2/](https://www.geeksforgeeks.org/check-if-a-destination-is-reachable-from-source-with-two-movements-allowed-set-2/)

给定一对坐标 **(X1，Y1)** (源)和 **(X2，Y2)** (目的地)，任务是检查是否有可能通过从任何单元格 **(X，Y)** 的以下移动从源到达目的地:

1.  **(X + Y，Y)**
2.  **(X，Y + X)**

**注:**所有坐标均为正，可以和**10<sup>18</sup>T5 一样大。**

**示例:**

> **输入:** X1 = 2，Y1 = 10，X2 = 26，Y2 = 12
> T3】输出:是
> 
> **解释:**可能的路径:(2，10) → (2，12) ⇾ (14，12) → (26，12)
> 因此，源和目的地之间存在路径。
> 
> **输入:** X1 = 20，Y1 = 10，X2 = 6，Y2 = 12
> T3】输出:否

**天真方法:**解决问题最简单的方法是使用[递归](https://www.geeksforgeeks.org/recursion/)。参考文章[检查目的地是否可从源到达，递归方法允许两次移动](https://www.geeksforgeeks.org/check-destination-reachable-source-two-movements-allowed/)。

**高效方法:**主要思想是检查从目的地坐标(X2，Y2)到源(X1，Y1)的路径是否存在。

按照以下步骤解决问题:

*   继续从 **(X2，Y2)** 的最大值中减去 **(X2，Y2)** 的最小值，如果 **X2** 变得小于 **X1** 或 **Y2** 变得小于 **Y1** 则停止。
*   现在比较一下 **(X1，Y1)** 和修改后的 **(X2，Y2)** 。如果 **X1** 等于**X2****Y1**等于 **Y2** ，则打印“**是**”。
*   如果 **X1** 不等于 **X2** 或 **Y1** 相等，不等于 **Y2** ，则打印“**否**”。

为了优化减法运算的复杂度，可以使用**模**运算来代替。只需执行 **x2 = x2 % y2** 和 **y2 = y2 % x2** 并检查上述必要条件。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Check if (x2, y2) can be reached
// from (x1, y1)
bool isReachable(long long x1, long long y1,
                 long long x2, long long y2)
{
    while (x2 > x1 && y2 > y1) {

        // Reduce x2 by y2 until it is
        // less than or equal to x1
        if (x2 > y2)
            x2 %= y2;

        // Reduce y2 by x2 until it is
        // less than or equal to y1
        else
            y2 %= x2;
    }

    // If x2 is reduced to x1
    if (x2 == x1)

        // Check if y2 can be
        // reduced to y1 or not
        return (y2 - y1) >= 0
               && (y2 - y1) % x1 == 0;

    // If y2 is reduced to y1
    else if (y2 == y1)

        // Check if x2 can be
        // reduced to x1 or not
        return (x2 - x1) >= 0
               && (x2 - x1) % y1 == 0;
    else
        return 0;
}

// Driver Code
int main()
{
    long long source_x = 2, source_y = 10;
    long long dest_x = 26, dest_y = 12;

    if (isReachable(source_x, source_y,
                    dest_x, dest_y))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Check if (x2, y2) can be reached
# from (x1, y1)
def isReachable(x1, y1, x2, y2):

    while(x2 > x1 and y2 > y1):

        # Reduce x2 by y2 until it is
        # less than or equal to x1
        if(x2 > y2):
            x2 %= y2

        # Reduce y2 by x2 until it is
        # less than or equal to y1
        else:
            y2 %= x2

    # If x2 is reduced to x1
    if(x2 == x1):

        # Check if y2 can be
        # reduced to y1 or not
        return (y2 - y1) >= 0 and (
                y2 - y1) % x1 == 0

    # If y2 is reduced to y1
    elif(y2 == y1):

        # Check if x2 can be
        # reduced to x1 or not
        return (x2 - x1) >= 0 and (
                x2 - x1) % y1 == 0
    else:
        return 0

# Driver Code
source_x = 2
source_y = 10
dest_x = 26
dest_y = 12

# Function call
if(isReachable(source_x, source_y,
                 dest_x, dest_y)):
    print("Yes")
else:
    print("No")

# This code is contributed by Shivam Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Check if (x2, y2) can be reached
// from (x1, y1)
static boolean isReachable(long x1, long y1,
                           long x2, long y2)
{
    while (x2 > x1 && y2 > y1)
    {
        // Reduce x2 by y2 until it is
        // less than or equal to x1
        if (x2 > y2)
            x2 %= y2;

        // Reduce y2 by x2 until it is
        // less than or equal to y1
        else
            y2 %= x2;
    }

    // If x2 is reduced to x1
    if (x2 == x1)

        // Check if y2 can be
        // reduced to y1 or not
        return (y2 - y1) >= 0 &&
               (y2 - y1) % x1 == 0;

    // If y2 is reduced to y1
    else if (y2 == y1)

        // Check if x2 can be
        // reduced to x1 or not
        return (x2 - x1) >= 0 &&
               (x2 - x1) % y1 == 0;
    else
        return false;
}

// Driver Code
public static void main(String[] args)
{
    long source_x = 2, source_y = 10;
    long dest_x = 26, dest_y = 12;

    if (isReachable(source_x, source_y,
                    dest_x, dest_y))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by shikhasingrajput
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Check if (x2, y2) can be reached
// from (x1, y1)
static bool isReachable(long x1, long y1,
                        long x2, long y2)
{
  while (x2 > x1 &&
         y2 > y1)
  {
    // Reduce x2 by y2
    // until it is less
    // than or equal to x1
    if (x2 > y2)
      x2 %= y2;

    // Reduce y2 by x2
    // until it is less
    // than or equal to y1
    else
      y2 %= x2;
  }

  // If x2 is reduced to x1
  if (x2 == x1)

    // Check if y2 can be
    // reduced to y1 or not
    return (y2 - y1) >= 0 &&
           (y2 - y1) % x1 == 0;

  // If y2 is reduced to y1
  else if (y2 == y1)

    // Check if x2 can be
    // reduced to x1 or not
    return (x2 - x1) >= 0 &&
           (x2 - x1) % y1 == 0;
  else
    return false;
}

// Driver Code
public static void Main(String[] args)
{
  long source_x = 2, source_y = 10;
  long dest_x = 26, dest_y = 12;

  if (isReachable(source_x, source_y,
                  dest_x, dest_y))
    Console.Write("Yes");
  else
    Console.Write("No");
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript  program for
//the above approach

// Check if (x2, y2) can be reached
// from (x1, y1)
function isReachable(x1, y1, x2, y2)
{
    while (x2 > x1 && y2 > y1)
    {
        // Reduce x2 by y2 until it is
        // less than or equal to x1
        if (x2 > y2)
            x2 %= y2;

        // Reduce y2 by x2 until it is
        // less than or equal to y1
        else
            y2 %= x2;
    }

    // If x2 is reduced to x1
    if (x2 == x1)

        // Check if y2 can be
        // reduced to y1 or not
        return (y2 - y1) >= 0 &&
               (y2 - y1) % x1 == 0;

    // If y2 is reduced to y1
    else if (y2 == y1)

        // Check if x2 can be
        // reduced to x1 or not
        return (x2 - x1) >= 0 &&
               (x2 - x1) % y1 == 0;
    else
        return false;
}

// Driver Code

    let source_x = 2, source_y = 10;
    let dest_x = 26, dest_y = 12;

    if (isReachable(source_x, source_y,
                    dest_x, dest_y))
        document.write("Yes");
    else
       document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)