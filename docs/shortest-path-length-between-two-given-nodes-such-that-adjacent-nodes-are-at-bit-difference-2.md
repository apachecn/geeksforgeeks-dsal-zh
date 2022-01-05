# 两个给定节点之间的最短路径长度，使得相邻节点的位差为 2

> 原文:[https://www . geeksforgeeks . org/两个给定节点之间的最短路径长度-这样相邻节点的位差为-2/](https://www.geeksforgeeks.org/shortest-path-length-between-two-given-nodes-such-that-adjacent-nodes-are-at-bit-difference-2/)

给定一个由 N 个节点和两个整数组成的[未加权无向图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)**a**和 **b** 。任意两个节点之间的边只有当它们之间的[位差](https://www.geeksforgeeks.org/sum-of-bit-differences-among-all-pairs/)为 **2** 时才存在，任务是找出节点 **a** 和 **b** 之间[最短路径](https://www.geeksforgeeks.org/shortest-path-unweighted-graph/)的长度。如果节点 **a** 和 **b** 之间不存在路径，则打印 **-1** 。

**示例:**

> **输入:** N = 15，a = 15，b = 3
> **输出:** 1
> **说明:** a = 15 = (1111) <sub>2</sub> 和 b = 3 = (0011) <sub>2</sub> 。15 和 3 之间的位差是 2。因此，在 15 和 3 之间有一条直接的边。因此，最短路径的长度为 1。
> 
> **输入:** N = 15，a = 15，b = 2
> **输出:** -1
> **说明:** a = 15 = (1111) <sub>2</sub> 和 b= 2 = (0010) <sub>2</sub> 。15 和 2 之间的位差是 3。由于位差只能是 2，从 2 不可能达到 15
> 。

**朴素方法:**解决这个问题最简单的方法是首先利用给定的条件构造图，然后通过考虑 **a** 作为图的源节点，利用 **a** 和 **b** 找到节点之间的最短路径。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效方法:**通过观察任意两个节点之间的[位差](https://www.geeksforgeeks.org/sum-of-bit-differences-among-all-pairs/)之和必须是因子 **2** 并且它们的最短距离必须是该和的一半，可以解决该问题。按照下面给出的步骤理解该方法:

1.  [对 **a** 和 **b** 的](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)[逐位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)中的设置位的计数给出了节点 **a** 和 **b** 之间的[位差](https://www.geeksforgeeks.org/sum-of-bit-differences-among-all-pairs/)的计数。
2.  如果 **a** 和 **b** 的按位异或中设置位的[计数是 **2** 的倍数，则 **a** 和 **b** 相连。](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)
3.  如果设置位的计数是 **2** ，这意味着它们是彼此分开的 **1** 单元。如果 **a** 和 **b** 的[异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)中的[设定位计数为 **4** ，则表示节点 **a** 和 **b** 相隔 **2** 个单位。因此，如果位差为 **x** ，则最短路径为 **x/2** 。](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)
4.  如果位差为奇数，则它们没有连接，因此，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count set bits
// in a number
int countbitdiff(int xo)
{

    // Stores count of
    // set bits in xo
    int count = 0;

    // Iterate over each
    // bits of xo
    while (xo) {

        // If current bit of xo
        // is 1
        if (xo % 2 == 1) {

            //  Update count
            count++;
        }

        // Update xo
        xo = xo / 2;
    }
    return count;
}

// Function to find length of shortest
// path between the nodes a and b
void shortestPath(int n, int a, int b)
{

    // Stores XOR of a and b
    int xorVal = a ^ b;

    // Stores the count of
    // set bits in xorVal
    int cnt = countbitdiff(xorVal);

    // If cnt is an even number
    if (cnt % 2 == 0)
        cout << cnt / 2 << endl;
    else
        cout << "-1" << endl;
}

// Driver Code
int main()
{
    // Given N
    int n = 15;

    // Given a and b
    int a = 15, b = 3;

    // Function call
    shortestPath(n, a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count set bits
// in a number
static int countbitdiff(int xo)
{

    // Stores count of
    // set bits in xo
    int count = 0;

    // Iterate over each
    // bits of xo
    while (xo != 0)
    {

        // If current bit of xo
        // is 1
        if (xo % 2 == 1)
        {

            // Update count
            count++;
        }

        // Update xo
        xo = xo / 2;
    }
    return count;
}

// Function to find length of shortest
// path between the nodes a and b
static void shortestPath(int n, int a, int b)
{

    // Stores XOR of a and b
    int xorVal = a ^ b;

    // Stores the count of
    // set bits in xorVal
    int cnt = countbitdiff(xorVal);

    // If cnt is an even number
    if (cnt % 2 == 0)
        System.out.print(cnt / 2);
    else
        System.out.print("-1");
}

// Driver Code
public static void main(String[] args)
{

    // Given N
    int n = 15;

    // Given a and b
    int a = 15, b = 3;

    // Function call
    shortestPath(n, a, b);
}   
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count set bits
# in a number
def countbitdiff(xo):

    # Stores count of
    # set bits in xo
    count = 0

    # Iterate over each
    # bits of xo
    while (xo):

        # If current bit of xo
        # is 1
        if (xo % 2 == 1):
            #  Update count
            count+=1

        # Update xo
        xo = xo // 2

    return count

# Function to find length of shortest
# path between the nodes a and b
def shortestPath(n, a, b):

    # Stores XOR of a and b
    xorVal = a ^ b

    # Stores the count of
    # set bits in xorVal
    cnt = countbitdiff(xorVal)

    # If cnt is an even number
    if (cnt % 2 == 0):
        print(cnt // 2)
    else:
        print("-1")

# Driver Code
if __name__ == '__main__':
    # Given N
    n = 15

    # Given a and b
    a,b = 15,3

    # Function call
    shortestPath(n, a, b)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG {

// Function to count set bits
// in a number
static int countbitdiff(int xo)
{

    // Stores count of
    // set bits in xo
    int count = 0;

    // Iterate over each
    // bits of xo
    while (xo != 0)
    {

        // If current bit of xo
        // is 1
        if (xo % 2 == 1)
        {

            // Update count
            count++;
        }

        // Update xo
        xo = xo / 2;
    }
    return count;
}

// Function to find length of shortest
// path between the nodes a and b
static void shortestPath(int n, int a, int b)
{

    // Stores XOR of a and b
    int xorVal = a ^ b;

    // Stores the count of
    // set bits in xorVal
    int cnt = countbitdiff(xorVal);

    // If cnt is an even number
    if (cnt % 2 == 0)
        Console.Write(cnt / 2);
    else
        Console.Write("-1");
}

  // Driver code
  public static void Main (String[] args)
  {

    // Given N
    int n = 15;

    // Given a and b
    int a = 15, b = 3;

    // Function call
    shortestPath(n, a, b);
  }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count set bits
// in a number
function countbitdiff(xo) {

    // Stores count of
    // set bits in xo
    let count = 0;

    // Iterate over each
    // bits of xo
    while (xo) {

        // If current bit of xo
        // is 1
        if (xo % 2 == 1) {

            //  Update count
            count++;
        }

        // Update xo
        xo = Math.floor(xo / 2);
    }
    return count;
}

// Function to find length of shortest
// path between the nodes a and b
function shortestPath(n, a, b) {

    // Stores XOR of a and b
    let xorVal = a ^ b;

    // Stores the count of
    // set bits in xorVal
    let cnt = countbitdiff(xorVal);

    // If cnt is an even number
    if (cnt % 2 == 0)
        document.write(cnt / 2 + "<br>");
    else
        document.write("-1" + "<br>");
}

// Driver Code

// Given N
let n = 15;

// Given a and b
let a = 15, b = 3;

// Function call
shortestPath(n, a, b);

// This code is contributed by gfgking.
</script>
```

**Output:**

```
1
```

***时间复杂度:**O(log<sub>2</sub>(N)*
***辅助空间:** O(1)*