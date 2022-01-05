# 计算二进制矩阵中所有被 1 阻挡的 0

> 原文:[https://www . geesforgeks . org/count-all-0-哪些被二进制矩阵中的 1 阻塞/](https://www.geeksforgeeks.org/count-all-0s-which-are-blocked-by-1s-in-binary-matrix/)

给定二元矩阵。任务是计算被 1 包围的所有 0(可能不是直接邻居)。
**注:**这里我们只取四个方向，上、左、下、右。
示例:

```
Input :  Int M[][] = {{ 0, 1, 1, 0},
                      { 1, 0, 0, 1},
                      { 0, 1, 0, 1},
                      { 1, 0, 1, 1}}
Output : 3 
Explanation : All zeros which are surrounded 
by 1 are (1, 1), (1, 2) and (2, 2)    
```

想法基于 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 。
首先，我们使用 DFS 去除矩阵中所有可以从矩阵边界到达的零值单元。请注意，从边界 0 单元可到达的任何单元都不被 1 包围。

```
  Int M[][] =  {{  0, 1, 1,  0},
                { 1, 0, 0, 1},
                { 0, 1, 1, 1},
                { 1,  0, 1, 1}}
All zero cell which are reachable from boundary are in read color.
```

然后，我们计算二进制矩阵中剩下的所有零。
下面是上面思路的实现。

## C++

```
// C++ program to count number of zeros
// surrounded by 1
#include <iostream>
using namespace std;
#define Row 4
#define Col 5
int r[4] = { 0, 0, 1, -1 };
int c[4] = { 1, -1, 0, 0 };

bool isSafe(int x, int y, int M[][Col])
{
    if (x >= 0 && x <= Row && y >= 0 &&
        y <= Col && M[x][y] == 0)
        return true;
    return false;
}

// DFS function to mark all reachable cells from
// (x, y)
void DFS(int x, int y, int M[][Col])
{
    // make it's visited
    M[x][y] = 1;
    for (int k = 0; k < 4; k++)
        if (isSafe(x + r[k], y + c[k], M))
            DFS(x + r[k], y + c[k], M);
}

// function return count of 0's which are surrounded by 1
int CountAllZero(int M[][Col])
{
    // first we remove all zeros which are not
    // surrounded by 1 that means we only remove
    // those zeros which are reachable from
    // any boundary of given matrix.
    for (int i = 0; i < Col; i++)
        if (M[0][i] == 0)
            DFS(0, i, M);
    for (int i = 0; i < Col; i++)
        if (M[Row - 1][i] == 0)
            DFS(Row - 1, i, M);
    for (int i = 0; i < Row; i++)
        if (M[i][0] == 0)
            DFS(i, 0, M);
    for (int i = 0; i < Row; i++)
        if (M[i][Col - 1] == 0)
            DFS(i, Col - 1, M);

    // count all zeros which are surrounded by 1
    int result = 0;
    for (int i = 0; i < Row; i++)
        for (int j = 0; j < Col; j++)
            if (M[i][j] == 0)
                result++;
    return result;
}

// driver program to test above function
int main()
{
    int M[][Col] = { { 1, 1, 1, 0, 1 },
                     { 1, 0, 0, 1, 0 },
                     { 1, 0, 1, 0, 1 },
                     { 0, 1, 1, 1, 1 } };
    cout << CountAllZero(M) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of zeros
// surrounded by 1
class GFG {

    final static int Row = 4;
    final static int Col = 5;
    static int r[] = {0, 0, 1, -1};
    static int c[] = {1, -1, 0, 0};

    static boolean isSafe(int x, int y, int M[][]) {
        if (x >= 0 && x <Row && y >= 0
                && y < Col && M[x][y] == 0) {
            return true;
        }
        return false;
    }

// DFS function to mark all reachable cells from
// (x, y)
    static void DFS(int x, int y, int M[][]) {
        // make it's visited
        M[x][y] = 1;
        for (int k = 0; k < 4; k++) {
            if (isSafe(x + r[k], y + c[k], M)) {
                DFS(x + r[k], y + c[k], M);
            }
        }
    }

// function return count of 0's which are surrounded by 1
    static int CountAllZero(int M[][]) {
        // first we remove all zeros which are not
        // surrounded by 1 that means we only remove
        // those zeros which are reachable from
        // any boundary of given matrix.
        for (int i = 0; i < Col; i++) {
            if (M[0][i] == 0) {
                DFS(0, i, M);
            }
        }
        for (int i = 0; i < Col; i++) {
            if (M[Row - 1][i] == 0) {
                DFS(Row - 1, i, M);
            }
        }
        for (int i = 0; i < Row; i++) {
            if (M[i][0] == 0) {
                DFS(i, 0, M);
            }
        }
        for (int i = 0; i < Row; i++) {
            if (M[i][Col - 1] == 0) {
                DFS(i, Col - 1, M);
            }
        }

        // count all zeros which are surrounded by 1
        int result = 0;
        for (int i = 0; i < Row; i++) {
            for (int j = 0; j < Col; j++) {
                if (M[i][j] == 0) {
                    result++;
                }
            }
        }
        return result;
    }

// driver program to test above function
    public static void main(String[] args) {
        int M[][] = {{1, 1, 1, 0, 1},
        {1, 0, 0, 1, 0},
        {1, 0, 1, 0, 1},
        {0, 1, 1, 1, 1}};
        System.out.print(CountAllZero(M));
    }
}
// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to count number of zeros
# surrounded by 1
Row = 4
Col = 5
r = [0, 0, 1, -1 ]
c = [1, -1, 0, 0 ]

def isSafe(x, y, M):

    if (x >= 0 and x < Row and y >= 0 and y < Col):
        if M[x][y] == 0:
            return True

    return False

# DFS function to mark all reachable cells from
# (x, y)
def DFS(x, y, M):

    # make it's visited
    M[x][y] = 1
    for k in range(4):
        if (isSafe(x + r[k], y + c[k], M)):
            DFS(x + r[k], y + c[k], M)

# function return count of 0's which are surrounded by 1
def CountAllZero(M):

    # first we remove all zeros which are not
    # surrounded by 1 that means we only remove
    # those zeros which are reachable from
    # any boundary of given matrix.
    for i in range(Col):
        if (M[0][i] == 0):
            DFS(0, i, M)
    for i in range(Col):
        if (M[Row - 1][i] == 0):
            DFS(Row - 1, i, M)
    for i in range(Row):
        if (M[i][0] == 0):
            DFS(i, 0, M)
    for i in range(Row):
        if (M[i][Col - 1] == 0):
            DFS(i, Col - 1, M)

    # count all zeros which are surrounded by 1
    result = 0
    for i in range(Row):
        for j in range(Col):
            if (M[i][j] == 0):
                result += 1

    return result

# Driver code
M = [[1, 1, 1, 0, 1], [1, 0, 0, 1, 0 ],
    [1, 0, 1, 0, 1] , [ 0, 1, 1, 1, 1 ]]
print(CountAllZero(M))

# This code is contributed by shubhamsingh10
```

## C#

```

// C# program to count number of zeros
// surrounded by 1
using System;
public class GFG {

    readonly static int Row = 4;
    readonly static int Col = 5;
    static int []r = {0, 0, 1, -1};
    static int []c = {1, -1, 0, 0};

    static bool isSafe(int x, int y, int [,]M) {
        if (x >= 0 && x <Row && y >= 0
                && y < Col && M[x,y] == 0) {
            return true;
        }
        return false;
    }

// DFS function to mark all reachable cells from
// (x, y)
    static void DFS(int x, int y, int [,]M) {
        // make it's visited
        M[x,y] = 1;
        for (int k = 0; k < 4; k++) {
            if (isSafe(x + r[k], y + c[k], M)) {
                DFS(x + r[k], y + c[k], M);
            }
        }
    }

// function return count of 0's which are surrounded by 1
    static int CountAllZero(int [,]M) {
        // first we remove all zeros which are not
        // surrounded by 1 that means we only remove
        // those zeros which are reachable from
        // any boundary of given matrix.
        for (int i = 0; i < Col; i++) {
            if (M[0,i] == 0) {
                DFS(0, i, M);
            }
        }
        for (int i = 0; i < Col; i++) {
            if (M[Row - 1,i] == 0) {
                DFS(Row - 1, i, M);
            }
        }
        for (int i = 0; i < Row; i++) {
            if (M[i,0] == 0) {
                DFS(i, 0, M);
            }
        }
        for (int i = 0; i < Row; i++) {
            if (M[i,Col - 1] == 0) {
                DFS(i, Col - 1, M);
            }
        }

        // count all zeros which are surrounded by 1
        int result = 0;
        for (int i = 0; i < Row; i++) {
            for (int j = 0; j < Col; j++) {
                if (M[i,j] == 0) {
                    result++;
                }
            }
        }
        return result;
    }

// driver program to test above function
    public static void Main() {
        int [,]M = {{1, 1, 1, 0, 1},
        {1, 0, 0, 1, 0},
        {1, 0, 1, 0, 1},
        {0, 1, 1, 1, 1}};
        Console.Write(CountAllZero(M));
    }
}
// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to count number of zeros
// surrounded by 1
var Row = 4;
var Col = 5;
var r = [ 0, 0, 1, -1 ];
var c = [ 1, -1, 0, 0 ];

function isSafe(x, y, M)
{
    if (x >= 0 && x < Row && y >= 0 &&
        y < Col && M[x][y] == 0)
        return true;
    return false;
}

// DFS function to mark all reachable cells from
// (x, y)
function DFS(x, y, M)
{
    // make it's visited
    M[x][y] = 1;
    for (var k = 0; k < 4; k++)
        if (isSafe(x + r[k], y + c[k], M))
            DFS(x + r[k], y + c[k], M);
}

// function return count of 0's which are surrounded by 1
function CountAllZero(M)
{
    // first we remove all zeros which are not
    // surrounded by 1 that means we only remove
    // those zeros which are reachable from
    // any boundary of given matrix.
    for (var i = 0; i < Col; i++)
        if (M[0][i] == 0)
            DFS(0, i, M);
    for (var i = 0; i < Col; i++)
        if (M[Row - 1][i] == 0)
            DFS(Row - 1, i, M);
    for (var i = 0; i < Row; i++)
        if (M[i][0] == 0)
            DFS(i, 0, M);
    for (var i = 0; i < Row; i++)
        if (M[i][Col - 1] == 0)
            DFS(i, Col - 1, M);

    // count all zeros which are surrounded by 1
    var result = 0;
    for (var i = 0; i < Row; i++)
        for (var j = 0; j < Col; j++)
            if (M[i][j] == 0)
                result++;
    return result;
}

// driver program to test above function
var M = [ [ 1, 1, 1, 0, 1 ],
                 [ 1, 0, 0, 1, 0 ],
                 [ 1, 0, 1, 0, 1 ],
                 [ 0, 1, 1, 1, 1 ] ];
document.write( CountAllZero(M));

</script>
```

**输出:**

```
4
```

**时间复杂度:** O(Row*Col)
本文由 [**尼尚·辛格**](https://www.facebook.com/nishant.chaudhary.7334) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。