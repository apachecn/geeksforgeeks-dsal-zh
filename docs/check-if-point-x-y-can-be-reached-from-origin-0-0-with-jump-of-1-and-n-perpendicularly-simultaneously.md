# 检查点(X，Y)是否可以从原点(0，0)同时垂直跳跃 1 和 N 到达

> 原文:[https://www . geeksforgeeks . org/check-if-point-x-y-can-from-origin-0-0-with-jump-of-1-n-垂直-同时/](https://www.geeksforgeeks.org/check-if-point-x-y-can-be-reached-from-origin-0-0-with-jump-of-1-and-n-perpendicularly-simultaneously/)

给定一个正整数 **N** 和坐标 **(X，Y)** ，任务是检查在垂直方向上 **1** 和 **N** 同时跳跃时是否有可能从 **(0，0)** 到达 **(X，Y)** 。如果有可能到达 **(X，Y)** ，则打印**是**。否则，打印**否**。

**示例:**

> **输入:** N = 2，X = 5，Y = 4
> **输出:**是
> **解释:**
> 以下是从当前坐标(0，0)到点(X，Y)的可能移动:
> 
> 1.  从当前坐标执行(2，1)的跳转会将其修改为(2，1)。
> 2.  从当前坐标执行(2，1)的跳转会将其修改为(4，2)。
> 3.  从当前坐标执行(1，2)的跳转会将其修改为(5，4)。
> 
> **输入:** N = 3，X = 5，Y = 4
> T3】输出:否

**方法:**给定的问题可以基于以下观察来解决:从任意坐标跳跃有 4 种可能的方式: **(1，N)、(1，-N)、(-1，N)** 、 **(-1，-N)** 。此外，这个问题可以分为 3 种不同的情况:

*   **<u>情况 1–其中 N 是偶数</u> :** 在这种情况下，任何坐标(X，Y)都是可达的。让我们一次考虑 X 和 Y。对于一个坐标 X，可以遵循 **(1，N)、(1，-N)、(1，N)、(1，-N)、…** 跳跃的顺序。生成的坐标将是所需坐标 **(X，0)** ，或 **(X，N)** 。由于 **N** 为偶数，所以也可以按照跳跃的顺序 **(N，-1)、(-N，-1)、(N，-1)、……**到达 **(X，0)** 。同样可以到达 **(0，Y)** ，结合跳转的顺序到达 **(X，0)** 、 **(0，Y)、(X，Y)** 。
*   **<u>情况 2–其中 N 是奇数，X 和 Y 都是偶数或奇数</u> :** 这些情况可以通过遵循类似于**情况 1** 的操作序列来处理。
*   **<u>情况 3–其中 N 是奇数，X 和 Y 具有不同的奇偶校验</u> :** 在这种情况下，没有可能的跳跃序列到达 **(X，Y)** ，因为根据情况 2， **(X + 1，Y)** 和 **(X，Y + 1)** 必须是可达的，因为它们都将具有相同的奇偶校验，并且没有可能的操作序列覆盖 **(1，0)** 或**的距离**

因此，从 **(0，0)** 无法到达 **(X，Y)** 的唯一情况是 **N** 为奇数而 **X** 和 **Y** 具有不同的奇偶性，即 **X** 为偶数而 **Y** 为奇数，反之亦然。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if (X, Y) is reachable
// from (0, 0) using the jumps of given type
string checkReachability(int N, int X, int Y)
{
    // Case where source & destination
    // are the same
    if (X == 0 && Y == 0) {
        return "YES";
    }

    // Check for even N (X, Y) is
    // reachable or not
    if (N % 2 == 0) {
        return "YES";
    }

    // If N is odd and parity of X and
    // Y is different return, no valid
    // sequence of jumps exist
    else {
        if (X % 2 != Y % 2) {
            return "NO";
        }
        else {
            return "YES";
        }
    }
}

// Driver Code
int main()
{
    int N = 2;
    int X = 5, Y = 4;
    cout << checkReachability(N, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;

class GFG
{

  // Function to check if (X, Y) is reachable
// from (0, 0) using the jumps of given type
static String checkReachability(int N, int X, int Y)
{

    // Case where source & destination
    // are the same
    if (X == 0 && Y == 0) {
        return "YES";
    }

    // Check for even N (X, Y) is
    // reachable or not
    if (N % 2 == 0) {
        return "YES";
    }

    // If N is odd and parity of X and
    // Y is different return, no valid
    // sequence of jumps exist
    else {
        if (X % 2 != Y % 2) {
            return "NO";
        }
        else {
            return "YES";
        }
    }
}

// Driver Code
    public static void main (String[] args) {
      int N = 2;
    int X = 5, Y = 4;

        System.out.println(checkReachability(N, X, Y));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to check if (X, Y) is reachable
# from (0, 0) using the jumps of given type
def checkReachability(N, X, Y):

    # Case where source & destination
    # are the same
    if (X == 0 and Y == 0):
        return "YES"

    # Check for even N (X, Y) is
    # reachable or not
    if (N % 2 == 0):
        return "YES"

    # If N is odd and parity of X and
    # Y is different return, no valid
    # sequence of jumps exist
    else:
        if (X % 2 != Y % 2):
            return "NO"
        else:
            return "YES"

# Driver Code
if __name__ == '__main__':
    N = 2
    X = 5
    Y = 4
    print(checkReachability(N, X, Y))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# code for the above approach
using System;

class GFG
{

  // Function to check if (X, Y) is reachable
// from (0, 0) using the jumps of given type
static string checkReachability(int N, int X, int Y)
{

    // Case where source & destination
    // are the same
    if (X == 0 && Y == 0) {
        return "YES";
    }

    // Check for even N (X, Y) is
    // reachable or not
    if (N % 2 == 0) {
        return "YES";
    }

    // If N is odd and parity of X and
    // Y is different return, no valid
    // sequence of jumps exist
    else {
        if (X % 2 != Y % 2) {
            return "NO";
        }
        else {
            return "YES";
        }
    }
}

// Driver Code
    public static void Main (string[] args) {
      int N = 2;
      int X = 5, Y = 4;

    Console.WriteLine(checkReachability(N, X, Y));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
    // Function to check if (X, Y) is reachable
// from (0, 0) using the jumps of given type
string checkReachability(int N, int X, int Y)
{

    // Case where source & destination
    // are the same
    if (X == 0 && Y == 0) {
        return "YES";
    }

    // Check for even N (X, Y) is
    // reachable or not
    if (N % 2 == 0) {
        return "YES";
    }

    // If N is odd and parity of X and
    // Y is different return, no valid
    // sequence of jumps exist
    else {
        if (X % 2 != Y % 2) {
            return "NO";
        }
        else {
            return "YES";
        }
    }
}
    // Driver Code

    let N = 2, X = 5, Y = 4;
    document.write(checkReachability(N, X, Y));

// This code is contributed by dwivediyash.
</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)