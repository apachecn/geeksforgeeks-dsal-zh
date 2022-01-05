# 找到不属于任何方块的坐标

> 原文:[https://www . geesforgeks . org/find-不属于任何方块的坐标/](https://www.geeksforgeeks.org/find-the-coordinate-that-does-not-belong-to-any-square/)

给定一个由 **(4 * N + 1)** 对坐标组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，这些坐标代表任何 **N** 个正方形的角的坐标，因此只有一个坐标不属于任何正方形，任务是找到那个不属于任何正方形的坐标。

**示例:**

> **输入:** N = 2，arr[] = { {0，0}，{0，1}，{0，2}，{1，0}，{1，1}，{1，2}，{2，0}，{2，2 } }
> T3】输出:1 1
> T6】解释:T8】正方形有四条边:x = 0，x = 2，y = 0，y = 2，现在除了
> 
> **输入:** N = 2，arr[] = { {0，0}，{0，1}，{0，2}，{1，0}，{0，3}，{1，2}，{2，0}，{2，1}，{2，2} }
> **输出:** 0 3

**方法:**给定的问题可以基于以下观察来解决:

*   因为 **N ≥ 2** ，正方形边的坐标至少会出现两次。因此，由于只有一个点不在边界上，至少出现两次的 x 坐标之间的最大值将为我们提供正方形右侧的 x 坐标。
*   其他三个边可以用最大/最小和 x/y 坐标的不同组合类似地获得。
*   知道了正方形的边之后，就很容易识别出不在边界上的点。

按照以下步骤解决问题:

*   [使用变量 **i** 迭代一个范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   用 **2e9** 初始化变量 **x1，y1** ，用 **-2e9** 初始化变量 **x2，y2** ，存储正方形上下边界的点。
    *   [使用变量 **j** 迭代一个范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
        *   如果 **i** 不等于 **j** ，则执行以下步骤:
            *   将 **x1** 设置为 **x1** 或 **p[j]的最小值。首先**。
            *   将 **x2** 设置为 **x2** 或 **p[j]的最大值。首先**。
            *   将 **y1** 设置为 **y1** 或**p【j】的最小值。第二**。
            *   将 **y2** 设置为 **y2** 或**p【j】的最小值。第二**。
    *   初始化一个变量，将 **ok** 设为 **true** ，将变量 **cnt1、cnt2、cnt3、cnt4** 设为 **0** ，将最大和最小点数存储为 **x1、x2、y1、y2** 。
    *   [使用变量 **j** 迭代一个范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
        *   如果 **i** 不等于 **j** ，则执行以下步骤:
            *   若 **p[j]。首先**等于 **x1、**，然后将 **cnt1** 的值增加 **1** 。
            *   若 **p[j]。首先**等于 **x2、**，然后将 **cnt2** 的值增加 **1** 。
            *   若 **p[j]。第二个**等于 **y1、**，然后将 **cnt3** 的值增加 **1** 。
            *   若 **p[j]。第二个**等于 **y2、**，然后将 **cnt4** 的值增加 **1** 。
        *   否则，将 **ok** 的值设置为 **false** 。
    *   如果 **ok** 的值为**真**且 **cnt1、cnt2、cnt3、cnt4** 的值大于等于 **N、**和**x2–x2**等于**y2–y1**，则， **p[i]** 为要求点。打印答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;
#define fi first
#define se second

// Function to find the point that is
// not a part of the side of a square
void findPoint(int n,
               vector<pair<int, int> > p)
{
    // Traverse each pair of coordinates
    for (int i = 0; i < n * 4 + 1; ++i) {

        int x1 = 2e9, x2 = -2e9;
        int y1 = 2e9, y2 = -2e9;

        for (int j = 0; j < n * 4 + 1; ++j)
            if (i != j) {

                // Minimize x-coordinate
                // in all the points
                // except current point
                x1 = min(x1, p[j].fi);

                // Maximize x-coordinate in
                // all the points except
                // the current point
                x2 = max(x2, p[j].fi);

                // Minimize y-coordinate
                // in all the points
                // except current point
                y1 = min(y1, p[j].se);

                // Maximize y-coordinate
                // in all the points
                // except current point
                y2 = max(y2, p[j].se);
            }

        bool ok = 1;

        int c1 = 0, c2 = 0;
        int c3 = 0, c4 = 0;

        for (int j = 1; j <= n * 4 + 1; ++j)
            if (i != j) {

                // If x-coordinate matches
                // with other same line
                if ((p[j].fi == x1
                     || p[j].fi == x2)
                    || ((p[j].se == y1
                         || p[j].se == y2))) {

                    if (p[j].fi == x1)
                        ++c1;

                    if (p[j].fi == x2)
                        ++c2;

                    // If y coordinate matches
                    // with other same line
                    if (p[j].se == y1)
                        ++c3;

                    if (p[j].se == y2)
                        ++c4;
                }
                else
                    ok = 0;
            }

        // Check if the condition
        // for square exists or not
        if (ok && c1 >= n && c2 >= n
            && c3 >= n && c4 >= n
            && x2 - x1 == y2 - y1) {

            // Print the output
            cout << p[i].fi << " "
                 << p[i].se << "\n";
        }
    }
}

// Driver Code
int main()
{
    int N = 2;
    vector<pair<int, int> > arr
        = { { 0, 0 }, { 0, 1 }, { 0, 2 },
            { 1, 0 }, { 1, 1 }, { 1, 2 },
            { 2, 0 }, { 2, 1 }, { 2, 2 } };

    findPoint(N, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.ArrayList;

//Java program for above approach
class GFG{
    static class pair<T, V>{
        T fi;
        V se;
        pair(T a, V b){
            this.fi = a;
            this.se = b;
        }
    }

    // Function to find the point that is
    // not a part of the side of a square
    static void findPoint(int n,
                   ArrayList<pair<Integer, Integer> > p)
    {
        // Traverse each pair of coordinates
        for (int i = 0; i < n * 4 + 1; ++i) {

            int x1 = (int) 2e9, x2 = (int) -2e9;
            int y1 = (int) 2e9, y2 = (int) -2e9;

            for (int j = 0; j < n * 4 + 1; ++j)
                if (i != j) {

                    // Minimize x-coordinate
                    // in all the points
                    // except current point
                    x1 = Math.min(x1, p.get(j).fi);

                    // Maximize x-coordinate in
                    // all the points except
                    // the current point
                    x2 = Math.max(x2, p.get(j).fi);

                    // Minimize y-coordinate
                    // in all the points
                    // except current point
                    y1 = Math.min(y1, p.get(j).se);

                    // Maximize y-coordinate
                    // in all the points
                    // except current point
                    y2 = Math.max(y2, p.get(j).se);
                }

            boolean ok = true;

            int c1 = 0, c2 = 0;
            int c3 = 0, c4 = 0;

            for (int j = 1; j < n * 4 + 1; ++j)
                if (i != j) {

                    // If x-coordinate matches
                    // with other same line
                    if ((p.get(j).fi == x1
                            || p.get(j).fi == x2)
                            || ((p.get(j).se == y1
                            || p.get(j).se == y2))) {

                        if (p.get(j).fi == x1)
                            ++c1;

                        if (p.get(j).fi == x2)
                            ++c2;

                        // If y coordinate matches
                        // with other same line
                        if (p.get(j).se == y1)
                            ++c3;

                        if (p.get(j).se == y2)
                            ++c4;
                    }
                    else
                        ok = false;
                }

            // Check if the condition
            // for square exists or not
            if (ok && c1 >= n && c2 >= n
                    && c3 >= n && c4 >= n
                    && x2 - x1 == y2 - y1) {

                // Print the output
                System.out.println(p.get(i).fi + " " + p.get(i).se);

            }
        }
    }

    //Driver Code
    public static void main(String[] args) {
        int N = 2;
        ArrayList<pair<Integer, Integer> > arr = new ArrayList<>();
        arr.add(new pair<Integer, Integer>(0,0));
        arr.add(new pair<Integer, Integer>(0,1));
        arr.add(new pair<Integer, Integer>(0,2));
        arr.add(new pair<Integer, Integer>(1,0));
        arr.add(new pair<Integer, Integer>(1,1));
        arr.add(new pair<Integer, Integer>(1,2));
        arr.add(new pair<Integer, Integer>(2,0));
        arr.add(new pair<Integer, Integer>(2,1));
        arr.add(new pair<Integer, Integer>(2,2));
        findPoint(N, arr);

    }
}

// This code is contributed by hritikrommie.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the point that is
# not a part of the side of a square
def findPoint(n, p):
    # Traverse each pair of coordinates
    for i in range(n * 4 + 1):
        x1 = 2e9
        x2 = -2e9
        y1 = 2e9
        y2 = -2e9

        for j in range(n * 4 + 1):
            if (i != j):

                # Minimize x-coordinate
                # in all the points
                # except current point
                x1 = min(x1, p[j][0])

                # Maximize x-coordinate in
                # all the points except
                # the current point
                x2 = max(x2, p[j][0])

                # Minimize y-coordinate
                # in all the points
                # except current point
                y1 = min(y1, p[j][1])

                # Maximize y-coordinate
                # in all the points
                # except current point
                y2 = max(y2, p[j][1])

        ok = 1

        c1 = 0
        c2 = 0
        c3 = 0
        c4 = 0

        for j in range(1,n * 4 + 1,1):
            if (i != j):

                # If x-coordinate matches
                # with other same line
                if ((p[j][0] == x1 or p[j][0] == x2) or (p[j][1] == y1 or p[j][1] == y2)):
                    if (p[j][0] == x1):
                        c1 += 1

                    if (p[j][0] == x2):
                        c2 += 1

                    # If y coordinate matches
                    # with other same line
                    if (p[j][1] == y1):
                        c3 += 1

                    if (p[j][1] == y2):
                        c4 += 1
                else:
                    ok = 0

        # Check if the condition
        # for square exists or not
        if (ok and c1 >= n and c2 >= n and c3 >= n and c4 >= n and x2 - x1 == y2 - y1):

            # Print the output
            print(p[i][0],p[i][1])

# Driver Code
if __name__ == '__main__':
    N = 2
    arr =  [[0, 0],[0, 1],[0, 2],[1, 0],[1, 1],[1, 2],[2, 0],[2, 1],[2, 2]]

    findPoint(N, arr)

    # This code is contributed by ipg2016107.
```

**Output:** 

```
1 1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*