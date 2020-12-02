# 查找字母顺序，以便可以将单词视为已排序

> 原文： [https://www.geeksforgeeks.org/find-alphabetical-order-such-that-words-can-be-considered-sorted/](https://www.geeksforgeeks.org/find-alphabetical-order-such-that-words-can-be-considered-sorted/)

给定一个单词数组，找到英语字母中的任何字母顺序，以便给定的单词可以被视为已排序（递增）（如果存在这样的顺序），否则将无法输出。

例子：

```
Input :  words[] = {"zy", "ab"}
Output : zabcdefghijklmnopqrstuvwxy
Basically we need to make sure that 'z' comes
before 'a'.

Input :  words[] = {"geeks", "gamers", "coders", 
                    "everyoneelse"}
Output : zyxwvutsrqponmlkjihgceafdb

Input : words[] = {"marvel", "superman", "spiderman", 
                                           "batman"
Output : zyxwvuptrqonmsbdlkjihgfeca

```

**天真的方法：**蛮力方法是检查所有可能的顺序，并检查其中是否满足给定的单词顺序。 考虑到英语中有 **26 个**字母，因此有 **26 个！** 可以作为有效订单的排列数。 考虑到我们检查每一对来验证订单，此方法的复杂度达到 **O（26！* N ^ 2）**，远远超出了实际首选的时间复杂度。

**使用拓扑排序：**此解决方案需要[图及其以邻接表](https://www.geeksforgeeks.org/graph-and-its-representations/)， [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 和[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)表示的知识。

按照我们要求的顺序，要求打印字母，以便每个字母后面必须紧跟优先级低于它们的字母。 似乎与[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)定义为相似–在拓扑排序中，我们需要在其相邻顶点之前打印一个顶点。 让我们将字母表中的每个字母定义为标准有向图中的节点。 如果 **A** 依次位于 **B** 之前，则 **A** 被连接到 **B** （A– > B）。 该算法可以表述为：

1.  如果 **n** 为 **1** ，则任何顺序均有效。
2.  拿前两个字。 识别单词中的第一个不同字母（在单词的相同索引处）。 第一个单词中的字母将在第二个单词中的字母之前。
3.  如果不存在这样的字母，则第一个字符串的长度必须小于第二个字符串的长度。
4.  将第二个单词分配给第一个单词，然后将第三个单词输入第二个单词。 重复 **2** ， **3** 和 **4** **（n-1）**次。
5.  按拓扑顺序运行 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 遍历。
6.  检查是否所有节点都已访问。 按照拓扑顺序，如果图中存在循环，则循环中的节点将保持不访问状态，因为在访问与其相邻的每个节点之后都无法访问这些节点。 在这种情况下，不存在订单。 在这种情况下，这意味着我们列表中的顺序相互矛盾。

```

/* CPP program to find an order of alphabets 
so that given set of words are considered 
sorted */
#include <bits/stdc++.h> 
using namespace std; 
#define MAX_CHAR 26 

void findOrder(vector<string> v) 
{ 
    int n = v.size(); 

    /* If n is 1, then any order works */
    if (n == 1) { 
        cout << "abcdefghijklmnopqrstuvwxyz"; 
        return; 
    } 

    /* Adjacency list of 26 characters*/
    vector<int> adj[MAX_CHAR]; 

    /* Array tracking the number of edges that are  
    inward to each node*/
    vector<int> in(MAX_CHAR, 0); 

    // Traverse through all words in given array 
    string prev = v[0]; 

    /* (n-1) loops because we already acquired the  
    first word in the list*/
    for (int i = 1; i < n; ++i) { 
        string s = v[i]; 

        /* Find first such letter in the present string that is different  
        from the letter in the previous string at the same index*/
        int j; 
        for (j = 0; j < min(prev.length(), s.length()); ++j) 
            if (s[j] != prev[j]) 
                break; 

        if (j < min(prev.length(), s.length())) { 

            /* The letter in the previous string precedes the one 
            in the present string, hence add the letter in the present 
            string as the child of the letter in the previous string*/
            adj[prev[j] - 'a'].push_back(s[j] - 'a'); 

            /* The number of inward pointing edges to the node representing  
            the letter in the present string increases by one*/
            in[s[j] - 'a']++; 

            /* Assign present string to previous string for the next  
            iteration. */
            prev = s; 
            continue; 
        } 

        /* If there exists no such letter then the string length of  
        the previous string must be less than or equal to the  
        present string, otherwise no such order exists*/
        if (prev.length() > s.length()) { 
            cout << "Impossible"; 
            return; 
        } 

        /* Assign present string to previous string for the next 
        iteration */
        prev = s; 
    } 

    /* Topological ordering requires the source nodes  
    that have no parent nodes*/
    stack<int> stk; 
    for (int i = 0; i < MAX_CHAR; ++i) 
        if (in[i] == 0) 
            stk.push(i); 

    /* Vector storing required order (anyone that satisfies) */
    vector<char> out; 

    /* Array to keep track of visited nodes */
    bool vis[26]; 
    memset(vis, false, sizeof(vis)); 

    /* Standard DFS */
    while (!stk.empty()) { 

        /* Acquire present character */
        char x = stk.top(); 
        stk.pop(); 

        /* Mark as visited */
        vis[x] = true; 

        /* Insert character to output vector */
        out.push_back(x + 'a'); 

        for (int i = 0; i < adj[x].size(); ++i) { 
            if (vis[adj[x][i]]) 
                continue; 

            /* Since we have already included the present  
            character in the order, the number edges inward  
            to this child node can be reduced*/
            in[adj[x][i]]--; 

            /* If the number of inward edges have been removed,  
            we can include this node as a source node*/
            if (in[adj[x][i]] == 0) 
                stk.push(adj[x][i]); 
        } 
    } 

    /* Check if all nodes(alphabets) have been visited. 
    Order impossible if any one is unvisited*/
    for (int i = 0; i < MAX_CHAR; ++i) 
        if (!vis[i]) { 
            cout << "Impossible"; 
            return; 
        } 

    for (int i = 0; i < out.size(); ++i) 
        cout << out[i]; 
} 

// Driver code 
int main() 
{ 
    vector<string> v{ "efgh", "abcd" }; 
    findOrder(v); 
    return 0; 
} 

```

输出：

```
zyxwvutsrqponmlkjihgfeadcb
```

此方法的复杂度为 **O（N * | S |）+ O（V + E）**，其中 **| V |** = 26（节点数与字母数相同）， **| E |** < **N** （因为每个单词最多可创建 1 个边沿作为输入）。 因此，总体复杂度为 **O（N * | S | + N）**。 **| S |** 表示每个单词的长度。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。