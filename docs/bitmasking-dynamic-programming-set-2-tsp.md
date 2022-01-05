# 位屏蔽和动态编程| Set-2 (TSP)

> 原文:[https://www . geesforgeks . org/bit masking-dynamic-programming-set-2-tsp/](https://www.geeksforgeeks.org/bitmasking-dynamic-programming-set-2-tsp/)

在这篇文章中，我们将使用我们的动态编程和位屏蔽技术的知识来解决一个著名的 NP 难问题“旅行推销员问题”。
在解决问题之前，我们假设读者具备
的知识

*   [DP 与 DP 过渡关系的形成](https://www.geeksforgeeks.org/solve-dynamic-programming-problem/)
*   [DP 中的位屏蔽](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)
*   [旅行推销员问题](https://www.geeksforgeeks.org/travelling-salesman-problem-set-1/)

要理解这个概念，让我们考虑以下问题:
**问题描述** :

```
Given a 2D grid of characters representing 
a town where '*' represents the 
houses, '#' represents the blockage, 
'.' represents the vacant street 
area. Currently you are (0, 0) position.

Our task is to determine the minimum distance 
to be moved to visit all the houses and return
to our initial position at (0, 0). You can 
only move to adjacent cells that share exactly
1 edge with the current cell.
```

上述问题就是大家熟知的旅行推销员问题。
第一部分是计算两个像元之间的最小距离。我们可以通过简单地使用 BFS 来实现，因为所有的距离都是单位距离。为了优化我们的解决方案，我们将预先计算距离，将初始位置和房屋位置作为 BFS 的来源点。
每次 BFS 遍历需要 O(网格大小)时间。因此，整体预算是 **O(X * size_of_grid)** ，其中 X =房屋数量+ 1(初始位置)
**<u>现在让我们考虑一个 DP 状态</u>**
这样我们将需要跟踪被访问的房屋和最后被访问的房屋来唯一地识别这个问题中的一个状态。
因此，我们将把 **dp【索引】【掩码】**作为我们的 dp 状态。

在这里，
**索引**:告诉我们当前房屋的位置
**:掩码**:告诉我们被访问的房屋(如果掩码中设置了 ith 位，那么这意味着 ith 脏瓷砖被清理了)

而 dp[index][mask]将告诉我们访问 X(mask 中的设置位数)房屋的最小距离，该距离对应于它们在 mask 中出现的顺序，其中最后访问的房屋是位置索引处的房屋。
**<u>状态转换关系</u>**
所以我们的初始状态将是**DP【0】【0】**这告诉我们当前处于初始瓦片，这是我们的初始位置，掩码为 0，表示到目前为止没有房屋被访问。
而我们最终的目的地状态将是 **dp【任意指数】【LIMIT _ MASK】**，这里 LIMIT _ MASK =**(1<<N)–1**
N =房屋数量。
因此我们的差压状态转换可以表述为

```
dp(curr_idx)(curr_mask) = min{
    for idx : off_bits_in_curr_mask
       dp(idx)(cur_mask.set_bit(idx)) + dist[curr_idx][idx]
}
```

上述关系可以被可视化为通过站在 curr_idx house 并且通过已经访问 cur _ mask houses 来访问所有房屋的最小距离等于 curr_idx house 和 idx house 之间的最小距离+通过站在 idx house 并且通过已经访问(**cur _ mask |(1<<【idx)**)房屋来访问所有房屋的最小距离。
因此，这里我们迭代所有可能的 idx 值，使得 cur_mask 的 i <sup>第</sup>位为 0，这告诉我们 i <sup>第</sup>座房屋未被访问。
每当我们有了我们的 mask = LIMIT_MASK，这意味着我们已经参观了镇上所有的房子。因此，我们将添加从最后访问的城镇(即 cur_idx 位置的城镇)到初始位置(0，0)的距离。
上述实现的 C++程序如下:

## C++

```
#include <bits/stdc++.h>
using namespace std;

#define INF 99999999
#define MAXR 12
#define MAXC 12
#define MAXMASK 2048
#define MAXHOUSE 12

// stores distance taking source
// as every dirty tile
int dist[MAXR][MAXC][MAXHOUSE];

// memoization for dp states
int dp[MAXHOUSE][MAXMASK];

// stores coordinates for
// dirty tiles
vector < pair < int, int > > dirty;

// Directions
int X[] = {-1, 0, 0, 1};
int Y[] = {0, 1, -1, 0};

char arr[21][21];

// len : number of dirty tiles + 1
// limit : 2 ^ len -1
// r, c : number of rows and columns
int len, limit, r, c;

// Returns true if current position
// is safe to visit
// else returns false
// Time Complexity : O(1)
bool safe(int x, int y)
{
    if (x >= r or y>= c or x<0 or y<0)
       return false;
    if (arr[x][y] == '#')
       return false;
    return true;
}

// runs BFS traversal at tile idx
// calculates distance to every cell
// in the grid
// Time Complexity : O(r*c)
void getDist(int idx){

    // visited array to track visited cells
    bool vis[21][21];
    memset(vis, false, sizeof(vis));

    // getting current position
    int cx = dirty[idx].first;
    int cy = dirty[idx].second;

    // initializing queue for bfs
    queue < pair < int, int > > pq;
    pq.push({cx, cy});

    // initializing the dist to max
    // because some cells cannot be visited
    // by taking source cell as idx
    for (int i = 0;i<= r;i++)
        for (int j = 0;j<= c;j++)
            dist[i][j][idx] = INF;

    // base conditions
    vis[cx][cy] = true;
    dist[cx][cy][idx] = 0;

    while (! pq.empty())
    {
        auto x = pq.front();
        pq.pop();
        for (int i = 0;i<4;i++)
        {
           cx = x.first + X[i];
           cy = x.second + Y[i];
           if (safe(cx, cy))
           {
               if (vis[cx][cy])
                   continue;
               vis[cx][cy] = true;
               dist[cx][cy][idx] = dist[x.first][x.second][idx] + 1;
               pq.push({cx, cy});
            }
         }
    }
}

// Dynamic Programming state transition recursion
// with memoization. Time Complexity: O(n*n*2 ^ n)
int solve(int idx, int mask)
{
    // goal state
    if (mask == limit)
       return dist[0][0][idx];

    // if already visited state
    if (dp[idx][mask] != -1)
       return dp[idx][mask];

    int ret = INT_MAX;

    // state transition relation
    for (int i = 0;i<len;i++)
    {
        if ((mask & (1<<i)) == 0)
        {
            int newMask = mask | (1<<i);
            ret = min( ret, solve(i, newMask)
                + dist[dirty[i].first][dirty[i].second][idx]);
        }
    }

    // adding memoization and returning
    return dp[idx][mask] = ret;
}

void init()
{
    // initializing containers
    memset(dp, -1, sizeof(dp));
    dirty.clear();

    // populating dirty tile positions
    for (int i = 0;i<r;i++)
        for (int j = 0;j<c;j++)
        {
            if (arr[i][j] == '*')
               dirty.push_back({i, j});
        }

    // inserting ronot's location at the
    // beginning of the dirty tile
    dirty.insert(dirty.begin(), {0, 0});

    len = dirty.size();

    // calculating LIMIT_MASK
    limit = (1<<len) - 1;

    // precalculating distances from all
    // dirty tiles to each cell in the grid
    for (int i = 0;i<len;i++)
       getDist(i);
}

int main(int argc, char const *argv[])
{
    // Test case #1:
    //     .....*.
    //     ...#...
    //     .*.#.*.
    //     .......

char A[4][7] = {    {'.', '.', '.', '.', '.', '*', '.'},
                    {'.', '.', '.', '#', '.', '.', '.'},
                    {'.', '*', '.', '#', '.', '*', '.'},
                    {'.', '.', '.', '.', '.', '.', '.'}
                };

    r = 4; c = 7;

    cout << "The given grid : " << endl;

    for (int i = 0;i<r;i++)
    {
        for (int j = 0;j<c;j++)
        {
            cout << A[i][j] << " ";
            arr[i][j] = A[i][j];
        }
        cout << endl;
    }

    // - initialization
    // - precalculations
    init();

    int ans = solve(0, 1);

    cout << "Minimum distance for the given grid : ";
    cout << ans << endl;

    // Test Case #2
    //     ...#...
    //     ...#.*.
    //     ...#...
    //     .*.#.*.
    //     ...#...

    char Arr[5][7] = {  {'.', '.', '.', '#', '.', '.', '.'},
                        {'.', '.', '.', '#', '.', '*', '.'},
                        {'.', '.', '.', '#', '.', '.', '.'},
                        {'.', '*', '.', '#', '.', '*', '.'},
                        {'.', '.', '.', '#', '.', '.', '.'}
                };

    r = 5; c = 7;

    cout << "The given grid : " << endl;

    for (int i = 0;i<r;i++)
    {
        for (int j = 0;j<c;j++)
        {
            cout << Arr[i][j] << " ";
            arr[i][j] = Arr[i][j];
        }
        cout << endl;
    }

    // - initialization
    // - precalculations
    init();
    ans = solve(0, 1);
    cout << "Minimum distance for the given grid : ";
    if (ans >= INF)
        cout << "not possible" << endl;
    else
        cout << ans << endl;

    return 0;
}
```

输出:

```
The given grid : 
. . . . . * . 
. . . # . . . 
. * . # . * . 
. . . . . . . 
Minimum distance for the given grid : 16
The given grid : 
. . . # . . . 
. . . # . * . 
. . . # . . . 
. * . # . * . 
. . . # . . . 
Minimum distance for the given grid : not possible
```

**注** :
我们用初始状态为**DP【0】【1】**是因为我们把起始位置推到了房屋集装箱中的第一个位置。因此，我们的位掩码将为 1，因为设置了第 0<sup>位，即我们已经访问了旅程的起始位置。
**时间复杂度** :
考虑房屋数量为 **n** 。因此，有 **n * (2 <sup>n</sup> )** 个状态，并且在每个状态，我们循环 n 个房屋以过渡到下一个状态，并且由于记忆，我们对每个状态只进行一次循环转换。因此，我们的时间复杂度是**O(n<sup>2</sup>* 2<sup>n</sup>)**。
**推荐** :</sup> 

*   [http://www.spoj.com/problems/CLEANRBT/](http://www.spoj.com/problems/CLEANRBT/)
*   [https://www . YouTube . com/watch？v=-JjA4BLQyqE](https://www.youtube.com/watch?v=-JjA4BLQyqE)

本文由 [**尼提什·库马尔**](https://www.linkedin.com/in/nk17kumar/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。