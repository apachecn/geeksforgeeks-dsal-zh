# 查找从矩阵的一个单元格移动到另一个单元格所需的最少移动次数

> 原文： [https://www.geeksforgeeks.org/find-minimum-numbers-moves-needed-move-one-cell-matrix-another/](https://www.geeksforgeeks.org/find-minimum-numbers-moves-needed-move-one-cell-matrix-another/)

给定一个 N X N 矩阵（M），该矩阵填充有 1，0，2，3。 找到从源移动到目的地（接收器）所需的最少移动次数。 而仅遍历空白单元格。 您可以上下左右移动。

单元格`1`的值表示源。

单元格`2`的值表示目的地。

单元格`3`的值表示空白单元格。

单元格**的值 0** 表示空白墙。

**注意**：只有一个来源和一个目的地。它们可能从来源到目的地（汇）的路径不止一个。在矩阵中的每一步我们都认为是“ 1”

**示例**：

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

询问： [Adob​​e 访谈](https://www.geeksforgeeks.org/adobe-interview-experience-set-41-software-engineer/)

。 ![minimum_move](img/0309f6e58e9c0be41d7d925357545272.png) 

这个想法是使用 Level 图（广度优先遍历）。 将每个像元视为一个节点，并将任意两个相邻像元之间的每个边界作为一条边。 所以 Node 的总数是 N * N。

```
 1\. Create an empty Graph having N*N node ( Vertex ).
 2\. Push all node into graph.
 3\. Note down source and sink vertices.
 4\. Now Apply  level graph concept ( that we achieve using BFS  ) .
    In which we find level of every node from source vertex.
    After that we return  'Level[d]' ( d is destination ).
    (which is the minimum move from source to sink )

```

以下是上述想法的实现。

## C++

```cpp

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