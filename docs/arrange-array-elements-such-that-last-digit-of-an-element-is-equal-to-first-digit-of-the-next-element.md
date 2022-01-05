# 排列数组元素，使一个元素的最后一个数字等于下一个元素的第一个数字

> 原文:[https://www . geeksforgeeks . org/array-array-elements-这样一个元素的最后一位数字等于下一个元素的第一位数字/](https://www.geeksforgeeks.org/arrange-array-elements-such-that-last-digit-of-an-element-is-equal-to-first-digit-of-the-next-element/)

给定一个整数数组 **arr[]** ，任务是排列数组元素，使得一个元素的最后一个数字等于下一个元素的第一个数字。

**示例:**

> **输入:** arr[] = {123，321 }
> T3】输出: 123 321
> 
> **输入:** arr[] = {451，378，123，1254 }
> T3】输出: 1254 451 123 378

**天真法:**找出数组元素的所有排列，然后打印出符合要求条件的排列数组。这种方法的时间复杂度是 **O(N！)**

**有效方法:**创建一个有向图，如果节点 **A** 表示的数字的最后一位数字等于节点 **B** 表示的数字的第一位数字，则从节点 **A** 到节点 **B** 会有一条有向边。现在，为形成的图形找到[欧拉路径](https://www.geeksforgeeks.org/fleurys-algorithm-for-printing-eulerian-path/)。上述算法的复杂度为 **O(E * E)** ，其中 **E** 为图中的边数。

下面是上述方法的实现:

## C++

```
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

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

// To store the array elements
static List<String> arr = new ArrayList<String>();

// Adjacency list for the graph nodes
static List<List<Integer>> graph = new ArrayList<List<Integer>>();

// To store the euler path
static List<String> path = new ArrayList<String>();

// Print eulerian path
static boolean print_euler(int i, int []visited,
                           int count)
{

    // Mark node as visited
    // and increase the count
    visited[i] = 1;
    count++;

    // If all the nodes are visited
    // then we have traversed the euler path
    if (count == graph.size())
    {
        path.add(arr.get(i));
        return true;
    }

    // Check if the node lies in euler path
    boolean b = false;

    // Traverse through remaining edges
    for(int j = 0; j < graph.get(i).size(); j++)
        if (visited[graph.get(i).get(j)] == 0)
        {
            b |= print_euler(graph.get(i).get(j),
                             visited, count);
        }

    // If the euler path is found
    if (b)
    {
        path.add(arr.get(i));
        return true;
    }

    // Else unmark the node
    else
    {
        visited[i] = 0;
        count--;
        return false;
    }
}

// Function to create the graph and
// print the required path
static void connect()
{
    int n = arr.size();
    graph = new ArrayList<List<Integer>>(n);

    for(int i = 0; i < n; i++)
    {
        graph.add(new ArrayList<Integer>());
    }

    // Connect the nodes
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < n; j++)
        {
            if (i == j)
                continue;

            // If the last character matches with the
            // first character
            if (arr.get(i).charAt((arr.get(i).length()) - 1) ==
                arr.get(j).charAt(0))
            {
                graph.get(i).add(j);
            }
        }
    }

    // Print the path
    for(int i = 0; i < n; i++)
    {
        int []visited = new int[n];
        int count = 0;

        // If the euler path starts
        // from the ith node
        if (print_euler(i, visited, count))
            break;
    }

    // Print the euler path
    for(int i = path.size() - 1; i >= 0; i--)
    {
        System.out.print(path.get(i));

        if (i != 0)
            System.out.print(" ");
    }
}

// Driver code
public static void main(String []args)
{
    arr.add("451");
    arr.add("378");
    arr.add("123");
    arr.add("1254");

    // Create graph and print the path
    connect();
}
}

// This code is contributed by pratham76
```

## 蟒蛇 3

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
        print(path[i], end="")
        if i != 0:
            print(" ", end="")

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

## C#

```
// C# implementation of the approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// To store the array elements
static List<string> arr = new List<string>();

// Adjacency list for the graph nodes
static List<List<int> > graph=  new List<List<int>>();

// To store the euler path
static List<string> path = new List<string>();

// Print eulerian path
static bool print_euler(int i, int []visited, int count)
{
    // Mark node as visited
    // and increase the count
    visited[i] = 1;
    count++;

    // If all the nodes are visited
    // then we have traversed the euler path
    if (count == graph.Count) {
        path.Add(arr[i]);
        return true;
    }

    // Check if the node lies in euler path
    bool b = false;

    // Traverse through remaining edges
    for (int j = 0; j < graph[i].Count; j++)
        if (visited[graph[i][j]] == 0) {
            b |= print_euler(graph[i][j], visited, count);
        }

    // If the euler path is found
    if (b) {
        path.Add(arr[i]);
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
static void connect()
{
    int n = arr.Count;
    graph=new List<List<int>>(n);

    for(int i = 0; i < n; i++)
    {
        graph.Add(new List<int>());
    }

    // Connect the nodes
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (i == j)
                continue;

            // If the last character matches with the
            // first character
            if (arr[i][(arr[i].Length) - 1] == arr[j][0]) {
                graph[i].Add(j);
            }
        }
    }

    // Print the path
    for (int i = 0; i < n; i++) {

        int []visited = new int[n];
        int count = 0;

        // If the euler path starts
        // from the ith node
        if (print_euler(i, visited, count))
            break;
    }

    // Print the euler path
    for (int i = path.Count - 1; i >= 0; i--) {
        Console.Write(path[i]);
        if (i != 0)
            Console.Write(" ");
    }
}

// Driver code
public static void Main(params string []args)
{
    arr.Add("451");
    arr.Add("378");
    arr.Add("123");
    arr.Add("1254");

    // Create graph and print the path
    connect();
}
}

// This code is contributed by rutvik_56.
```

**Output:** 

```
1254 451 123 378
```

**时间复杂度:** O(N* log(N))

**辅助空间** : O(N)