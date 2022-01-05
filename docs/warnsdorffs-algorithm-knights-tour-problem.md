# Warnsdorff 的骑士之旅问题算法

> 原文:[https://www . geesforgeks . org/warnsdorffs-算法-骑士-游览-问题/](https://www.geeksforgeeks.org/warnsdorffs-algorithm-knights-tour-problem/)

**问题:**一个骑士被放在一个空棋盘的第一个方块上，按照国际象棋的规则移动，必须精确地访问每个方块一次。

下面是 Knight 覆盖所有单元格的示例路径。下面的格子代表一个有 8×8 个格子的棋盘。单元格中的数字表示骑士的移动次数。

![knight-tour-problem](img/8af43210e216548144b476bd608f7bcf.png)

我们讨论了[回溯算法求解骑士之旅](https://www.geeksforgeeks.org/backtracking-set-1-the-knights-tour-problem/)。在这篇文章中[沃恩斯多夫的启发](https://en.wikipedia.org/wiki/Knight%27s_tour#Warnsdorf.27s_rule)被讨论。
**沃恩斯多夫法则:**

1.  我们可以从骑士在棋盘上的任何初始位置开始。
2.  我们总是以最小的度数(最小数量的未访问的相邻)移动到相邻的、未访问的正方形。

该算法也可以更普遍地应用于任何图形。

**一些定义:**

*   如果 P 可以通过单个骑士的移动移动到 Q，并且 Q 还没有被访问过，那么 Q 位置可以从 P 位置进入。
*   位置 P 的可访问性是可从位置 P 访问的位置数量

**算法:**

1.  将 P 设置为棋盘上的随机初始位置
2.  用移动编号“1”标记板 P
3.  对棋盘上从 2 到方块数的每个移动数执行以下操作:
    *   设 S 是可从 p 得到的一组位置
    *   将 P 设置为 S 中可访问性最低的位置
    *   用当前的移动号码在 P 标记棋盘
4.  返回标记的板-每个方块将被标记上它被访问的移动号码。

下面是上述算法的实现。

## C++

```
// C++ program to for Kinight's tour problem using
// Warnsdorff's algorithm
#include <bits/stdc++.h>
#define N 8

// Move pattern on basis of the change of
// x coordinates and y coordinates respectively
static int cx[N] = {1,1,2,2,-1,-1,-2,-2};
static int cy[N] = {2,-2,1,-1,2,-2,1,-1};

// function restricts the knight to remain within
// the 8x8 chessboard
bool limits(int x, int y)
{
    return ((x >= 0 && y >= 0) && (x < N && y < N));
}

/* Checks whether a square is valid and empty or not */
bool isempty(int a[], int x, int y)
{
    return (limits(x, y)) && (a[y*N+x] < 0);
}

/* Returns the number of empty squares adjacent
   to (x, y) */
int getDegree(int a[], int x, int y)
{
    int count = 0;
    for (int i = 0; i < N; ++i)
        if (isempty(a, (x + cx[i]), (y + cy[i])))
            count++;

    return count;
}

// Picks next point using Warnsdorff's heuristic.
// Returns false if it is not possible to pick
// next point.
bool nextMove(int a[], int *x, int *y)
{
    int min_deg_idx = -1, c, min_deg = (N+1), nx, ny;

    // Try all N adjacent of (*x, *y) starting
    // from a random adjacent. Find the adjacent
    // with minimum degree.
    int start = rand()%N;
    for (int count = 0; count < N; ++count)
    {
        int i = (start + count)%N;
        nx = *x + cx[i];
        ny = *y + cy[i];
        if ((isempty(a, nx, ny)) &&
           (c = getDegree(a, nx, ny)) < min_deg)
        {
            min_deg_idx = i;
            min_deg = c;
        }
    }

    // IF we could not find a next cell
    if (min_deg_idx == -1)
        return false;

    // Store coordinates of next point
    nx = *x + cx[min_deg_idx];
    ny = *y + cy[min_deg_idx];

    // Mark next move
    a[ny*N + nx] = a[(*y)*N + (*x)]+1;

    // Update next point
    *x = nx;
    *y = ny;

    return true;
}

/* displays the chessboard with all the
  legal knight's moves */
void print(int a[])
{
    for (int i = 0; i < N; ++i)
    {
        for (int j = 0; j < N; ++j)
            printf("%d\t",a[j*N+i]);
        printf("\n");
    }
}

/* checks its neighbouring squares */
/* If the knight ends on a square that is one
   knight's move from the beginning square,
   then tour is closed */
bool neighbour(int x, int y, int xx, int yy)
{
    for (int i = 0; i < N; ++i)
        if (((x+cx[i]) == xx)&&((y + cy[i]) == yy))
            return true;

    return false;
}

/* Generates the legal moves using warnsdorff's
  heuristics. Returns false if not possible */
bool findClosedTour()
{
    // Filling up the chessboard matrix with -1's
    int a[N*N];
    for (int i = 0; i< N*N; ++i)
        a[i] = -1;

    // Randome initial position
    int sx = rand()%N;
    int sy = rand()%N;

    // Current points are same as initial points
    int x = sx, y = sy;
    a[y*N+x] = 1; // Mark first move.

    // Keep picking next points using
    // Warnsdorff's heuristic
    for (int i = 0; i < N*N-1; ++i)
        if (nextMove(a, &x, &y) == 0)
            return false;

    // Check if tour is closed (Can end
    // at starting point)
    if (!neighbour(x, y, sx, sy))
        return false;

    print(a);
    return true;
}

// Driver code
int main()
{
    // To make sure that different random
    // initial positions are picked.
    srand(time(NULL));

    // While we don't get a solution
    while (!findClosedTour())
    {
    ;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to for Kinight's tour problem using
// Warnsdorff's algorithm
import java.util.concurrent.ThreadLocalRandom;

class GFG
{
    public static final int N = 8;

    // Move pattern on basis of the change of
    // x coordinates and y coordinates respectively
    public static final int cx[] = {1, 1, 2, 2, -1, -1, -2, -2};
    public static final int cy[] = {2, -2, 1, -1, 2, -2, 1, -1};

    // function restricts the knight to remain within
    // the 8x8 chessboard
    boolean limits(int x, int y)
    {
        return ((x >= 0 && y >= 0) &&
                 (x < N && y < N));
    }

    /* Checks whether a square is valid and
    empty or not */
    boolean isempty(int a[], int x, int y)
    {
        return (limits(x, y)) && (a[y * N + x] < 0);
    }

    /* Returns the number of empty squares
    adjacent to (x, y) */
    int getDegree(int a[], int x, int y)
    {
        int count = 0;
        for (int i = 0; i < N; ++i)
            if (isempty(a, (x + cx[i]),
                           (y + cy[i])))
                count++;

        return count;
    }

    // Picks next point using Warnsdorff's heuristic.
    // Returns false if it is not possible to pick
    // next point.
    Cell nextMove(int a[], Cell cell)
    {
        int min_deg_idx = -1, c,
            min_deg = (N + 1), nx, ny;

        // Try all N adjacent of (*x, *y) starting
        // from a random adjacent. Find the adjacent
        // with minimum degree.
        int start = ThreadLocalRandom.current().nextInt(1000) % N;
        for (int count = 0; count < N; ++count)
        {
            int i = (start + count) % N;
            nx = cell.x + cx[i];
            ny = cell.y + cy[i];
            if ((isempty(a, nx, ny)) &&
                (c = getDegree(a, nx, ny)) < min_deg)
            {
                min_deg_idx = i;
                min_deg = c;
            }
        }

        // IF we could not find a next cell
        if (min_deg_idx == -1)
            return null;

        // Store coordinates of next point
        nx = cell.x + cx[min_deg_idx];
        ny = cell.y + cy[min_deg_idx];

        // Mark next move
        a[ny * N + nx] = a[(cell.y) * N +
                           (cell.x)] + 1;

        // Update next point
        cell.x = nx;
        cell.y = ny;

        return cell;
    }

    /* displays the chessboard with all the
    legal knight's moves */
    void print(int a[])
    {
        for (int i = 0; i < N; ++i)
        {
            for (int j = 0; j < N; ++j)
                System.out.printf("%d\t", a[j * N + i]);
            System.out.printf("\n");
        }
    }

    /* checks its neighbouring squares */
    /* If the knight ends on a square that is one
    knight's move from the beginning square,
    then tour is closed */
    boolean neighbour(int x, int y, int xx, int yy)
    {
        for (int i = 0; i < N; ++i)
            if (((x + cx[i]) == xx) &&
                ((y + cy[i]) == yy))
                return true;

        return false;
    }

    /* Generates the legal moves using warnsdorff's
    heuristics. Returns false if not possible */
    boolean findClosedTour()
    {
        // Filling up the chessboard matrix with -1's
        int a[] = new int[N * N];
        for (int i = 0; i < N * N; ++i)
            a[i] = -1;

        // initial position
        int sx = 3;
        int sy = 2;

        // Current points are same as initial points
        Cell cell = new Cell(sx, sy);

        a[cell.y * N + cell.x] = 1; // Mark first move.

        // Keep picking next points using
        // Warnsdorff's heuristic
        Cell ret = null;
        for (int i = 0; i < N * N - 1; ++i)
        {
            ret = nextMove(a, cell);
            if (ret == null)
                return false;
        }

        // Check if tour is closed (Can end
        // at starting point)
        if (!neighbour(ret.x, ret.y, sx, sy))
            return false;

        print(a);
        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // While we don't get a solution
        while (!new GFG().findClosedTour())
        {
            ;
        }
    }
}

class Cell
{
    int x;
    int y;

    public Cell(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

// This code is contributed by SaeedZarinfam
```

**输出:**

```
59    14    63    32    1    16    19    34    
62    31    60    15    56    33    2    17    
13    58    55    64    49    18    35    20    
30    61    42    57    54    51    40    3    
43    12    53    50    41    48    21    36    
26    29    44    47    52    39    4    7    
11    46    27    24    9    6    37    22    
28    25    10    45    38    23    8    5    
```

***哈密顿路径问题一般是 NP 难的。在实践中，沃恩斯多夫的启发式算法成功地在线性时间内找到了解决方案。**T3】*

**你知道吗？**
“在一个 8 × 8 的棋盘上，正好有 26，534，728，821，064 个定向封闭游(也就是说，沿着同一路径的两个相反方向的游是分开计算的，旋转和反射也是一样)。无向封闭游的数量是这个数字的一半，因为每一个游都可以反向追踪！”

本文由 **Uddalak Bhaduri** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。