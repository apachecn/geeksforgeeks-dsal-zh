# 到达目的地的最少步数

> Original: [https://www.geeksforgeeks.org/minimum-steps-to-reach-a-destination/](https://www.geeksforgeeks.org/minimum-steps-to-reach-a-destination/)

给定一条从-无穷大到+无穷大的数线。你从 0 开始，可以向左也可以向右。条件是，在我的行动中，你要迈出步伐。
a)找到你是否能到达给定的数字 x
b)找到到达给定的数字 x 的最佳方式，如果我们确实能到达的话。例如，3 可以在 2 个步骤中到达，(0，1) (1，3)，4 可以在 3 个步骤中到达(0，-1)，(-1，1) (1，4)。
来源: [Flipkart 采访提问](https://www.geeksforgeeks.org/flipkart-interview-experience-set-30for-sde-2/)

需要注意的重要一点是，我们可以到达任何目的地，因为总是有可能进行长度为 1 的移动。在任何一步 I，我们都可以向前 I，然后向后 i + 1。
下面是 Arpit Thapar [在这里](https://www.geeksforgeeks.org/flipkart-interview-experience-set-30for-sde-2/)建议的递归解。
1)由于 0 到+ 5 和-5 的距离相同，因此我们找到了目的地绝对值的答案。

2)我们使用递归函数，该函数将以下参数作为参数:
i)源顶点
ii)最后一步的值
iii)目的地

3)如果在任一点源顶点=目的地；返回步数。

4)否则我们可以朝两个可能的方向走。在这两种情况下，采取最少的步骤。
从任意一个顶点我们都可以到:
(电流源+最后一步+1)和
(电流源-最后一步-1)

5)如果在任何一点，我们位置的绝对值超过了我们目的地的绝对值，那么从这里走最短路径是不可能的，这是很直观的。因此，我们将步长值设为 INT_MAX，这样，当我取两种可能性中的最小值时，这一个被消除了。

如果我们不使用这最后一步，程序进入无限递归并给出运行时错误。

以下是上述想法的实现。请注意，该解决方案只计算步骤。

## C++

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

## Java 语言(一种计算机语言，尤用于创建网站)

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

## 蟒蛇 3

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

## C#

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

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

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

## java 描述语言

```
<script>
// JavaScript program to count number of
// steps to reach a point

// Function to count number of steps
// required to reach a destination

// source -> source vertex
// step -> value of last step taken
// dest -> destination vertex
function steps(source, step, dest)
{

    // base cases
    if (Math.abs(source) > (dest))
        return Number.MAX_SAFE_INTEGER;
    if (source == dest) return step;

    // at each point we can go either way
    // if we go on positive side
    let pos = steps(source + step + 1,
                    step + 1, dest);

    // if we go on negative side
    let neg = steps(source - step - 1,
                    step + 1, dest);

    // minimum of both cases
    return Math.min(pos, neg);
}

// Driver code
    let dest = 11;
    document.write("No. of steps required to reach "
                            + dest + " is "
                        + steps(0, 0, dest));

// This code is contributed by Surbhi Tyagi.
</script>
```

**输出:**

```
No. of steps required to reach 11 is 5
```

感谢 Arpit Thapar 提供上述算法和实现。
**优化解决方案:** [找到到达无限线上目标的最小移动量](https://www.geeksforgeeks.org/find-minimum-moves-reach-target-infinite-line/)

本文由 Abhay 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。