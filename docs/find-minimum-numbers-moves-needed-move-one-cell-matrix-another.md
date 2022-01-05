# 找出从矩阵的一个单元移动到另一个单元所需的最小移动次数

> 原文:[https://www . geesforgeks . org/find-最小-数字-移动-需要-移动-一个单元-矩阵-另一个/](https://www.geeksforgeeks.org/find-minimum-numbers-moves-needed-move-one-cell-matrix-another/)

给定一个由 1，0，2，3 填充的 N×N 矩阵(M)。找出从源移动到目标(接收器)所需的最小移动次数。同时仅遍历空白单元格。你可以上下左右移动。
一个单元格的值 **1** 表示来源。
单元格的值 **2** 表示目的地。
单元格 **3** 的值表示空白单元格。
单元格 **0** 的值表示空白墙。

**注意**:只有一个源和一个目的地，从源到目的地(宿)可能有多条路径。我们认为矩阵中的每一步都是“1”

**示例:**

```
Input : M[3][3] = {{ 0 , 3 , 2 },
                   { 3 , 3 , 0 },
                   { 1 , 3 , 0 }};
Output : 4 

Input : M[4][4] = {{ 3 , 3 , 1 , 0 },
                   { 3 , 0 , 3 , 3 },
                   { 2 , 3 , 0 , 3 },
                   { 0 , 3 , 3 , 3 }};
Output : 4
```

问于:[土坯面试](https://www.geeksforgeeks.org/adobe-interview-experience-set-41-software-engineer/)
。

![minimum_move](img/0309f6e58e9c0be41d7d925357545272.png)

想法是使用水平图(广度优先遍历)。将每个像元视为一个节点，任何两个相邻像元之间的每个边界都是一条边。所以节点总数是 N*N

1.  1.创建一个有 N*N 个节点(顶点)的空图。
2.  2.将所有节点推入图中。
3.  3.记下源顶点和汇顶点。
4.  4.现在应用水平图概念(我们使用 BFS 实现)。其中我们找到了从源顶点开始的每个节点的级别。之后，我们返回‘第[d]层’(d 是目的地)。(这是从源到宿的最小移动)

以下是上述想法的实现。

## C++

```
// C++ program to find the minimum numbers
// of moves needed to move from source to
// destination .
#include<bits/stdc++.h>
using namespace std;
#define N 4

class Graph
{
    int V ;
    list < int > *adj;
public :
    Graph( int V )
    {
        this->V = V ;
        adj = new list<int>[V];
    }
    void addEdge( int s , int d ) ;
    int BFS ( int s , int d) ;
};

// add edge to graph
void Graph :: addEdge ( int s , int d )
{
    adj[s].push_back(d);
    adj[d].push_back(s);
}

// Level  BFS function to find minimum path
// from source to sink
int Graph :: BFS(int s, int d)
{
    // Base case
    if (s == d)
        return 0;

    // make initial distance of all vertex -1
    // from source
    int *level = new int[V];
    for (int i = 0; i < V; i++)
        level[i] = -1  ;

    // Create a queue for BFS
    list<int> queue;

    // Mark the source node level[s] = '0'
    level[s] = 0 ;
    queue.push_back(s);

    // it will be used to get all adjacent
    // vertices of a vertex
    list<int>::iterator i;

    while (!queue.empty())
    {
        // Dequeue a vertex from queue
        s = queue.front();
        queue.pop_front();

        // Get all adjacent vertices of the
        // dequeued vertex s. If a adjacent has
        // not been visited ( level[i] < '0') ,
        // then update level[i] == parent_level[s] + 1
        // and enqueue it
        for (i = adj[s].begin(); i != adj[s].end(); ++i)
        {
            // Else, continue to do BFS
            if (level[*i] < 0 || level[*i] > level[s] + 1 )
            {
                level[*i] = level[s] + 1 ;
                queue.push_back(*i);
            }
        }

    }

    // return minimum moves from source to sink
    return level[d] ;
}

bool isSafe(int i, int j, int M[][N])
{
    if ((i < 0 || i >= N) ||
            (j < 0 || j >= N ) || M[i][j] == 0)
        return false;
    return true;
}

// Returns minimum numbers of  moves  from a source (a
// cell with value 1) to a destination (a cell with
// value 2)
int MinimumPath(int M[][N])
{
    int s , d ; // source and destination
    int V = N*N+2;
    Graph g(V);

    // create graph with n*n node
    // each cell consider as node
    int k = 1 ; // Number of current vertex
    for (int i =0 ; i < N ; i++)
    {
        for (int j = 0 ; j < N; j++)
        {
            if (M[i][j] != 0)
            {
                // connect all 4 adjacent cell to
                // current cell
                if ( isSafe ( i , j+1 , M ) )
                    g.addEdge ( k , k+1 );
                if ( isSafe ( i , j-1 , M ) )
                    g.addEdge ( k , k-1 );
                if (j< N-1 && isSafe ( i+1 , j , M ) )
                    g.addEdge ( k , k+N );
                if ( i > 0 && isSafe ( i-1 , j , M ) )
                    g.addEdge ( k , k-N );
            }

            // source index
            if( M[i][j] == 1 )
                s = k ;

            // destination index
            if (M[i][j] == 2)
                d = k;
            k++;
        }
    }

    // find minimum moves
    return g.BFS (s, d) ;
}

// driver program to check above function
int main()
{
    int M[N][N] = {{ 3 , 3 , 1 , 0 },
        { 3 , 0 , 3 , 3 },
        { 2 , 3 , 0 , 3 },
        { 0 , 3 , 3 , 3 }
    };

    cout << MinimumPath(M) << endl;

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to find the minimum numbers
# of moves needed to move from source to
# destination .

class Graph:
    def __init__(self, V):
        self.V = V
        self.adj = [[] for i in range(V)]

    # add edge to graph
    def addEdge (self, s , d ):
        self.adj[s].append(d)
        self.adj[d].append(s)

    # Level BFS function to find minimum
    # path from source to sink
    def BFS(self, s, d):

        # Base case
        if (s == d):
            return 0

        # make initial distance of all
        # vertex -1 from source
        level = [-1] * self.V

        # Create a queue for BFS
        queue = []

        # Mark the source node level[s] = '0'
        level[s] = 0
        queue.append(s)

        # it will be used to get all adjacent
        # vertices of a vertex

        while (len(queue) != 0):

            # Dequeue a vertex from queue
            s = queue.pop()

            # Get all adjacent vertices of the
            # dequeued vertex s. If a adjacent has
            # not been visited ( level[i] < '0') ,
            # then update level[i] == parent_level[s] + 1
            # and enqueue it
            i = 0
            while i < len(self.adj[s]):

                # Else, continue to do BFS
                if (level[self.adj[s][i]] < 0 or
                    level[self.adj[s][i]] > level[s] + 1 ):
                    level[self.adj[s][i]] = level[s] + 1
                    queue.append(self.adj[s][i])
                i += 1

        # return minimum moves from source
        # to sink
        return level[d]

def isSafe(i, j, M):
    global N
    if ((i < 0 or i >= N) or
        (j < 0 or j >= N ) or M[i][j] == 0):
        return False
    return True

# Returns minimum numbers of moves from a
# source (a cell with value 1) to a destination
# (a cell with value 2)
def MinimumPath(M):
    global N
    s , d = None, None # source and destination
    V = N * N + 2
    g = Graph(V)

    # create graph with n*n node
    # each cell consider as node
    k = 1 # Number of current vertex
    for i in range(N):
        for j in range(N):
            if (M[i][j] != 0):

                # connect all 4 adjacent cell to
                # current cell
                if (isSafe (i , j + 1 , M)):
                    g.addEdge (k , k + 1)
                if (isSafe (i , j - 1 , M)):
                    g.addEdge (k , k - 1)
                if (j < N - 1 and isSafe (i + 1 , j , M)):
                    g.addEdge (k , k + N)
                if (i > 0 and isSafe (i - 1 , j , M)):
                    g.addEdge (k , k - N)

            # source index
            if(M[i][j] == 1):
                s = k

            # destination index
            if (M[i][j] == 2):
                d = k
            k += 1

    # find minimum moves
    return g.BFS (s, d)

# Driver Code
N = 4
M = [[3 , 3 , 1 , 0 ], [3 , 0 , 3 , 3 ],
     [2 , 3 , 0 , 3 ], [0 , 3 , 3 , 3]]

print(MinimumPath(M))

# This code is contributed by PranchalK
```

**输出:**

```
4
```

**另一种方法:(DFS 实现**的**问题)**

使用 **DFS** 也可以实现同样的操作，其中将从源到**目的地**的**完整路径进行比较，以获得最小的移动。**

**接近**:

1.  遍历输入矩阵中的每个元素，并根据该矩阵创建一个图形
    1.  创建一个有 N*N 个顶点的图。
    2.  添加从 **k** 顶点到 **k+1** / **k-1** (如果边在矩阵中是左或右元素)或 **k** 到**k+N/**/**k-N**(如果边在矩阵中是顶部或底部元素)的边。
    3.  始终检查元素是否存在于矩阵和元素中！= 0.
    4.  if(element == 1)映射源 if (element == 2)映射目标。
2.  对形成的图执行 DFS，从源到目标。
    1.  基本条件:如果 source==destination 返回 0 作为最小移动次数。
    2.  最小移动将是最小的(对未访问的相邻顶点执行 DFS 的结果)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#define N 4

// To be used in DFS while comparing the
// minimum element
#define MAX (INT_MAX - 1)
using namespace std;

// Graph with the adjacency
// list representationo
class Graph {
private:
    int V;
    vector<int>* adj;

public:
    Graph(int V)
        : V{ V }
    {

        // Initializing the
        // adjacency list
        adj = new vector<int>[V];
    }

    // Clearing the memory after
    // its use (best practice)
    ~Graph()
    {
        delete[] adj;
    }

    // Adding the element to the
    // adjacency list matrix
    // representation
    void add_edges(int u, int v)
    {
      adj[u].push_back(v);
    }

    // performing the DFS for the minimum moves
    int DFS(int s, int d, unordered_set<int>& visited)
    {

        // Base condition for the recursion
        if (s == d)
            return 0;

        // Initializing the result
        int res{ MAX };
        visited.insert(s);
        for (int item : adj[s])
            if (visited.find(item) ==
                         visited.end())

                // comparing the res with
                // the result of DFS
                // to get the minimum moves
                res = min(res, 1 + DFS(item, d, visited));
        return res;
    }
};

// ruling out the cases where the element
// to be inserted is outside the matrix
bool is_safe(int arr[][4], int i, int j)
{
    if ((i < 0 || i >= N) || (j < 0 || j >= N)
        || arr[i][j] == 0)
        return false;
    return true;
}

int min_moves(int arr[][N])
{
    int s{ -1 }, d{ -1 }, V{ N * N };

    /* k be the variable which represents the
       positions( 0 - N*N ) inside the graph.
    */

     // k moves from top-left to bottom-right
    int k{ 0 };
    Graph g{ V };
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++) {

            // Adding the edge
            if (arr[i][j] != 0) {
                if (is_safe(arr, i, j + 1))
                    g.add_edges(k, k + 1); // left
                if (is_safe(arr, i, j - 1))
                    g.add_edges(k, k - 1); // right
                if (is_safe(arr, i + 1, j))
                    g.add_edges(k, k + N); // bottom
                if (is_safe(arr, i - 1, j))
                    g.add_edges(k, k - N); // top
            }

            // Source from which DFS to be
            // performed
            if (arr[i][j] == 1)
                s = k;

            // Destination
            else if (arr[i][j] == 2)
                d = k;

            // Moving k from top-left
            // to bottom-right
            k++;
        }
    }
    unordered_set<int> visited;

    // DFS performed from
    // source to destination
    return g.DFS(s, d, visited);
}

