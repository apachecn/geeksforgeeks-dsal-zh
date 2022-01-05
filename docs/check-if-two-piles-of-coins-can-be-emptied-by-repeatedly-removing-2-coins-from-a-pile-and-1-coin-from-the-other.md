# 反复从一堆中取出 2 枚硬币，从另一堆中取出 1 枚硬币，检查两堆硬币是否可以清空

> 原文:[https://www . geeksforgeeks . org/check-if-两堆硬币-可以通过从一堆中反复取出 2 个硬币并从另一堆中取出 1 个硬币来清空/](https://www.geeksforgeeks.org/check-if-two-piles-of-coins-can-be-emptied-by-repeatedly-removing-2-coins-from-a-pile-and-1-coin-from-the-other/)

给定两堆由硬币数量 **N** 和 **M** 组成的硬币，任务是通过重复从一堆中取出 **2 枚硬币**和从另一堆中取出 **1 枚硬币**来检查两堆硬币是否可以同时清空。如果两堆都可以清空，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** N = 1，M = 2
> **输出:**是
> **说明:**
> 从 1 <sup>st</sup> 堆中取出 1 枚硬币，从另一堆中取出 2 枚硬币。因此，两堆硬币的数量都是 0。
> 
> **输入:** N = 2，M = 2
> T3】输出:否

**方法:**给定的问题可以基于以下观察来解决:

*   从堆中取出硬币有两种方式，即从**堆 1** 取出 **2 枚硬币**，从**堆 2** 取出 **1 枚硬币**，或者从**堆 1** 取出 **1 枚硬币**，从**堆 2** 取出 **2 枚硬币**。
*   设 **X** 为第一次移出的步数， **Y** 为第二次移出的步数，则两堆中剩余的硬币数分别为**(N–2 * X–Y)**和**(M–2 * Y–X)**。
*   执行 **(X + Y)** 移动后，必须清空堆，即:

> (N–2 * X–Y)= 0 和(M–2 * Y–X)= 0
> 
> 重新排列上述等式中的项会生成以下等式:
> 
> N = 2*X + Y，M = 2*Y + X

*   两堆硬币总数为**(N+M)**=**(2 * X+Y)+(X+2 * Y)= 3(X+Y)**。
*   因此，要使两个堆都为空，以下是条件:
    *   两堆硬币的总和应为 3 的[倍。](https://www.geeksforgeeks.org/find-the-largest-number-multiple-of-3/)
    *   **N** 和 **M** 的[最大值](https://www.geeksforgeeks.org/stdmax-in-cpp/)必须小于 **N** 和 **M** 的[最小值](https://www.geeksforgeeks.org/stdmin-in-cpp/)的两倍，因为一整堆硬币会变空，一些硬币仍会留在另一堆硬币中。因此，大桩的尺寸不应超过小桩尺寸的两倍。

因此，思路是[检查硬币总数之和是否为**3**T3 的倍数，最大硬币数最多为最小硬币数的两倍，然后打印**“是”**。否则，打印**“否”**。](https://www.geeksforgeeks.org/check-whether-large-number-given-form-multiple-3/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if two given piles
// can be emptied by repeatedly removing
// 2 coins from a pile and 1 coin from the other
void canBeEmptied(int A, int B)
{
    // If maximum of A & B exceeds
    // the twice of minimum of A & B
    if (max(A, B) > 2 * min(A, B)) {

        // Not possible to
        // empty the piles
        cout << "No";
        return;
    }

    // If sum of both the coins is
    // divisible by 3, then print Yes
    if ((A + B) % 3 == 0)
        cout << "Yes";

    // Otherwise, print "No"
    else
        cout << "No";
}

// Driver Code
int main()
{
    int A = 1, B = 2;
    canBeEmptied(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;

class GFG{

// Function to check if two given piles
// can be emptied by repeatedly removing
// 2 coins from a pile and 1 coin from the other
static void canBeEmptied(int A, int B)
{

    // If maximum of A & B exceeds
    // the twice of minimum of A & B
    if (Math.max(A, B) > 2 * Math.min(A, B))
    {

        // Not possible to
        // empty the piles
        System.out.println("No");
        return;
    }

    // If sum of both the coins is
    // divisible by 3, then print Yes
    if ((A + B) % 3 == 0)
        System.out.println("Yes");

    // Otherwise, print "No"
    else
        System.out.println("No");
}

// Driver Code
public static void main (String[] args)
{
    int A = 1, B = 2;

    canBeEmptied(A, B);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if two given piles
# can be emptied by repeatedly removing
# 2 coins from a pile and 1 coin from the other
def canBeEmptied(A, B):

    # If maximum of A & B exceeds
    # the twice of minimum of A & B
    if (max(A, B) > 2 * min(A, B)):

        # Not possible to
        # empty the piles
        print("No")
        return

    # If sum of both the coins is
    # divisible by 3, then print Yes
    if ((A + B) % 3 == 0):
        print("Yes")

    # Otherwise, print "No"
    else:
        print("No")

# Driver Code
if __name__ == '__main__':
    A = 1
    B = 2
    canBeEmptied(A, B)

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if two given piles
// can be emptied by repeatedly removing
// 2 coins from a pile and 1 coin from the other
static void canBeEmptied(int A, int B)
{

    // If maximum of A & B exceeds
    // the twice of minimum of A & B
    if (Math.Max(A, B) > 2 * Math.Min(A, B))
    {

        // Not possible to
        // empty the piles
        Console.WriteLine("No");
        return;
    }

    // If sum of both the coins is
    // divisible by 3, then print Yes
    if ((A + B) % 3 == 0)
        Console.WriteLine("Yes");

    // Otherwise, print "No"
    else
        Console.WriteLine("No");
}

// Driver Code
public static void Main ()
{
    int A = 1, B = 2;

    canBeEmptied(A, B);
}
}

// This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if two given piles
// can be emptied by repeatedly removing
// 2 coins from a pile and 1 coin from the other
function canBeEmptied(A, B)
{

    // If maximum of A & B exceeds
    // the twice of minimum of A & B
    if (Math.max(A, B) > 2 * Math.min(A, B))
    {

        // Not possible to
        // empty the piles
        document.write("No");
        return;
    }

    // If sum of both the coins is
    // divisible by 3, then print Yes
    if ((A + B) % 3 == 0)
        document.write("Yes");

    // Otherwise, print "No"
    else
        document.write("No");
}

// Driver Code
let A = 1, B = 2;

canBeEmptied(A, B);

// This code is contributed by subhammahato348

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)