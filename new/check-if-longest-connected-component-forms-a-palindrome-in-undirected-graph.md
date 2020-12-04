# 检查最长连通组件是否在无向图

中形成回文

> 原文： [https://www.geeksforgeeks.org/check-if-longest-connected-component-forms-a-palindrome-in-undirected-graph/](https://www.geeksforgeeks.org/check-if-longest-connected-component-forms-a-palindrome-in-undirected-graph/)

给定[无向图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)并具有`V`顶点和`E`边，任务是检查图的[最大连通分量](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)是否形成 无向图中的回文。

**范例**：

> **输入**：
> 
> ![](img/38fe7f7974b8fefc4a3e3aea3a91f3da.png)
> 
> **输出**：
> 最长连通组件是回文
> **解释**：
> 最长连通组件是{5，15，5}
> ，它通过值形成一个回文 。
> **输入**：[
> 
> ![](img/beabc5855ca715c86b194a754a8f3b8e.png)
> 
> **输出**：
> 最长连通组件不是回文
> **解释**：
> 最长的链是{2，3，4，5}，不是回文。

**方法**：的想法是使用[深度优先搜索遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)来跟踪无向图中的连通组件。 在每次遍历时，如果连通组件的当前长度大于连通组件的全局长度的长度，则更新最长的连通组件。 最后，检查最长的连通组件形成回文。

以下是上述方法的实现：

## C++

```cpp

// C++ implementation to check if
// longest connected component is 
// palindrome in undirected graph

#include <bits/stdc++.h>

using namespace std;

// Function to traverse the undirected
// graph using the Depth first traversal
void depthFirst(int v, vector<int> graph[],
                vector<bool>& visited,
                vector<int>& storeChain)
{
    // Marking the visited 
    // vertex as true
    visited[v] = true;

    // Store the connected chain
    storeChain.push_back(v);

    for (auto i : graph[v]) {
        if (visited[i] == false) {

            // Recursive call to 
            // the DFS algorithm
            depthFirst(i, graph, 
               visited, storeChain);
        }
    }
}

// Function to check that the connected
// component forms a palindrome
void checkPalin(int arr[], int n)
{
    // Container to store the frequency
    // of each occurring element
    map<int,int> frequency;

    // Container to visit elements
    unordered_set<int> element;

    for(int i = 0; i < n; i ++)
    {
        // If element has not been visited already
        // the element is inserted with freq = 1
        // frequency of occurrence, if visited
        // already, then frequency is updated
        if(!(element.find(arr[i]) != element.end()))
        {
            frequency.insert({arr[i], 1});
        }
        else
        {
            frequency[arr[i]] ++;
        }
        element.insert(arr[i]);
    }

    // Variable to store final result
    int result = 1;

    // For even array size, all the elements
    // are checked for even occurrences, if
    // odd array size, then it is checked if
    // a single element with odd frequency
    // is present or not
    if(n % 2 == 0)
    {
        for(auto i: frequency)
        {
            if(i.second % 2 != 0)
            {
                result = 0;
                break;
            }
        }
    }
    else
    {
        int countFreq = 0;
        for(auto i: frequency)
        {
            if(i.second % 2 != 0)
            {
                countFreq ++;
            }
        }
        if(countFreq != 1)
            result = 0;
    }

    // Printing the final result
    if(result)
        cout << "Longest connected component is Palindrome";
    else
        cout << "Longest connected component not a Palindrome";
}

// Function to check that longest connected
// component forms a palindrome
void longestConnectionPalin(
    vector<int> graph[], int vertices,
                   vector<int> values)
{
    // Initializing boolean array
    // to mark visited vertices
    vector<bool> visited(10001, false);

    // maxChain stores the 
    // maximum chain size
    int maxChain = 0;

    // Container to store longest chain
    vector<int> maxStoreChain;

    // Following loop invokes DFS algorithm
    for (int i = 1; i <= vertices; i++) {
        if (visited[i] == false) {

            // Variable to hold 
            // temporary length
            int sizeChain;

            // Container to store each chain
            vector<int> storeChain;

            // DFS algorithm
            depthFirst(i, graph, visited, storeChain);

            // Variable to hold each chain size
            sizeChain = storeChain.size();

            if (sizeChain > maxChain) {
                maxChain = sizeChain;
                maxStoreChain = storeChain;
            }
        }
    }

    // Container to store values
    // of vertices of longest chain
    int longChainValues[maxChain+1];

    // Storing the values of longest chain
    for(int i = 0; i < maxChain; i ++)
    {
        int temp = values[maxStoreChain[i]-1];
        longChainValues[i] = temp;
    }

    // Function call to check for Palindrome
    checkPalin(longChainValues, maxChain);
}

// Driver function to test above function
int main()
{
    // Initializing graph in the form of adjacency list
    vector<int> graph[1001];

    // Defining the number of edges and vertices
    int E, V;
    E = 4;
    V = 7;

    // Assigning the values for each
    // vertex of the undirected graph
    vector<int> values;
    values.push_back(10);
    values.push_back(25);
    values.push_back(5);
    values.push_back(15);
    values.push_back(5);
    values.push_back(20);
    values.push_back(0);

    // Constructing the undirected graph
    graph[1].push_back(2);
    graph[2].push_back(1);
    graph[3].push_back(4);
    graph[4].push_back(3);
    graph[3].push_back(5);
    graph[5].push_back(3);
    graph[6].push_back(7);
    graph[7].push_back(6);

    longestConnectionPalin(graph, V, values);
    return 0;
}

```

## Java

```java

// Java implementation to check if 
// longest connected component is 
// palindrome in undirected graph 
import java.util.*;
class GFG{ 

// Initializing boolean array 
// to mark visited vertices 
static boolean [] visited = 
       new boolean[10001];

// Container to store longest chain 
static Vector<Integer>storeChain = 
                      new Vector<>(); 

// Function to traverse 
// the undirected graph 
// using the Depth first 
// traversal 
static void depthFirst(int v, 
                       Vector<Integer> graph[]) 
{ 
  // Marking the visited 
  // vertex as true 
  visited[v] = true; 

  // Store the connected chain 
  storeChain.add(v); 

  for (int i : graph[v]) 
  { 
    if (visited[i] == false) 
    {
      // Recursive call to 
      // the DFS algorithm 
      depthFirst(i, graph); 
    } 
  } 
} 

// Function to check that 
// the connected component 
// forms a palindrome 
static void checkPalin(int arr[], 
                       int n) 
{ 
  // Container to store the 
  // frequency of each occurring 
  // element 
  HashMap<Integer,
          Integer> frequency = 
                   new HashMap<>(); 

  // Container to visit elements 
  HashSet<Integer> element = 
                   new HashSet<>(); 

  for(int i = 0; i < n; i ++) 
  { 
    // If element has not been 
    // visited already the element 
    // is inserted with freq = 1 
    // frequency of occurrence, 
    // if visited already, then 
    // frequency is updated 
    if((element.contains(arr[i]))) 
    { 
      frequency.put(arr[i], 
      frequency.get(arr[i]) + 1); 
    } 
    else
    { 
      frequency.put(arr[i], 1); 
    } 

    element.add(arr[i]); 
  } 

  // Variable to store 
  // final result 
  int result = 1; 

  // For even array size, all 
  // the elements are checked 
  // for even occurrences, if 
  // odd array size, then it 
  // is checked if a single 
  // element with odd frequency 
  // is present or not 
  if(n % 2 == 0) 
  { 
    for (Map.Entry<Integer,
                   Integer> i : frequency.entrySet())
    { 
      if(i.getValue() % 2 != 0) 
      { 
        result = 0; 
        break; 
      } 
    } 
  } 
  else
  { 
    int countFreq = 0; 
    for (Map.Entry<Integer,
                   Integer> i : frequency.entrySet())
    { 
      if(i.getValue() % 2 != 0) 
      { 
        countFreq ++; 
      } 
    } 
    if(countFreq != 1) 
      result = 0; 
  } 

  // Printing the 
  // final result 
  if(result != 0) 
    System.out.print("Longest connected " +
                     "component is Palindrome"); 
  else
    System.out.print("Longest connected " +
                     "component not a Palindrome"); 
} 

// Function to check that longest 
// connected component forms a palindrome 
static void longestConnectionPalin(Vector<Integer> graph[], 
                                   int vertices, 
                                   Vector<Integer> values) 
{ 
  // maxChain stores the ;
  // maximum chain size 
  int maxChain = 0; 

  // Container to store each chain 
  Vector<Integer> maxStoreChain = 
                  new Vector<>();  
  // Following loop invokes
  // DFS algorithm 
  for (int i = 1; i <= vertices; i++) 
  { 
    if (visited[i] == false) 
    {
      // Variable to hold 
      // temporary length 
      int sizeChain; 

      // DFS algorithm 
      depthFirst(i, graph); 

      // Variable to hold each chain size 
      sizeChain = storeChain.size(); 

      if (sizeChain > maxChain) 
      { 
        maxChain = sizeChain; 
        maxStoreChain = storeChain; 
      } 
    } 
  } 

  // Container to store values 
  // of vertices of longest chain 
  int []longChainValues = 
        new int[maxChain+1]; 

  // Storing the values of 
  // longest chain 
  for(int i = 0; i < maxChain; i ++) 
  { 
    int temp = values.get(maxStoreChain.get(i) - 1); 
    longChainValues[i] = temp; 
  } 

  // Function call to check 
  // for Palindrome 
  checkPalin(longChainValues, 
             maxChain); 
} 

// Driver code
public static void main(String[] args) 
{ 
  // Initializing graph in the 
  // form of adjacency list 
  Vector<Integer> graph[] = 
                  new Vector[1001]; 

  for (int i = 0; i < graph.length; i++)
    graph[i] = new Vector<Integer>();

  // Defining the number of 
  // edges and vertices 
  int E, V; 
  E = 4; 
  V = 7; 

  // Assigning the values 
  // for each vertex of 
  // the undirected graph 
  Vector<Integer> values = 
         new Vector<>(); 
  values.add(10); 
  values.add(25); 
  values.add(5); 
  values.add(15); 
  values.add(5); 
  values.add(20); 
  values.add(0); 

  // Constructing the 
  // undirected graph 
  graph[1].add(2); 
  graph[2].add(1); 
  graph[3].add(4); 
  graph[4].add(3); 
  graph[3].add(5); 
  graph[5].add(3); 
  graph[6].add(7); 
  graph[7].add(6); 

  longestConnectionPalin(graph, V, values); 
}
} 

// This code is contributed by gauravrajput1

```

**Output:** 

```
Longest connected component is Palindrome

```

**时间复杂度**：`O(V + E)`

![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。