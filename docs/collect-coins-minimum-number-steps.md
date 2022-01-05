# 以最少的步数收集所有硬币

> 原文:[https://www . geesforgeks . org/collect-coins-最小数量-steps/](https://www.geeksforgeeks.org/collect-coins-minimum-number-steps/)

给定许多相邻排列的硬币堆。我们需要在最少的步骤中收集所有这些硬币，在一个步骤中，我们可以收集一条水平线或垂直线的硬币，并且收集的硬币应该是连续的。
**例:**

```
Input : height[] = [2 1 2 5 1]
Each value of this array corresponds to
the height of stack that is we are given
five stack of coins, where in first stack
2 coins are there then in second stack 
1 coin is there and so on.
Output : 4
We can collect all above coins in 4 steps 
which are shown in below diagram.
Each step is shown by different color.

First, we have collected last horizontal
line of coins after which stacks remains
as [1 0 1 4 0] after that, another horizontal
line of coins is collected from stack 3 
and 4 then a vertical line from stack 4 
and at the end a horizontal line from
stack 1\. Total steps are 4.
```

我们可以用分治法来解决这个问题。我们可以看到，从下面去掉水平线总是有益的。假设我们在递归步骤中处理从 l 索引到 r 索引的堆栈，每次我们将选择最小高度，移除那些许多水平线，之后堆栈将被分成两部分，l 到最小值和最小值+1 到 r，我们将在这些子数组中递归调用。另一件事是，我们也可以使用垂直线收集硬币，因此我们将在递归调用的结果和(r–l)之间选择最小值，因为使用(r–l)垂直线，我们总是可以收集所有硬币。
当我们每次调用每个子阵列并找到其中的最小值时，解决方案的总时间复杂度将是 O(N)<sup>2</sup>)

## C++

