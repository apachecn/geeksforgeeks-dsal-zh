# 获得相反奇偶性元素的最小跳转次数

> 原文： [https://www.geeksforgeeks.org/minimum-number-of-jumps-to-obtain-an-element-of-opposite-parity/](https://www.geeksforgeeks.org/minimum-number-of-jumps-to-obtain-an-element-of-opposite-parity/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** 和 **jumps []** ，它们由`N`个正整数组成，每个数组元素 **arr 的任务 [i]** 将找到达到相对奇偶性元素所需的最小跳转数。 任何数组元素 **arr [i]** 唯一可能的跳转是**（i + jumps [i]）**或**（i – jumps [i]）**。

**示例**：

> **输入**：arr [] = {4，2，5，2，1}，跳跃[] = {1,2,3,1,2}
> **输出**：3 2 -1 1 -1
> **说明**：
> 以下是每个元素所需的最小步骤：
> **arr [4]**：由于跳跃[4] = 2，唯一可能的跳转是（4 – jumps [4]）=2。由于 arr [2]与 arr [4]具有相同的奇偶校验，并且在数组索引范围内无法进行进一步的跳转，请打印`-1`。
> **arr [3]**：由于 jumps [3] = 1，所以两个跳转（3 + jumps [3]）= 4 或（3 – jumps [3]）= 2 都是可能的。 由于元素 arr [2]和 arr [4]与 arr [3]的奇偶性相反，因此请打印`1`。
> **arr [2]**：打印`-1`。
> **arr [1]**：唯一可能的跳跃是（2 +跳跃[2]）。 由于 arr [3]与 arr [2]具有相同的奇偶校验，并且从 arr [3]到达具有相反奇偶校验的数组元素所需的最小跳转为 1，因此所需的跳转次数为 2。
> **arr [ 0]**：arr [0]-> arr [3]->（arr [4]或 arr [2]）。 因此，所需的最小跳跃为 3。
> 
> **输入**：arr [] = {4，5，7，6，7，5，4，4，6，4}，jumps [] = {1,2,3,3,5,2 、、 7、2、4、1}
> **输出**：1 1 2 2 1 1 -1 1 1 2

**天真的方法**：解决问题的最简单方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并对每个数组元素 **arr [i]执行[广度优先遍历](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) ]** ，方法是反复将 arr [i – jumps [i]] 和 **arr [i + jumps [i]]** 转换为**，直到出现无效索引为止， 转换，检查数组元素是否与前一个元素具有相反的奇偶校验。 相应地打印每个数组元素所需的最小跳转数。**

***时间复杂度**：O（N <sup>2</sup> ）*

***辅助空间**：O（N）*

