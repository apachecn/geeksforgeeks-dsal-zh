# 给网格着色，使所有相同颜色的单元格水平或垂直连接

> 原文:[https://www . geeksforgeeks . org/color-a-grid-so-all-同色单元格-水平或垂直连接/](https://www.geeksforgeeks.org/color-a-grid-such-that-all-same-color-cells-are-connected-either-horizontally-or-vertically/)

给定三个整数 **R，C，N** ，和一个大小为 **N** 的数组 **arr[]** 。任务是为 R 行和 C 列网格的所有单元格着色，以便所有相同颜色的单元格水平或垂直连接。N 表示从 1 到 N 的颜色，arr[]表示每种颜色的数量。颜色的总量正好等于网格的单元格总数。
**进场:**

> **输入:** R = 3，C = 5，N = 5，arr[] = {1，2，3，4，5}
> **输出:**
> 1 4 4 4 3
> 2 5 4 5 3
> 2 5 5 3
> **说明:**可用颜色有 1(计数= 1)、2(计数= 2)、3(计数= 3)等。
> 对于颜色 5:我们可以通过水平或垂直穿过同一个颜色 5 到达所有颜色 5s。
> 同样对于颜色 3，最右边一行包含全部 3 等。
> 同样，对于其余颜色 1、2、4。
> 下面是无效网格:
> 1 4**3**4 4
> 2 5 4 5 3
> 2 5 5 5 3
> 这是因为颜色 3 和 4 的连接被位置(0，2)中 3
> 的无效位置断开了。我们不能再通过仅穿过相应的 3 和 4 来横向或纵向穿过所有 4 或所有 3。
> **输入** : R = 2，C = 2，N = 3，arr[] = {2，1，1}
> **输出:**
> 1 1
> 2 3

**进场:**

乍一看，似乎需要图形算法。然而，我们将遵循一个优化的[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)。

1.  创建一个新的 2D 阵列，这将是我们的最终网格。我们称之为 **dp[][]。**
2.  遍历颜色数组[A]
3.  对于每种颜色，我有 A[i]数量
    *   如果该行是奇数行，则从左到右填充 dp 数组
    *   否则，如果是偶数行，从右向左填充
4.  如果颜色的数量用完了，贪婪地继续下一种颜色

下面是上述方法的实现:

## C++

```
// C++ Program to Color a grid
// such that all same color cells
// are connected either
// horizontally or vertically

#include <bits/stdc++.h>
using namespace std;

void solve(vector<int>& arr,
        int r, int c)
{
    // Current color
    int idx = 1;

    // final grid
    int dp[r];

    for (int i = 0; i < r; i++) {

        // if even row
        if (i % 2 == 0) {

            // traverse from left to
            // right
            for (int j = 0; j < c; j++) {

                // if color has been exhausted
                //, move to the next color
                if (arr[idx - 1] == 0)
                    idx++;

                // color the grid at
                // this position
                dp[i][j] = idx;

                // reduce the color count
                arr[idx - 1]--;
            }
        }
        else {

            // traverse from right to
            // left for odd rows
            for (int j = c - 1; j >= 0; j--) {
                if (arr[idx - 1] == 0)
                    idx++;
                dp[i][j] = idx;
                arr[idx - 1]--;
            }
        }
    }

    // print the grid
    for (int i = 0; i < r; ++i) {
        for (int j = 0; j < c; ++j) {
            cout << dp[i][j] << " ";
        }
        cout << endl;
    }
}

// Driver code
int main()
{
    int r = 3, c = 5;
    int n = 5;
    vector<int> arr
        = { 1, 2, 3, 4, 5 };
    solve(arr, r, c);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to color a grid       
// such that all same color cells       
// are connected either       
// horizontally or vertically       
import java.util.*;   

class GFG{       

static void solve(List<Integer> arr,
                int r, int c)       
{

    // Current color       
    int idx = 1;       

    // Final grid       
    int[][] dp = new int[r];       

    for(int i = 0; i < r; i++)
    {       

        // If even row       
        if (i % 2 == 0)
        {

            // Traverse from left to       
            // right       
            for(int j = 0; j < c; j++)
            {

                // If color has been exhausted
                //, move to the next color
                if (arr.get(idx - 1) == 0)   
                    idx++;

                // Color the grid at
                // this position
                dp[i][j] = idx;

                // Reduce the color count
                arr.set(idx - 1,
                arr.get(idx - 1) - 1);
            }
        }
        else
        {

            // Traverse from right to
            // left for odd rows
            for(int j = c - 1; j >= 0; j--)
            {
                if (arr.get(idx - 1) == 0)   
                    idx++;

                dp[i][j] = idx;

                arr.set(idx - 1,
                arr.get(idx - 1) - 1);
            }       
        }       
    }       

    // Print the grid       
    for(int i = 0; i < r; ++i)
    {       
        for(int j = 0; j < c; ++j)
        {       
            System.out.print(dp[i][j] + " ");       
        }       
        System.out.println();       
    }       
}       

// Driver Code       
public static void main (String[] args)
{       
    int r = 3, c = 5;       
    int n = 5;       
    List<Integer> arr = Arrays.asList(1, 2, 3, 4, 5);

    solve(arr, r, c);       
}       
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to color a grid
# such that all same color cells
# are connected either
# horizontally or vertically
def solve(arr, r, c):

    # Current color
    idx = 1

    # Final grid
    dp = [[0 for i in range(c)]
            for i in range(r)]

    for i in range(r):

        # If even row
        if (i % 2 == 0):

            # Traverse from left to
            # right
            for j in range(c):

                # If color has been exhausted,
                # move to the next color
                if (arr[idx - 1] == 0):
                    idx += 1

                # Color the grid at
                # this position
                # print(i,j)
                dp[i][j] = idx

                # Reduce the color count
                arr[idx - 1] -= 1
        else:

            # Traverse from right to
            # left for odd rows
            for j in range(c - 1, -1, -1):
                if (arr[idx - 1] == 0):
                    idx += 1

                dp[i][j] = idx
                arr[idx - 1] -= 1

    # Print the grid
    for i in range(r):
        for j in range(c):
            print(dp[i][j], end = " ")

        print()

# Driver code
if __name__ == '__main__':

    r = 3
    c = 5
    n = 5
    arr = [ 1, 2, 3, 4, 5 ]

    solve(arr, r, c)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to color a grid       
// such that all same color cells       
// are connected either       
// horizontally or vertically       
using System;
using System.Collections.Generic;

class GFG{       

static void solve(List<int> arr,
                int r, int c)       
{

    // Current color       
    int idx = 1;       

    // Final grid       
    int[,] dp = new int[r, c];       

    for(int i = 0; i < r; i++)
    {       

        // If even row       
        if (i % 2 == 0)
        {

            // Traverse from left to       
            // right       
            for(int j = 0; j < c; j++)
            {

                // If color has been exhausted,
                // move to the next color
                if (arr[idx - 1] == 0)   
                    idx++;

                // Color the grid at
                // this position
                dp[i, j] = idx;

                // Reduce the color count
                arr[idx - 1] = arr[idx - 1] - 1;
            }
        }
        else
        {

            // Traverse from right to
            // left for odd rows
            for(int j = c - 1; j >= 0; j--)
            {
                if (arr[idx - 1] == 0)   
                    idx++;

                dp[i, j] = idx;
                arr[idx - 1] = arr[idx - 1] - 1;
            }       
        }       
    }       

    // Print the grid       
    for(int i = 0; i < r; ++i)
    {       
        for(int j = 0; j < c; ++j)
        {       
            Console.Write(dp[i, j] + " ");       
        }       
        Console.Write('\n');       
    }       
}       

// Driver Code       
public static void Main (string[] args)
{       
    int r = 3, c = 5;       
    //int n = 5;   

    List<int> arr = new List<int>();
    arr.Add(1);
    arr.Add(2);
    arr.Add(3);
    arr.Add(4);
    arr.Add(5);

    solve(arr, r, c);       
}       
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

//  Javascript Program to Color a grid
//  such that all same color cells
//  are connected either
//  horizontally or vertically

function solve(arr,r,c)
{
    // Current color
    var idx = 1;

    // final grid
    var dp = new Array(r);

    var i,j;
    for(i=0;i<r;i++)
      dp[i] = new Array(c);
    for(i = 0; i < r; i++) {

        // if even row
        if (i % 2 == 0) {

            // traverse from left to
            // right
            for(j = 0; j < c; j++) {

                // if color has been exhausted
                //, move to the next color
                if (arr[idx - 1] == 0)
                    idx++;

                // color the grid at
                // this position
                dp[i][j] = idx;

                // reduce the color count
                arr[idx - 1]--;
            }
        }
        else {

            // traverse from right to
            // left for odd rows
            for (j = c - 1; j >= 0; j--) {
                if (arr[idx - 1] == 0)
                    idx++;
                dp[i][j] = idx;
                arr[idx - 1]--;
            }
        }
    }

    // print the grid
    for(i = 0; i < r; ++i) {
        for(j = 0; j < c; ++j) {
            document.write(dp[i][j] + " ");
        }
        document.write("<br>");
    }
}

// Driver code

    var r = 3, c = 5;
    var n = 5;
    var arr = [1, 2, 3, 4, 5];
    solve(arr, r, c);

</script>
```

**输出:**

```
1 2 2 3 3
4 4 4 4 3
5 5 5 5 5
```