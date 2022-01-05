# 检查是否有可能从原点到达(x，y ),使得每次移动增量 x 或 y 坐标与 3^i

一致

> 原文:[https://www . geeksforgeeks . org/check-如果有可能从原点到达-x-y-这样-在每次移动中-增量-x-或-y-坐标与-3i/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-reach-x-y-from-origin-such-that-in-each-ith-move-increment-x-or-y-coordinate-with-3i/)

给定两个正整数 **X** 和 **Y** ，任务是找出一个点 **(X，Y)** 是否可以从点 **(0，0)** 到达，从而在每次移动中 X 坐标或 Y 坐标可以增加 **3 <sup>i</sup>** 。如果可能，则打印**是**。否则，打印**否**。

**示例:**

> **输入:** X = 1，Y = 3
> **输出:**是
> **说明:**
> 以下是从(0，0)到(1，3)的步骤:
> 
> **第 0 步:**将 X 坐标增加 3 <sup>0</sup> (= 1)将坐标修改为(1，0)。
> **步骤 1:** 将 Y 坐标增加 3 <sup>1</sup> (= 2)将坐标修改为(1，3)。
> 
> 因此，坐标(1，3)可以从(0，0)到达。因此，打印“是”。
> 
> **输入:** X = 10，Y = 30
> T3】输出:是

**天真方法:**解决给定问题的最简单方法是通过在每一步中递减 **3 <sup>i</sup>** 从 **(X，Y)** 生成所有可能的移动，并检查这些移动组合是否达到 **(0，0)** 。如果可能，则打印**是**。否则，打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find whether (0, 0) can
// be reached from (X, Y) by decrementing
// 3^i at each ith step
bool canReach(int X, int Y, int steps)
{
    // Termination Condition
    if (X == 0 && Y == 0) {
        return true;
    }

    if (X < 0 || Y < 0) {
        return false;
    }

    // Otherwise, recursively call by
    // decrementing 3^i at each step
    return (
        canReach(X - (int)pow(3, steps),
                 Y, steps + 1)
        | canReach(X, Y - (int)pow(3, steps),
                   steps + 1));
}

// Driver Code
int main()
{
    int X = 10, Y = 30;
    if (canReach(X, Y, 0)) {
        cout << "YES" << endl;
    }
    else
        cout << "NO" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to find whether (0, 0) can
// be reached from (X, Y) by decrementing
// 3^i at each ith step
static boolean canReach(int X, int Y, int steps)
{

    // Termination Condition
    if (X == 0 && Y == 0) {
        return true;
    }

    if (X < 0 || Y < 0) {
        return false;
    }

    // Otherwise, recursively call by
    // decrementing 3^i at each step
    return (
        canReach(X - (int)Math.pow(3, steps),
                 Y, steps + 1)
        | canReach(X, Y - (int)Math.pow(3, steps),
                   steps + 1));
}

// Driver Code
public static void main(String[] args)
{
    int X = 10, Y = 30;
    if (canReach(X, Y, 0)) {
        System.out.print("YES" +"\n");
    }
    else
        System.out.print("NO" +"\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find whether (0, 0) can
# be reached from (X, Y) by decrementing
# 3^i at each ith step
def canReach(X, Y, steps):
    # Termination Condition
    if (X == 0 and Y == 0):
        return True

    if (X < 0 or Y < 0):
        return False

    # Otherwise, recursively call by
    # decrementing 3^i at each step
    return (canReach(X - int(pow(3, steps)),Y, steps + 1)| canReach(X, Y - int(pow(3, steps)),steps + 1))

# Driver Code
if __name__ == '__main__':
    X = 10
    Y = 30
    if(canReach(X, Y, 0)):
        print("YES")
    else:
        print("NO")

        # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

// Function to find whether (0, 0) can
// be reached from (X, Y) by decrementing
// 3^i at each ith step
static Boolean canReach(int X, int Y, int steps)
{

    // Termination Condition
    if (X == 0 && Y == 0) {
        return true;
    }

    if (X < 0 || Y < 0) {
        return false;
    }

    // Otherwise, recursively call by
    // decrementing 3^i at each step
    return (
        canReach(X - (int)Math.Pow(3, steps),
                 Y, steps + 1)
        | canReach(X, Y - (int)Math.Pow(3, steps),
                   steps + 1));
}

// Driver Code
public static void Main(String[] args)
{
    int X = 10, Y = 30;
    if (canReach(X, Y, 0)) {
        Console.Write("YES" +"\n");
    }
    else
        Console.Write("NO" +"\n");
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find whether (0, 0) can
// be reached from (X, Y) by decrementing
// 3^i at each ith step
function canReach(X, Y, steps) {
  // Termination Condition
  if (X == 0 && Y == 0) {
    return true;
  }

  if (X < 0 || Y < 0) {
    return false;
  }

  // Otherwise, recursively call by
  // decrementing 3^i at each step
  return (
    canReach(X - Math.pow(3, steps), Y, steps + 1) |
    canReach(X, Y - Math.pow(3, steps), steps + 1)
  );
}

// Driver Code

let X = 10,
  Y = 30;
if (canReach(X, Y, 0)) {
  document.write("YES");
} else document.write("NO");

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(2 <sup>K</sup> ，其中 K 为执行的最大步数。*
***辅助空间:** O(1)*

**高效方法:**通过将 X 和 Y 转换为基数 3，可以基于以下观察优化上述方法:

*   如果基数 3 中 X 和 Y 的值都有 **1** ，那么(X，Y)就不能达到，因为这一步不能在两个方向上进行。
*   如果基数 3 中 X 和 Y 的任何值中有 **2** ，那么(X，Y)就不能达到，因为这不能用 3 的[完美幂来表示。](https://www.geeksforgeeks.org/find-whether-given-integer-power-3-not/)
*   如果基数 3 中 X 和 Y 的任意值中有 **0** ，则不能达到(X，Y)，因为除了最后一步之外，该步不能执行。
*   否则，在所有剩余的情况下(X，Y)都可以从(0，0)到达。

根据以上观察，相应地打印结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find whether (0, 0) can
// be reached from (X, Y) by decrementing
// 3^i at each ith step
bool canReach(int X, int Y)
{
    // Stores the number of steps
    // performed to reach (X, Y)
    int steps = 0;
    while (X || Y) {

        // Value of X in base 3
        int pos1 = X % 3;

        // Value of Y in base 3
        int pos2 = Y % 3;

        // Check if any has value 2
        if (pos1 == 2 || pos2 == 2) {
            return false;
        }

        // If both have value 1
        if (pos1 == 1 && pos2 == 1) {
            return false;
        }

        // If both have value 0
        if (pos1 == 0 && pos2 == 0) {
            return false;
        }

        X /= 3;
        Y /= 3;
        steps++;
    }

    // Otherwise, return true
    return true;
}

// Driver Code
int main()
{
    int X = 10, Y = 30;
    if (canReach(X, Y)) {
        cout << "YES";
    }
    else {
        cout << "NO";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to find whether (0, 0) can
    // be reached from (X, Y) by decrementing
    // 3^i at each ith step
    static boolean canReach(int X, int Y)
    {

        // Stores the number of steps
        // performed to reach (X, Y)
        int steps = 0;
        while (X != 0 || Y != 0) {

            // Value of X in base 3
            int pos1 = X % 3;

            // Value of Y in base 3
            int pos2 = Y % 3;

            // Check if any has value 2
            if (pos1 == 2 || pos2 == 2) {
                return false;
            }

            // If both have value 1
            if (pos1 == 1 && pos2 == 1) {
                return false;
            }

            // If both have value 0
            if (pos1 == 0 && pos2 == 0) {
                return false;
            }

            X /= 3;
            Y /= 3;
            steps++;
        }

        // Otherwise, return true
        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int X = 10, Y = 30;
        if (canReach(X, Y)) {
            System.out.println("YES");
        }
        else {
            System.out.println("NO");
        }
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find whether (0, 0) can
# be reached from (X, Y) by decrementing
# 3^i at each ith step
def canReach(X, Y):

    # Stores the number of steps
    # performed to reach (X, Y)
    steps = 0
    while (X != 0 or Y != 0):

        # Value of X in base 3
        pos1 = X % 3

        # Value of Y in base 3
        pos2 = Y % 3

        # Check if any has value 2
        if (pos1 == 2 or pos2 == 2):
            return False

        # If both have value 1
        if (pos1 == 1 and pos2 == 1):
            return False

        # If both have value 0
        if (pos1 == 0 and pos2 == 0):
            return False

        X /= 3
        Y /= 3
        steps += 1

    # Otherwise, return true
    return True

# Driver Code
X = 10
Y = 30
if (canReach(X, Y)):
    print("YES")
else:
    print("NO")

# This code is contributed by _saurabh_jaiswal
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

    // Function to find whether (0, 0) can
    // be reached from (X, Y) by decrementing
    // 3^i at each ith step
    static bool canReach(int X, int Y)
    {

        // Stores the number of steps
        // performed to reach (X, Y)
        int steps = 0;
        while (X != 0 || Y != 0) {

            // Value of X in base 3
            int pos1 = X % 3;

            // Value of Y in base 3
            int pos2 = Y % 3;

            // Check if any has value 2
            if (pos1 == 2 || pos2 == 2) {
                return false;
            }

            // If both have value 1
            if (pos1 == 1 && pos2 == 1) {
                return false;
            }

            // If both have value 0
            if (pos1 == 0 && pos2 == 0) {
                return false;
            }

            X /= 3;
            Y /= 3;
            steps++;
        }

        // Otherwise, return true
        return true;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int X = 10, Y = 30;
        if (canReach(X, Y)) {
            Console.WriteLine("YES");
        }
        else {
            Console.WriteLine("NO");
        }
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to find whether (0, 0) can
    // be reached from (X, Y) by decrementing
    // 3^i at each ith step
    function canReach(X , Y)
    {

        // Stores the number of steps
        // performed to reach (X, Y)
        var steps = 0;
        while (X != 0 || Y != 0) {

            // Value of X in base 3
            var pos1 = X % 3;

            // Value of Y in base 3
            var pos2 = Y % 3;

            // Check if any has value 2
            if (pos1 == 2 || pos2 == 2) {
                return false;
            }

            // If both have value 1
            if (pos1 == 1 && pos2 == 1) {
                return false;
            }

            // If both have value 0
            if (pos1 == 0 && pos2 == 0) {
                return false;
            }

            X /= 3;
            Y /= 3;
            steps++;
        }

        // Otherwise, return true
        return true;
    }

    // Driver Code
      var X = 10, Y = 30;
        if (canReach(X, Y)) {
            document.write("YES");
        }
        else {
            document.write("NO");
        }

// This code contributed by shikhasingrajput
</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(log <sub>3</sub> (max(X，Y))
T5】辅助空间: O(1)