**高效方法**：为了优化上述方法，其思想是将[多源 BFS](https://www.geeksforgeeks.org/multi-source-shortest-path-in-unweighted-graph/) 分别用于偶数和奇数数组元素。 请按照以下步骤解决问题：

1.  初始化[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，例如 **ans []** ，以存储每个数组元素到达相对奇偶校验元素所需的最小跳转。

2.  初始化向量， **Adj []** 的[数组，以存储生成的图](https://www.geeksforgeeks.org/array-of-vectors-in-c-stl/)的[邻接表。](https://www.geeksforgeeks.org/graph-and-its-representations/)

3.  对于每个索引的有效跳转的每对**（i，j）**，数组的`i`通过将边初始化为**（j，i）**来创建一个倒置图形。 。

4.  对奇数元素执行**多源 BFS 遍历**。 执行以下步骤：

    *   [将包含奇数数组元素的所有索引推入](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)到[队列](https://www.geeksforgeeks.org/queue-data-structure/)中，并将所有这些节点标记为同时访问。

    *   迭代直到[队列为非空](https://www.geeksforgeeks.org/queueempty-queuesize-c-stl/)并执行以下操作：

        *   弹出出现在队列前面[的节点，并检查现在连接到该节点的任何节点是否具有相同的奇偶校验。 如果发现为真，则将子节点的**距离更新为 **1 +父节点的距离。****](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)

        *   将子节点标记为已访问并将其推入队列。

5.  对偶数元素执行**多源 BFS 遍历**并将距离存储在 **ans []** 中。

6.  完成上述步骤后，打印存储在 **ans []** 中的值作为结果。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Bfs for odd numbers are source
void bfs(int n, vector<int>& a,
         vector<int> invGr[],
         vector<int>& ans, int parity)
{
    // Initialize queue
    queue<int> q;

    // Stores for each node, the nodes
    // visited and their distances
    vector<int> vis(n + 1, 0);
    vector<int> dist(n + 1, 0);

    // Push odd and even numbers
    // as sources to the queue

    // If parity is 0 -> odd
    // Otherwise -> even
    for (int i = 1; i <= n; i++) {
        if ((a[i] + parity) & 1) {
            q.push(i);
            vis[i] = 1;
        }
    }

    // Peform multi-source bfs
    while (!q.empty()) {

        // Extract the front element
        // of the queue
        int v = q.front();
        q.pop();

        // Traverse nodes connected
        // to the current node
        for (int u : invGr[v]) {

            // If u is not visited
            if (!vis[u]) {

                dist[u] = dist[v] + 1;
                vis[u] = 1;

                // If element with opposite
                // parity is obtained
                if ((a[u] + parity) % 2 == 0) {
                    if (ans[u] == -1)

                        // Store its distance from
                        // source in ans[]
                        ans[u] = dist[u];
                }

                // Push the current neighbour
                // to the queue
                q.push(u);
            }
        }
    }
}

// Function to find the minimum jumps
// required by each index to reach
// element of opposite parity
void minJumps(vector<int>& a,
              vector<int>& jump, int n)
{
    // Initialise Inverse Graph
    vector<int> invGr[n + 1];

    // Stores the result for each index
    vector<int> ans(n + 1, -1);

    for (int i = 1; i <= n; i++) {

        // For the jumped index
        for (int ind : { i + jump[i],
                         i - jump[i] }) {

            // If the ind is valid then
            // add reverse directed edge
            if (ind >= 1 and ind <= n) {
                invGr[ind].push_back(i);
            }
        }
    }

    // Multi-source bfs with odd
    // numbers as source by passing 0
    bfs(n, a, invGr, ans, 0);

    // Multi-source bfs with even
    // numbers as source by passing 1
    bfs(n, a, invGr, ans, 1);

    // Print the answer
    for (int i = 1; i <= n; i++) {
        cout << ans[i] << ' ';
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 0, 4, 2, 5, 2, 1 };
    vector<int> jump = { 0, 1, 2, 3, 1, 2 };

    int N = arr.size();

    minJumps(arr, jump, N - 1);

    return 0;
}

```

## Python

```py

# Python3 program for the above approach

# Bfs for odd numbers are source
def bfs(n, a, invGr, ans, parity):

    # Initialize queue
    q = []

    # Stores for each node, the nodes
    # visited and their distances
    vis = [0 for i in range(n + 1)]
    dist = [0 for i in range(n + 1)]

    # Push odd and even numbers
    # as sources to the queue

    # If parity is 0 -> odd
    # Otherwise -> even
    for i in range(1, n + 1):
        if ((a[i] + parity) & 1):
            q.append(i)
            vis[i] = 1

    # Peform multi-source bfs
    while (len(q) != 0):

        # Extract the front element
        # of the queue
        v = q[0]
        q.pop(0)

        # Traverse nodes connected
        # to the current node
        for u in invGr[v]:

            # If u is not visited
            if (not vis[u]):
                dist[u] = dist[v] + 1
                vis[u] = 1

                # If element with opposite
                # parity is obtained
                if ((a[u] + parity) % 2 == 0):
                    if (ans[u] == -1):

                        # Store its distance from
                        # source in ans[]
                        ans[u] = dist[u]

                # Push the current neighbour
                # to the queue
                q.append(u)

# Function to find the minimum jumps
# required by each index to reach
# element of opposite parity
def minJumps(a, jump, n):

    # Initialise Inverse Graph
    invGr = [[] for i in range(n + 1)]

    # Stores the result for each index
    ans = [-1 for i in range(n + 1)]

    for i in range(1, n + 1):

        # For the jumped index
        for ind in [i + jump[i], i - jump[i]]:

            # If the ind is valid then
            # add reverse directed edge
            if (ind >= 1 and ind <= n):
                invGr[ind].append(i)

    # Multi-source bfs with odd
    # numbers as source by passing 0
    bfs(n, a, invGr, ans, 0)

    # Multi-source bfs with even
    # numbers as source by passing 1
    bfs(n, a, invGr, ans, 1)

    # Print the answer
    for i in range(1, n + 1):
        print(str(ans[i]), end = ' ')

# Driver Code
if __name__=='__main__':

    arr = [ 0, 4, 2, 5, 2, 1 ]
    jump = [ 0, 1, 2, 3, 1, 2 ]

    N = len(arr)

    minJumps(arr, jump, N - 1)

# This code is contributed by pratham76

```

**Output:** 

```
3 2 -1 1 -1
```

***时间复杂度**：O（N）*

***辅助空间**：O（N）*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。