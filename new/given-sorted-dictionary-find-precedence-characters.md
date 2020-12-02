# 给定外语排序字典，找到字符顺序

> 原文： [https://www.geeksforgeeks.org/given-sorted-dictionary-find-precedence-characters/](https://www.geeksforgeeks.org/given-sorted-dictionary-find-precedence-characters/)

给定外语的排序字典（单词数组），找到该语言中字符的顺序。

**示例：**

```
Input:  words[] = {"baa", "abcd", "abca", "cab", "cad"}
Output: Order of characters is 'b', 'd', 'a', 'c'
Note that words are sorted and in the given language "baa" 
comes before "abcd", therefore 'b' is before 'a' in output.
Similarly we can find other orders.

Input:  words[] = {"caa", "aaa", "aab"}
Output: Order of characters is 'c', 'a', 'b'

```

这个想法是创建一个字符图，然后找到所创建图的[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)。 以下是详细步骤。

1）创建图 *g* ，其顶点数量等于给定外语中字母的大小。 例如，如果字母大小为 5，则单词中可以有 5 个字符。 最初，图中没有边。

2）对给定排序数组中的每对相邻单词进行跟随。
…..a）令当前单词对为 *word1* 和 *word2* 。 逐个比较两个单词的字符并找到第一个不匹配的字符。
…..b）在 *g* 中从 *word1* 的不匹配字符到 *word2* 的不匹配字符创建一条边。

3）打印上面创建的图的[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)。

以下是上述算法的实现。

## C ++

```

// A C++ program to order of characters in an alien language 
#include<bits/stdc++.h> 
using namespace std; 

// Class to represent a graph 
class Graph 
{ 
    int V;    // No. of vertices' 

    // Pointer to an array containing adjacency listsList 
    list<int> *adj; 

    // A function used by topologicalSort 
    void topologicalSortUtil(int v, bool visited[], stack<int> &Stack); 
public: 
    Graph(int V);   // Constructor 

    // function to add an edge to graph 
    void addEdge(int v, int w); 

    // prints a Topological Sort of the complete graph 
    void topologicalSort(); 
}; 

Graph::Graph(int V) 
{ 
    this->V = V; 
    adj = new list<int>[V]; 
} 

void Graph::addEdge(int v, int w) 
{ 
    adj[v].push_back(w); // Add w to v’s list. 
} 

// A recursive function used by topologicalSort 
void Graph::topologicalSortUtil(int v, bool visited[], stack<int> &Stack) 
{ 
    // Mark the current node as visited. 
    visited[v] = true; 

    // Recur for all the vertices adjacent to this vertex 
    list<int>::iterator i; 
    for (i = adj[v].begin(); i != adj[v].end(); ++i) 
        if (!visited[*i]) 
            topologicalSortUtil(*i, visited, Stack); 

    // Push current vertex to stack which stores result 
    Stack.push(v); 
} 

// The function to do Topological Sort. It uses recursive topologicalSortUtil() 
void Graph::topologicalSort() 
{ 
    stack<int> Stack; 

    // Mark all the vertices as not visited 
    bool *visited = new bool[V]; 
    for (int i = 0; i < V; i++) 
        visited[i] = false; 

    // Call the recursive helper function to store Topological Sort 
    // starting from all vertices one by one 
    for (int i = 0; i < V; i++) 
        if (visited[i] == false) 
            topologicalSortUtil(i, visited, Stack); 

    // Print contents of stack 
    while (Stack.empty() == false) 
    { 
        cout << (char) ('a' + Stack.top()) << " "; 
        Stack.pop(); 
    } 
} 

int min(int x, int y) 
{ 
    return (x < y)? x : y; 
} 

// This function fidns and prints order of characer from a sorted 
// array of words. n is size of words[].  alpha is set of possible 
// alphabets. 
// For simplicity, this function is written in a way that only 
// first 'alpha' characters can be there in words array.  For 
// example if alpha is 7, then words[] should have only 'a', 'b', 
// 'c' 'd', 'e', 'f', 'g' 
void printOrder(string words[], int n, int alpha) 
{ 
    // Create a graph with 'aplha' edges 
    Graph g(alpha); 

    // Process all adjacent pairs of words and create a graph 
    for (int i = 0; i < n-1; i++) 
    { 
        // Take the current two words and find the first mismatching 
        // character 
        string word1 = words[i], word2 = words[i+1]; 
        for (int j = 0; j < min(word1.length(), word2.length()); j++) 
        { 
            // If we find a mismatching character, then add an edge 
            // from character of word1 to that of word2 
            if (word1[j] != word2[j]) 
            { 
                g.addEdge(word1[j]-'a', word2[j]-'a'); 
                break; 
            } 
        } 
    } 

    // Print topological sort of the above created graph 
    g.topologicalSort(); 
} 

// Driver program to test above functions 
int main() 
{ 
    string words[] = {"caa", "aaa", "aab"}; 
    printOrder(words, 3, 3); 
    return 0; 
} 

```