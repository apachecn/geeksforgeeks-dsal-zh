# 使两个字符串相同所需的最小对数

> 原文： [https://www.geeksforgeeks.org/minimum-number-of-pairs-required-to-make-two-strings-same/](https://www.geeksforgeeks.org/minimum-number-of-pairs-required-to-make-two-strings-same/)

给定两个长度相同的字符串 **s1** 和 **s2** ，任务是计算字符对**（c1，c2）**的最小对数，从而通过转换[ **c1 到 c2** 或 **c2 到 c1** 在任意字符串中任意次数使两个字符串相同。

**示例：**

> **输入：** s1 =“ abb”，s2 =“ dad”
> **输出：** 2
> 变换'a'->'d'，'b'- s1 中的>'a'和'b'->'a'->'d'。
> 我们不能将（a，d），（b，a），（b，d）成对使用，因为
> （b，d）可以通过以下变换'b'->'a 实现 '->'d'
> 
> **输入：** s1 =“ drpepper”，s2 =“可口可乐”
> **输出：** 7

**方法：**可以通过使用图形或不连续集来解决此问题。 建立一个空图 G 并遍历字符串。 仅当满足以下条件之一时，才在图形 G 中添加边：

*   **s1 [i]** 和 **s2 [i]** 都不在 G 中。
*   **s1 [i]** 在 G 中，但 **s2 [i]** 在 G 中。
*   **s2 [i]** 在 G 中，但 **s1 [i]** 在 G 中。
*   从 **s1 [i]** 到 **s2 [i]** 没有路径。

最小对数将是最终图形 G 中的边数。

下面是上述方法的实现：

## C ++

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function which will check if there is 
// a path between a and b by using BFS 
bool checkPath(char a, char b,  
           map<char, vector<char>> &G) 
{ 
    map<char, bool> visited; 
    deque<char> queue; 
    queue.push_back(a); 
    visited[a] = true; 

    while (!queue.empty())  
    { 
        int n = queue.front(); 
        queue.pop_front(); 

        if (n == b) return true; 
        for (auto i : G[n])  
        { 
            if (visited[i] == false) 
            { 
                queue.push_back(i); 
                visited[i] = true; 
            } 
        } 
    } 
    return false; 
} 

// Function to return the  
// minimum number of pairs 
int countPairs(string s1, string s2, 
         map<char, vector<char>> &G, int x)  
{ 

    // To store the count of pairs 
    int count = 0; 

    // Iterating through the strings 
    for (int i = 0; i < x; i++)  
    { 
        char a = s1[i]; 
        char b = s2[i]; 

        // Check if we can add an edge in the graph 
        if (G.find(a) != G.end() and  
            G.find(b) == G.end() and a != b) 
        { 
            G[a].push_back(b); 
            G[b].push_back(a); 
            count++; 
        } 
        else if (G.find(b) != G.end() and 
                 G.find(a) == G.end() and a != b)  
        { 
            G[b].push_back(a); 
            G[a].push_back(b); 
            count++; 
        }  
        else if (G.find(a) == G.end() and  
                 G.find(b) == G.end() and a != b)  
        { 
            G[a].push_back(b); 
            G[b].push_back(a); 
            count++; 
        }  
        else
        { 
            if (!checkPath(a, b, G) and a != b) 
            { 
                G[a].push_back(b); 
                G[b].push_back(a); 
                count++; 
            } 
        } 
    } 

    // Return the count of pairs 
    return count; 
} 

// Driver Code 
int main()  
{ 
    string s1 = "abb", s2 = "dad"; 
    int x = s1.length(); 
    map<char, vector<char>> G; 
    cout << countPairs(s1, s2, G, x) << endl; 

    return 0; 
} 

// This code is contributed by 
// sanjeev2552 

```