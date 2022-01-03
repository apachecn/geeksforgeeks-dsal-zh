# 彼得森图问题

> 原文： [https://www.geeksforgeeks.org/peterson-graph/](https://www.geeksforgeeks.org/peterson-graph/)

下图 G 被称为 Petersen 图，其顶点的编号从 0 到 9。从下图可以看出，一些字母也分配给了 G 的顶点：

让我们考虑图中的游走 W G，由 L 个顶点 W1，W2，...，WL 组成。 如果沿 W 书写的字母序列等于 S，则通过行走 W 可以实现由 L 个字母“ A”至“ E”组成的字符串 S。沿着 W 行走时，可以多次访问顶点。

例如，S ='ABBECCD'由 W =（0，1，6，9，9，7，2，3）实现。 确定在图 G 中是否存在实现给定字符串 S 的走行 W，如果是，则从字典上找到最小的走行。 输入的唯一行包含一个字符串 S。如果没有实现 S 的走行 W，则输出-1，否则，应输出实现 S 的最小词典走道 W。

![](img/93400bc3fb918f88886000766023dd97.png)

例子：

```
Input : s = 'ABB'
Output: 016
Explanation: As we can see in the graph
             the path from ABB is 016.
Input : s = 'AABE'
Output :-1
Explanation: As there is no path that
             exists, hence output is -1.

```

我们应用广度优先搜索来访问图的每个顶点。

## C++

```cpp

// C++ program to find the 
// path in Peterson graph 
#include <bits/stdc++.h> 
using namespace std; 

// path to be checked  
char S[100005];  

// adjacency matrix.  
bool adj[10][10]; 

// resulted path - way  
char result[100005]; 

// we are applying breadth first search 
// here 
bool findthepath(char* S, int v) 
{ 
    result[0] = v + '0'; 
    for (int i = 1; S[i]; i++) { 

        // first traverse the outer graph 
        if (adj[v][S[i] - 'A'] || adj[S[i] - 
                              'A'][v]) { 
            v = S[i] - 'A'; 
        } 

        // then traverse the inner graph 
        else if (adj[v][S[i] - 'A' + 5] ||  
                 adj[S[i] - 'A' + 5][v]) { 
            v = S[i] - 'A' + 5; 
        } 

        // if the condition failed to satisfy 
        // return false 
        else 
            return false; 

        result[i] = v + '0'; 
    } 

    return true; 
} 

// driver code 
int main() 
{ 
    // here we have used adjacency matrix to make 
    // connections between the connected nodes 
    adj[0][1] = adj[1][2] = adj[2][3] = adj[3][4] =  
    adj[4][0] = adj[0][5] = adj[1][6] = adj[2][7] = 
    adj[3][8] = adj[4][9] = adj[5][7] = adj[7][9] = 
    adj[9][6] = adj[6][8] = adj[8][5] = true; 

    // path to be checked 
    char S[] = "ABB"; 

    if (findthepath(S, S[0] - 'A') ||  
        findthepath(S, S[0] - 'A' + 5)) { 
        cout << result; 
    } else { 
        cout << "-1"; 
    } 
    return 0; 
} 

```