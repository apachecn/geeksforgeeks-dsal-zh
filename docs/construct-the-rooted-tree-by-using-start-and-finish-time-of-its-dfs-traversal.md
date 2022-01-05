# 利用其 DFS 遍历的开始和结束时间

构造根树

> 原文:[https://www . geeksforgeeks . org/通过使用其 dfs 遍历的开始和结束时间来构造根树/](https://www.geeksforgeeks.org/construct-the-rooted-tree-by-using-start-and-finish-time-of-its-dfs-traversal/)

给定根树中可用的 N 个顶点的 DFS 遍历的开始和结束时间，任务是构建树(打印每个节点的父节点)。
根节点的父节点为 0。
**例:**

```
Input: Start[] = {2, 4, 1, 0, 3}, End[] = {3, 5, 4, 5, 4}
Output: 3 4 4 0 3
Given Tree is -:
                      4(0, 5)
                    /   \
              (1, 4)3     2(4, 5)
                 /  \    
           (2, 3)1    5(3, 4)
The root will always have start time = 0
processing a node takes 1 unit time but backtracking 
does not consume time, so the finishing time 
of two nodes can be the same.

Input: Start[] = {4, 3, 2, 1, 0}, End[] = {5, 5, 3, 3, 5}
Output: 2 5 4 5 0
```

**进场:**

*   树根是开始时间为零的顶点。
*   现在，找到一个顶点的后代就足够了，这样我们就可以找到每个顶点的父节点。
*   将恒等式[i]定义为起点等于 I 的顶点的索引
*   由于 Start[v]和 End[v]是顶点 v 的开始和结束时间，v 的第一个孩子是 Identity[Start[v]+1]，
    第(i+1) <sup>个</sup>是 Identity[End[chv[i]]，其中 chv[i]是 v 的第一个孩子
*   以 DFS 方式向下遍历并更新每个节点的父节点。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int N;

// Function to find the parent of each node.
vector<int> Restore_Tree(int Start[], int End[])
{

    // Storing index of vertex with starting
    // time Equal to i
    vector<int> Identity(N,0);

    for (int i = 0; i < N; i++)
    {
        Identity[Start[i]] = i;
    }

    // Parent array
    vector<int> parent(N,-1);
    int curr_parent = Identity[0];

    for (int j = 1; j < N; j++)
    {

        // Find the vertex with starting time j
        int child = Identity[j];

        // If end time of this child is greater than
        // (start time + 1), then we traverse down and
        // store curr_parent as the parent of child
        if (End[child] - j > 1)
        {
            parent[child] = curr_parent;
            curr_parent = child;
        }

        // Find the parent of current vertex
        // over iterating on the finish time
        else
            parent[child] = curr_parent;

        // Backtracking takes zero time
        while (End[child]== End[parent[child]])
        {
            child = parent[child];
            curr_parent = parent[child];
            if (curr_parent == Identity[0])
                break;
        }
    }
    for (int i = 0; i < N; i++)
        parent[i] += 1;

    // Return the parent array
    return parent;
}

// Driver Code
int main()
{
    N = 5;

    // Start and End time of DFS
    int Start[] = {2, 4, 1, 0, 3};
    int End[] = {3, 5, 4, 5, 4};
    vector<int> a = Restore_Tree(Start, End);

    for(int ans:a)
        cout << ans << " ";

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.Arrays;

class GFG
{

static int N = 5;

// Function to find the parent of each node.
static int[] Restore_Tree(int []S, int []End)
{

    // Storing index of vertex with starting
    // time Equal to i
    int []Identity = new int[N];

    for(int i = 0; i < N; i++)
        Identity[S[i]] = i;

    // Parent array
    int []parent = new int[N];
    Arrays.fill(parent,-1);
    int curr_parent = Identity[0];

    for(int j = 1; j < N; j++)
    {

        // Find the vertex with starting time j
        int child = Identity[j];

        // If end time of this child is greater than
        // (start time + 1), then we traverse down and
        // store curr_parent as the parent of child
        if(End[child] - j > 1)
        {
            parent[child] = curr_parent;
            curr_parent = child;
        }

        // Find the parent of current vertex
        // over iterating on the finish time
        else{
            parent[child] = curr_parent;

            // Backtracking takes zero time
            while(parent[child]>-1 && End[child] == End[parent[child]])
            {
                child = parent[child];
                curr_parent = parent[child];
                if(curr_parent == Identity[0])
                    break;
            }
        }
    }
    for(int i = 0; i < N; i++)
        parent[i] += 1;

    // Return the parent array
    return parent;
}

// Driver Code
public static void main(String[] args)
{
    // Start and End time of DFS
    int []Start = {2, 4, 1, 0, 3};
    int []End = {3, 5, 4, 5, 4};
    int ans[] =Restore_Tree(Start, End);
    for(int a:ans)
        System.out.print(a + " ");
}
}

// This code has been contributed by 29AjayKumar
```

## 计算机编程语言

```
# Python implementation of the above approach

# Function to find the parent of each node.
def Restore_Tree(S, E):

    # Storing index of vertex with starting
    # time Equal to i
    Identity = N*[0] 

    for i in range(N):
        Identity[Start[i]] = i

    # Parent array
    parent = N*[-1]
    curr_parent = Identity[0]

    for j in range(1, N):

        # Find the vertex with starting time j
        child = Identity[j]

        # If end time of this child is greater than
        # (start time + 1), then we traverse down and
        # store curr_parent as the parent of child
        if End[child] - j > 1:
            parent[child] = curr_parent
            curr_parent = child

        # Find the parent of current vertex
        # over iterating on the finish time
        else:    
            parent[child] = curr_parent

            # Backtracking takes zero time
            while End[child]== End[parent[child]]:
                child = parent[child]
                curr_parent = parent[child]
                if curr_parent == Identity[0]:
                    break
    for i in range(N):
        parent[i]+= 1

    # Return the parent array
    return parent

# Driver Code
if __name__=="__main__":
    N = 5

    # Start and End time of DFS
    Start = [2, 4, 1, 0, 3]
    End = [3, 5, 4, 5, 4]
    print(*Restore_Tree(Start, End))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int N = 5;

// Function to find the parent of each node.
static int[] Restore_Tree(int []S, int []End)
{

    // Storing index of vertex with starting
    // time Equal to i
    int []Identity = new int[N];

    for(int i = 0; i < N; i++)
        Identity[S[i]] = i;

    // Parent array
    int []parent = new int[N];
    for(int i = 0; i < N; i++)
        parent[i]=-1;
    int curr_parent = Identity[0];

    for(int j = 1; j < N; j++)
    {

        // Find the vertex with starting time j
        int child = Identity[j];

        // If end time of this child is greater than
        // (start time + 1), then we traverse down and
        // store curr_parent as the parent of child
        if(End[child] - j > 1)
        {
            parent[child] = curr_parent;
            curr_parent = child;
        }

        // Find the parent of current vertex
        // over iterating on the finish time
        else
        {
            parent[child] = curr_parent;

            // Backtracking takes zero time
            while(parent[child]>-1 && End[child] == End[parent[child]])
            {
                child = parent[child];
                curr_parent = parent[child];
                if(curr_parent == Identity[0])
                    break;
            }
        }
    }
    for(int i = 0; i < N; i++)
        parent[i] += 1;

    // Return the parent array
    return parent;
}

// Driver Code
public static void Main(String[] args)
{
    // Start and End time of DFS
    int []Start = {2, 4, 1, 0, 3};
    int []End = {3, 5, 4, 5, 4};
    int []ans =Restore_Tree(Start, End);
    foreach(int a in ans)
        Console.Write(a + " ");
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

var N = 5;

// Function to find the parent of each node.
function Restore_Tree(S, End)
{

    // Storing index of vertex with starting
    // time Equal to i
    var Identity = Array(N);

    for(var i = 0; i < N; i++)
        Identity[S[i]] = i;

    // Parent array
    var parent = Array(N);
    for(var i = 0; i < N; i++)
        parent[i]=-1;
    var curr_parent = Identity[0];

    for(var j = 1; j < N; j++)
    {

        // Find the vertex with starting time j
        var child = Identity[j];

        // If end time of this child is greater than
        // (start time + 1), then we traverse down and
        // store curr_parent as the parent of child
        if(End[child] - j > 1)
        {
            parent[child] = curr_parent;
            curr_parent = child;
        }

        // Find the parent of current vertex
        // over iterating on the finish time
        else
        {
            parent[child] = curr_parent;

            // Backtracking takes zero time
            while(parent[child]>-1 &&
            End[child] == End[parent[child]])
            {
                child = parent[child];
                curr_parent = parent[child];
                if(curr_parent == Identity[0])
                    break;
            }
        }
    }
    for(var i = 0; i < N; i++)
        parent[i] += 1;

    // Return the parent array
    return parent;
}

// Driver Code

// Start and End time of DFS
var Start = [2, 4, 1, 0, 3];
var End = [3, 5, 4, 5, 4];
var ans =Restore_Tree(Start, End);
for(var a of ans)
    document.write(a + " ");

</script>
```

**Output:** 

```
3 4 4 0 3
```

**时间复杂度:** O(N)
其中 N 是树中的节点数。