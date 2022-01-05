# 2D 二进制数组中的最佳交汇点

> 原文:[https://www . geesforgeks . org/best-meeting-point-2d-binary-array/](https://www.geeksforgeeks.org/best-meeting-point-2d-binary-array/)

给你一个值为 0 或 1 的 2D 网格，其中每个 1 代表一个组中某个人的家。而两个或两个以上的人组成的群体希望见面并尽量减少总的旅行距离。他们可以在任何地方见面，这意味着可能有家，也可能没有家。

*   距离使用曼哈顿距离计算，其中距离(p1，p2)= | p2 . x–P1 . x |+| p2 . y–P1 . y |。
*   找出到达最佳会合点需要行驶的总距离(总行驶距离最小)。

![](img/0578f12373bfd2ff223c972f88d954bb.png)

示例:

```
Input : grid[][] = {{1, 0, 0, 0, 1}, 
                   {0, 0, 0, 0, 0},
                   {0, 0, 1, 0, 0}};
Output : 6
Best meeting point is (0, 2).
Total distance traveled is 2 + 2 + 2 = 6

Input : grid[3][5] = {{1, 0, 1, 0, 1},
                     {0, 1, 0, 0, 0}, 
                     {0, 1, 1, 0, 0}};
Output : 11
```

**步骤:-**
1)存储所有组成员的所有水平和垂直位置。
2)现在排序，找到最小中间位置，这将是最佳的交汇点。
3)找出所有成员距离最佳会合点的距离。
例如上图中，水平位置为{0，2，0}，垂直位置为{0，2，4}。对两者进行排序后，我们得到{0，0，2}和{0，2，4}。中间点是(0，2)。
**注:**即使 1 号有两个中间点，也有效。两个中间点意味着它总是有两个最佳交汇点。两种情况给出的距离相同。所以我们只考虑一个最佳的会合点，以避免更多的开销，因为我们的目标只是找到距离。

## C++

```
/* C++ program to find best meeting point in 2D array*/
#include <bits/stdc++.h>
using namespace std;
#define ROW 3
#define COL 5

int minTotalDistance(int grid[][COL]) {
    if (ROW == 0 || COL == 0)
         return 0;

    vector<int> vertical;
    vector<int> horizontal;

    // Find all members home's position
    for (int i = 0; i < ROW; i++) {
        for (int j = 0; j < COL; j++) {
            if (grid[i][j] == 1) {
                vertical.push_back(i);
                horizontal.push_back(j);
            }
        }
    }

    // Sort positions so we can find most
    // beneficial point
    sort(vertical.begin(),vertical.end());
    sort(horizontal.begin(),horizontal.end());

    // middle position will always beneficial
    // for all group members but it will be
    // sorted which we have already done
    int size = vertical.size()/2;
    int x = vertical[size];
    int y = horizontal[size];

    // Now find total distance from best meeting
    // point (x,y) using Manhattan Distance formula
    int distance = 0;
    for (int i = 0; i < ROW; i++)
        for (int j = 0; j < COL; j++)
            if (grid[i][j] == 1)
                distance += abs(x - i) + abs(y - j);

    return distance;
}

// Driver program to test above functions
int main() {
    int grid[ROW][COL] = {{1, 0, 1, 0, 1}, {0, 1, 0, 0, 0},{0, 1, 1, 0, 0}};
    cout << minTotalDistance(grid);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to find best
meeting point in 2D array*/
import java.util.*;

class GFG
{

static int ROW = 3;
static int COL =5 ;

static int minTotalDistance(int grid[][])
{
    if (ROW == 0 || COL == 0)
        return 0;

    Vector<Integer> vertical = new Vector<Integer>();
    Vector<Integer> horizontal = new Vector<Integer>();

    // Find all members home's position
    for (int i = 0; i < ROW; i++)
    {
        for (int j = 0; j < COL; j++)
        {
            if (grid[i][j] == 1)
            {
                vertical.add(i);
                horizontal.add(j);
            }
        }
    }

    // Sort positions so we can find most
    // beneficial point
    Collections.sort(vertical);
    Collections.sort(horizontal);

    // middle position will always beneficial
    // for all group members but it will be
    // sorted which we have already done
    int size = vertical.size() / 2;
    int x = vertical.get(size);
    int y = horizontal.get(size);

    // Now find total distance from best meeting
    // point (x,y) using Manhattan Distance formula
    int distance = 0;
    for (int i = 0; i < ROW; i++)
        for (int j = 0; j < COL; j++)
            if (grid[i][j] == 1)
                distance += Math.abs(x - i) +
                Math.abs(y - j);

    return distance;
}

// Driver code
public static void main(String[] args)
{
    int grid[][] = {{1, 0, 1, 0, 1},
                    {0, 1, 0, 0, 0},
                    {0, 1, 1, 0, 0}};
    System.out.println(minTotalDistance(grid));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to find best meeting point in 2D array
ROW = 3
COL = 5

def minTotalDistance(grid: list) -> int:
    if ROW == 0 or COL == 0:
        return 0

    vertical = []
    horizontal = []

    # Find all members home's position
    for i in range(ROW):
        for j in range(COL):
            if grid[i][j] == 1:
                vertical.append(i)
                horizontal.append(j)

    # Sort positions so we can find most
    # beneficial point
    vertical.sort()
    horizontal.sort()

    # middle position will always beneficial
    # for all group members but it will be
    # sorted which we have already done
    size = len(vertical) // 2
    x = vertical[size]
    y = horizontal[size]

    # Now find total distance from best meeting
    # point (x,y) using Manhattan Distance formula
    distance = 0
    for i in range(ROW):
        for j in range(COL):
            if grid[i][j] == 1:
                distance += abs(x - i) + abs(y - j)

    return distance

# Driver Code
if __name__ == "__main__":

    grid = [[1, 0, 1, 0, 1],
            [0, 1, 0, 0, 0],
            [0, 1, 1, 0, 0]]
    print(minTotalDistance(grid))

# This code is contributed by
# sanjeev2552
```

