# 排列数组元素，以使元素的最后一位等于下一个元素的第一位

> 原文： [https://www.geeksforgeeks.org/arrange-array-elements-such-that-last-digit-of-an-element-is-equal-to-first-digit-of-the-next-element/](https://www.geeksforgeeks.org/arrange-array-elements-such-that-last-digit-of-an-element-is-equal-to-first-digit-of-the-next-element/)

给定整数数组 **arr []** ，任务是排列数组元素，以使元素的最后一位等于下一个元素的第一位。

**示例**：

> **输入**：arr [] = {123，321}
> **输出**：123321
> 
> **输入**：arr [] = {451，378，123，1254}
> **输出**：1254 451 123378

**天真的方法**：找到数组元素的所有排列，然后打印满足所需条件的排列好的数组。 此方法的时间复杂度为 **O（N！）**

**有效方法**：创建一个有向图，其中如果节点[表示的数字]的最后一位数字是从节点`A`到节点`B`的有向边，`A`等于节点`B`表示的数字的第一位。 现在，找到所形成图的[欧拉路径](https://www.geeksforgeeks.org/fleurys-algorithm-for-printing-eulerian-path/)。 上述算法的复杂度为 **O（E * E）**，其中`E`是图中的边数。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// To store the array elements 
vector<string> arr; 

// Adjacency list for the graph nodes 
vector<vector<int> > graph; 

// To store the euler path 
vector<string> path; 

// Print eulerian path 
bool print_euler(int i, int visited[], int count) 
{ 
    // Mark node as visited 
    // and increase the count 
    visited[i] = 1; 
    count++; 

    // If all the nodes are visited 
    // then we have traversed the euler path 
    if (count == graph.size()) { 
        path.push_back(arr[i]); 
        return true; 
    } 

    // Check if the node lies in euler path 
    bool b = false; 

    // Traverse through remaining edges 
    for (int j = 0; j < graph[i].size(); j++) 
        if (visited[graph[i][j]] == 0) { 
            b |= print_euler(graph[i][j], visited, count); 
        } 

    // If the euler path is found 
    if (b) { 
        path.push_back(arr[i]); 
        return true; 
    } 

    // Else unmark the node 
    else { 
        visited[i] = 0; 
        count--; 
        return false; 
    } 
} 

// Function to create the graph and 
// print the required path 
void connect() 
{ 
    int n = arr.size(); 
    graph.clear(); 
    graph.resize(n); 

    // Connect the nodes 
    for (int i = 0; i < n; i++) { 
        for (int j = 0; j < n; j++) { 
            if (i == j) 
                continue; 

            // If the last character matches with the 
            // first character 
            if (arr[i][arr[i].length() - 1] == arr[j][0]) { 
                graph[i].push_back(j); 
            } 
        } 
    } 

    // Print the path 
    for (int i = 0; i < n; i++) { 
        int visited[n] = { 0 }, count = 0; 

        // If the euler path starts 
        // from the ith node 
        if (print_euler(i, visited, count)) 
            break; 
    } 

    // Print the euler path 
    for (int i = path.size() - 1; i >= 0; i--) { 
        cout << path[i]; 
        if (i != 0) 
            cout << " "; 
    } 
} 
// Driver code 
int main() 
{ 
    arr.push_back("451"); 
    arr.push_back("378"); 
    arr.push_back("123"); 
    arr.push_back("1254"); 

    // Create graph and print the path 
    connect(); 

    return 0; 
} 

```

## Python3

```

# Python3 implementation of the approach  

# Print eulerian path  
def print_euler(i, visited, count):  

    # Mark node as visited  
    # and increase the count  
    visited[i] = 1
    count += 1

    # If all the nodes are visited then  
    # we have traversed the euler path  
    if count == len(graph):  
        path.append(arr[i])  
        return True

    # Check if the node lies in euler path  
    b = False

    # Traverse through remaining edges  
    for j in range(0, len(graph[i])):  
        if visited[graph[i][j]] == 0:  
            b |= print_euler(graph[i][j], visited, count)  

    # If the euler path is found  
    if b:  
        path.append(arr[i])  
        return True

    # Else unmark the node  
    else:  
        visited[i] = 0
        count -= 1
        return False

# Function to create the graph  
# and print the required path  
def connect():  

    n = len(arr) 
    # Connect the nodes  
    for i in range(0, n):  
        for j in range(0, n):  
            if i == j:  
                continue

            # If the last character matches  
            # with the first character  
            if arr[i][-1] == arr[j][0]:  
                graph[i].append(j)  

    # Print the path  
    for i in range(0, n):  
        visited = [0] * n 
        count = 0

        # If the euler path starts  
        # from the ith node  
        if print_euler(i, visited, count):  
            break

    # Print the euler path  
    for i in range(len(path) - 1, -1, -1):  
        print(path[i], end = "")  
        if i != 0: 
            print(" ", end = "")  

# Driver code  
if __name__ == "__main__": 

    # To store the array elements  
    arr = [] 
    arr.append("451")  
    arr.append("378")  
    arr.append("123")  
    arr.append("1254") 

    # Adjacency list for the graph nodes 
    graph = [[] for i in range(len(arr))] 

    # To store the euler path 
    path = [] 

    # Create graph and print the path  
    connect() 

# This code is contributed by Rituraj Jain 

```

**Output:**

```
1254 451 123 378

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。