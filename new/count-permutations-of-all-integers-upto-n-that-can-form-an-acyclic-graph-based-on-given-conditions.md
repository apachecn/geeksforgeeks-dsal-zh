# 根据给定条件计数最多 N 个可以形成无环图的整数的排列[H​​TG1]

> 原文： [https://www.geeksforgeeks.org/count-permutations-of-all-integers-upto-n-that-can-form-an-acyclic-graph-based-on-given-conditions/](https://www.geeksforgeeks.org/count-permutations-of-all-integers-upto-n-that-can-form-an-acyclic-graph-based-on-given-conditions/)

给定整数 **N，**的任务是从 **[1，N]** 范围中找到整数的排列数目，该范围可以形成[非循环图](https://en.wikipedia.org/wiki/Directed_acyclic_graph) 以下条件：

*   对于每个 **1≤i≤N** ，找到最大的 **j** ，使得 **1≤j < i** 和 **A [j] > A [i** ]，并在节点 **i** 和节点 **j** 之间添加[无向边缘](https://www.geeksforgeeks.org/count-number-edges-undirected-graph/)。
*   对于每个 **1≤i≤N** ，找到最小的 **j** ，使 **i < j≤N** 和 **A [j] > A [i]** ，并在节点 **i** 和节点 **j** 之间添加**无向边缘**。

**示例：**

> **输入：** 3
> **输出：** 4
> **说明：**
> {1,2,3}：可能（图形边缘：{[ 1，2]，[2，3]}。因此，不存在循环）
> {1，3，2}：可能的（图形边缘：{[1，3]，[2，3]}。因此， 不存在循环）
> {2，1，3}：不可能（图形边缘：{[2，3]，[1，3]，[1，2]}。因此，循环存在）
> { 2，3，1}：可能（图形边缘：{[2，3]，[1，3]}。因此，不存在循环）。
> {3，1，2}：不可能（图形边缘：{ [1，2]，[1，3]，[2，3]}。因此，存在循环。
> {3，2，1}：可能（图形边缘：{[2，3]，[1， 2]}。因此，不存在循环）
> 
> **输入：** 4
> **输出：** 8

**方法：**请按照以下步骤解决问题：

*   共有 **N 个！** 可能生成的数组，这些数组由 **[1，N]** 范围内的整数置换组成。
*   根据给定条件，如果 **i，j，k（i < j < k）**是数组中的索引，则如果 **A [i] > A [j ]** 和 **A [j] < A [k]** ，那么将存在一个由边{ **[A [j]，A [i]]，[A]组成的循环 [j]，A [k]]，[A [i]，A [k]]}** 。
*   除去这些置换，剩下 2 个<sup>（N – 1）</sup>可能的置换。
*   对于 **[1，N – 1]** 和**范围内的整数，剩余的排列仅给出两个可能的位置。 **N** 的可能位置为 1** 。

> **插图：**
> 对于 N = 3：
> 排列{2，1，3}包含一个循环，如 A [0] > A [1]和 A [1] < A2]。
> 置换{3，1，2}包含一个循环，如 A [0] > A [1]和 A [1] < A [2]。
> 所有剩余的排列都可以生成一个非循环图。
> 因此，有效排列数= 3！ – 2 = 4 = 2 <sup>3 – 1</sup>

*   因此，打印 **2 <sup>N – 1</sup>** 作为要求的答案。

下面是上述方法的实现：

## C ++

```

// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Find the count of possible graphs
void possibleAcyclicGraph(int N)
{
    cout << pow(2, N - 1);
    return;
}

// Driver Code
int main()
{

    int N = 4;
    possibleAcyclicGraph(N);

    return 0;
}

```

## 爪哇

```

// Java implementation of 
// the above approach
import java.util.*;
class GFG{

// Find the count of 
// possible graphs
static void possibleAcyclicGraph(int N)
{
  System.out.print((int)Math.pow(2, 
                                 N - 1));
  return;
}

// Driver Code
public static void main(String[] args)
{
  int N = 4;
  possibleAcyclicGraph(N);
}
}

// This code is contributed by Princi Singh

```

## Python3

```

# Python3 implementation of above approach

# Find the count of possible graphs
def possibleAcyclicGraph(N):

    print(pow(2, N - 1))
    return

# Driver code
if __name__ == '__main__':

    N = 4

    possibleAcyclicGraph(N)

# This code is contributed by mohit kumar 29

```

## C＃

```

// C# implementation of 
// the above approach
using System;

class GFG{

// Find the count of 
// possible graphs
static void possibleAcyclicGraph(int N)
{
    Console.Write((int)Math.Pow(2, N - 1));

    return;
}

// Driver Code
public static void Main()
{
    int N = 4;

    possibleAcyclicGraph(N);
}
}

// This code is contributed by sanjoy_62

```

**Output**

```
8

```

***时间复杂度：O（logN）***
***空间复杂度：O（1）***



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。