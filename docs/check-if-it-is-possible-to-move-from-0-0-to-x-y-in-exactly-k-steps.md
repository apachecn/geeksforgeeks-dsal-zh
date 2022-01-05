# 检查是否可以从(0，0)移动到(X，Y)正好 K 步

> 原文:[https://www . geeksforgeeks . org/check-如果有可能从 0-0 移动到 x-y-in-k-steps/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-move-from-0-0-to-x-y-in-exactly-k-steps/)

给定二维平面上的一个点 **(X，Y)** 和一个整数 **K** ，任务是检查是否有可能从 **(0，0)** 移动到精确 **K** 移动中的给定点 **(X，Y)** 。在单次移动中，从 **(X，Y)** 可到达的位置是 **(X，Y + 1)** 、 **(X，Y–1)**、 **(X + 1，Y)** 和**(X–1，Y)** 。
**例:**

> **输入:** X = 0，Y = 0，K = 2
> **输出:**是
> 移动 1: (0，0) - > (0，1)
> 移动 2: (0，1) - > (0，0)
> **输入:** X = 5，Y = 8，K = 20
> **输出:**否

**途径:**很明显，从 **(0，0)** 到达 **(X，Y)** 的最短路径将是**最小移动= (|X| + |Y|)** 。所以，如果 **K <最小移动**那么就不可能达到 **(X，Y)** 但是如果 **K ≥最小移动**那么在达到**最小移动**中的 **(X，Y)** 步数之后，剩余的**(K–最小移动)**步数必须是偶数，以便在剩余的步数中保持在该点。
所以只有当 **K ≥ (|X| + |Y|)和(K –( | X |+| Y |))% 2 = 0**时，才有可能从 **(0，0)** 到达 **(X，Y)** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if it is
// possible to move from (0, 0) to
// (x, y) in exactly k moves
bool isPossible(int x, int y, int k)
{
    // Minimum moves required
    int minMoves = abs(x) + abs(y);

    // If possible
    if (k >= minMoves && (k - minMoves) % 2 == 0)
        return true;

    return false;
}

// Driver code
int main()
{
    int x = 5, y = 8, k = 20;

    if (isPossible(x, y, k))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function that returns true if it is
    // possible to move from (0, 0) to
    // (x, y) in exactly k moves
    static boolean isPossible(int x, int y, int k)
    {
        // Minimum moves required
        int minMoves = Math.abs(x) + Math.abs(y);

        // If possible
        if (k >= minMoves && (k - minMoves) % 2 == 0)
            return true;

        return false;
    }

    // Driver code
    public static void main (String[] args)
    {
        int x = 5, y = 8, k = 20;

        if (isPossible(x, y, k))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if it is
# possible to move from (0, 0) to
# (x, y) in exactly k moves
def isPossible(x, y, k):

    # Minimum moves required
    minMoves = abs(x) + abs(y)

    # If possible
    if (k >= minMoves and (k - minMoves) % 2 == 0):
        return True

    return False

# Driver code
x = 5
y = 8
k = 20

if (isPossible(x, y, k)):
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

    // Function that returns true if it is
    // possible to move from (0, 0) to
    // (x, y) in exactly k moves
    static bool isPossible(int x, int y, int k)
    {
        // Minimum moves required
        int minMoves = Math.Abs(x) + Math.Abs(y);

        // If possible
        if (k >= minMoves && (k - minMoves) % 2 == 0)
            return true;

        return false;
    }

    // Driver code
    public static void Main ()
    {
        int x = 5, y = 8, k = 20;

        if (isPossible(x, y, k))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by Nidhi
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function that returns true if it is
// possible to move from (0, 0) to
// (x, y) in exactly k moves
function isPossible(x , y , k)
{
    // Minimum moves required
    var minMoves = Math.abs(x) + Math.abs(y);

    // If possible
    if (k >= minMoves && (k - minMoves) % 2 == 0)
        return true;

    return false;
}

// Driver code

var x = 5, y = 8, k = 20;

if (isPossible(x, y, k))
    document.write("Yes");
else
    document.write("No");

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
No
```