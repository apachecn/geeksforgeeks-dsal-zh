# 如果仅当节点为绿色时才允许行驶，从节点 1 到达 N 的最短时间

> 原文:[https://www . geesforgeks . org/从节点 1 到节点 n 的最短到达时间-如果允许旅行-仅当节点为绿色时/](https://www.geeksforgeeks.org/minimum-time-to-reach-from-node-1-to-n-if-travel-is-allowed-only-when-node-is-green/)

给定 **N 个**节点和 **M 个**边的无向连通图。每个节点都有一盏灯，但一次可以是绿色或红色。最初，所有的节点都是绿色的。每过 **T** 秒，光的颜色从绿色变为红色，反之亦然。只有当节点 U 的颜色为绿色时，才可能从节点 U 行进到节点 V。通过任何边缘所需的时间为 **C** 秒。找出从节点 1 到节点 n 所需的最短时间

**示例:**

> **输入:** N = 5，M = 5，T = 3，C = 5
> 边[] = {{1，2}，{1，3}，{1，4}，{2，4}，{2，5}}
> **输出:** 11
> **说明:**0 秒时，节点 1 的颜色为绿色，因此从节点 1 行进到节点 2 需要 5 秒。
> 现在，在 5 秒钟时，节点 2 的颜色是红色，所以等待 1 秒钟变成绿色。
> 现在在 6 秒，节点 2 的颜色是绿色，所以在 5 秒内从节点 2 行进到节点 5。
> 总时间= 5(从节点 1 到节点 2) + 1(在节点 2 等待)+ 5(从节点 2 到节点 5) = 11 秒。

**方法:**给定的问题可以使用[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)和[迪克斯特拉算法](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)来解决，因为这个问题类似于[最短路径问题](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)。按照以下步骤解决问题:

*   初始化一个[队列](https://www.geeksforgeeks.org/queue-data-structure/)，比如说 **Q** ，存储将要穿越的节点以及到达该节点所需的时间。
*   创建一个布尔数组，比如 **V** ，存储当前节点是否被访问。
*   将节点 1 和时间 0 作为一对推入队列 **Q** 。
*   考虑到总是绿灯，通过边缘需要 1 秒钟，然后简单地运行 BFS，找到从节点 1 到达节点 N 所需的最短时间，并将其存储在一个变量中，比如**时间**。
*   通过执行以下步骤，创建一个函数**查找时间**，如果穿越边缘需要 **C** 秒，并且在 **T** 秒后灯光颜色发生变化，则查找时间:
    *   将变量**和**初始化为 0，这将存储从节点 1 到达节点 N 所需的最短时间
    *   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，时间】**中迭代，并执行以下步骤:
        *   如果 **(ans/T) %2 = 1** ，则将 **ans** 的值修改为 **(ans/T + 1)* T + C** 。
        *   否则，将 **C** 添加到变量 **ans** 中。
*   打印 **ans** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find min edge
int minEdge(vector<vector<int> > X,int N, int M, int T, int C) {

    // Initialize queue and push [1, 0]
    queue<pair<int, int> > Q;
    Q.push({1, 0});

    // Create visited array to keep the
    // track if node is visited or not
    vector<int> V(N+1, false);

    // Run infinite loop
      int crnt, c;
    while(1) {

        crnt = Q.front().first;
          c = Q.front().second;
          Q.pop();

        // If node is N, terminate loop
        if (crnt == N)
            break;

        // Travel adjacent nodes of crnt
        for(int _ : X[crnt]) {
            // Check whether we visited previously or not
            if (!V[_]) {

                // Push into queue and make as true
                Q.push({_, c + 1});
                V[_] = true;
             }
         }
    }

    return c;
}

// Function to Find time required to reach 1 to N
int findTime(int T, int C, int c) {

    int ans = 0;
    for (int _ = 0; _ < c; _++) {

        // Check color of node is red or green
        if ((ans/T) % 2)

            // Add C sec from next green color time
            ans = (ans/T + 1)*T + C;
        else
            // Add C
            ans += C;
     }

    // Return the answer
    return ans;
}

// Driver Code
int main() {

    // Given Input
    int N = 5;
    int M = 5;
    int T = 3;
    int C = 5;
    vector<vector<int> > X{{}, {2, 3, 4}, {4, 5}, {1}, {1, 2}, {2}};

    // Function Call
    int c = minEdge(X, N, M, T, C);
    int ans = findTime(T, C, c);

    // Print total time
    cout << (ans) << endl;

    return 0;
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python program for the above approach

# Import library for Queue
from queue import Queue

# Function to find min edge
def minEdge():

    # Initialize queue and push [1, 0]
    Q = Queue()
    Q.put([1, 0])

    # Create visited array to keep the
    # track if node is visited or not
    V = [False for _ in range(N + 1)]

    # Run infinite loop
    while 1:
        crnt, c = Q.get()

        # If node is N, terminate loop
        if crnt == N:
            break

        # Travel adjacent nodes of crnt
        for _ in X[crnt]:
            # Check whether we visited previously or not
            if not V[_]:

                # Push into queue and make as true
                Q.put([_, c + 1])
                V[_] = True

    return c

# Function to Find time required to reach 1 to N
def findTime(c):
    ans = 0
    for _ in range(c):

        # Check color of node is red or green
        if (ans//T) % 2:

            # Add C sec from next green color time
            ans = (ans//T + 1)*T + C
        else:
            # Add C
            ans += C

    # Return the answer
    return ans

# Driver Code
if __name__ == "__main__":

    # Given Input
    N = 5
    M = 5
    T = 3
    C = 5
    X = [[], [2, 3, 4], [4, 5], [1], [1, 2], [2]]

    # Function Call
    c = minEdge()
    ans = findTime(c)

    # Print total time
    print(ans)
```

**Output**

```
11
```

***时间复杂度:** O(N + M)*
***空间复杂度:** O(N + M)*