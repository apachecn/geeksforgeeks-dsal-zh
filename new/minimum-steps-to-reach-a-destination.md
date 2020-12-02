# 到达目的地的最少步骤

> 原文： [https://www.geeksforgeeks.org/minimum-steps-to-reach-a-destination/](https://www.geeksforgeeks.org/minimum-steps-to-reach-a-destination/)

给定一个从-infinity 到+ infinity 的数字线。 您从 0 开始，可以向左或向右移动。 条件是，在我采取行动时，您将采取步骤。
a）确定是否可以达到给定的数字 x
b）找到达到给定数字 x 的最佳方法（如果我们确实可以达到）。 例如，可以 2 步达到 3，（0，1）（1，3）和 4 可以 3 步达到（0，-1），（-1，1）（1，4）。
来源： [Flipkart 面试问题](https://www.geeksforgeeks.org/flipkart-interview-experience-set-30for-sde-2/)

需要注意的重要一点是，我们可以到达任何目的地，因为总是可以进行长度为 1 的移动。在任何步骤 i，我们都可以向前移动 i，然后向后移动 i +1。
下面是一个递归解决方案 作者 Arpit Thapar [在这里](https://www.geeksforgeeks.org/flipkart-interview-experience-set-30for-sde-2/)。
1）由于距 0 的+ 5 和– 5 的距离相同，因此我们找到了目的地绝对值的答案。

2）我们使用一个递归函数作为参数：
i）源顶点
ii）最后一步的值
iii）目标

3）如果在任何时候源顶点=目标； 返回步骤数。

4）否则我们可以朝两个可能的方向前进。 在两种情况下，都应采取最少的步骤。
从任何顶点我们可以转到：
（电流源+最后一步+1）和
（电流源–最后一步-1）

5）如果在任何时候我们位置的绝对值超过目的地的绝对值，那么很直觉的是，从这里不可能出现最短路径。 因此，我们将步长设为 INT_MAX，以便当我将两种可能性中的最小值时，将消除这一可能性。

如果我们不使用最后一步，则该程序将进入 INFINITE 递归并给出 RUN TIME ERROR。

以下是上述想法的实现。 请注意，该解决方案仅计算步骤。

## C ++

```

// C++ program to count number of 
// steps to reach a point
#include<bits/stdc++.h>
using namespace std;

// Function to count number of steps 
// required to reach a destination

// source -> source vertex
// step -> value of last step taken
// dest -> destination vertex
int steps(int source, int step, int dest)
{
    // base cases
    if (abs(source) > (dest)) 
         return INT_MAX;
    if (source == dest) return step;

    // at each point we can go either way

    // if we go on positive side
    int pos = steps(source + step + 1, 
                      step + 1, dest);

    // if we go on negative side
    int neg = steps(source - step - 1,
                      step + 1, dest);

    // minimum of both cases
    return min(pos, neg);
}

// Driver code
int main()
{
    int dest = 11;
    cout << "No. of steps required to reach "
                            << dest << " is "
                        << steps(0, 0, dest);
    return 0;
}

```

## 爪哇

```

// Java program to count number of
// steps to reach a point
import java.io.*;

class GFG 
{

    // Function to count number of steps
    // required to reach a destination

    // source -> source vertex
    // step -> value of last step taken
    // dest -> destination vertex
    static int steps(int source, int step,
                                int dest)
    {
        // base cases
        if (Math.abs(source) > (dest)) 
            return Integer.MAX_VALUE;

        if (source == dest) 
            return step;

        // at each point we can go either way

        // if we go on positive side
        int pos = steps(source + step + 1,
                        step + 1, dest);

        // if we go on negative side
        int neg = steps(source - step - 1, 
                        step + 1, dest);

        // minimum of both cases
        return Math.min(pos, neg);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int dest = 11;
        System.out.println("No. of steps required"+
                                " to reach " + dest +
                       " is " + steps(0, 0, dest));
    }
}

// This code is contributed by Prerna Saini

```

## Python3

```

# python program to count number of
# steps to reach a point
import sys

# Function to count number of steps
# required to reach a destination

# source -> source vertex
# step -> value of last step taken
# dest -> destination vertex
def steps(source, step, dest):

    #base cases
    if (abs(source) > (dest)) :
        return sys.maxsize 

    if (source == dest):
        return step

    # at each point we can go 
    # either way

    # if we go on positive side
    pos = steps(source + step + 1,
                    step + 1, dest)

    # if we go on negative side
    neg = steps(source - step - 1, 
                    step + 1, dest)

    # minimum of both cases
    return min(pos, neg)

# Driver Code
dest = 11;
print("No. of steps required",
               " to reach " ,dest , 
        " is " , steps(0, 0, dest));

# This code is contributed by Sam007.

```

## C＃

```

// C# program to count number of
// steps to reach a point
using System;

class GFG 
{
    // Function to count number of steps
    // required to reach a destination

    // source -> source vertex
    // step -> value of last step taken
    // dest -> destination vertex
    static int steps(int source, int step,
                                int dest)
    {
        // base cases
        if (Math.Abs(source) > (dest)) 
            return int.MaxValue;

        if (source == dest)     
            return step;

        // at each point we can go either way

        // if we go on positive side
        int pos = steps(source + step + 1,
                        step + 1, dest);

        // if we go on negative side
        int neg = steps(source - step - 1, 
                        step + 1, dest);

        // minimum of both cases
        return Math.Min(pos, neg);
    }

    // Driver Code
    public static void Main()
    {
        int dest = 11;
        Console.WriteLine("No. of steps required"+
                             " to reach " + dest + 
                      " is " + steps(0, 0, dest));
    }
}

// This code is contributed by Sam007

```

## 的 PHP

```

<?php
// PHP program to count number 
// of steps to reach a point

// Function to count number 
// of steps required to reach 
// a destination

// source -> source vertex
// step -> value of last step taken
// dest -> destination vertex
function steps($source, $step, $dest)
{
    // base cases
    if (abs($source) > ($dest)) 
        return PHP_INT_MAX;
    if ($source == $dest) 
        return $step;

    // at each point we 
    // can go either way

    // if we go on positive side
    $pos = steps($source + $step + 1, 
                   $step + 1, $dest);

    // if we go on negative side
    $neg = steps($source - $step - 1,
                   $step + 1, $dest);

    // minimum of both cases
    return min($pos, $neg);
}

// Driver code
$dest = 11;
echo "No. of steps required to reach ",
     $dest, " is ", steps(0, 0, $dest);

// This code is contributed by aj_36
?>

```

**输出：**

```
No. of steps required to reach 11 is 5

```

感谢 Arpit Thapar 提供上述算法和实现。
**优化解决方案：** [找出在无限线上达到目标的最小移动量](https://www.geeksforgeeks.org/find-minimum-moves-reach-target-infinite-line/)

本文由 Abhay 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

