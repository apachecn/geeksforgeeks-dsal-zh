# 最大化图表中与所有其他节点断开连接的节点数

> 原文： [https://www.geeksforgeeks.org/maximize-count-of-nodes-disconnected-from-all-other-nodes-in-a-graph/](https://www.geeksforgeeks.org/maximize-count-of-nodes-disconnected-from-all-other-nodes-in-a-graph/)

给定两个整数`N`和`E`，它们表示[无向图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)的节点数和边数，因此任务是最大化 在不使用任何自环的情况下，未连接到图中的任何其他节点。
**范例**：

> **输入**：N = 5，E = 1
> **输出**：3
> **说明**：
> 由于图形中只有 1 个边 可以用来连接两个节点。
> 因此，**三个**节点保持断开连接。
> 
> **输入**：N = 5，E = 2
> **输出**：2

**方法**：该方法基于以下思想：为了使断开连接的节点数最大化，只有在每两个不同的节点都连接好之后，才会将新节点添加到图中。 以下是解决此问题的步骤：

1.  初始化两个变量**和 **rem** ，分别存储连接的节点和未分配的边。**
2.  如果 **rem** 变为 0，则所需答案将为 **N – curr** 。
3.  否则，将 **curr** 的值增加 1。
4.  因此，当前步骤中保持每两个不同节点连接所需的最大边为 **min（rem，curr）**。 从 **rem** 中减去它，并增加 **curr** 。
5.  重复此过程，直到 **rem** 减小为零。
6.  最后，打印 **N – curr** 。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function which returns
// the maximum number of
// isolated nodes
int maxDisconnected(int N, int E)
{
    // Used nodes
    int curr = 1;

    // Remaining edges
    int rem = E;

    // Count nodes used
    while (rem > 0) {
        rem = rem
              - min(
                    curr, rem);
        curr++;
    }

    // If given edges are non-zero
    if (curr > 1) {
        return N - curr;
    }
    else {
        return N;
    }
}

// Driver Code
int main()
{
    // Given N and E
    int N = 5, E = 1;

    // Function Call
    cout << maxDisconnected(N, E);

    return 0;
}

```

## Java

```java

// Java implementation of
// the above approach
import java.util.*;

class GFG{

// Function which returns
// the maximum number of
// isolated nodes
static int maxDisconnected(int N, int E)
{

    // Used nodes
    int curr = 1;

    // Remaining edges
    int rem = E;

    // Count nodes used
    while (rem > 0) 
    {
        rem = rem - Math.min(
                    curr, rem);
        curr++;
    }

    // If given edges are non-zero
    if (curr > 1)
    {
        return N - curr;
    }
    else
    {
        return N;
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given N and E
    int N = 5, E = 1;

    // Function call
    System.out.print(maxDisconnected(N, E));
}
}

// This code is contributed by 29AjayKumar

```

## Python3

```

# Python3 implementation of
# the above approach

# Function which returns
# the maximum number of
# isolated nodes
def maxDisconnected(N, E):

    # Used nodes
    curr = 1

    # Remaining edges
    rem = E

    # Count nodes used
    while (rem > 0):
        rem = rem - min(curr, rem)
        curr += 1

    # If given edges are non-zero
    if (curr > 1):
        return N - curr
    else:
        return N

# Driver Code
if __name__ == '__main__':

    # Given N and E
    N = 5
    E = 1

    # Function call
    print(maxDisconnected(N, E))

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# implementation of
// the above approach
using System;
class GFG{

// Function which returns
// the maximum number of
// isolated nodes
static int maxDisconnected(int N, 
                           int E)
{    
  // Used nodes
  int curr = 1;

  // Remaining edges
  int rem = E;

  // Count nodes used
  while (rem > 0) 
  {
    rem = rem - Math.Min(curr, rem);
    curr++;
  }

  // If given edges are non-zero
  if (curr > 1)
  {
    return N - curr;
  }
  else
  {
    return N;
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given N and E
  int N = 5, E = 1;

  // Function call
  Console.Write(maxDisconnected(N, E));
}
}

// This code is contributed by 29AjayKumar

```

**Output:** 

```
3

```

***时间复杂度**：O（E）*
***辅助空间**：O（1）*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。