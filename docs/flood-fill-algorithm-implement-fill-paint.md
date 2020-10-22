# 洪水填充算法 – 如何在绘图中实现`fill()`？

> 原文： [https://www.geeksforgeeks.org/flood-fill-algorithm-implement-fill-paint/](https://www.geeksforgeeks.org/flood-fill-algorithm-implement-fill-paint/)

在 MS-Paint 中，当我们将画笔带到一个像素并单击时，该像素区域的颜色将替换为新的选定颜色。 以下是执行此任务的问题说明。

给定 2D 屏幕，屏幕中像素的位置和颜色，用给定颜色替换给定像素和所有相邻的相同彩色像素的颜色。

**示例**：

```
Input:
       screen[M][N] = {{1, 1, 1, 1, 1, 1, 1, 1},
                      {1, 1, 1, 1, 1, 1, 0, 0},
                      {1, 0, 0, 1, 1, 0, 1, 1},
                      {1, 2, 2, 2, 2, 0, 1, 0},
                      {1, 1, 1, 2, 2, 0, 1, 0},
                      {1, 1, 1, 2, 2, 2, 2, 0},
                      {1, 1, 1, 1, 1, 2, 1, 1},
                      {1, 1, 1, 1, 1, 2, 2, 1},
                      };
    x = 4, y = 4, newColor = 3
The values in the given 2D screen indicate colors of the pixels.
x and y are coordinates of the brush, newColor is the color that
should replace the previous color on screen[x][y] and all surrounding
pixels with same color.

Output:
Screen should be changed to following.
       screen[M][N] = {{1, 1, 1, 1, 1, 1, 1, 1},
                      {1, 1, 1, 1, 1, 1, 0, 0},
                      {1, 0, 0, 1, 1, 0, 1, 1},
                      {1, 3, 3, 3, 3, 0, 1, 0},
                      {1, 1, 1, 3, 3, 0, 1, 0},
                      {1, 1, 1, 3, 3, 3, 3, 0},
                      {1, 1, 1, 1, 1, 3, 1, 1},
                      {1, 1, 1, 1, 1, 3, 3, 1},
                      };

```



[**Flood-Fill 算法**](http://en.wikipedia.org/wiki/Flood_fill)：

这个想法很简单，我们首先替换当前像素的颜色，然后对 4 个周围的点进行递归。 以下是详细的算法。

```
// A recursive function to replace previous color 'prevC' at  '(x, y)' 
// and all surrounding pixels of (x, y) with new color 'newC' and
floodFil(screen[M][N], x, y, prevC, newC)
1) If x or y is outside the screen, then return.
2) If color of screen[x][y] is not same as prevC, then return
3) Recur for north, south, east and west.
    floodFillUtil(screen, x+1, y, prevC, newC);
    floodFillUtil(screen, x-1, y, prevC, newC);
    floodFillUtil(screen, x, y+1, prevC, newC);
    floodFillUtil(screen, x, y-1, prevC, newC); 
```

以下是上述算法的实现。

## C++ 

```cpp

// A C++ program to implement flood fill algorithm 
#include<iostream> 
using namespace std; 

// Dimentions of paint screen 
#define M 8 
#define N 8 

// A recursive function to replace previous color 'prevC' at  '(x, y)'  
// and all surrounding pixels of (x, y) with new color 'newC' and 
void floodFillUtil(int screen[][N], int x, int y, int prevC, int newC) 
{ 
    // Base cases 
    if (x < 0 || x >= M || y < 0 || y >= N) 
        return; 
    if (screen[x][y] != prevC) 
        return; 
    if (screen[x][y] == newC)  
        return;  

    // Replace the color at (x, y) 
    screen[x][y] = newC; 

    // Recur for north, east, south and west 
    floodFillUtil(screen, x+1, y, prevC, newC); 
    floodFillUtil(screen, x-1, y, prevC, newC); 
    floodFillUtil(screen, x, y+1, prevC, newC); 
    floodFillUtil(screen, x, y-1, prevC, newC); 
} 

// It mainly finds the previous color on (x, y) and 
// calls floodFillUtil() 
void floodFill(int screen[][N], int x, int y, int newC) 
{ 
    int prevC = screen[x][y]; 
    floodFillUtil(screen, x, y, prevC, newC); 
} 

// Driver program to test above function 
int main() 
{ 
    int screen[M][N] = {{1, 1, 1, 1, 1, 1, 1, 1}, 
                      {1, 1, 1, 1, 1, 1, 0, 0}, 
                      {1, 0, 0, 1, 1, 0, 1, 1}, 
                      {1, 2, 2, 2, 2, 0, 1, 0}, 
                      {1, 1, 1, 2, 2, 0, 1, 0}, 
                      {1, 1, 1, 2, 2, 2, 2, 0}, 
                      {1, 1, 1, 1, 1, 2, 1, 1}, 
                      {1, 1, 1, 1, 1, 2, 2, 1}, 
                     }; 
    int x = 4, y = 4, newC = 3; 
    floodFill(screen, x, y, newC); 

    cout << "Updated screen after call to floodFill: \n"; 
    for (int i=0; i<M; i++) 
    { 
        for (int j=0; j<N; j++) 
           cout << screen[i][j] << " "; 
        cout << endl; 
    } 
} 

```

## Java


```java
// Java program to implement flood fill algorithm
class GFG
{

// Dimentions of paint screen
static int M = 8;
static int N = 8;

// A recursive function to replace previous color 'prevC' at '(x, y)' 
// and all surrounding pixels of (x, y) with new color 'newC' and
static void floodFillUtil(int screen[][], int x, int y, 
                                    int prevC, int newC)
{
    // Base cases
    if (x < 0 || x >= M || y < 0 || y >= N)
        return;
    if (screen[x][y] != prevC)
        return;

    // Replace the color at (x, y)
    screen[x][y] = newC;

    // Recur for north, east, south and west
    floodFillUtil(screen, x+1, y, prevC, newC);
    floodFillUtil(screen, x-1, y, prevC, newC);
    floodFillUtil(screen, x, y+1, prevC, newC);
    floodFillUtil(screen, x, y-1, prevC, newC);
}

// It mainly finds the previous color on (x, y) and
// calls floodFillUtil()
static void floodFill(int screen[][], int x, int y, int newC)
{
    int prevC = screen[x][y];
    floodFillUtil(screen, x, y, prevC, newC);
}

// Driver code
public static void main(String[] args) 
{
    int screen[][] = {{1, 1, 1, 1, 1, 1, 1, 1},
                    {1, 1, 1, 1, 1, 1, 0, 0},
                    {1, 0, 0, 1, 1, 0, 1, 1},
                    {1, 2, 2, 2, 2, 0, 1, 0},
                    {1, 1, 1, 2, 2, 0, 1, 0},
                    {1, 1, 1, 2, 2, 2, 2, 0},
                    {1, 1, 1, 1, 1, 2, 1, 1},
                    {1, 1, 1, 1, 1, 2, 2, 1},
                    };
    int x = 4, y = 4, newC = 3;
    floodFill(screen, x, y, newC);

    System.out.println("Updated screen after call to floodFill: ");
    for (int i = 0; i < M; i++)
    {
        for (int j = 0; j < N; j++)
        System.out.print(screen[i][j] + " ");
        System.out.println();
    }
    }
}

// This code has been contributed by 29AjayKumar
```

## Python3

```py
# Python3 program to implement 
# flood fill algorithm

# Dimentions of paint screen 
M = 8
N = 8

# A recursive function to replace 
# previous color 'prevC' at '(x, y)' 
# and all surrounding pixels of (x, y) 
# with new color 'newC' and 
def floodFillUtil(screen, x, y, prevC, newC):
    
    # Base cases
    if (x < 0 or x >= M or y < 0 or 
        y >= N or screen[x][y] != prevC or 
        screen[x][y] == newC):
        return

    # Replace the color at (x, y)
    screen[x][y] = newC

    # Recur for north, east, south and west
    floodFillUtil(screen, x + 1, y, prevC, newC)
    floodFillUtil(screen, x - 1, y, prevC, newC)
    floodFillUtil(screen, x, y + 1, prevC, newC)
    floodFillUtil(screen, x, y - 1, prevC, newC)

# It mainly finds the previous color on (x, y) and 
# calls floodFillUtil() 
def floodFill(screen, x, y, newC):
    prevC = screen[x][y]
    floodFillUtil(screen, x, y, prevC, newC)

# Driver Code
screen = [[1, 1, 1, 1, 1, 1, 1, 1], 
          [1, 1, 1, 1, 1, 1, 0, 0], 
          [1, 0, 0, 1, 1, 0, 1, 1], 
          [1, 2, 2, 2, 2, 0, 1, 0], 
          [1, 1, 1, 2, 2, 0, 1, 0], 
          [1, 1, 1, 2, 2, 2, 2, 0], 
          [1, 1, 1, 1, 1, 2, 1, 1], 
          [1, 1, 1, 1, 1, 2, 2, 1]]

x = 4
y = 4
newC = 3
floodFill(screen, x, y, newC)

print ("Updated screen after call to floodFill:")
for i in range(M):
    for j in range(N):
        print(screen[i][j], end = ' ')
    print()

# This code is contributed by Ashutosh450
```

## C#

```cs
// C# program to implement
// flood fill algorithm 
using System; 
    
class GFG
{

// Dimentions of paint screen
static int M = 8;
static int N = 8;

// A recursive function to replace 
// previous color 'prevC' at '(x, y)' 
// and all surrounding pixels of (x, y) 
// with new color 'newC' and
static void floodFillUtil(int [,]screen, 
                          int x, int y, 
                          int prevC, int newC)
{
    // Base cases
    if (x < 0 || x >= M || 
        y < 0 || y >= N)
        return;
    if (screen[x, y] != prevC)
        return;

    // Replace the color at (x, y)
    screen[x, y] = newC;

    // Recur for north, east, south and west
    floodFillUtil(screen, x + 1, y, prevC, newC);
    floodFillUtil(screen, x - 1, y, prevC, newC);
    floodFillUtil(screen, x, y + 1, prevC, newC);
    floodFillUtil(screen, x, y - 1, prevC, newC);
}

// It mainly finds the previous color 
// on (x, y) and calls floodFillUtil()
static void floodFill(int [,]screen, int x,
                      int y, int newC)
{
    int prevC = screen[x, y];
    floodFillUtil(screen, x, y, prevC, newC);
}

// Driver code
public static void Main(String[] args) 
{
    int [,]screen = {{1, 1, 1, 1, 1, 1, 1, 1},
                     {1, 1, 1, 1, 1, 1, 0, 0},
                     {1, 0, 0, 1, 1, 0, 1, 1},
                     {1, 2, 2, 2, 2, 0, 1, 0},
                     {1, 1, 1, 2, 2, 0, 1, 0},
                     {1, 1, 1, 2, 2, 2, 2, 0},
                     {1, 1, 1, 1, 1, 2, 1, 1},
                     {1, 1, 1, 1, 1, 2, 2, 1}};
    int x = 4, y = 4, newC = 3;
    floodFill(screen, x, y, newC);

    Console.WriteLine("Updated screen after" + 
                      "call to floodFill: ");
    for (int i = 0; i < M; i++)
    {
        for (int j = 0; j < N; j++)
        Console.Write(screen[i, j] + " ");
        Console.WriteLine();
    }
    }
}

// This code is contributed by PrinciRaj1992 
```

输出：

```
Updated screen after call to floodFill: 
1 1 1 1 1 1 1 1 
1 1 1 1 1 1 0 0 
1 0 0 1 1 0 1 1 
1 3 3 3 3 0 1 0 
1 1 1 3 3 0 1 0 
1 1 1 3 3 3 3 0 
1 1 1 1 1 3 1 1 
1 1 1 1 1 3 3 1 
```

2 - 使用 BFS 方法：

基于 BFS 的方法算法：

1.  创建一个成对队列。

2.  插入队列中给定的初始索引。

3.  在`vis[][]`矩阵中将初始索引标记为已访问。

4.  直到队列不为空，重复步骤 3.1 到 3.6

    +   从队列中取出最前面的元素
    +   从队列中弹出
    +   将当前值/颜色存储在从队列中取出的坐标处（预色）
    +   更新从队列中取出的当前索引的值/颜色
    +   检查所有4个方向，即`（x + 1, y)`，`(x-1, y)`，`(x, y + 1)`，`(x, y-1)`是否有效，如果有效，则检查坐标处的那个值应等于原色，并且`vis[][]`中该坐标的值为 0。
    +   如果以上所有条件都为真，则将相应的坐标推入队列并在`vis[][]`中标记为 1。
5.  打印矩阵。

下面是上述方法的实现：

## C++

```cpp
// CPP program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check valid coordinate
int validCoord(int x, int y, int n, int m)
{

    if (x < 0 || y < 0) {
        return 0;
    }
    if (x >= n || y >= m) {
        return 0;
    }
    return 1;
}

// Function to run bfs
void bfs(int n, int m, int data[][8], 
                     int x, int y, int color)
{
  
  // Visiing array
  int vis[101][101];
  
  // Initialing all as zero
  memset(vis, 0, sizeof(vis));
  
  // Creating queue for bfs
  queue<pair<int, int> > obj;
  
  // Pushing pair of {x, y}
  obj.push({ x, y });
  
  // Marking {x, y} as visited
  vis[x][y] = 1;
  
  // Untill queue is emppty
  while (obj.empty() != 1) 
  {

    // Extrating front pair
    pair<int, int> coord = obj.front();
    int x = coord.first;
    int y = coord.second;
    int preColor = data[x][y];

    data[x][y] = color;
    
    // Poping front pair of queue
    obj.pop();

    // For Upside Pixel or Cell
    if (validCoord(x + 1, y, n, m)
        && vis[x + 1][y] == 0
        && data[x + 1][y] == preColor)
    {
      obj.push({ x + 1, y });
      vis[x + 1][y] = 1;
    }
    
    // For Downside Pixel or Cell
    if (validCoord(x - 1, y, n, m)
        && vis[x - 1][y] == 0
        && data[x - 1][y] == preColor) 
    {
      obj.push({ x - 1, y });
      vis[x - 1][y] = 1;
    }
    
    // For Right side Pixel or Cell
    if (validCoord(x, y + 1, n, m)
        && vis[x][y + 1] == 0
        && data[x][y + 1] == preColor) 
    {
      obj.push({ x, y + 1 });
      vis[x][y + 1] = 1;
    }
    
    // For Left side Pixel or Cell
    if (validCoord(x, y - 1, n, m)
        && vis[x][y - 1] == 0
        && data[x][y - 1] == preColor) 
    {
      obj.push({ x, y - 1 });
      vis[x][y - 1] = 1;
    }
  }
  
  // Printing The Changed Matrix Of Pixels
  for (int i = 0; i < n; i++) 
  {
    for (int j = 0; j < m; j++) 
    {
      cout << data[i][j] << " ";
    }
    cout << endl;
  }
  cout << endl;
}

// Driver Code
int main()
{
  int n, m, x, y, color;
  n = 8;
  m = 8;

  int data[8][8] = {
    { 1, 1, 1, 1, 1, 1, 1, 1 },
    { 1, 1, 1, 1, 1, 1, 0, 0 },
    { 1, 0, 0, 1, 1, 0, 1, 1 },
    { 1, 2, 2, 2, 2, 0, 1, 0 },
    { 1, 1, 1, 2, 2, 0, 1, 0 },
    { 1, 1, 1, 2, 2, 2, 2, 0 },
    { 1, 1, 1, 1, 1, 2, 1, 1 },
    { 1, 1, 1, 1, 1, 2, 2, 1 },
  };

  x = 4, y = 4, color = 3;
  
  // Function Call
  bfs(n, m, data, x, y, color);
  return 0;
}
```

输出：

```
1 1 1 1 1 1 1 1 
1 1 1 1 1 1 0 0 
1 0 0 1 1 0 1 1 
1 3 3 3 3 0 1 0 
1 1 1 3 3 0 1 0 
1 1 1 3 3 3 3 0 
1 1 1 1 1 3 1 1 
1 1 1 1 1 3 3 1 
```

参考：

<http://en.wikipedia.org/wiki/Flood_fill>