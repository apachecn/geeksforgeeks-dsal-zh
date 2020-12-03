# 任意一对顶点之间的最长路径

> 原文： [https://www.geeksforgeeks.org/longest-path-between-any-pair-of-vertices/](https://www.geeksforgeeks.org/longest-path-between-any-pair-of-vertices/)

我们获得了一张城市地图，这些城市通过电缆相互连接，因此任何两个城市之间都没有周期。 对于给定的城市地图，我们需要找到任意两个城市之间的最大电缆长度。

```
Input : n = 6  
        1 2 3  // Cable length from 1 to 2 (or 2 to 1) is 3
        2 3 4
        2 6 2
        6 4 6
        6 5 5
Output: maximum length of cable = 12

```

**方法 1（简单 DFS）**

我们为给定的城市地图创建无向图，并从每个城市进行 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 以查找最大电缆长度。 在遍历时，我们寻找到达当前城市的电缆总长度，如果没有访问它的相邻城市，则为其调用 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，但是如果当前节点访问了所有相邻城市，则更新 max_length 的值 如果 max_length 的先前值小于电缆总长度的当前值。

## C++

```cpp

// C++ program to find the longest cable length 
// between any two cities. 
#include<bits/stdc++.h> 
using namespace std; 

// visited[] array to make nodes visited 
// src is starting node for DFS traversal 
// prev_len is sum of cable length till current node 
// max_len is pointer which stores the maximum length 
// of cable value after DFS traversal 
void DFS(vector< pair<int,int> > graph[], int src, 
         int prev_len, int *max_len, 
         vector <bool> &visited) 
{ 
    // Mark the src node visited 
    visited[src] = 1; 

    // curr_len is for length of cable from src 
    // city to its adjacent city 
    int curr_len = 0; 

    // Adjacent is pair type which stores 
    // destination city and cable length 
    pair < int, int > adjacent; 

    // Traverse all adjacent 
    for (int i=0; i<graph[src].size(); i++) 
    { 
        // Adjacent element 
        adjacent = graph[src][i]; 

        // If node or city is not visited 
        if (!visited[adjacent.first]) 
        { 
            // Total length of cable from src city 
            // to its adjacent 
            curr_len = prev_len + adjacent.second; 

            // Call DFS for adjacent city 
            DFS(graph, adjacent.first, curr_len, 
                max_len,  visited); 
        } 

        // If total cable length till now greater than 
        // previous length then update it 
        if ((*max_len) < curr_len) 
            *max_len = curr_len; 

        // make curr_len = 0 for next adjacent 
        curr_len = 0; 
    } 
} 

// n is number of cities or nodes in graph 
// cable_lines is total cable_lines among the cities 
// or edges in graph 
int longestCable(vector<pair<int,int> > graph[], 
                                          int n) 
{ 
    // maximum length of cable among the connected 
    // cities 
    int max_len = INT_MIN; 

    // call DFS for each city to find maximum 
    // length of cable 
    for (int i=1; i<=n; i++) 
    { 
        // initialize visited array with 0 
        vector< bool > visited(n+1, false); 

        // Call DFS for src vertex i 
        DFS(graph, i, 0, &max_len, visited); 
    } 

    return max_len; 
} 

// driver program to test the input 
int main() 
{ 
    // n is number of cities 
    int n = 6; 

    vector< pair<int,int> > graph[n+1]; 

    // create undirected graph 
    // first edge 
    graph[1].push_back(make_pair(2, 3)); 
    graph[2].push_back(make_pair(1, 3)); 

    // second edge 
    graph[2].push_back(make_pair(3, 4)); 
    graph[3].push_back(make_pair(2, 4)); 

    // third edge 
    graph[2].push_back(make_pair(6, 2)); 
    graph[6].push_back(make_pair(2, 2)); 

    // fourth edge 
    graph[4].push_back(make_pair(6, 6)); 
    graph[6].push_back(make_pair(4, 6)); 

    // fifth edge 
    graph[5].push_back(make_pair(6, 5)); 
    graph[6].push_back(make_pair(5, 5)); 

    cout << "Maximum length of cable = "
         << longestCable(graph, n); 

    return 0; 
} 

```