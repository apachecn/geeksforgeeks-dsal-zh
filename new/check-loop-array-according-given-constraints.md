# 根据给定的约束检查数组中的循环

> 原文： [https://www.geeksforgeeks.org/check-loop-array-according-given-constraints/](https://www.geeksforgeeks.org/check-loop-array-according-given-constraints/)

给定数组 arr [0..n-1]的正数和负数，我们需要确定数组中是否存在具有给定运动规则的循环。 如果 i 索引处的数字为正，则将 arr [i]％n 向前移动，即下一个要访问的索引为（i + arr [i]）％n。 相反，如果为负，则向后移动 arr [i]％n 步，即，下一个要访问的索引为（i – arr [i]）％n。 这里 n 是数组的大小。 如果 arr [i]％n 的值为零，则表示从索引 i 开始没有移动。

**示例：**

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

注意，自循环不被视为一个循环。 例如，{0}不是循环的。

想法是使用给定的规则集形成数组元​​素的有向图。 形成图表时，我们不会进行自我循环，因为值 arr [i]％n 等于 0 表示没有移动。 最后，我们的任务减少到有向图中的[检测周期。 为了检测周期，我们使用 DFS，在 DFS 中，如果到达被访问的节点和递归调用堆栈，则说存在一个周期。](https://www.geeksforgeeks.org/detect-cycle-in-a-graph/)

## C ++

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

## 爪哇

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

## Python3

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

**Output :**

```
 Yes
```

本文由 **Roshni Agarwal** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

