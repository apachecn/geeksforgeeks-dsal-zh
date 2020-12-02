# 从给定单元格到矩阵的所有其他单元格的最小距离

> 原文： [https://www.geeksforgeeks.org/minimum-distance-from-a-given-cell-to-all-other-cells-of-a-matrix/](https://www.geeksforgeeks.org/minimum-distance-from-a-given-cell-to-all-other-cells-of-a-matrix/)

给定两个整数`R`和`C`，表示矩阵中的行和列数，以及两个整数`X`和`Y`， 任务是找到从给定单元格到矩阵所有其他单元格的最小距离。

**示例**：

> **输入**：R = 5，C = 5，X = 2，Y = 2
> **输出**：
> 2 2 2 2 2
> 2 1 1 1 2
> 2 1 0 1 2
> 2 1 1 1 2 2
> 2 2 2 2 2
> 
> **输入**：R = 5，C = 5，X = 1，Y = 1
> **输出**：
> 1 1 1 2 3
> 1 0 1 2 3
> 1 1 1 2 3
> 2 2 2 2 3
> 3 3 3 3 3

**方法**：
请按照以下步骤解决问题：

*   将初始像元的距离分配为`0`。
*   初始化[队列](http://www.geeksforgeeks.org/queue-data-structure/)，然后将 **{X，Y}** 对插入**队列**中。
*   进行迭代，直到**队列**不为空，并为每个未访问的单元分配当前距离，然后使用[[G] [BFS](http://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 技术。
*   在末尾打印每个单元格的距离。

下面是上述方法的实现：

## C ++

```

// C++ Program to implement 
// the above approach 
#include <bits/stdc++.h> 
using namespace std; 

int mat[1001][1001]; 
int r, c, x, y; 

// Stores the accessible directions 
int dx[] = { 0, -1, -1, -1, 0, 1, 1, 1 }; 
int dy[] = { 1, 1, 0, -1, -1, -1, 0, 1 }; 

// Function to find the minimum distance from a 
// given cell to all other cells in the matrix 
void FindMinimumDistance() 
{ 
    // Stores the accessible cells 
    // from current cell 
    queue<pair<int, int> > q; 

    // Insert pair (x, y) 
    q.push({ x, y }); 
    mat[x][y] = 0; 

    // Iterate untill queue is empty 
    while (!q.empty()) { 

        // Extract the pair 
        x = q.front().first; 
        y = q.front().second; 

        // Pop them 
        q.pop(); 

        for (int i = 0; i < 8; i++) { 
            int a = x + dx[i]; 
            int b = y + dy[i]; 

            // Checking boundary condition 
            if (a < 0 || a >= r || b >= c || b < 0) 
                continue; 

            // If the cell is not visited 
            if (mat[a][b] == 0) { 

                // Assign the minimum distance 
                mat[a][b] = mat[x][y] + 1; 

                // Insert the traversed neighbour 
                // into the queue 
                q.push({ a, b }); 
            } 
        } 
    } 
} 

// Driver Code 
int main() 
{ 
    r = 5, c = 5, x = 1, y = 1; 

    int t = x; 
    int l = y; 
    mat[x][y] = 0; 

    FindMinimumDistance(); 

    mat[t][l] = 0; 

    // Print the required distances 
    for (int i = 0; i < r; i++) { 
        for (int j = 0; j < c; j++) { 
            cout << mat[i][j] << " "; 
        } 
        cout << endl; 
    } 
} 

```

## 爪哇

```

// Java program to implement 
// the above approach 
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

static int [][]mat = new int[1001][1001]; 
static int r, c, x, y; 

// Stores the accessible directions 
static int dx[] = { 0, -1, -1, -1, 0, 1, 1, 1 }; 
static int dy[] = { 1, 1, 0, -1, -1, -1, 0, 1 }; 

// Function to find the minimum distance from a 
// given cell to all other cells in the matrix 
static void FindMinimumDistance() 
{ 

    // Stores the accessible cells 
    // from current cell 
    Queue<pair> q = new LinkedList<>(); 

    // Insert pair (x, y) 
    q.add(new pair(x, y)); 
    mat[x][y] = 0; 

    // Iterate untill queue is empty 
    while (!q.isEmpty()) 
    { 

        // Extract the pair 
        x = q.peek().first; 
        y = q.peek().second; 

        // Pop them 
        q.remove(); 

        for(int i = 0; i < 8; i++) 
        { 
            int a = x + dx[i]; 
            int b = y + dy[i]; 

            // Checking boundary condition 
            if (a < 0 || a >= r || 
               b >= c || b < 0) 
                continue; 

            // If the cell is not visited 
            if (mat[a][b] == 0)  
            { 

                // Assign the minimum distance 
                mat[a][b] = mat[x][y] + 1; 

                // Insert the traversed neighbour 
                // into the queue 
                q.add(new pair(a, b)); 
            } 
        } 
    } 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    r = 5; c = 5; x = 1; y = 1; 

    int t = x; 
    int l = y; 
    mat[x][y] = 0; 

    FindMinimumDistance(); 

    mat[t][l] = 0; 

    // Print the required distances 
    for(int i = 0; i < r; i++) 
    { 
        for(int j = 0; j < c; j++) 
        { 
            System.out.print(mat[i][j] + " "); 
        } 
        System.out.println(); 
    } 
} 
} 

// This code is contributed by Amit Katiyar

```

## Python3

```

# Python3 program to implement 
# the above approach 
mat = [[0 for x in range(1001)]  
          for y in range(1001)] 

# Stores the accessible directions 
dx = [ 0, -1, -1, -1, 0, 1, 1, 1 ] 
dy = [ 1, 1, 0, -1, -1, -1, 0, 1 ] 

# Function to find the minimum distance 
# from a given cell to all other cells 
# in the matrix 
def FindMinimumDistance(): 

    global x, y, r, c 

    # Stores the accessible cells 
    # from current cell 
    q = [] 

    # Insert pair (x, y) 
    q.append([x, y]) 
    mat[x][y] = 0

    # Iterate untill queue is empty 
    while(len(q) != 0): 

        # Extract the pair 
        x = q[0][0] 
        y = q[0][1] 

        # Pop them 
        q.pop(0) 

        for i in range(8): 
            a = x + dx[i] 
            b = y + dy[i] 

            # Checking boundary condition 
            if(a < 0 or a >= r or 
              b >= c or b < 0): 
                continue

            # If the cell is not visited 
            if(mat[a][b] == 0): 

                # Assign the minimum distance 
                mat[a][b] = mat[x][y] + 1

                # Insert the traversed neighbour 
                # into the queue 
                q.append([a, b]) 

# Driver Code 
r = 5
c = 5
x = 1
y = 1
t = x 
l = y 

mat[x][y] = 0

FindMinimumDistance() 
mat[t][l] = 0

# Print the required distances  
for i in range(r): 
    for j in range(c): 
        print(mat[i][j], end = " ") 

    print() 

# This code is contributed by Shivam Singh 

```

## C＃

```

// C# program to implement 
// the above approach 
using System; 
using System.Collections.Generic; 

class GFG{ 

class pair 
{  
    public int first, second;  
    public pair(int first, int second)  
    {  
        this.first = first;  
        this.second = second;  
    }  
}  

static int [,]mat = new int[1001, 1001]; 
static int r, c, x, y; 

// Stores the accessible directions 
static int []dx = { 0, -1, -1, -1, 0, 1, 1, 1 }; 
static int []dy = { 1, 1, 0, -1, -1, -1, 0, 1 }; 

// Function to find the minimum distance from a 
// given cell to all other cells in the matrix 
static void FindMinimumDistance() 
{ 

    // Stores the accessible cells 
    // from current cell 
    Queue<pair> q = new Queue<pair>(); 

    // Insert pair (x, y) 
    q.Enqueue(new pair(x, y)); 
    mat[x, y] = 0; 

    // Iterate untill queue is empty 
    while (q.Count != 0) 
    { 

        // Extract the pair 
        x = q.Peek().first; 
        y = q.Peek().second; 

        // Pop them 
        q.Dequeue(); 

        for(int i = 0; i < 8; i++) 
        { 
            int a = x + dx[i]; 
            int b = y + dy[i]; 

            // Checking boundary condition 
            if (a < 0 || a >= r || 
                b >= c || b < 0) 
                continue; 

            // If the cell is not visited 
            if (mat[a, b] == 0)  
            { 

                // Assign the minimum distance 
                mat[a, b] = mat[x, y] + 1; 

                // Insert the traversed neighbour 
                // into the queue 
                q.Enqueue(new pair(a, b)); 
            } 
        } 
    } 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    r = 5; c = 5; x = 1; y = 1; 

    int t = x; 
    int l = y; 
    mat[x, y] = 0; 

    FindMinimumDistance(); 

    mat[t, l] = 0; 

    // Print the required distances 
    for(int i = 0; i < r; i++) 
    { 
        for(int j = 0; j < c; j++) 
        { 
            Console.Write(mat[i, j] + " "); 
        } 
        Console.WriteLine(); 
    } 
} 
} 

// This code is contributed by shikhasingrajput 

```

**Output:** 

```
1 1 1 2 3 
1 0 1 2 3 
1 1 1 2 3 
2 2 2 2 3 
3 3 3 3 3

```

***时间复杂度**：O（R * C）*
***辅助空间**：O（R * C）*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。