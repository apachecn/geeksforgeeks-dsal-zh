# 在给定的布尔矩阵中找到最常见区域大小的区域

> 原文:[https://www . geeksforgeeks . org/find-区域-具有给定布尔矩阵中最常见的区域大小/](https://www.geeksforgeeks.org/find-regions-with-most-common-region-size-in-a-given-boolean-matrix/)

给定一个大小为 **N*M** 的布尔 [2D 阵列](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)、 **arr[][]** ，其中一组相连的 1 形成一个岛。如果两个单元在水平方向、垂直方向或对角方向上相邻，则称它们是相连的。任务是找到所有具有最常见区域大小的区域的左上角的位置。

**示例:**

> **输入:** arr[][] = {{0，0，1，1，0}，
> {1，0，1，0}，
> {0，0，0，0，0}，
> {0，0，0，0，1}}
> **输出:** {1，0}，{3，4}
> **说明:**共有 3 个区域，两个区域长度为 1，另一个区域长度为 4。所以最常见区域的长度是 1，这些区域的位置是{1，0}，{3，4}。
> 
> **输入:** arr[][] = {{0，0，1，1，0}，
> {0，0，1，0}，
> {0，0，0，0，0}，
> {0，0，0，0，1}}
> **输出:** {0，2}
> **说明:**共有 2 个区域，一个区域长度为 1，另一个区域长度为 4。由于两个区域具有相同的频率，因此两者都是最常见的区域。因此，打印任何一个区域的位置。

**方法:**这个想法是基于在布尔 2D 矩阵中寻找[岛数量的问题。这个想法是将区域的大小以及左上角的位置存储在一个](https://www.geeksforgeeks.org/find-number-of-islands/)[散列表](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)中。然后[遍历 hashmap](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) 找到最常见的区域，打印出需要的区域。按照以下步骤解决问题:

*   初始化一个[散列表](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) 来存储区域的大小和左上角的位置。
*   维护一个被访问的数组来跟踪所有被访问的单元。
*   [逐行遍历给定的 2D 数组](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)，如果当前元素为“1”且未被访问，则从该节点开始执行 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)。遍历后，在地图中存储区域的大小。
*   完成以上步骤后，[遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)找到最常见的区域，然后打印出地图中与按键对应的所有位置。**T3】**

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define ROW 4
#define COL 5

// Function to check if a given cell
// can be included in DFS
int isSafe(int M[][COL], int row, int col,
           bool visited[][COL])
{
    return (row >= 0)
 && (row < ROW) && (col >= 0)
           && (col < COL)
           && (M[row][col] 
&& !visited[row][col]);
}

// Utility function to do DFS for a 2D
// boolean matrix
void DFS(int M[][COL], int row, int col,
         bool visited[][COL], int& count)
{
    // Initialize arrays to get row and column
    // numbers of 8 neighbours of a given cell
    static int rowNbr[] 
= { -1, -1, -1, 0, 0, 1, 1, 1 };
    static int colNbr[] 
= { -1, 0, 1, -1, 1, -1, 0, 1 };

    // Mark this cell as visited
    visited[row][col] = true;

    // Recur for all connected neighbours
    for (int k = 0; k < 8; ++k) {
        if (isSafe(M, row + rowNbr[k], 
col + colNbr[k], visited)) {

            // Increment region length by one
            count++;
            DFS(M, row + rowNbr[k], col + colNbr[k],
                visited, count);
        }
    }
}

// Function to find all the regions with most
// common length in the given boolean 2D matrix
void commonRegion(int M[][COL])
{
    // Make a bool array to mark visited cells,
    // initially all cells are unvisited
    bool visited[ROW][COL];
    memset(visited, 0, sizeof(visited));

    // Map to store the size and the regions
    unordered_map<int, vector<vector<int> > > um;

    // Traverse through the
    // all cells of given matrix
    for (int i = 0; i < ROW; ++i) {
        for (int j = 0; j < COL; ++j) {

            // If the current cell is 1 and is
            // not visited
            if (M[i][j] && !visited[i][j]) {

                // Increment count by 1
                int count = 1;

                // Perform DFS
                DFS(M, i, j, visited, count);
                um[count].push_back({ i, j });
            }
        }
    }

    // Store the most common region length
    int mostCommonRegion = 0;

    // Traverse the map to find the most common
    // region length
    for (auto it = um.begin(); it != um.end(); it++) {
        int x = it->second.size();
        mostCommonRegion = max(mostCommonRegion, x);
    }

    // Traverse the map to print the regions
    // having most common length
    for (auto it = um.begin(); it != um.end(); it++) {

        int x = it->second.size();
        if (mostCommonRegion == x) {

            // Print the top left position
// of the regions
            for (int i = 0; i < it->second.size(); i++) {
                int x = it->second[i][0];
                int y = it->second[i][1];
                cout << "{" << x << ", " << y << "}, ";
            }
            break;
        }
    }
}

// Driver code
int main()
{
    // Given Input
    int arr[][COL] = { { 0, 0, 1, 1, 0 },
                       { 1, 0, 1, 1, 0 },
                       { 0, 0, 0, 0, 0 },
                       { 0, 0, 0, 0, 1 } };

    // Function call
    commonRegion(arr);

    return 0;
}
```

**Output**

```
{1, 0}, {3, 4}, 
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N*M)*