## C#

```
/* C# program to find best
meeting point in 2D array*/
using System;
using System.Collections.Generic;

class GFG
{

static int ROW = 3;
static int COL = 5 ;

static int minTotalDistance(int [,]grid)
{
    if (ROW == 0 || COL == 0)
        return 0;

    List<int> vertical = new List<int>();
    List<int> horizontal = new List<int>();

    // Find all members home's position
    for (int i = 0; i < ROW; i++)
    {
        for (int j = 0; j < COL; j++)
        {
            if (grid[i, j] == 1)
            {
                vertical.Add(i);
                horizontal.Add(j);
            }
        }
    }

    // Sort positions so we can find most
    // beneficial point
    vertical.Sort();
    horizontal.Sort();

    // middle position will always beneficial
    // for all group members but it will be
    // sorted which we have already done
    int size = vertical.Count / 2;
    int x = vertical[size];
    int y = horizontal[size];

    // Now find total distance from best meeting
    // point (x,y) using Manhattan Distance formula
    int distance = 0;
    for (int i = 0; i < ROW; i++)
        for (int j = 0; j < COL; j++)
            if (grid[i, j] == 1)
                distance += Math.Abs(x - i) +
                Math.Abs(y - j);

    return distance;
}

// Driver code
public static void Main(String[] args)
{
    int [,]grid = {{1, 0, 1, 0, 1},
                    {0, 1, 0, 0, 0},
                    {0, 1, 1, 0, 0}};
    Console.WriteLine(minTotalDistance(grid));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
/* Javascript program to find best
meeting point in 2D array*/

let ROW = 3;
let COL =5 ;

function minTotalDistance(grid)
{
    if (ROW == 0 || COL == 0)
        return 0;

    let vertical = [];
    let horizontal = [];

    // Find all members home's position
    for (let i = 0; i < ROW; i++)
    {
        for (let j = 0; j < COL; j++)
        {
            if (grid[i][j] == 1)
            {
                vertical.push(i);
                horizontal.push(j);
            }
        }
    }

    // Sort positions so we can find most
    // beneficial point
    (vertical).sort(function(a,b){return a-b;});
    (horizontal).sort(function(a,b){return a-b;});

    // middle position will always beneficial
    // for all group members but it will be
    // sorted which we have already done
    let size = vertical.length / 2;
    let x = vertical[size];
    let y = horizontal[size];

    // Now find total distance from best meeting
    // point (x,y) using Manhattan Distance formula
    let distance = 0;
    for (let i = 0; i < ROW; i++)
        for (let j = 0; j < COL; j++)
            if (grid[i][j] == 1)
                distance += Math.abs(x - i) +
                Math.abs(y - j);

    return distance;
}

// Driver code
let grid = [[1, 0, 1, 0, 1],
                    [0, 1, 0, 0, 0],
                    [0, 1, 1, 0, 0]];
document.write(minTotalDistance(grid));

// This code is contributed by rag2127
</script>
```

**输出:**

```
11
```

**时间复杂度:**O(M * N)
T3】辅助空间: O(N)
本文由 **Harshit Agrawal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。