# 将雨水收集在矩阵中

> 原文:[https://www . geesforgeks . org/trapping-雨-水-在矩阵中/](https://www.geeksforgeeks.org/trapping-rain-water-in-a-matrix/)

给定一个由正整数组成的维度为 **M*N** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**arr【】【】【】T3】，其中**arr【I】【j】**代表每个单元电池的高度，任务是找出雨后困在矩阵中的水的总体积。**

**示例:**

> **输入:** arr[][] = {{4，2，7}，{2，1，10}，{5，10，2}}
> **输出:** 1
> **解释:**
> 雨水可以通过以下方式被困:
> 
> 1.  细胞，{(0，0)、(0，1)、(0，2)、(1，0)、(1，2)、(2，0)、(2，1)、(2，2)}捕捉0 单位体积的雨水，因为所有的水都从基质中流出，因为细胞在边界上。
> 2.  单元(2，2)在单元{(0，1)、(1，0)、(1，2)和(2，1)}之间截留 1 单位体积的雨水。
> 
> 因此，总共有 1 单位体积的雨水被截留在基质内。
> 
> **输入:** arr[][] = {{1，4，3，1，3，2}，{3，2，1，3，2，4}，{2，3，3，2，3，1}}
> **输出:** 4

**方法:**给定的问题可以使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)和[最小堆](https://www.geeksforgeeks.org/min-heap-in-java/)来解决。按照以下步骤解决问题:

*   使用[优先级队列](https://www.geeksforgeeks.org/stl-priority-queue-for-structure-or-class/)初始化[最小堆](https://www.geeksforgeeks.org/implement-min-heap-using-stl/)，比如 **PQ** ，以存储单元的位置对及其高度。
*   推送 **PQ** 中的所有边界单元格，并将所有推送的单元格标记为已访问。
*   初始化两个变量，说 **ans** 为 **0** 和 **maxHeight** 为 **0** ，分别存储 **PQ** 中所有单元格的总体积和最大高度。
*   重复[直到 **PQ** 不为空](https://www.geeksforgeeks.org/priority_queueempty-priority_queuesize-c-stl/)并执行以下步骤:
    *   [将 **PQ**](https://www.geeksforgeeks.org/priority_queuetop-c-stl/) 的顶部节点存储在一个变量中，前面说**，[擦除 **PQ** 的顶部元素](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)。**
    *   **将**最大高度**的值更新为**最大高度**和**前高度**的最大值。**
    *   **现在，[遍历当前单元格**的所有相邻节点**](https://www.geeksforgeeks.org/find-all-reachable-nodes-from-every-node-present-in-a-given-set/)(前面。x，前面。Y) 并执行以下操作:

        *   如果相邻单元格有效，即该单元格未超出界限且尚未被访问，则将相邻单元格的值推入 **PQ。**
        *   如果相邻单元格的高度小于**最大高度**，则按**最大高度**与相邻单元格的高度之差增加**和**。** 
*   **最后，完成上述步骤后，打印**和**的值，作为雨后积水的结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores the direction of all the
// adjacent cells
vector<vector<int> > dir
    = { { -1, 0 }, { 0, 1 }, { 1, 0 }, { 0, -1 } };

// Node structure
struct node {

    int height;
    int x, y;
};

// Comparator function to implement
// the min heap using priority queue
struct Compare {

    // Comparator function
    bool operator()(node const& a, node const& b)
    {
        return a.height > b.height;
    }
};

// Function to find the amount of water
// the matrix is capable to hold
int trapRainWater(vector<vector<int> >& heightMap)
{
    int M = heightMap.size();
    int N = heightMap[0].size();

    // Stores if a cell of the matrix
    // is visited or not
    vector<vector<bool> > visited(M,
                                  vector<bool>(N, false));

    // Initialize a priority queue
    priority_queue<node, vector<node>, Compare> pq;

    // Traverse over the matrix
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++) {

            // If element is not on
            // the boundary
            if (!(i == 0 || j == 0 || i == M - 1
                  || j == N - 1))
                continue;

            // Mark the current cell
            // as visited
            visited[i][j] = true;

            // Node for priority queue
            node t;
            t.x = i;
            t.y = j;
            t.height = heightMap[i][j];

            // Pushe all the adjacent
            // node in the pq
            pq.push(t);
        }
    }

    // Stores the total volume
    int ans = 0;

    // Stores the maximum height
    int max_height = INT_MIN;

    // Iterate while pq is not empty
    while (!pq.empty()) {

        // Store the top node of pq
        node front = pq.top();

        // Delete the top element of pq
        pq.pop();

        // Update the max_height
        max_height = max(max_height, front.height);

        // Stores the position of the
        // current cell
        int curr_x = front.x;
        int curr_y = front.y;

        for (int i = 0; i < 4; i++) {

            int new_x = curr_x + dir[i][0];
            int new_y = curr_y + dir[i][1];

            // If adjacent cells are out
            // of bound or already visited
            if (new_x < 0 || new_y < 0 || new_x >= M
                || new_y >= N || visited[new_x][new_y]) {
                continue;
            }

            // Stores the height of the
            // adjacent cell
            int height = heightMap[new_x][new_y];

            // If height of current cell
            // is smaller than max_height
            if (height < max_height) {

                // Increment the ans by
                // (max_height-height)
                ans = ans + (max_height - height);
            }

            // Define a new node
            node temp;
            temp.x = new_x;
            temp.y = new_y;
            temp.height = height;

            // Push the current node
            // in the pq
            pq.push(temp);

            // Mark the current cell
            // as visited
            visited[new_x][new_y] = true;
        }
    }

    return ans;
}

// Driver Code
int main()
{
    vector<vector<int> > arr = { { 1, 4, 3, 1, 3, 2 },
                                 { 3, 2, 1, 3, 2, 4 },
                                 { 2, 3, 3, 2, 3, 1 } };
    cout << trapRainWater(arr);

    return 0;
}
```

****Output**

```
4
```** 

*****时间复杂度:**(N * M * log(N * M))*
***辅助空间:** O(N * M)***