int32_t main()
{
    int arr[][N] = { { 3, 3, 1, 0 },
                     { 3, 0, 3, 3 },
                     { 2, 3, 0, 3 },
                     { 0, 3, 3, 3 } };

    // if(min_moves(arr) == MAX) there
    // doesn't exist a path
    // from source to destination
    cout << min_moves(arr) << endl;
    return 0;

    // the DFS approach and code
    // is contributed by Lisho
    // Thomas
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# To be used in DFS while comparing the
# minimum element
# define MAX (I4T_MAX - 1)
visited = {}
adj = [[] for i in range(16)]

# Performing the DFS for the minimum moves
def add_edges(u, v):

    global adj
    adj[u].append(v)

def DFS(s, d):

    global visited

    # Base condition for the recursion
    if (s == d):
        return 0

    # Initializing the result
    res = 10**9
    visited[s] = 1

    for item in adj[s]:
        if (item not in visited):

            # Comparing the res with
            # the result of DFS
            # to get the minimum moves
            res = min(res, 1 + DFS(item, d))

    return res

# Ruling out the cases where the element
# to be inserted is outside the matrix
def is_safe(arr, i, j):

    if ((i < 0 or i >= 4) or
        (j < 0 or j >= 4) or arr[i][j] == 0):
        return False

    return True

def min_moves(arr):

    s, d, V = -1,-1, 16
    # k be the variable which represents the
    # positions( 0 - 4*4 ) inside the graph.

    # k moves from top-left to bottom-right
    k = 0
    for i in range(4):
        for j in range(4):

            # Adding the edge
            if (arr[i][j] != 0):
                if (is_safe(arr, i, j + 1)):
                    add_edges(k, k + 1) # left
                if (is_safe(arr, i, j - 1)):
                    add_edges(k, k - 1) # right
                if (is_safe(arr, i + 1, j)):
                    add_edges(k, k + 4) # bottom
                if (is_safe(arr, i - 1, j)):
                    add_edges(k, k - 4) # top

            # Source from which DFS to be
            # performed
            if (arr[i][j] == 1):
                s = k

            # Destination
            elif (arr[i][j] == 2):
                d = k

            # Moving k from top-left
            # to bottom-right
            k += 1

    # DFS performed from
    # source to destination
    return DFS(s, d)

# Driver code
if __name__ == '__main__':

    arr = [ [ 3, 3, 1, 0 ],
            [ 3, 0, 3, 3 ],
            [ 2, 3, 0, 3 ],
            [ 0, 3, 3, 3 ] ]

    # If(min_moves(arr) == MAX) there
    # doesn't exist a path
    # from source to destination
    print(min_moves(arr))

# This code is contributed by mohit kumar 29
```

**Output**

```
4
```

本文由 [**尼尚辛格**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。