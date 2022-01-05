# 兔舍|谷歌 Kickstart 2021 轮

> 原文:[https://www . geesforgeks . org/rabbit-house-Google-kickstart-2021-round-a/](https://www.geeksforgeeks.org/rabbit-house-google-kickstart-2021-round-a/)

芭芭拉去年在学校成绩非常好，所以她的父母决定送她一只宠物兔子。她太兴奋了，为兔子建了一个房子，可以看做是一个有 RR 行和 CC 列的 2D 网格。

兔子喜欢跳，所以芭芭拉在格子的几个格子上叠了几个盒子。每个框都是一个具有相等维度的立方体，这些维度与网格中一个单元格的维度完全匹配。

然而，芭芭拉很快意识到兔子跳超过 11 格的高度可能是危险的，所以她决定通过对房子进行一些调整来避免这种情况。对于每一对相邻的牢房，芭芭拉希望它们的绝对高度差最多为 11 格。如果两个单元共享一条公共边，则它们被认为是相邻的。

由于所有的盒子都是用强力胶粘起来的，芭芭拉无法移除任何最初在那里的盒子，但是她可以在它们上面添加盒子。她可以添加任意多个框，添加任意多个单元格(可能为零)。帮助她确定要添加的最小盒子总数，以便兔子的房子是安全的。

运筹学

给定一个由 **R** 行和 **M** 列组成的矩阵。仅通过增加单元格值，使相邻单元格之间的绝对差值小于或等于 1。单元格上的总增量应该最小化。任务是返回完成的最小增量操作。

**示例:**

> **输入:**【【0 0 0】、
> 【0 2 0】、
> 【0 0 0】】
> **输出:** 4
> **说明:**网格中间的单元格高度绝对差为 2，其所有四个相邻单元格的高度正好增加 1 个单位，这样
> 任意一对相邻单元格的绝对差最多为 1。结果矩阵将是:
> [[0 1 0]，
> [1 2 1]，
> [0 1 0]]
> 
> **输入:**[【1 0 5 4 2】，
> 【1 5 6 4 8】，
> 【2 3 4 2 1】，
> 【2 3 4 9 8】]
> 
> **输出:** 52
> **解释:**结果矩阵将为:【【3 4 5 6 7】，
> 【4 5 6 7 8】，
> 【5 6 7 8】，
> 【6 7 8 9 8】

**方法:**给定问题可以使用多源[迪克斯特拉算法](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-using-set-in-stl/)来解决。方法是将值最大的信元存储在[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)中，逐个弹出优先级队列，并相应更新相邻信元，在更新信元值的同时，我们也将更新我们的优先级队列。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

void solve(long long int r, long long int c,
           vector<vector<long long int> >& grid)
{
    priority_queue<pair<long long int,
                        pair<long long int, long long int> > >
        pq;

    for (long long int i = 0; i < r; i++) {
        for (long long int j = 0; j < c; j++) {
            pq.push(make_pair(grid[i][j],
                              make_pair(i, j)));
        }
    }

    long long int res = 0;

    while (!pq.empty()) {
        long long int height = pq.top().first,
                      i = pq.top().second.first,
                      j = pq.top().second.second;
        pq.pop();
        if (height != grid[i][j])
            continue;
        if (i == 0) {
            // Down
            if (i != r - 1) {
                if (grid[i + 1][j] < height - 1) {

                    res += height - 1 - grid[i + 1][j];
                    grid[i + 1][j] = height - 1;

                    pq.push(make_pair(height - 1,
                                      make_pair(i + 1, j)));
                }
            }
            // Left
            if (j != 0) {
                if (grid[i][j - 1] < height - 1) {

                    res += height - 1 - grid[i][j - 1];
                    grid[i][j - 1] = height - 1;

                    pq.push(make_pair(height - 1,
                                      make_pair(i, j - 1)));
                }
            }
            // Right
            if (j != c - 1) {
                if (grid[i][j + 1] < height - 1) {

                    res += height - 1 - grid[i][j + 1];
                    grid[i][j + 1] = height - 1;

                    pq.push(make_pair(height - 1,
                                      make_pair(i, j + 1)));
                }
            }
        }
        else if (i == r - 1) {
            // Up
            if (i != 0) {
                if (grid[i - 1][j] < height - 1) {

                    res += height - 1 - grid[i - 1][j];
                    grid[i - 1][j] = height - 1;

                    pq.push(make_pair(height - 1,
                                      make_pair(i - 1, j)));
                }
            }
            // Left
            if (j != 0) {
                if (grid[i][j - 1] < height - 1) {

                    res += height - 1 - grid[i][j - 1];
                    grid[i][j - 1] = height - 1;

                    pq.push(make_pair(height - 1,
                                      make_pair(i, j - 1)));
                }
            }
            // Right
            if (j != c - 1) {
                if (grid[i][j + 1] < height - 1) {

                    res += height - 1 - grid[i][j + 1];
                    grid[i][j + 1] = height - 1;

                    pq.push(make_pair(height - 1,
                                      make_pair(i, j + 1)));
                }
            }
        }
        else {
            // Down
            if (grid[i + 1][j] < height - 1) {

                res += height - 1 - grid[i + 1][j];
                grid[i + 1][j] = height - 1;

                pq.push(make_pair(height - 1,
                                  make_pair(i + 1, j)));
            }
            // Up
            if (grid[i - 1][j] < height - 1) {

                res += height - 1 - grid[i - 1][j];
                grid[i - 1][j] = height - 1;

                pq.push(make_pair(height - 1,
                                  make_pair(i - 1, j)));
            }
            // Left
            if (j != 0) {
                if (grid[i][j - 1] < height - 1) {

                    res += height - 1 - grid[i][j - 1];
                    grid[i][j - 1] = height - 1;

                    pq.push(make_pair(height - 1,
                                      make_pair(i, j - 1)));
                }
            }
            // Right
            if (j != c - 1) {
                if (grid[i][j + 1] < height - 1) {

                    res += height - 1 - grid[i][j + 1];
                    grid[i][j + 1] = height - 1;

                    pq.push(make_pair(height - 1,
                                      make_pair(i, j + 1)));
                }
            }
        }
    }
    cout << res;
}

// Driver code
int main()
{

    long long int r = 4, c = 5;
    vector<vector<long long int> > grid{ { 1, 0, 5, 4, 2 },
                                         { 1, 5, 6, 4, 8 },
                                         { 2, 3, 4, 2, 1 },
                                         { 2, 3, 4, 9, 8 } };

    solve(r, c, grid);
}
```

**Output:**

```
52

```

**时间复杂度:** O(RM * Log(RM))
**辅助空间:** O(RM)