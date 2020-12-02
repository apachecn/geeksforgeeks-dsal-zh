# 用 1 的

填充整个矩阵所需的最短时间

> 原文： [https://www.geeksforgeeks.org/minimum-time-required-to-fill-the-entire-matrix-with-1s/](https://www.geeksforgeeks.org/minimum-time-required-to-fill-the-entire-matrix-with-1s/)

给定大小为`N`的矩阵，该矩阵由`0`和`1`组成，任务是找出用[`1`的。 矩阵中的每个`1`都可以在其八个相邻单元中将所有`0`转换为`1`。 **（i，j）**上存在的`1`可以将位置**（i，j -1）**，**（i，j + 1）**，**（i-1，j）**，**（i + 1，j）**，**（i-1，j-1）**，**（i-1，j + 1）**，**（i + 1，j-1）**， **（i + 1，j + 1）**。

**示例**：

> **输入**：N = 3，mtrx [] [] = {{1,0,0}，{0,0,1}，{0,0,0}}
> **输出 **：2
> **说明**：
> 最初，矩阵看起来是
>`1`，0、0
> 0、0，`1`
> 0，0，0
> 在第一时刻之后，新矩阵为
> 1，1，1，
> 1，1，1，
> 0，1，1 [
> 在第二个瞬间之后，剩余的 0 将转换为 1。
> 
> **输入**：N = 5，
> mtrx [] [] = {{0,0,0,0,0}，
> {1,0,0,0,0}，
> {0,0,0,0,0}，
> {0,0,1,0,0}，
> {0,0,0,1,0}}
> **输出**：3

**方法**：
为了解决此问题，我们使用 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 方法。 遍历矩阵并将矩阵的索引初始存储为 1。 循环直到队列变空并将所有队列元素的相邻有效单元格转换为 1。答案是，BFS 遍历的级别数导致至少一个 0 到 1 的转换。

以下代码是上述方法的实现：

## C++

```cpp

// C++ program to calculate the number of steps
// in fill all entire matrix with '1'
#include<bits/stdc++.h>
using namespace std;

// Function to return total number 
// of steps required to fill
// entire matrix with '1'
int numberOfSteps(int n,vector<vector<int>> mtrx)
{
    // Queue to store indices with 1
    queue<pair<int,int>> q;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (mtrx[i][j] == 1) {
                q.push({i,j});
            }
        }
    }

    // Intialise step variable as zero
    int step = 0 ;

    // BFS approach
    while (!q.empty())
    {
        int qsize = q.size();
        // Visit all indices with 1 and
        // fill its neighbouring cells by 1
        while (qsize--) 
        {
            pair<int,int> p  = q.front();
            q.pop();
            int i = p.first;
            int j = p.second;
            // Convert the neighbour from '0' to '1'
            if((j > 0) && mtrx[i][j-1] == 0)
            {
                mtrx[i][j-1] = 1;
                q.push({i,j-1});
            }
            // Convert the neighbour from '0' to '1'
            if((i < n-1) && mtrx[i+1][j] == 0)
            {
                mtrx[i+1][j] = 1;
                q.push({i+1,j});
            }
            // Convert the neighbour from '0' to '1'
            if((j < n-1) && mtrx[i][j+1] == 0)
            {
                mtrx[i][j+1] = 1;
                q.push({i,j + 1});
            }
            // Convert the neighbour from '0' to '1'
            if((i > 0) && mtrx[i-1][j] == 0)
            {
                mtrx[i-1][j] = 1;
                q.push({i-1,j});
            }
            // Convert the neighbour from '0' to '1'
            if((i > 0) && (j > 0) && 
                                mtrx[i-1][j-1] == 0)
            {
                mtrx[i-1][j-1] = 1;
                q.push({i-1,j-1});
            }
            // Convert the neighbour from '0' to '1'
            if((i > 0) && (j < (n-1)) && 
                                mtrx[i-1][j+1] == 0)
            {
                mtrx[i-1][j+1] = 1;
                q.push({i-1,j+1});
            }
            // Convert the neighbour from '0' to '1'
            if((i < (n-1)) && (j < (n-1)) && 
                                mtrx[i+1][j+1] == 0)
            {
                mtrx[i+1][j+1] = 1;
                q.push({i+1,j + 1});
            }
            // Convert the neighbour from '0' to '1'
            if((i < (n-1)) && (j > 0) && 
                                mtrx[i+1][j-1] == 0)
            {
                mtrx[i+1][j-1] = 1;
                q.push({i+1,j-1});
            }
        } 
        //count steps
        step++;
    }

    return step-1;
}

// Driver code
int main()
{
    int n = 5 ; //dimension of matrix NXN
    vector<vector<int>> mtrx = {{0,0,0,0,0},
                                {1,0,0,0,0},
                                {0,0,0,0,0},
                                {0,0,1,0,0},
                                {0,0,0,1,0}};
    // Print number of steps
    cout << numberOfSteps(n, mtrx);

    return 0;
}

```

## Java

```java

// Java program to calculate the
// number of steps in fill all 
// entire matrix with '1'
import java.util.*;

class GFG{

static class pair
{ 
    int first, second;

    public pair(int first, int second)  
    { 
        this.first = first; 
        this.second = second; 
    }    
}

// Function to return total number 
// of steps required to fill
// entire matrix with '1'
static int numberOfSteps(int n, int[][] mtrx)
{

    // Queue to store indices with 1
    Queue<pair> q = new LinkedList<>();

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            if (mtrx[i][j] == 1) 
            {
                q.add(new pair(i, j));
            }
        }
    }

    // Intialise step variable as zero
    int step = 0;

    // BFS approach
    while (!q.isEmpty())
    {
        int qsize = q.size();

        // Visit all indices with 1 and
        // fill its neighbouring cells by 1
        while (qsize-- > 0) 
        {
            pair p  = q.peek();
            q.remove();

            int i = p.first;
            int j = p.second;

            // Convert the neighbour from '0' to '1'
            if ((j > 0) && mtrx[i][j - 1] == 0)
            {
                mtrx[i][j - 1] = 1;
                q.add(new pair(i, j - 1));
            }

            // Convert the neighbour from '0' to '1'
            if ((i < n - 1) && mtrx[i + 1][j] == 0)
            {
                mtrx[i + 1][j] = 1;
                q.add(new pair(i + 1, j));
            }

            // Convert the neighbour from '0' to '1'
            if ((j < n - 1) && mtrx[i][j + 1] == 0)
            {
                mtrx[i][j + 1] = 1;
                q.add(new pair(i, j + 1));
            }

            // Convert the neighbour from '0' to '1'
            if ((i > 0) && mtrx[i - 1][j] == 0)
            {
                mtrx[i - 1][j] = 1;
                q.add(new pair(i - 1, j));
            }

            // Convert the neighbour from '0' to '1'
            if ((i > 0) && (j > 0) && 
                mtrx[i - 1][j - 1] == 0)
            {
                mtrx[i - 1][j - 1] = 1;
                q.add(new pair(i - 1, j - 1));
            }

            // Convert the neighbour from '0' to '1'
            if ((i > 0) && (j < (n - 1)) && 
                mtrx[i - 1][j + 1] == 0)
            {
                mtrx[i - 1][j + 1] = 1;
                q.add(new pair(i - 1, j + 1));
            }

            // Convert the neighbour from '0' to '1'
            if ((i < (n - 1)) && (j < (n - 1)) && 
                mtrx[i + 1][j + 1] == 0)
            {
                mtrx[i + 1][j + 1] = 1;
                q.add(new pair(i + 1, j + 1));
            }

            // Convert the neighbour from '0' to '1'
            if ((i < (n - 1)) && (j > 0) && 
                mtrx[i + 1][j - 1] == 0)
            {
                mtrx[i + 1][j - 1] = 1;
                q.add(new pair(i + 1, j - 1));
            }
        } 

        // Count steps
        step++;
    }
    return step - 1;
}

// Driver code
public static void main(String[] args)
{

    // Dimension of matrix NXN
    int n = 5; 
    int [][]mtrx = { { 0, 0, 0, 0, 0 },
                     { 1, 0, 0, 0, 0 },
                     { 0, 0, 0, 0, 0 },
                     { 0, 0, 1, 0, 0 },
                     { 0, 0, 0, 1, 0 } };

    // Print number of steps
    System.out.print(numberOfSteps(n, mtrx));
}
}

// This code is contributed by Amit Katiyar

```

## Python

```py

# Python 3 program to calculate the number of steps
# in fill all entire matrix with '1'

# Function to return total number 
# of steps required to fill
# entire matrix with '1'
def numberOfSteps(n,mtrx):

    # Queue to store indices with 1
    q = []
    for i in range(n):
        for j in range(n):
            if (mtrx[i][j] == 1):
                q.append([i,j])

    # Intialise step variable as zero
    step = 0

    # BFS approach
    while (len(q)):
        qsize = len(q)

        # Visit all indices with 1 and
        # fill its neighbouring cells by 1
        while(qsize):
            p = q[0]
            q.remove(q[0])
            i = p[0]
            j = p[1]

            # Convert the neighbour from '0' to '1'
            if((j > 0) and mtrx[i][j - 1] == 0):
                mtrx[i][j - 1] = 1
                q.append([i, j - 1])

            # Convert the neighbour from '0' to '1'
            if((i < n-1) and mtrx[i + 1][j] == 0):
                mtrx[i + 1][j] = 1
                q.append([i + 1, j])

            # Convert the neighbour from '0' to '1'
            if((j < n-1) and mtrx[i][j + 1] == 0):
                mtrx[i][j + 1] = 1
                q.append([i, j + 1])

            # Convert the neighbour from '0' to '1'
            if((i > 0) and mtrx[i - 1][j] == 0):
                mtrx[i - 1][j] = 1
                q.append([i - 1, j])

            # Convert the neighbour from '0' to '1'
            if((i > 0) and (j > 0) and
                                   mtrx[i - 1][j - 1] == 0):
                mtrx[i - 1][j - 1] = 1
                q.append([i - 1, j - 1])

            # Convert the neighbour from '0' to '1'
            if((i > 0) and (j < (n-1)) and 
                                    mtrx[i - 1][j + 1] == 0):
                mtrx[i - 1][j + 1] = 1
                q.append([i - 1, j + 1])

            # Convert the neighbour from '0' to '1'
            if((i < (n - 1)) and (j < (n - 1)) and
                                     mtrx[i + 1][j + 1] == 0):
                mtrx[i + 1][j + 1] = 1
                q.append([i + 1, j + 1])

            # Convert the neighbour from '0' to '1'
            if((i < (n - 1)) and (j > 0) and
                                    mtrx[i + 1][j - 1] == 0):
                mtrx[i + 1][j - 1] = 1
                q.append([i + 1,j - 1])

            qsize -= 1

        #count steps
        step += 1

    return step-1

# Driver code
if __name__ == '__main__':

    #dimension of matrix NXN
    n = 5
    mtrx = [[ 0, 0, 0, 0, 0 ],
            [ 1, 0, 0, 0, 0 ],
            [ 0, 0, 0, 0, 0 ],
            [ 0, 0, 1, 0, 0 ],
            [ 0, 0, 0, 1, 0 ]]

    # Print number of steps
    print(numberOfSteps(n, mtrx))

# This code is contributed by Samarth

```

## C#

```cs

// C# program to calculate the
// number of steps in fill all 
// entire matrix with '1'
using System;
using System.Collections.Generic;
class GFG{

public class pair
{ 
  public int first, second;
  public pair(int first, int second)  
  { 
    this.first = first; 
    this.second = second; 
  }    
}

// Function to return total number 
// of steps required to fill
// entire matrix with '1'
static int numberOfSteps(int n, 
                         int[,] mtrx)
{
  // Queue to store indices with 1
  Queue<pair> q = new Queue<pair>();

  for(int i = 0; i < n; i++)
  {
    for(int j = 0; j < n; j++)
    {
      if (mtrx[i, j] == 1) 
      {
        q.Enqueue(new pair(i, j));
      }
    }
  }

  // Intialise step variable as zero
  int step = 0;

  // BFS approach
  while (q.Count != 0)
  {
    int qsize = q.Count;

    // Visit all indices 
    // with 1 and fill 
    // its neighbouring 
    // cells by 1
    while (qsize-- > 0) 
    {
      pair p  = q.Peek();
      q.Dequeue();
      int i = p.first;
      int j = p.second;

      // Convert the neighbour 
      // from '0' to '1'
      if ((j > 0) && 
           mtrx[i, j - 1] == 0)
      {
        mtrx[i, j - 1] = 1;
        q.Enqueue(new pair(i, j - 1));
      }

      // Convert the neighbour 
      // from '0' to '1'
      if ((i < n - 1) && 
           mtrx[i + 1, j] == 0)
      {
        mtrx[i + 1, j] = 1;
        q.Enqueue(new pair(i + 1, j));
      }

      // Convert the neighbour 
      // from '0' to '1'
      if ((j < n - 1) && 
           mtrx[i, j + 1] == 0)
      {
        mtrx[i, j + 1] = 1;
        q.Enqueue(new pair(i, j + 1));
      }

      // Convert the neighbour 
      // from '0' to '1'
      if ((i > 0) && 
           mtrx[i - 1, j] == 0)
      {
        mtrx[i - 1, j] = 1;
        q.Enqueue(new pair(i - 1, j));
      }

      // Convert the neighbour 
      // from '0' to '1'
      if ((i > 0) && (j > 0) && 
           mtrx[i - 1, j - 1] == 0)
      {
        mtrx[i - 1, j - 1] = 1;
        q.Enqueue(new pair(i - 1, j - 1));
      }

      // Convert the neighbour 
      // from '0' to '1'
      if ((i > 0) && (j < (n - 1)) && 
           mtrx[i - 1, j + 1] == 0)
      {
        mtrx[i - 1, j + 1] = 1;
        q.Enqueue(new pair(i - 1, j + 1));
      }

      // Convert the neighbour 
      // from '0' to '1'
      if ((i < (n - 1)) && (j < (n - 1)) && 
           mtrx[i + 1, j + 1] == 0)
      {
        mtrx[i + 1, j + 1] = 1;
        q.Enqueue(new pair(i + 1, j + 1));
      }

      // Convert the neighbour 
      // from '0' to '1'
      if ((i < (n - 1)) && (j > 0) && 
           mtrx[i + 1, j - 1] == 0)
      {
        mtrx[i + 1, j - 1] = 1;
        q.Enqueue(new pair(i + 1, j - 1));
      }
    } 

    // Count steps
    step++;
  }
  return step - 1;
}

// Driver code
public static void Main(String[] args)
{
  // Dimension of matrix NXN
  int n = 5; 
  int [,]mtrx = {{0, 0, 0, 0, 0},
                 {1, 0, 0, 0, 0},
                 {0, 0, 0, 0, 0},
                 {0, 0, 1, 0, 0},
                 {0, 0, 0, 1, 0}};

  // Print number of steps
  Console.Write(numberOfSteps(n, mtrx));
}
}

// This code is contributed by Rajput-Ji

```

**Output:** 

```
3

```

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。