```
// C++ program to find minimum number of
// steps to collect stack of coins
#include <bits/stdc++.h>
using namespace std;

// recursive method to collect coins from
// height array l to r, with height h already
// collected
int minStepsRecur(int height[], int l, int r, int h)
{
    // if l is more than r, no steps needed
    if (l >= r)
        return 0;

    // loop over heights to get minimum height
    // index
    int m = l;
    for (int i = l; i < r; i++)
        if (height[i] < height[m])
            m = i;

    /* choose minimum from,
        1) collecting coins using all vertical
        lines (total r - l)
        2) collecting coins using lower horizontal
        lines and recursively on left and right
        segments */
    return min(r - l,
               minStepsRecur(height, l, m, height[m]) +
               minStepsRecur(height, m + 1, r, height[m]) +
               height[m] - h);
}

// method returns minimum number of step to
// collect coin from stack, with height in
// height[] array
int minSteps(int height[], int N)
{
    return minStepsRecur(height, 0, N, 0);
}

// Driver code to test above methods
int main()
{
    int height[] = { 2, 1, 2, 5, 1 };
    int N = sizeof(height) / sizeof(int);

    cout << minSteps(height, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Code to Collect all coins in
// minimum number of steps
import java.util.*;

class GFG {

    // recursive method to collect coins from
    // height array l to r, with height h already
    // collected
    public static int minStepsRecur(int height[], int l,
                                           int r, int h)
    {
        // if l is more than r, no steps needed
        if (l >= r)
            return 0;

        // loop over heights to get minimum height
        // index
        int m = l;
        for (int i = l; i < r; i++)
            if (height[i] < height[m])
                m = i;

        /* choose minimum from,
            1) collecting coins using all vertical
            lines (total r - l)
            2) collecting coins using lower horizontal
            lines and recursively on left and right
            segments */
        return Math.min(r - l,
                        minStepsRecur(height, l, m, height[m]) +
                        minStepsRecur(height, m + 1, r, height[m]) +
                        height[m] - h);
    }

    // method returns minimum number of step to
    // collect coin from stack, with height in
    // height[] array
    public static int minSteps(int height[], int N)
    {
        return minStepsRecur(height, 0, N, 0);
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {

        int height[] = { 2, 1, 2, 5, 1 };
        int N = height.length;

        System.out.println(minSteps(height, N));
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python 3 program to find
# minimum number of steps
# to collect stack of coins

# recursive method to collect
# coins from height array l to
# r, with height h already
# collected
def minStepsRecur(height, l, r, h):

    # if l is more than r,
    # no steps needed
    if l >= r:
        return 0;

    # loop over heights to
    # get minimum height index
    m = l
    for i in range(l, r):
        if height[i] < height[m]:
            m = i

    # choose minimum from,
    # 1) collecting coins using
    # all vertical lines (total r - l)
    # 2) collecting coins using
    # lower horizontal lines and
    # recursively on left and
    # right segments
    return min(r - l,
            minStepsRecur(height, l, m, height[m]) +
            minStepsRecur(height, m + 1, r, height[m]) +
            height[m] - h)

# method returns minimum number
# of step to collect coin from
# stack, with height in height[] array
def minSteps(height, N):
    return minStepsRecur(height, 0, N, 0)

# Driver code
height = [ 2, 1, 2, 5, 1 ]
N = len(height)
print(minSteps(height, N))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# Code to Collect all coins in
// minimum number of steps
using System;

class GFG {

    // recursive method to collect coins from
    // height array l to r, with height h already
    // collected
    public static int minStepsRecur(int[] height, int l,
                                           int r, int h)
    {
        // if l is more than r, no steps needed
        if (l >= r)
            return 0;

        // loop over heights to
        // get minimum height index
        int m = l;
        for (int i = l; i < r; i++)
            if (height[i] < height[m])
                m = i;

        /* choose minimum from,
            1) collecting coins using all vertical
            lines (total r - l)
            2) collecting coins using lower horizontal
            lines and recursively on left and right
            segments */
        return Math.Min(r - l,
                        minStepsRecur(height, l, m, height[m]) +
                        minStepsRecur(height, m + 1, r, height[m]) +
                        height[m] - h);
    }

    // method returns minimum number of step to
    // collect coin from stack, with height in
    // height[] array
    public static int minSteps(int[] height, int N)
    {
        return minStepsRecur(height, 0, N, 0);
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int[] height = { 2, 1, 2, 5, 1 };
        int N = height.Length;

        Console.Write(minSteps(height, N));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum number of
// steps to collect stack of coins

// recursive method to collect
// coins from height array l to
// r, with height h already
// collected
function minStepsRecur($height, $l,
                            $r, $h)
{

    // if l is more than r,
    // no steps needed
    if ($l >= $r)
        return 0;

    // loop over heights to
    // get minimum height
    // index
    $m = $l;
    for ($i = $l; $i < $r; $i++)
        if ($height[$i] < $height[$m])
            $m = $i;

    /* choose minimum from,
        1) collecting coins using
           all vertical lines
           (total r - l)
        2) collecting coins using
           lower horizontal lines
           and recursively on left
           and right segments */
    return min($r - $l,
           minStepsRecur($height, $l, $m, $height[$m]) +
           minStepsRecur($height, $m + 1, $r, $height[$m]) +
           $height[$m] - $h);
}

// method returns minimum number of step to
// collect coin from stack, with height in
// height[] array
function minSteps($height, $N)
{
    return minStepsRecur($height, 0, $N, 0);
}

    // Driver Code
    $height = array(2, 1, 2, 5, 1);
    $N = sizeof($height);

    echo minSteps($height, $N) ;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// Javascript Code to Collect all coins in
// minimum number of steps

    // recursive method to collect coins from
    // height array l to r, with height h already
    // collected
    function minStepsRecur(height,l,r,h)
    {
        // if l is more than r, no steps needed
        if (l >= r)
            return 0;

        // loop over heights to get minimum height
        // index
        let m = l;
        for (let i = l; i < r; i++)
            if (height[i] < height[m])
                m = i;

        /* choose minimum from,
            1) collecting coins using all vertical
            lines (total r - l)
            2) collecting coins using lower horizontal
            lines and recursively on left and right
            segments */
        return Math.min(r - l,
                        minStepsRecur(height, l, m, height[m]) +
                        minStepsRecur(height, m + 1, r, height[m]) +
                        height[m] - h);
    }

    // method returns minimum number of step to
    // collect coin from stack, with height in
    // height[] array
    function minSteps(height,N)
    {
        return minStepsRecur(height, 0, N, 0);
    }

     /* Driver program to test above function */
    let height=[2, 1, 2, 5, 1 ];
    let N = height.length;
    document.write(minSteps(height, N));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
4
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。