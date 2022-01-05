# 洗牌后找出球的正确位置

> 原文:[https://www . geeksforgeeks . org/洗牌后找出正确的球位/](https://www.geeksforgeeks.org/find-out-the-correct-position-of-the-ball-after-shuffling/)

考虑一个洗牌游戏。从 **1 到 3** 有 **3 个**玻璃杯，任何一个玻璃杯下面都藏着一个球。**然后任意两个杯子被洗牌**。这个操作做了 3 次。
给定整数 **N** 排列相同范围的**【1，3】**和 3 **对整数**。**第 N 个**玻璃最初包含球，每对给定的整数代表需要洗牌的玻璃的指数。请记住，每次洗牌后眼镜都会重新编号。
任务是在所有洗牌操作后，找出包含球的玻璃的索引。
**举例:**

> **输入:**
> N = 3
> 3 1
> 2 1
> 1 2
> **输出:** 1
> 首先**第三个**玻璃包含球。
> 第一次洗牌操作后 **(3，1)** ，**第一次**玻璃装球。
> 第二次洗牌操作后 **(2，1)** ，**第二次**玻璃装球。
> 第三次洗牌操作后 **(1，2)** ，**第一次**玻璃装球。
> **输入:**
> N = 1
> 1 3
> 1 2
> 2 3
> T35】输出: 2

**方法:**最简单的方法是为每个洗牌操作运行一个循环。
如果正在洗牌的 2 个玻璃杯中有任何一个装有球，那么很明显要将 **N** 的值改为正在洗牌的玻璃杯的指数。
如果 2 个洗牌玻璃杯中的任何一个不含球，则无需进行任何操作。
以下是上述代码的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

const int M = 3, N = 2;

// Function to generate the index of the glass
// containing the ball
void getIndex(int n, int shuffle[][N])
{
    for (int i = 0; i < 3; i++) {

        // Checking if the glasses
        // being shuffled contain
        // the ball

        // Change the index
        if (shuffle[i][0] == n)
            n = shuffle[i][1];

        // Change the index
        else if (shuffle[i][1] == n)
            n = shuffle[i][0];
    }

    // Print the index
    cout << n;
}

// Driver's Code
int main()
{
    int n = 3;

    // Storing all the shuffle operation
    int shuffle[M][N] = {
        { 3, 1 },
        { 2, 1 },
        { 1, 2 }
    };

    getIndex(n, shuffle);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG
{
static int M = 3;
static int N = 2;

// Function to generate the index of the glass
// containing the ball
static void getIndex(int n, int shuffle[][])
{
    for (int i = 0; i < 3; i++)
    {

        // Checking if the glasses
        // being shuffled contain
        // the ball

        // Change the index
        if (shuffle[i][0] == n)
            n = shuffle[i][1];

        // Change the index
        else if (shuffle[i][1] == n)
            n = shuffle[i][0];
    }

    // Print the index
    System.out.println (n);
}

// Driver Code
public static void main (String[] args)
{
    int n = 3;

    // Storing all the shuffle operation
    int shuffle[][] = {{ 3, 1 },
                       { 2, 1 },
                       { 1, 2 }};

    getIndex(n, shuffle);
}
}

// This code is contributed by ajit.
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach
M = 3; N = 2;

# Function to generate the index of
# the glass containing the ball
def getIndex(n, shuffle) :

    for i in range(3) :

        # Checking if the glasses
        # being shuffled contain
        # the ball

        # Change the index
        if (shuffle[i][0] == n) :
            n = shuffle[i][1];

        # Change the index
        elif (shuffle[i][1] == n) :
            n = shuffle[i][0];

    # Print the index
    print(n);

# Driver Code
if __name__ == "__main__" :

    n = 3;

    # Storing all the shuffle operation
    shuffle = [[ 3, 1 ],
               [ 2, 1 ],
               [ 1, 2 ]];

    getIndex(n, shuffle);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
static int M = 3;
static int N = 2;

// Function to generate the index of
// the glass containing the ball
static void getIndex(int n, int [,]shuffle)
{
    for (int i = 0; i < 3; i++)
    {

        // Checking if the glasses
        // being shuffled contain
        // the ball

        // Change the index
        if (shuffle[i, 0] == n)
            n = shuffle[i, 1];

        // Change the index
        else if (shuffle[i, 1] == n)
            n = shuffle[i, 0];
    }

    // Print the index
    Console.WriteLine(n);
}

// Driver Code
public static void Main (String[] args)
{
    int n = 3;

    // Storing all the shuffle operation
    int [,]shuffle = {{ 3, 1 },
                      { 2, 1 },
                       { 1, 2 }};

    getIndex(n, shuffle);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// javascript implementation of the above approach
     M = 3;
     N = 2;

    // Function to generate the index of the glass
    // containing the ball
    function getIndex(n , shuffle) {
        for (i = 0; i < 3; i++) {

            // Checking if the glasses
            // being shuffled contain
            // the ball

            // Change the index
            if (shuffle[i][0] == n)
                n = shuffle[i][1];

            // Change the index
            else if (shuffle[i][1] == n)
                n = shuffle[i][0];
        }

        // Print the index
        document.write(n);
    }

    // Driver Code

        var n = 3;

        // Storing all the shuffle operation
        var shuffle = [ [ 3, 1 ],
                        [ 2, 1 ],
                        [ 1, 2 ] ];

        getIndex(n, shuffle);

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
1
```