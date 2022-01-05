# 洪水填充算法

> 原文:[https://www.geeksforgeeks.org/flood-fill-algorithm/](https://www.geeksforgeeks.org/flood-fill-algorithm/)

给定 2D 屏幕 **arr[][]** ，其中每个 **arr[i][j]** 是表示该像素颜色的整数，也给定像素 **(X，Y)** 和颜色 **C** 的位置，任务是用给定颜色替换给定像素和所有相邻同色像素的颜色。
**例:**

> **输入:** arr[][] = {
> {1，1，1，1，1，1，1}，
> {1，1，1，1，1，0，0}，
> {1，0，0，1，1，0，1，1，1，1}，
> {1， **2，2，2，2，** 0，1，0}，
> {1，1，1， **2，2，** 1，1， **2，2，** 1}}
> X = 4，Y = 4， C = 3
> **输出:**
> 1 1 1 1 1 1 1 1
> 1 1 1 1 1 0 0
> 1 0 1 0 1 0 1 1 1
> 1**3 3 3 3**0 1 0
> 1 1**3 3**0 1 0
> 1 1 1**3 3 3**0
> 1 1 1 1 1**3【T33 1 1 1 **3 3** 1
> **说明:**
> 给定 2D 屏幕中的值表示像素的颜色。 X 和 Y 是画笔的坐标，C 是应该替换屏幕上先前颜色的颜色[X][Y]以及周围所有颜色相同的像素。因此所有的 2 都被 3 取代了。**

**BFS 进场:**思路是用 [BFS 遍历](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)用新颜色替换颜色。

*   创建一个空的[队列](https://www.geeksforgeeks.org/queue-data-structure/)让我们说 *Q* 。
*   按输入中给定的像素起始位置，并对其应用替换颜色。
*   迭代直到 **Q** 不为空，弹出前节点(像素位置)。
*   检查与当前像素相邻的像素，如果有效，将其推入队列(没有用替换颜色着色，并且颜色与旧颜色相同)。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if
// the given pixel is valid
bool isValid(int screen[][8], int m, int n, int x, int y, int prevC, int newC)
{
    if(x < 0 || x >= m || y < 0 || y >= n || screen[x][y] != prevC
       || screen[x][y]== newC)
        return false;
    return true;
}

// FloodFill function
void floodFill(int screen[][8], int m, int n, int x, int y, int prevC, int newC)
{
    vector<pair<int,int>> queue;

    // Append the position of starting
    // pixel of the component
    pair<int,int> p(x,y);
    queue.push_back(p);

    // Color the pixel with the new color
    screen[x][y] = newC;

    // While the queue is not empty i.e. the
    // whole component having prevC color
    // is not colored with newC color
    while(queue.size() > 0)
    {
        // Dequeue the front node
        pair<int,int> currPixel = queue[queue.size() - 1];
        queue.pop_back();

        int posX = currPixel.first;
        int posY = currPixel.second;

        // Check if the adjacent
        // pixels are valid
        if(isValid(screen, m, n, posX + 1, posY, prevC, newC))
        {
            // Color with newC
            // if valid and enqueue
            screen[posX + 1][posY] = newC;
            p.first = posX + 1;
            p.second = posY;
            queue.push_back(p);
        }

        if(isValid(screen, m, n, posX-1, posY, prevC, newC))
        {
            screen[posX-1][posY]= newC;
            p.first = posX-1;
            p.second = posY;
            queue.push_back(p);
        }

        if(isValid(screen, m, n, posX, posY + 1, prevC, newC))
        {
            screen[posX][posY + 1]= newC;
            p.first = posX;
            p.second = posY + 1;
            queue.push_back(p);
        }

        if(isValid(screen, m, n, posX, posY-1, prevC, newC))
        {
            screen[posX][posY-1]= newC;
            p.first = posX;
            p.second = posY-1;
            queue.push_back(p);
        }
    }
}

int main()
{
    int screen[][8] ={
    {1, 1, 1, 1, 1, 1, 1, 1},
    {1, 1, 1, 1, 1, 1, 0, 0},
    {1, 0, 0, 1, 1, 0, 1, 1},
    {1, 2, 2, 2, 2, 0, 1, 0},
    {1, 1, 1, 2, 2, 0, 1, 0},
    {1, 1, 1, 2, 2, 2, 2, 0},
    {1, 1, 1, 1, 1, 2, 1, 1},
    {1, 1, 1, 1, 1, 2, 2, 1}};

    // Row of the display
    int m = 8;

    // Column of the display
    int n = 8;

    // Co-ordinate provided by the user
    int x = 4;
    int y = 4;

    // Current color at that co-ordinate
    int prevC = screen[x][y];

    // New color that has to be filled
    int newC = 3;
    floodFill(screen, m, n, x, y, prevC, newC);

    // Printing the updated screen
    for(int i = 0; i < m; i++)
    {
        for(int j = 0; j < n; j++)
        {
            cout << screen[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}

// This code is contributed by suresh07.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.awt.Point;
public class Main
{
    // Function that returns true if
    // the given pixel is valid
    static boolean isValid(int[][] screen, int m, int n, int x, int y, int prevC, int newC)
    {
        if(x < 0 || x >= m || y < 0 || y >= n || screen[x][y] != prevC
           || screen[x][y]== newC)
            return false;
        return true;
    }

    // FloodFill function
    static void floodFill(int[][] screen, int m, int n, int x, int y, int prevC, int newC)
    {
        Vector<Point> queue = new Vector<Point>();

        // Append the position of starting
        // pixel of the component
        queue.add(new Point(x, y));

        // Color the pixel with the new color
        screen[x][y] = newC;

        // While the queue is not empty i.e. the
        // whole component having prevC color
        // is not colored with newC color
        while(queue.size() > 0)
        {
            // Dequeue the front node
            Point currPixel = queue.get(queue.size() - 1);
            queue.remove(queue.size() - 1);

            int posX = currPixel.x;
            int posY = currPixel.y;

            // Check if the adjacent
            // pixels are valid
            if(isValid(screen, m, n, posX + 1, posY, prevC, newC))
            {
                // Color with newC
                // if valid and enqueue
                screen[posX + 1][posY] = newC;
                queue.add(new Point(posX + 1, posY));
            }

            if(isValid(screen, m, n, posX-1, posY, prevC, newC))
            {
                screen[posX-1][posY]= newC;
                queue.add(new Point(posX-1, posY));
            }

            if(isValid(screen, m, n, posX, posY + 1, prevC, newC))
            {
                screen[posX][posY + 1]= newC;
                queue.add(new Point(posX, posY + 1));
            }

            if(isValid(screen, m, n, posX, posY-1, prevC, newC))
            {
                screen[posX][posY-1]= newC;
                queue.add(new Point(posX, posY-1));
            }
        }
    }

    public static void main(String[] args) {
        int[][] screen ={
        {1, 1, 1, 1, 1, 1, 1, 1},
        {1, 1, 1, 1, 1, 1, 0, 0},
        {1, 0, 0, 1, 1, 0, 1, 1},
        {1, 2, 2, 2, 2, 0, 1, 0},
        {1, 1, 1, 2, 2, 0, 1, 0},
        {1, 1, 1, 2, 2, 2, 2, 0},
        {1, 1, 1, 1, 1, 2, 1, 1},
        {1, 1, 1, 1, 1, 2, 2, 1}};

        // Row of the display
        int m = screen.length;

        // Column of the display
        int n = screen.length;

        // Co-ordinate provided by the user
        int x = 4;
        int y = 4;

        // Current color at that co-ordinate
        int prevC = screen[x][y];

        // New color that has to be filled
        int newC = 3;
        floodFill(screen, m, n, x, y, prevC, newC);

        // Printing the updated screen
        for(int i = 0; i < m; i++)
        {
            for(int j = 0; j < n; j++)
            {
                System.out.print(screen[i][j] + " ");
            }
            System.out.println();
        }
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if
# the given pixel is valid
def isValid(screen, m, n, x, y, prevC, newC):
    if x<0 or x>= m\
       or y<0 or y>= n or\
       screen[x][y]!= prevC\
       or screen[x][y]== newC:
        return False
    return True

# FloodFill function
def floodFill(screen, 
            m, n, x, 
            y, prevC, newC):
    queue = []

    # Append the position of starting
    # pixel of the component
    queue.append([x, y])

    # Color the pixel with the new color
    screen[x][y] = newC

    # While the queue is not empty i.e. the
    # whole component having prevC color
    # is not colored with newC color
    while queue:

        # Dequeue the front node
        currPixel = queue.pop()

        posX = currPixel[0]
        posY = currPixel[1]

        # Check if the adjacent
        # pixels are valid
        if isValid(screen, m, n, 
                posX + 1, posY, 
                        prevC, newC):

            # Color with newC
            # if valid and enqueue
            screen[posX + 1][posY] = newC
            queue.append([posX + 1, posY])

        if isValid(screen, m, n, 
                    posX-1, posY, 
                        prevC, newC):
            screen[posX-1][posY]= newC
            queue.append([posX-1, posY])

        if isValid(screen, m, n, 
                posX, posY + 1, 
                        prevC, newC):
            screen[posX][posY + 1]= newC
            queue.append([posX, posY + 1])

        if isValid(screen, m, n, 
                    posX, posY-1, 
                        prevC, newC):
            screen[posX][posY-1]= newC
            queue.append([posX, posY-1])

# Driver code
screen =[
[1, 1, 1, 1, 1, 1, 1, 1],
[1, 1, 1, 1, 1, 1, 0, 0],
[1, 0, 0, 1, 1, 0, 1, 1],
[1, 2, 2, 2, 2, 0, 1, 0],
[1, 1, 1, 2, 2, 0, 1, 0],
[1, 1, 1, 2, 2, 2, 2, 0],
[1, 1, 1, 1, 1, 2, 1, 1],
[1, 1, 1, 1, 1, 2, 2, 1],
    ]

# Row of the display
m = len(screen)

# Column of the display
n = len(screen[0])

# Co-ordinate provided by the user
x = 4
y = 4

# Current color at that co-ordinate
prevC = screen[x][y]

# New color that has to be filled
newC = 3

floodFill(screen, m, n, x, y, prevC, newC)

# Printing the updated screen
for i in range(m):
    for j in range(n):
        print(screen[i][j], end =' ')
    print()
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG {

    // Function that returns true if
    // the given pixel is valid
    static bool isValid(int[,] screen, int m, int n, int x, int y, int prevC, int newC)
    {
        if(x < 0 || x >= m || y < 0 || y >= n || screen[x, y] != prevC
           || screen[x,y]== newC)
            return false;
        return true;
    }

    // FloodFill function
    static void floodFill(int[,] screen, int m, int n, int x, int y, int prevC, int newC)
    {
        List<Tuple<int,int>> queue = new List<Tuple<int,int>>();

        // Append the position of starting
        // pixel of the component
        queue.Add(new Tuple<int,int>(x, y));

        // Color the pixel with the new color
        screen[x,y] = newC;

        // While the queue is not empty i.e. the
        // whole component having prevC color
        // is not colored with newC color
        while(queue.Count > 0)
        {
            // Dequeue the front node
            Tuple<int,int> currPixel = queue[queue.Count - 1];
            queue.RemoveAt(queue.Count - 1);

            int posX = currPixel.Item1;
            int posY = currPixel.Item2;

            // Check if the adjacent
            // pixels are valid
            if(isValid(screen, m, n, posX + 1, posY, prevC, newC))
            {
                // Color with newC
                // if valid and enqueue
                screen[posX + 1,posY] = newC;
                queue.Add(new Tuple<int,int>(posX + 1, posY));
            }

            if(isValid(screen, m, n, posX-1, posY, prevC, newC))
            {
                screen[posX-1,posY]= newC;
                queue.Add(new Tuple<int,int>(posX-1, posY));
            }

            if(isValid(screen, m, n, posX, posY + 1, prevC, newC))
            {
                screen[posX,posY + 1]= newC;
                queue.Add(new Tuple<int,int>(posX, posY + 1));
            }

            if(isValid(screen, m, n, posX, posY-1, prevC, newC))
            {
                screen[posX,posY-1]= newC;
                queue.Add(new Tuple<int,int>(posX, posY-1));
            }
        }
    }

  static void Main() {
    int[,] screen ={
    {1, 1, 1, 1, 1, 1, 1, 1},
    {1, 1, 1, 1, 1, 1, 0, 0},
    {1, 0, 0, 1, 1, 0, 1, 1},
    {1, 2, 2, 2, 2, 0, 1, 0},
    {1, 1, 1, 2, 2, 0, 1, 0},
    {1, 1, 1, 2, 2, 2, 2, 0},
    {1, 1, 1, 1, 1, 2, 1, 1},
    {1, 1, 1, 1, 1, 2, 2, 1}};

    // Row of the display
    int m = screen.GetLength(0);

    // Column of the display
    int n = screen.GetLength(1);

    // Co-ordinate provided by the user
    int x = 4;
    int y = 4;

    // Current color at that co-ordinate
    int prevC = screen[x,y];

    // New color that has to be filled
    int newC = 3;
    floodFill(screen, m, n, x, y, prevC, newC);

    // Printing the updated screen
    for(int i = 0; i < m; i++)
    {
        for(int j = 0; j < n; j++)
        {
            Console.Write(screen[i,j] + " ");
        }
        Console.WriteLine();
    }
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function that returns true if
    // the given pixel is valid
    function isValid(screen, m, n, x, y, prevC, newC)
    {
        if(x<0 || x>= m || y<0 || y>= n || screen[x][y]!= prevC
           || screen[x][y]== newC)
            return false;
        return true;
    }

    // FloodFill function
    function floodFill(screen, m, n, x, y, prevC, newC)
    {
        let queue = [];

        // Append the position of starting
        // pixel of the component
        queue.push([x, y]);

        // Color the pixel with the new color
        screen[x][y] = newC;

        // While the queue is not empty i.e. the
        // whole component having prevC color
        // is not colored with newC color
        while(queue.length > 0)
        {
            // Dequeue the front node
            currPixel = queue[queue.length - 1];
            queue.pop();

            let posX = currPixel[0];
            let posY = currPixel[1];

            // Check if the adjacent
            // pixels are valid
            if(isValid(screen, m, n, posX + 1, posY, prevC, newC))
            {
                // Color with newC
                // if valid and enqueue
                screen[posX + 1][posY] = newC;
                queue.push([posX + 1, posY]);
            }

            if(isValid(screen, m, n, posX-1, posY, prevC, newC))
            {
                screen[posX-1][posY]= newC;
                queue.push([posX-1, posY]);
            }

            if(isValid(screen, m, n, posX, posY + 1, prevC, newC))
            {
                screen[posX][posY + 1]= newC;
                queue.push([posX, posY + 1]);
            }

            if(isValid(screen, m, n, posX, posY-1, prevC, newC))
            {
                screen[posX][posY-1]= newC;
                queue.push([posX, posY-1]);
            }
        }
    }

    let screen =[
    [1, 1, 1, 1, 1, 1, 1, 1],
    [1, 1, 1, 1, 1, 1, 0, 0],
    [1, 0, 0, 1, 1, 0, 1, 1],
    [1, 2, 2, 2, 2, 0, 1, 0],
    [1, 1, 1, 2, 2, 0, 1, 0],
    [1, 1, 1, 2, 2, 2, 2, 0],
    [1, 1, 1, 1, 1, 2, 1, 1],
    [1, 1, 1, 1, 1, 2, 2, 1]];

    // Row of the display
    let m = screen.length;

    // Column of the display
    let n = screen[0].length;

    // Co-ordinate provided by the user
    let x = 4;
    let y = 4;

    // Current color at that co-ordinate
    let prevC = screen[x][y];

    // New color that has to be filled
    let newC = 3;

    floodFill(screen, m, n, x, y, prevC, newC);

    // Printing the updated screen
    for(let i = 0; i < m; i++)
    {
        for(let j = 0; j < n; j++)
        {
            document.write(screen[i][j] + " ");
        }
        document.write("</br>");
    }

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

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

**离散傅立叶变换方法:**类似地，离散傅立叶变换方法也可以用于实现洪水填充算法。