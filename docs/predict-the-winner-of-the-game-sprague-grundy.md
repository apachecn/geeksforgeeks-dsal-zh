# 预测比赛的胜者|斯普拉格-格伦迪

> 原文:[https://www . geesforgeks . org/predict-the-winner-the-game-Sprague-grundy/](https://www.geeksforgeeks.org/predict-the-winner-of-the-game-sprague-grundy/)

给定一个 4×4 二元矩阵。两个玩家 A 和 B 在玩一个游戏，在每一步中，一个玩家可以选择任何一个 1 都在里面的矩形，并用 0 替换所有的 1。不能选择任何矩形的玩家输掉游戏。预测游戏中的赢家，假设他们都以最佳状态玩游戏，A 开始游戏。

**示例:**

> **输入:**
> 0 1 1 0
> 0 0 0 0 0
> 0 0 0 0
> 0 0 0 1
> **输出:** A
> 步骤 1:玩家 A 在位置(1，2)选择单个 1 的矩形，因此新矩阵变为
> 0 0 1 0
> 0 0 0
> 0 0 0
> 0 0 1
> 
> 第二步:玩家 B 在位置(1，3)选择单个的矩形，那么新矩阵就变成了
> 0 0 0 0
> 0 0 0 0
> 0 0 0
> 0 0 0 1
> 
> 第三步:玩家 A 在位置(4，4)选择单个矩形，新矩阵变为
> 0 0 0 0
> 0 0 0 0
> 0 0 0 0
> 0 0 0 0 0 0 0
> 
> 第四步:玩家乙不能移动，因此甲赢得游戏。
> 
> **输入:**
> 0 0 1 0
> 0 0 0 0
> 0 0 0 0
> 0 0 1
> T7】输出: B

**方法:**这个问题可以用[斯普拉格-格鲁迪](https://www.geeksforgeeks.org/combinatorial-game-theory-set-4-sprague-grundy-theorem/)定理来解决。Sprague-Grundy 的基本情况是 Grundy[0] = 0，即矩阵中的所有位置都用 0 填充，然后 B 获胜，因此为 0。在 grundy 中，我们递归地用所有可能的状态调用 grundy 函数。

4×4 矩阵可以表示为一个二进制 16 位数，在 int 中为 65535，其中每一位代表矩阵中的位置。以下是解决上述问题的步骤。

*   将矩阵转换为 int val。
*   使用 val 调用递归函数，该函数使用 memoization 生成 grundy 值。
*   在递归函数中，所有的 grundy 状态都可以通过生成所有可能的矩形来访问(循环使用四个矩形)。
*   检查生成的矩形，如果它是矩阵的矩形。那这就是格鲁迪要去的州。
*   使用 MEX 获取 Grundy 值，请参见[本](https://www.geeksforgeeks.org/combinatorial-game-theory-set-4-sprague-grundy-theorem/)。
*   如果递归返回 0，那么玩家 B 赢，否则玩家 A 赢。

下面是上述方法的实现

```
#include <bits/stdc++.h>
using namespace std;

// Gets the max value
int getMex(const unordered_set<int>& s)
{
    int mex = 0;
    while (s.find(mex) != s.end())
        mex++;
    return mex;
}

// Find check if the rectangle is a part of the
// the original rectangle
int checkOne(int mat, int i, int j, int k, int l)
{

    // initially create the bitset
    // of original intValue
    bitset<16> m(mat);

    // Check if it is a part of the rectangle
    for (int x = i; x <= j; x++) {
        for (int y = k; y <= l; y++) {
            int pos = 15 - ((x * 4) + y);

            // If not set, then not part
            if (!m.test(pos)) {
                return -1;
            }
            m.reset(pos);
        }
    }

    // If part of rectangle
    // then convert to int again and return
    int res = m.to_ullong();
    return res;
}

// Recursive function to get the grundy value
int getGrundy(int pos, int grundy[])
{

    // If state has been visited
    if (grundy[pos] != -1)
        return grundy[pos];

    // For obtaining the MEX value
    unordered_set<int> gSet;

    // Generate all the possible rectangles
    for (int i = 0; i <= 3; i++) {
        for (int j = i; j <= 3; j++) {
            for (int k = 0; k <= 3; k++) {
                for (int l = k; l <= 3; l++) {

                    // check if it is part of the original
                    // rectangle, if yes then get the int value
                    int res = checkOne(pos, i, j, k, l);

                    // If it is a part of original matrix
                    if (res != -1) {

                        // Store the grundy value
                        // Memorize
                        grundy[res] = getGrundy(res, grundy);

                        // Find MEX
                        gSet.insert(grundy[res]);
                    }
                }
            }
        }
    }

    // Return the MEX
    return getMex(gSet);
}

// Conver the matrix to INT
int toInt(int matrix[4][4])
{
    int h = 0;

    // Traverse in the matrix
    for (int i = 0; i < 4; ++i)
        for (int j = 0; j < 4; ++j)
            h = 2 * h + matrix[i][j];
    return h;
}

// Driver Code
int main()
{
    int mat[4][4] = { { 0, 1, 1, 0 },
                      { 0, 0, 0, 0 },
                      { 0, 0, 0, 0 },
                      { 0, 0, 0, 1 } };

    // Get the int value of the matrix
    int intValue = toInt(mat);

    int grundy[intValue + 1];

    // Initially with -1
    // used for memoization
    memset(grundy, -1, sizeof grundy);

    // Base case
    grundy[0] = 0;

    // If returned value is non-zero
    if (getGrundy(intValue, grundy))
        cout << "Player A wins";
    else
        cout << "Player B wins";

    return 0;
}
```

**Output:**

```
Player A wins

```

**时间复杂度:**

O(N)
**辅助空间:** O(N)