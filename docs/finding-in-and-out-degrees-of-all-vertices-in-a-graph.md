# 查找图形中所有顶点的入度和出度

> 原文： [https://www.geeksforgeeks.org/finding-in-and-out-degrees-of-all-vertices-in-a-graph/](https://www.geeksforgeeks.org/finding-in-and-out-degrees-of-all-vertices-in-a-graph/)

给定一个有向图，任务是计算图的每个顶点的内外度。

**范例**：

```
Input:

Output:
Vertex    In    Out
0         1    2
1          2    1
2          2    3
3          2    2
4          2    2
5          2    2
6          2    1

```

**方法**：遍历每个顶点，如果顶点`i`的邻接列表的大小为`x`，则 **i 的出界度 i = x [** 并从`i`递增具有传入边的每个顶点的度数。 对每个顶点重复上述步骤，并在最后打印所有顶点的进出度。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find the in and out degrees 
// of the vertices of the given graph 
#include <bits/stdc++.h> 
using namespace std; 

// Function to print the in and out degrees 
// of all the vertices of the given graph 
void findInOutDegree(list<list<int>> adjlist, 
                     int n) 
{ 
    int* iN = new int[n](); 
    int* ouT = new int[n](); 

    list<list<int> >::iterator nest_list; 
    int i = 0; 

    for(nest_list = adjlist.begin();  
        nest_list != adjlist.end(); 
        nest_list++)  
    { 
        list<int> lst = *nest_list; 

        // Out degree for ith vertex will be the count 
        // of direct paths from i to other vertices 
        ouT[i] = lst.size(); 

        for(auto it = lst.begin();  
                 it != lst.end(); it++) 
        { 
            // Every vertex that has an incoming 
            // edge from i 
            iN[*it]++; 
        } 
        i++; 
    } 

    cout << "Vertex\t\tIn\t\tOut" << endl; 
    for(int k = 0; k < n; k++) 
    { 
        cout << k << "\t\t"
             << iN[k] << "\t\t" 
             << ouT[k] << endl; 
    } 
} 

// Driver code 
int main() 
{ 

    // Adjacency list representation of the graph 
    list<list<int>> adjlist; 

    // Vertices 1 and 2 have an incoming edge 
    // from vertex 0 
    list<int> tmp; 
    tmp.push_back(1); 
    tmp.push_back(2); 
    adjlist.push_back(tmp); 
    tmp.clear(); 

    // Vertex 3 has an incoming edge  
    // from vertex 1 
    tmp.push_back(3); 
    adjlist.push_back(tmp); 
    tmp.clear(); 

    // Vertices 0, 5 and 6 have an incoming 
    // edge from vertex 2 
    tmp.push_back(0); 
    tmp.push_back(5); 
    tmp.push_back(6); 
    adjlist.push_back(tmp); 
    tmp.clear(); 

    // Vertices 1 and 4 have an incoming  
    // edge from vertex 3 
    tmp.push_back(1); 
    tmp.push_back(4); 
    adjlist.push_back(tmp); 
    tmp.clear(); 

    // Vertices 2 and 3 have an incoming  
    // edge from vertex 4 
    tmp.push_back(2); 
    tmp.push_back(3); 
    adjlist.push_back(tmp); 
    tmp.clear(); 

    // Vertices 4 and 6 have an incoming  
    // edge from vertex 5 
    tmp.push_back(4); 
    tmp.push_back(6); 
    adjlist.push_back(tmp); 
    tmp.clear(); 

    // Vertex 5 has an incoming  
    // edge from vertex 6 
    tmp.push_back(5); 
    adjlist.push_back(tmp); 
    tmp.clear(); 

    int n = adjlist.size(); 

    findInOutDegree(adjlist, n); 
} 

// This code is contributed by saurabhgpta248     

```

## Java

```java

// Java program to find the in and out degrees 
// of the vertices of the given graph 
import java.util.*; 

class GFG { 

    // Function to print the in and out degrees 
    // of all the vertices of the given graph 
    static void findInOutDegree(List<List<Integer> > adjList, int n) 
    { 
        int in[] = new int[n]; 
        int out[] = new int[n]; 

        for (int i = 0; i < adjList.size(); i++) { 

            List<Integer> list = adjList.get(i); 

            // Out degree for ith vertex will be the count 
            // of direct paths from i to other vertices 
            out[i] = list.size(); 
            for (int j = 0; j < list.size(); j++) 

                // Every vertex that has an incoming  
                // edge from i 
                in[list.get(j)]++; 
        } 

        System.out.println("Vertex\tIn\tOut"); 
        for (int k = 0; k < n; k++) { 
            System.out.println(k + "\t" + in[k] + "\t" + out[k]); 
        } 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        // Adjacency list representation of the graph 
        List<List<Integer> > adjList = new ArrayList<>(); 

        // Vertices 1 and 2 have an incoming edge  
        // from vertex 0 
        List<Integer> tmp =  
           new ArrayList<Integer>(Arrays.asList(1, 2)); 
        adjList.add(tmp); 

        // Vertex 3 has an incoming edge from vertex 1 
        tmp = new ArrayList<Integer>(Arrays.asList(3)); 
        adjList.add(tmp); 

        // Vertices 0, 5 and 6 have an incoming 
        // edge from vertex 2 
        tmp =  
          new ArrayList<Integer>(Arrays.asList(0, 5, 6)); 
        adjList.add(tmp); 

        // Vertices 1 and 4 have an incoming edge  
        // from vertex 3 
        tmp = new ArrayList<Integer>(Arrays.asList(1, 4)); 
        adjList.add(tmp); 

        // Vertices 2 and 3 have an incoming edge 
        // from vertex 4 
        tmp = new ArrayList<Integer>(Arrays.asList(2, 3)); 
        adjList.add(tmp); 

        // Vertices 4 and 6 have an incoming edge 
        // from vertex 5 
        tmp = new ArrayList<Integer>(Arrays.asList(4, 6)); 
        adjList.add(tmp); 

        // Vertex 5 has an incoming edge from vertex 6 
        tmp = new ArrayList<Integer>(Arrays.asList(5)); 
        adjList.add(tmp); 

        int n = adjList.size(); 
        findInOutDegree(adjList, n); 
    } 
} 

```

## Python

```py

# Python3 program to find the in and out  
# degrees of the vertices of the given graph  

# Function to print the in and out degrees  
# of all the vertices of the given graph  
def findInOutDegree(adjList, n):  

    _in = [0] * n  
    out = [0] * n 

    for i in range(0, len(adjList)):  

        List = adjList[i]  

        # Out degree for ith vertex will be the count  
        # of direct paths from i to other vertices  
        out[i] = len(List)  
        for j in range(0, len(List)):  

            # Every vertex that has  
            # an incoming edge from i  
            _in[List[j]] += 1

    print("Vertex\tIn\tOut")  
    for k in range(0, n):  
        print(str(k) + "\t" + str(_in[k]) + 
                       "\t" + str(out[k]))  

# Driver code  
if __name__ == "__main__":  

    # Adjacency list representation of the graph  
    adjList = []  

    # Vertices 1 and 2 have an incoming edge  
    # from vertex 0  
    adjList.append([1, 2])  

    # Vertex 3 has an incoming edge from vertex 1  
    adjList.append([3])  

    # Vertices 0, 5 and 6 have an  
    # incoming edge from vertex 2  
    adjList.append([0, 5, 6])  

    # Vertices 1 and 4 have an  
    # incoming edge from vertex 3  
    adjList.append([1, 4])  

    # Vertices 2 and 3 have an  
    # incoming edge from vertex 4  
    adjList.append([2, 3])  

    # Vertices 4 and 6 have an  
    # incoming edge from vertex 5  
    adjList.append([4, 6])  

    # Vertex 5 has an incoming edge from vertex 6  
    adjList.append([5])  

    n = len(adjList)  
    findInOutDegree(adjList, n)  

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# program to find the in and out degrees 
// of the vertices of the given graph 
using System; 
using System.Collections.Generic;     

class GFG 
{ 

// Function to print the in and out degrees 
// of all the vertices of the given graph 
static void findInOutDegree(List<List<int>> adjList, int n) 
{ 
    int []iN = new int[n]; 
    int []ouT = new int[n]; 

    for (int i = 0; i < adjList.Count; i++)  
    { 

        List<int> list = adjList[i]; 

        // Out degree for ith vertex will be the count 
        // of direct paths from i to other vertices 
        ouT[i] = list.Count; 
        for (int j = 0; j < list.Count; j++) 

            // Every vertex that has an incoming  
            // edge from i 
            iN[list[j]]++; 
    } 

    Console.WriteLine("Vertex\t\tIn\t\tOut"); 
    for (int k = 0; k < n; k++) 
    { 
        Console.WriteLine(k + "\t\t" +  
                      iN[k] + "\t\t" + ouT[k]); 
    } 
} 

// Driver code 
public static void Main(String []args) 
{ 
    // Adjacency list representation of the graph 
    List<List<int> > adjList = new List<List<int>>(); 

    // Vertices 1 and 2 have an incoming edge  
    // from vertex 0 
    List<int> tmp =  
    new List<int>{1, 2}; 
    adjList.Add(tmp); 

    // Vertex 3 has an incoming edge from vertex 1 
    tmp = new List<int>{3}; 
    adjList.Add(tmp); 

    // Vertices 0, 5 and 6 have an incoming 
    // edge from vertex 2 
    tmp =  
    new List<int>{0, 5, 6}; 
    adjList.Add(tmp); 

    // Vertices 1 and 4 have an incoming edge  
    // from vertex 3 
    tmp = new List<int>{1, 4}; 
    adjList.Add(tmp); 

    // Vertices 2 and 3 have an incoming edge 
    // from vertex 4 
    tmp = new List<int>{2, 3}; 
    adjList.Add(tmp); 

    // Vertices 4 and 6 have an incoming edge 
    // from vertex 5 
    tmp = new List<int>{4, 6}; 
    adjList.Add(tmp); 

    // Vertex 5 has an incoming edge from vertex 6 
    tmp = new List<int>{5}; 
    adjList.Add(tmp); 

    int n = adjList.Count; 
    findInOutDegree(adjList, n); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:** 

```
Vertex    In    Out
0    1    2
1    2    1
2    2    3
3    2    2
4    2    2
5    2    2
6    2    1

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。