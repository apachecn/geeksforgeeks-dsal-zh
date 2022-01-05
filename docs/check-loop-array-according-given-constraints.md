# 根据给定的约束条件检查数组中的循环

> 原文:[https://www . geesforgeks . org/check-loop-array-根据给定的约束/](https://www.geeksforgeeks.org/check-loop-array-according-given-constraints/)

给定数组 arr[0..n-1]的正数和负数，我们需要找到数组中是否有给定运动规则的循环。如果 I 索引处的数字为正，则向前移动 arr[i]%n 步，即下一个要访问的索引为(i + arr[i])%n .相反，如果为负，则向后移动 arr[i]%n 步，即下一个要访问的索引为(I–arr[I])% n .这里 n 是数组的大小。如果 arr[i]%n 的值为零，则意味着没有从索引 I 的移动。
**示例:**

```
Input: arr[] = {2, -1, 1, 2, 2}
Output: Yes
Explanation: There is a loop in this array
because 0 moves to 2, 2 moves to 3, and 3 
moves to 0.

Input  : arr[] = {1, 1, 1, 1, 1, 1}
Output : Yes
Whole array forms a loop.

Input  : arr[] = {1, 2}
Output : No
We move from 0 to index 1\. From index
1, there is no move as 2%n is 0\. Note that
n is 2.
```

请注意，自循环不被视为一个循环。例如{0}不是循环的。

其思想是使用给定的一组规则形成数组元素的有向图。当形成图时，我们不进行自循环，因为值 arr[i]%n 等于 0 意味着没有移动。最后，我们的任务简化为有向图中的[检测周期。为了检测循环，我们使用 DFS，在 DFS 中，如果到达一个被访问的节点，递归调用栈，我们说有一个循环。](https://www.geeksforgeeks.org/detect-cycle-in-a-graph/) 

## C++

```
// C++ program to check if a given array is cyclic or not
#include<bits/stdc++.h>
using namespace std;

// A simple Graph DFS based recursive function to check if
// there is cycle in graph with vertex v as root of DFS.
// Refer below article for details.
// https://www.geeksforgeeks.org/detect-cycle-in-a-graph/
bool isCycleRec(int v, vector<int>adj[],
               vector<bool> &visited, vector<bool> &recur)
{
    visited[v] = true;
    recur[v] = true;
    for (int i=0; i<adj[v].size(); i++)
    {
        if (visited[adj[v][i]] == false)
        {
            if (isCycleRec(adj[v][i], adj, visited, recur))
                return true;
        }

        // There is a cycle if an adjacent is visited
        // and present in recursion call stack recur[]
        else if (visited[adj[v][i]] == true &&
                 recur[adj[v][i]] == true)
            return true;
    }

    recur[v] = false;
    return false;
}

// Returns true if arr[] has cycle
bool isCycle(int arr[], int n)
{
    // Create a graph using given moves in arr[]
    vector<int>adj[n];
    for (int i=0; i<n; i++)
      if (i != (i+arr[i]+n)%n)
        adj[i].push_back((i+arr[i]+n)%n);

    // Do DFS traversal of graph to detect cycle
    vector<bool> visited(n, false);
    vector<bool> recur(n, false);
    for (int i=0; i<n; i++)
        if (visited[i]==false)
            if (isCycleRec(i, adj, visited, recur))
                return true;
    return true;
}

// Driver code
int main(void)
{
    int arr[] = {2, -1, 1, 2, 2};
    int n = sizeof(arr)/sizeof(arr[0]);
    if (isCycle(arr, n))
        cout << "Yes"<<endl;
    else
        cout << "No"<<endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// a given array is cyclic or not
import java.util.Vector;

class GFG
{

    // A simple Graph DFS based recursive function
    // to check if there is cycle in graph with
    // vertex v as root of DFS. Refer below article for details.
    // https://www.geeksforgeeks.org/detect-cycle-in-a-graph/
    static boolean isCycleRec(int v, Vector<Integer>[] adj,
                                     Vector<Boolean> visited,
                                     Vector<Boolean> recur)
    {
        visited.set(v, true);
        recur.set(v, true);

        for (int i = 0; i < adj[v].size(); i++)
        {
            if (visited.elementAt(adj[v].elementAt(i)) == false)
            {
                if (isCycleRec(adj[v].elementAt(i),
                               adj, visited, recur))
                    return true;
            }

            // There is a cycle if an adjacent is visited
            // and present in recursion call stack recur[]
            else if (visited.elementAt(adj[v].elementAt(i)) == true &&
                       recur.elementAt(adj[v].elementAt(i)) == true)
                return true;
        }
        recur.set(v, false);
        return false;
    }

    // Returns true if arr[] has cycle
    @SuppressWarnings("unchecked")
    static boolean isCycle(int[] arr, int n)
    {

        // Create a graph using given moves in arr[]
        Vector<Integer>[] adj = new Vector[n];
        for (int i = 0; i < n; i++)
            if (i != (i + arr[i] + n) % n &&
                          adj[i] != null)
                adj[i].add((i + arr[i] + n) % n);

        // Do DFS traversal of graph to detect cycle
        Vector<Boolean> visited = new Vector<>();
        for (int i = 0; i < n; i++)
            visited.add(true);
        Vector<Boolean> recur = new Vector<>();
        for (int i = 0; i < n; i++)
            recur.add(true);

        for (int i = 0; i < n; i++)
            if (visited.elementAt(i) == false)
                if (isCycleRec(i, adj, visited, recur))
                    return true;
        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 2, -1, 1, 2, 2 };
        int n = arr.length;
        if (isCycle(arr, n) == true)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to check if a
# given array is cyclic or not

# A simple Graph DFS based recursive
# function to check if there is cycle
# in graph with vertex v as root of DFS.
# Refer below article for details.
# https:#www.geeksforgeeks.org/detect-cycle-in-a-graph/
def isCycleRec(v, adj, visited, recur):
    visited[v] = True
    recur[v] = True
    for i in range(len(adj[v])):
        if (visited[adj[v][i]] == False):
            if (isCycleRec(adj[v][i], adj,
                               visited, recur)):
                return True

        # There is a cycle if an adjacent is visited
        # and present in recursion call stack recur[]
        elif (visited[adj[v][i]] == True and
                recur[adj[v][i]] == True):
            return True

    recur[v] = False
    return False

# Returns true if arr[] has cycle
def isCycle(arr, n):

    # Create a graph using given
    # moves in arr[]
    adj = [[] for i in range(n)]
    for i in range(n):
        if (i != (i + arr[i] + n) % n):
            adj[i].append((i + arr[i] + n) % n)

    # Do DFS traversal of graph
    # to detect cycle  
    visited = [False] * n
    recur = [False] * n
    for i in range(n):
        if (visited[i] == False):
            if (isCycleRec(i, adj,
                           visited, recur)):
                return True
    return True

# Driver code
if __name__ == '__main__':

    arr = [2, -1, 1, 2, 2]
    n = len(arr)
    if (isCycle(arr, n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by PranchalK
```

## C#

```
// C# program to check if
// a given array is cyclic or not
using System;
using System.Collections.Generic;
public class GFG
{

  // A simple Graph DFS based recursive function
  // to check if there is cycle in graph with
  // vertex v as root of DFS. Refer below article for details.
  // https://www.geeksforgeeks.org/detect-cycle-in-a-graph/
  static bool isCycleRec(int v, List<int>[] adj,
                         List<Boolean> visited,
                         List<Boolean> recur)
  {
    visited[v] = true;
    recur[v] =  true;

    for (int i = 0; i < adj[v].Count; i++)
    {
      if (visited[adj[v][i]] == false)
      {
        if (isCycleRec(adj[v][i],
                       adj, visited, recur))
          return true;
      }

      // There is a cycle if an adjacent is visited
      // and present in recursion call stack recur[]
      else if (visited[adj[v][i]] == true &&
               recur[adj[v][i]] == true)
        return true;
    }
    recur[v] = false;
    return false;
  }

  // Returns true if []arr has cycle
  static bool isCycle(int[] arr, int n)
  {

    // Create a graph using given moves in []arr
    List<int>[] adj = new List<int>[n];
    for (int i = 0; i < n; i++)
      if (i != (i + arr[i] + n) % n &&
          adj[i] != null)
        adj[i].Add((i + arr[i] + n) % n);

    // Do DFS traversal of graph to detect cycle
    List<Boolean> visited = new List<Boolean>();
    for (int i = 0; i < n; i++)
      visited.Add(true);
    List<Boolean> recur = new List<Boolean>();
    for (int i = 0; i < n; i++)
      recur.Add(true);

    for (int i = 0; i < n; i++)
      if (visited[i] == false)
        if (isCycleRec(i, adj, visited, recur))
          return true;
    return true;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int[] arr = { 2, -1, 1, 2, 2 };
    int n = arr.Length;
    if (isCycle(arr, n) == true)
      Console.WriteLine("Yes");
    else
      Console.WriteLine("No");
  }
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

// JavaScript program to check if a given array is cyclic or not

// A simple Graph DFS based recursive function to check if
// there is cycle in graph with vertex v as root of DFS.
// Refer below article for details.
// https://www.geeksforgeeks.org/detect-cycle-in-a-graph/
function isCycleRec(v, adj, visited, recur) {
    visited[v] = true;
    recur[v] = true;
    for (let i = 0; i < adj[v].length; i++) {
        if (visited[adj[v][i]] == false) {
            if (isCycleRec(adj[v][i], adj, visited, recur))
                return true;
        }

        // There is a cycle if an adjacent is visited
        // and present in recursion call stack recur[]
        else if (visited[adj[v][i]] == true &&
            recur[adj[v][i]] == true)
            return true;
    }

    recur[v] = false;
    return false;
}

// Returns true if arr[] has cycle
function isCycle(arr, n) {
    // Create a graph using given moves in arr[]
    let adj = new Array(n).fill(0).map(() => []);
    for (let i = 0; i < n; i++)
        if (i != (i + arr[i] + n) % n)
            adj[i].push((i + arr[i] + n) % n);

    // Do DFS traversal of graph to detect cycle
    let visited = new Array(n).fill(false);
    let recur = new Array(n).fill(false);
    for (let i = 0; i < n; i++)
        if (visited[i] == false)
            if (isCycleRec(i, adj, visited, recur))
                return true;
    return true;
}

// Driver code

let arr = [2, -1, 1, 2, 2];
let n = arr.length;
if (isCycle(arr, n))
    document.write("Yes" + "<br>");
else
    document.write("No" + "<br>");

</script>
```

**输出:**

```
 Yes
```

本文由 **Roshni Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。