# 根据给定的规则

找到从点 0 到达点 N 所需的时间

> 原文:[https://www . geeksforgeeks . org/find-按给定规则从 0 点到 n 点所需的时间/](https://www.geeksforgeeks.org/find-time-required-to-reach-point-n-from-point-0-according-to-given-rules/)

给定两个正整数 **X** 和 **Y** 和 **N** 排成一行的点数，任务是根据以下规则找到从**点 0** 到达**点 N** 所需的时间:

*   每个点都有一个屏障，在每 **Y** 分钟后关闭，并在下一个 **Y** 分钟内保持关闭。
*   当到达一个点时，如果屏障是关闭的，那么这个人需要等到它打开。
*   从一点移动到另一点所花费的时间是 **X** 分钟。
*   最初，所有的障碍都被打开了。

**示例:**

> **输入:** N = 5，X = 4，Y = 3
> **输出:** 28
> **解释:**
> 从**点号 0** 到**点号 1** 需要 **4 个时间单位，再多等 2 分钟(直到第 4 个时间单位屏障在 3 个时间单位关闭，必须等待第 6 个时间单位才能重新打开)。因此，当前跳跃的总时间是 6 个单位。**
> 
> 同样，到达点 4 总共需要 24 个单位的时间并在那里等待，最后 4 个单位的时间到达点 28。
> 
> **输入:** N = 7，X = 6，Y = 2
> T3】输出: 54

**方法:**给定的问题可以基于以下观察来解决:

*   如果找到了到达第一个点的时间，即 **N=1** 或者第一个障碍什么时候会出现，那么就很容易找到答案了。
*   到达每个点时，记录当前时间。如果在到达一个城市时，障碍物是打开的，那么就移动到下一个点，否则就等到障碍物打开。
*   要检查屏障是否打开，请检查当前时间是否在屏障打开或关闭的时间段内。
*   将当前时间除以 **Y** ，如果除以时间，电流变得均匀，则屏障打开，否则屏障关闭。如果当前时间为奇数，则等待当前时间成为 **Y** 的下一个大倍数，然后继续前进。
*   观察如果 **X < Y，**那么每次到达一个点，等待屏障打开然后开始，过程重复，这样答案就是**(N–1)* Y+X**。同样，对于 **Y > =X，**当遇到第一道屏障时，计算到达该点所需的时间，并以此计算我们到达 **N** 的总时间。

按照以下步骤解决问题:

*   初始化变量，将**当前时间**设为 **0** ，存储所需的总时间。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    1.  初始化变量**检查**为**当前/是**。
    2.  如果**检查%2** 等于 **0** ，那么将 **x** 的值添加到变量**当前**中。
    3.  否则，将 **currtime** 的值增加 **(currtime+Y)/Y** ，将 **currtime** 乘以 **Y** ，将**curr time * repeat+(N –( repeat * I))* X**的值加到变量 **currtime** 和 [break](https://www.geeksforgeeks.org/break-statement-cc/) 上。
*   执行上述步骤后，打印 **currtime** 的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to get the total time to
// reach the point N
int getcurrtime(int N, int X, int Y)
{
    // Store the answer
    int currtime = 0;

    // Iterate over the range
    for (int i = 0; i < N; i++) {

        int check = currtime / Y;

        // If barrier is open
        if (check % 2 == 0)

            // Travel from that point
            // to the next one
            currtime += X;
        else {

            // Wait until it becomes the
            // next greater integer of Y
            currtime = (currtime + Y) / Y;
            currtime = currtime * Y;

            // Time to reach n point
            int repeat = (N - 1) / i;
            currtime = currtime * repeat
                       + (N - (repeat * i)) * X;
            break;
        }
    }
    return currtime;
}

// Driver Code
int main()
{

    int N = 7;
    int X = 6;
    int Y = 2;

    cout << getcurrtime(N, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to get the total time to
    // reach the point N
    static int getcurrtime(int N, int X, int Y)
    {
        // Store the answer
        int currtime = 0;

        // Iterate over the range
        for (int i = 0; i < N; i++) {

            int check = currtime / Y;

            // If barrier is open
            if (check % 2 == 0)

                // Travel from that point
                // to the next one
                currtime += X;
            else {

                // Wait until it becomes the
                // next greater integer of Y
                currtime = (currtime + Y) / Y;
                currtime = currtime * Y;

                // Time to reach n point
                int repeat = (N - 1) / i;
                currtime = currtime * repeat
                           + (N - (repeat * i)) * X;
                break;
            }
        }
        return currtime;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 7;
        int X = 6;
        int Y = 2;

        System.out.println(getcurrtime(N, X, Y));
    }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to get the total time to
# reach the point N
def getcurrtime(N, X, Y):
    # Store the answer
    currtime = 0

    # Iterate over the range
    for i in range(N):
        check = currtime / Y

        # If barrier is open
        if (check % 2 == 0):

            # Travel from that point
            # to the next one
            currtime += X
        else:

            # Wait until it becomes the
            # next greater integer of Y
            currtime = (currtime + Y) / Y
            currtime = currtime * Y

            # Time to reach n point
            repeat = (N - 1) / i
            currtime = currtime * repeat + (N - (repeat * i)) * X
            break
    return int(currtime)

# Driver Code
if __name__ == '__main__':
    N = 7
    X = 6
    Y = 2

    print(getcurrtime(N, X, Y))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    // Function to get the total time to
    // reach the point N
    static int getcurrtime(int N, int X, int Y)
    {

        // Store the answer
        int currtime = 0;

        // Iterate over the range
        for (int i = 0; i < N; i++) {

            int check = currtime / Y;

            // If barrier is open
            if (check % 2 == 0)

                // Travel from that point
                // to the next one
                currtime += X;
            else {

                // Wait until it becomes the
                // next greater integer of Y
                currtime = (currtime + Y) / Y;
                currtime = currtime * Y;

                // Time to reach n point
                int repeat = (N - 1) / i;
                currtime = currtime * repeat
                           + (N - (repeat * i)) * X;
                break;
            }
        }
        return currtime;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int N = 7;
        int X = 6;
        int Y = 2;

        Console.WriteLine(getcurrtime(N, X, Y));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to get the total time to
        // reach the point N
        function getcurrtime(N, X, Y)
        {

            // Store the answer
            let currtime = 0;

            // Iterate over the range
            for (let i = 0; i < N; i++) {

                let check = Math.floor(currtime / Y);

                // If barrier is open
                if (check % 2 == 0)

                    // Travel from that point
                    // to the next one
                    currtime += X;
                else {

                    // Wait until it becomes the
                    // next greater integer of Y
                    currtime = Math.floor((currtime + Y) / Y);
                    currtime = currtime * Y;

                    // Time to reach n point
                    let repeat = Math.floor((N - 1) / i);
                    currtime = currtime * repeat
                        + (N - (repeat * i)) * X;
                    break;
                }
            }
            return currtime;
        }

        // Driver Code
        let N = 7;
        let X = 6;
        let Y = 2;

        document.write(getcurrtime(N, X, Y));

     // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
54
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)