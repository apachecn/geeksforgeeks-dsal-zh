# 求 N 大小的环中任意整数点到 A 和 B 的距离的最小和

> 原文:[https://www . geeksforgeeks . org/find-最小距离之和-a 和-b-从任意整数点到 n 大小的环/](https://www.geeksforgeeks.org/find-the-minimum-sum-of-distance-to-a-and-b-from-any-integer-point-in-a-ring-of-size-n/)

给定一个圆环，圆环上有从 **1** 到 **N** 的标记。给定两个数字 **A** 和 **B** ，你可以站在任何地方(比如说 **X** )计算距离的总和(比如说 **Z** ，也就是从 **X 到 A** +从 **X 到 B** 的距离)。任务是选择 **X** 使得 **Z** 最小化。打印由此获得的 Z 值。**注意**的 **X** 既不能等于 **A** 也不能等于 **B** 。
**示例:**

> **输入:** N = 6，A = 2，B = 4
> **输出:** 2
> 选择 X 为 3，这样 X 到 A 的距离为 1，X 到 B 的距离为 1。
> **输入:** N = 4，A = 1，B = 2
> **输出:** 3
> 选择 X 为 3 或 4，二者给出的距离为 3。

**进场:**圆上位置 **A** 和 **B** 之间有两条路径，一条顺时针方向，一条逆时针方向。 **Z** 的一个最佳值是选择 **X** 作为 **A** 和 **B** 之间的最小路径上的任意一点，那么 **Z** 将等于两个位置之间的最小距离，但两个位置相邻的情况除外，即最小距离为 **1** 。在这种情况下，不能选择 **X** 作为它们之间的点，因为它必须不同于 **A** 和 **B** ，结果将是 **3** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum value of Z
int findMinimumZ(int n, int a, int b)
{

    // Change elements such that a < b
    if (a > b)
        swap(a, b);

    // Distance from (a to b)
    int distClock = b - a;

    // Distance from (1 to a) + (b to n)
    int distAntiClock = (a - 1) + (n - b + 1);

    // Minimum distance between a and b
    int minDist = min(distClock, distAntiClock);

    // If both the positions are
    // adjacent on the circle
    if (minDist == 1)
        return 3;

    // Return the minimum Z possible
    return minDist;
}

// Driver code
int main()
{
    int n = 4, a = 1, b = 2;
    cout << findMinimumZ(n, a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the minimum value of Z
    static int findMinimumZ(int n, int a, int b)
    {

        // Change elements such that a < b
        if (a > b)
        {
            swap(a, b);
        }

        // Distance from (a to b)
        int distClock = b - a;

        // Distance from (1 to a) + (b to n)
        int distAntiClock = (a - 1) + (n - b + 1);

        // Minimum distance between a and b
        int minDist = Math.min(distClock, distAntiClock);

        // If both the positions are
        // adjacent on the circle
        if (minDist == 1)
        {
            return 3;
        }

        // Return the minimum Z possible
        return minDist;
    }

    private static void swap(int x, int y)
    {
        int temp = x;
        x = y;
        y = temp;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4, a = 1, b = 2;
        System.out.println(findMinimumZ(n, a, b));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
# Function to return the minimum value of Z
def findMinimumZ(n, a, b):

    # Change elements such that a < b
    if (a > b):
        temp = a
        a = b
        b = temp

    # Distance from (a to b)
    distClock = b - a

    # Distance from (1 to a) + (b to n)
    distAntiClock = (a - 1) + (n - b + 1)

    # Minimum distance between a and b
    minDist = min(distClock, distAntiClock)

    # If both the positions are
    # adjacent on the circle
    if (minDist == 1):
        return 3

    # Return the minimum Z possible
    return minDist

# Driver code
if __name__ == '__main__':
    n = 4
    a = 1
    b = 2
    print(findMinimumZ(n, a, b))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimum value of Z
    static int findMinimumZ(int n, int a, int b)
    {

        // Change elements such that a < b
        if (a > b)
        {
            swap(a, b);
        }

        // Distance from (a to b)
        int distClock = b - a;

        // Distance from (1 to a) + (b to n)
        int distAntiClock = (a - 1) + (n - b + 1);

        // Minimum distance between a and b
        int minDist = Math.Min(distClock, distAntiClock);

        // If both the positions are
        // adjacent on the circle
        if (minDist == 1)
        {
            return 3;
        }

        // Return the minimum Z possible
        return minDist;
    }

    private static void swap(int x, int y)
    {
        int temp = x;
        x = y;
        y = temp;
    }

    // Driver code
    static public void Main ()
    {
        int n = 4, a = 1, b = 2;
        Console.WriteLine(findMinimumZ(n, a, b));
    }

}

/* This code contributed by ajit*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP implementation of the approach
// Function to return the minimum value of Z
function findMinimumZ($n, $a, $b)
{

    // Change elements such that a < b
    if ($a > $b)

        $a = $a ^ $b;
        $b = $a ^ $b;
        $a = $a ^ $b;

    // Distance from (a to b)
    $distClock = $b - $a;

    // Distance from (1 to a) + (b to n)
    $distAntiClock = ($a - 1) + ($n - $b + 1);

    // Minimum distance between a and b
    $minDist = min($distClock, $distAntiClock);

    // If both the positions are
    // adjacent on the circle
    if ($minDist == 1)
        return 3;

    // Return the minimum Z possible
    return $minDist;
}

// Driver code

$n = 4;
$a = 1;
$b = 2;
echo findMinimumZ($n, $a, $b);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

    // Function to return the minimum value of Z
    function findMinimumZ(n,a,b)
    {

        // Change elements such that a < b
        if (a > b)
        {
            swap(a, b);
        }

        // Distance from (a to b)
        let distClock = b - a;

        // Distance from (1 to a) + (b to n)
        let distAntiClock = (a - 1) + (n - b + 1);

        // Minimum distance between a and b
        let minDist = Math.min(distClock, distAntiClock);

        // If both the positions are
        // adjacent on the circle
        if (minDist == 1)
        {
            return 3;
        }

        // Return the minimum Z possible
        return minDist;
    }

    function swap(x,y)
    {
        let temp = x;
        x = y;
        y = temp;
    }

    // Driver code

        let n = 4, a = 1, b = 2;
        document.write(findMinimumZ(n, a, b));

// This code is contributed by sravan kumar Gottumukkala

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(1)

**辅助空间:** O(1)