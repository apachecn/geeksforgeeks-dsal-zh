# 生成位于矩形

内的所有积分点

给定长度为 **L** 且宽度为 **W** 的矩形，任务是生成位于矩形 pf 尺寸 **L * W 内的所有积分坐标（X，Y）** 在其原点**（0，0）**中具有其顶点之一。

**示例**：

> **输入**：L = 3，W = 2
> **输出**：（0，0）（0，1）（1，0）（1，1）（2，0 ）（2，1）
> **说明**：矩形内存在的积分坐标总数为 L×W =6。因此，输出为（0，0）（0，1）（1 ，0）（1，1）（2，0）（2，1）。
> 
> **输入**：L = 5，W = 3
> **输出**：（0，0）（0，1）（0，2）（1，0）（1，1 ）（1，2）（2，0）（2，1）（2，2）（3，0）（3，1）（3，2）（4，0）（4，1）（4，2 ）

**方法**：可通过为 **X** -坐标和**生成从 **0** 到 **L** 范围内的所有整数来解决该问题。 ] **Y** 的 0** 至 **W** -使用 [rand（）](https://www.geeksforgeeks.org/rand-and-srand-in-ccpp/)函数的坐标。 请按照以下步骤解决问题：

1.  创建一组[对](https://www.geeksforgeeks.org/sets-of-pairs-in-c/)，以存储矩形内的所有坐标（X，Y）。

2.  使用等式 **rand（）％L** 生成介于 **0** 至 **L** 和 **rand（）％W** 之间的所有整数 位于 **0** 至 **W** 之间的所有整数。

3.  打印矩形内所有可能的 **L×W** 坐标（X，Y）。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate coordinates
// lying within the rectangle
void generatePoints(int L, int W)
{
    // Store all possible coordinates
    // that lie within the rectangle
    set<pair<int, int> > hash;

    // Stores the number of possible
    // coordinates that lie within
    // the rectangle
    int total = (L * W);

    // Use current time as seed
    // for random generator
    srand(time(0));

    // Generate all possible
    // coordinates
    while (total--) {
        // Generate all possible
        // X-coordinates
        int X = rand() % L;

        // Generate all possible
        // Y-coordinates
        int Y = rand() % W;

        // If coordinates(X, Y) has
        // not been generated already
        while (hash.count({ X, Y })) {
            X = rand() % L;
            Y = rand() % W;
        }

        // Insert the coordinates(X, Y)
        hash.insert({ X, Y });
    }

    // Print the coordinates
    for (auto points : hash) {
        cout << "(" << points.first << ", "
             << points.second << ") ";
    }
}

// Driver Code
int main()
{
    // Rectangle dimensions
    int L = 3, W = 2;

    generatePoints(L, W);
}

```

## Python3

```py

# Python3 program to implement
# the above approach
import time
import random

random.seed(time.time())

# Function to generate coordinates
# lying within the rectangle
def generatePoints(L, W):

    # Store all possible coordinates
    # that lie within the rectangle
    hash = {}

    # Stores the number of possible
    # coordinates that lie within
    # the rectangle
    total = (L * W)

    # Generate all possible
    # coordinates
    for i in range(total):

        # Generate all possible
        # X-coordinates
        X = random.randint(0, L) % L

        # Generate all possible
        # Y-coordinates
        Y = random.randint(0, W) % W

        # If coordinates(X, Y) has
        # not been generated already
        while ((X, Y) in hash):
            X = random.randint(0, L) % L
            Y = random.randint(0, W) % W

        # Insert the coordinates(X, Y)
        hash[(X, Y)] = 1

    # Print the coordinates
    for points in sorted(hash):
        print("(", points[0], 
             ", ", points[1],
             ") ", end = "")

# Driver code 
if __name__ == '__main__':

    # Rectangle dimensions
    L, W = 3, 2

    generatePoints(L, W)

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program to implement
// the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

public class store : IComparer<KeyValuePair<int, int>>
{
    public int Compare(KeyValuePair<int, int> x,
                       KeyValuePair<int, int> y)
    {
        if (x.Key != y.Key)
        {
            return x.Key.CompareTo(y.Key);    
        }
        else
        {
            return x.Value.CompareTo(y.Value);    
        }
    }
}

// Function to generate coordinates
// lying within the rectangle
static void generatePoints(int L, int W)
{

    // Store all possible coordinates
    // that lie within the rectangle
    SortedSet<KeyValuePair<int,
                           int>> hash = new SortedSet<KeyValuePair<int,
                                                                   int>>(new store());

    // Stores the number of possible
    // coordinates that lie within
    // the rectangle
    int total = (L * W);

    // For random generator
    Random rand = new Random();

    // Generate all possible
    // coordinates
    while ((total--) != 0) 
    {

        // Generate all possible
        // X-coordinates
        int X = rand.Next() % L;

        // Generate all possible
        // Y-coordinates
        int Y = rand.Next() % W;

        // If coordinates(X, Y) has
        // not been generated already
        while (hash.Contains(
            new KeyValuePair<int, int>(X, Y)))
        {
            X = rand.Next() % L;
            Y = rand.Next() % W;
        }

        // Insert the coordinates(X, Y)
        hash.Add(new KeyValuePair<int, int>(X, Y));
    }

    // Print the coordinates
    foreach(KeyValuePair<int, int> x in hash)
    {
        Console.Write("(" + x.Key + ", " +
                          x.Value + ") ");
    }
}

// Driver Code
public static void Main(string[] args)
{

    // Rectangle dimensions
    int L = 3, W = 2;

    generatePoints(L, W);
}
}

// This code is contributed by rutvik_56

```

**Output:** 

```
(0, 0) (0, 1) (1, 0) (1, 1) (2, 0) (2, 1)

```

***时间复杂度**：O（L * W）*

***辅助空间**：O（L * W）*



* * *

* * *



