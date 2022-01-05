# 圆和格点

> 原文:[https://www.geeksforgeeks.org/circle-lattice-points/](https://www.geeksforgeeks.org/circle-lattice-points/)

给定一个以原点或(0，0)为中心的二维半径圆 **r** 。任务是求圆周上的总格点。格点是二维空间中坐标为整数的点。
示例:

```
Input  : r = 5.
Output : 12
Below are lattice points on a circle with
radius 5 and origin as (0, 0).
(0,5), (0,-5), (5,0), (-5,0),
(3,4), (-3,4), (-3,-4), (3,-4),
(4,3), (-4,3), (-4,-3), (4,-3).
are 12 lattice point.
```

求格点，基本上需要求满足方程 x<sup>2</sup>+y<sup>2</sup>= r<sup>2</sup>的(x，y)的值。
对于满足上述方程的任何(x，y)值，我们实际上总共有 4 个不同的组合满足该方程。例如，如果 r = 5 和(3，4)是满足等式的一对，实际上有 4 种组合(3，4)，(-3，4)，(-3，-4)，(3，-4)。但是有一个例外，在(0，r)或(r，0)的情况下，实际上有 2 个点，因为没有负 0。

```
// Initialize result as 4 for (r, 0), (-r. 0),
// (0, r) and (0, -r)
result = 4

Loop for x = 1 to r-1 and do following for every x.
    If r*r - x*x is a perfect square, then add 4 
    tor result.  
```

以下是上述想法的实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find countLattice points on a circle
#include<bits/stdc++.h>
using namespace std;

// Function to count Lattice points on a circle
int countLattice(int r)
{
    if (r <= 0)
        return 0;

    // Initialize result as 4 for (r, 0), (-r. 0),
    // (0, r) and (0, -r)
    int result = 4;

    // Check every value that can be potential x
    for (int x=1; x<r; x++)
    {
        // Find a potential y
        int ySquare = r*r - x*x;
        int y = sqrt(ySquare);

        // checking whether square root is an integer
        // or not. Count increments by 4 for four
        // different quadrant values
        if (y*y == ySquare)
            result += 4;
    }

    return result;
}

// Driver program
int main()
{
    int r = 5;
    cout << countLattice(r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// countLattice points on a circle

class GFG
{

// Function to count
// Lattice points on a circle
static int countLattice(int r)
{
    if (r <= 0)
        return 0;

    // Initialize result as 4 for (r, 0), (-r. 0),
    // (0, r) and (0, -r)
    int result = 4;

    // Check every value that can be potential x
    for (int x=1; x<r; x++)
    {
        // Find a potential y
        int ySquare = r*r - x*x;
        int y = (int)Math.sqrt(ySquare);

        // checking whether square root is an integer
        // or not. Count increments by 4 for four
        // different quadrant values
        if (y*y == ySquare)
            result += 4;
    }

    return result;
}

// Driver code
public static void main(String arg[])
{
    int r = 5;
    System.out.println(countLattice(r));
}
}
// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find
# countLattice podefs on a circle

import math

# Function to count Lattice
# podefs on a circle
def countLattice(r):

    if (r <= 0):
        return 0 

    # Initialize result as 4 for (r, 0), (-r. 0),
    # (0, r) and (0, -r)
    result = 4

    # Check every value that can be potential x
    for x in range(1, r):

        # Find a potential y
        ySquare = r*r - x*x
        y = int(math.sqrt(ySquare))

        # checking whether square root is an defeger
        # or not. Count increments by 4 for four
        # different quadrant values
        if (y*y == ySquare):
            result += 4

    return result

# Driver program
r = 5
print(countLattice(r))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to find countLattice
// points on a circle
using System;

class GFG {

    // Function to count Lattice
    // points on a circle
    static int countLattice(int r)
    {
        if (r <= 0)
            return 0;

        // Initialize result as 4
        // for (r, 0), (-r. 0),
        // (0, r) and (0, -r)
        int result = 4;

        // Check every value that
        // can be potential x
        for (int x = 1; x < r; x++)
        {

            // Find a potential y
            int ySquare = r*r - x*x;
            int y = (int)Math.Sqrt(ySquare);

            // checking whether square root
            // is an integer or not. Count
            // increments by 4 for four
            // different quadrant values
            if (y*y == ySquare)
                result += 4;
        }

        return result;
    }

    // Driver code
    public static void Main()
    {
        int r = 5;

        Console.Write(countLattice(r));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find countLattice
// points on a circle

// Function to count Lattice
// points on a circle
function countLattice($r)
{
    if ($r <= 0)
        return 0;

    // Initialize result as 4
    // for (r, 0), (-r. 0),
    // (0, r) and (0, -r)
    $result = 4;

    // Check every value that
    // can be potential x
    for ($x = 1; $x < $r; $x++)
    {

        // Find a potential y
        $ySquare = $r * $r - $x * $x;
        $y = ceil(sqrt($ySquare));

        // checking whether square
        // root is an integer
        // or not. Count increments
        // by 4 for four different
        // quadrant values
        if ($y * $y == $ySquare)
            $result += 4;
    }

    return $result;
}

    // Driver Code
    $r = 5;
    echo countLattice($r);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// javascript program to find
// countLattice points on a circle

    // Function to count
    // Lattice points on a circle
    function countLattice(r) {
        if (r <= 0)
            return 0;

        // Initialize result as 4 for (r, 0), (-r. 0),
        // (0, r) and (0, -r)
        var result = 4;

        // Check every value that can be potential x
        for (x = 1; x < r; x++)
        {

            // Find a potential y
            var ySquare = r * r - x * x;
            var y = parseInt( Math.sqrt(ySquare));

            // checking whether square root is an integer
            // or not. Count increments by 4 for four
            // different quadrant values
            if (y * y == ySquare)
                result += 4;
        }

        return result;
    }

    // Driver code
        var r = 5;
        document.write(countLattice(r));

// This code is contributed by umadevi9616
</script>
```

输出:

```
12
```

**参考:**
[http://mathworld.wolfram.com/CircleLatticePoints.html](http://mathworld.wolfram.com/CircleLatticePoints.html)
本文由**Shivam Pradhan(anuj _ charm)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。