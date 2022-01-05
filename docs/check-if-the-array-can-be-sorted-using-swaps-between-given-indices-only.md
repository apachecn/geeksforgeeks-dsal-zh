# 检查数组是否只能使用给定索引之间的交换来排序

> 原文:[https://www . geesforgeks . org/check-if-the-array-can-sort-use-swaps-with-给定索引-only/](https://www.geeksforgeeks.org/check-if-the-array-can-be-sorted-using-swaps-between-given-indices-only/)

给定大小为 **N** 的数组 **arr[]** ，该数组由范围**【0，N–1】**中以随机顺序排列的不同整数组成。也给定几对，其中每对表示数组元素可以交换的索引。允许的互换数量没有限制。任务是找出是否有可能使用这些交换以升序排列数组。如果可能，则打印**是**否则打印**否**。
**举例:**

> **输入:** arr[] = {0，4，3，2，1，5}，对[][] = {{1，4}，{2，3}}
> **输出:** Yes
> swap(arr[1]，arr[4]) - > arr[] = {0，1，3，2，4，5}
> swap(arr[2]，arr[3]) - > arr[] = {0，1，2，3，4，5}

**方法:**给定的问题可以被认为是一个图问题，其中 **N** 表示图中节点的总数，每个交换对表示图中的一条无向边。我们必须找出是否有可能将输入数组转换为 **{0，1，2，3，…，N–1 }**的形式。
让我们将上面的数组称为 b。现在找出两个数组的所有连接的组件，如果至少一个组件的元素不同，那么答案是**否**否则答案是**是**。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the array elements
// can be sorted with the given operation
bool canBeSorted(int N, vector<int> a, int P,
vector<pair<int, int> > vp)
{

    // To create the adjacency list of the graph
    vector<int> v[N];

    // Boolean array to mark the visited nodes
    bool vis[N] = { false };

    // Creating adjacency list for undirected graph
    for (int i = 0; i < P; i++) {
        v[vp[i].first].push_back(vp[i].second);
        v[vp[i].second].push_back(vp[i].first);
    }

    for (int i = 0; i < N; i++) {

        // If not already visited
        // then apply BFS
        if (!vis[i]) {
            queue<int> q;
            vector<int> v1;
            vector<int> v2;

            // Set visited to true
            vis[i] = true;

            // Push the node to the queue
            q.push(i);

            // While queue is not empty
            while (!q.empty()) {
                int u = q.front();
                v1.push_back(u);
                v2.push_back(a[u]);
                q.pop();

                // Check all the adjacent nodes
                for (auto s : v[u]) {

                    // If not visited
                    if (!vis[s]) {

                        // Set visited to true
                        vis[s] = true;
                        q.push(s);
                    }
                }
            }
            sort(v1.begin(), v1.end());
            sort(v2.begin(), v2.end());

            // If the connected component does not
            // contain same elements then return false
            if (v1 != v2)
                return false;
        }
    }
    return true;
}

// Driver code
int main()
{
    vector<int> a = { 0, 4, 3, 2, 1, 5 };
    int n = a.size();
    vector<pair<int, int> > vp = { { 1, 4 }, { 2, 3 } };
    int p = vp.size();

    if (canBeSorted(n, a, p, vp))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function that returns true if the array elements
  // can be sorted with the given operation
  static boolean canBeSorted(int N, ArrayList<Integer> a,
                             int p, ArrayList<ArrayList<Integer>> vp)
  {

    // To create the adjacency list of the graph
    ArrayList<ArrayList<Integer>> v = new ArrayList<ArrayList<Integer>>();
    for(int i = 0; i < N; i++)
    {
      v.add(new ArrayList<Integer>());
    }

    // Boolean array to mark the visited nodes
    boolean[] vis = new boolean[N];

    // Creating adjacency list for undirected graph
    for (int i = 0; i < p; i++)
    {
      v.get(vp.get(i).get(0)).add(vp.get(i).get(1));
      v.get(vp.get(i).get(1)).add(vp.get(i).get(0));
    }
    for (int i = 0; i < N; i++)
    {

      // If not already visited
      // then apply BFS
      if (!vis[i])
      {
        Queue<Integer> q = new LinkedList<>();
        ArrayList<Integer> v1 = new ArrayList<Integer>();
        ArrayList<Integer> v2 = new ArrayList<Integer>();

        // Set visited to true    
        vis[i] = true;

        // Push the node to the queue
        q.add(i);

        // While queue is not empty
        while (q.size() > 0)
        {
          int u = q.poll();
          v1.add(u);
          v2.add(a.get(u));

          // Check all the adjacent nodes
          for(int s: v.get(u))
          {

            // If not visited
            if (!vis[s])
            {

              // Set visited to true
              vis[s] = true;
              q.add(s);
            }
          }

        }
        Collections.sort(v1);
        Collections.sort(v2);

        // If the connected component does not
        // contain same elements then return false
        if(!v1.equals(v2))
        {
          return false;
        }
      }
    }
    return true;
  }

  // Driver code
  public static void main (String[] args)
  {
    ArrayList<Integer> a = new ArrayList<Integer>(Arrays.asList(0, 4, 3, 2, 1, 5));
    int n = a.size();
    ArrayList<ArrayList<Integer>> vp = new ArrayList<ArrayList<Integer>>();
    vp.add(new ArrayList<Integer>(Arrays.asList(1, 4)));
    vp.add(new ArrayList<Integer>(Arrays.asList(2, 3)));
    int p = vp.size();
    if (canBeSorted(n, a, p, vp))
    {
      System.out.println("Yes");   
    }
    else
    {
      System.out.println("No");
    }

  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import deque as queue

# Function that returns true if the array elements
# can be sorted with the given operation
def canBeSorted(N, a, P, vp):

    # To create the adjacency list of the graph
    v = [[] for i in range(N)]

    # Boolean array to mark the visited nodes
    vis = [False]*N

    # Creating adjacency list for undirected graph
    for i in range(P):
        v[vp[i][0]].append(vp[i][1])
        v[vp[i][1]].append(vp[i][0])

    for i in range(N):

        # If not already visited
        # then apply BFS
        if (not vis[i]):
            q = queue()
            v1 = []
            v2 = []

            # Set visited to true
            vis[i] = True

            # Push the node to the queue
            q.append(i)

            # While queue is not empty
            while (len(q) > 0):
                u = q.popleft()
                v1.append(u)
                v2.append(a[u])

                # Check all the adjacent nodes
                for s in v[u]:

                    # If not visited
                    if (not vis[s]):

                        # Set visited to true
                        vis[s] = True
                        q.append(s)

            v1 = sorted(v1)
            v2 = sorted(v2)

            # If the connected component does not
            # contain same elements then return false
            if (v1 != v2):
                return False
    return True

# Driver code
if __name__ == '__main__':
    a = [0, 4, 3, 2, 1, 5]
    n = len(a)
    vp = [ [ 1, 4 ], [ 2, 3 ] ]
    p = len(vp)

    if (canBeSorted(n, a, p, vp)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

    // Function that returns true if the array elements
   // can be sorted with the given operation
    function canBeSorted(N,a,p,vp)
    {
        // To create the adjacency list of the graph
    let v= [];
    for(let i = 0; i < N; i++)
    {
      v.push([]);
    }

    // Boolean array to mark the visited nodes
    let vis = new Array(N);

    // Creating adjacency list for undirected graph
    for (let i = 0; i < p; i++)
    {
      v[vp[i][0]].push(vp[i][1]);
      v[vp[i][1]].push(vp[i][0]);
    }
    for (let i = 0; i < N; i++)
    {

      // If not already visited
      // then apply BFS
      if (!vis[i])
      {
        let q = [];
        let v1 = [];
        let v2 = [];

        // Set visited to true   
        vis[i] = true;

        // Push the node to the queue
        q.push(i);

        // While queue is not empty
        while (q.length > 0)
        {
          let u = q.shift();
          v1.push(u);
          v2.push(a[u]);

          // Check all the adjacent nodes
          for(let s=0;s<v[u].length;s++)
          {

            // If not visited
            if (!vis[v[u][s]])
            {

              // Set visited to true
              vis[v[u][s]] = true;
              q.push(v[u][s]);
            }
          }

        }
        v1.sort(function(c,d){return c-d;});
        v2.sort(function(c,d){return c-d;});

        // If the connected component does not
        // contain same elements then return false
        if(v1.toString()!=(v2).toString())
        {
          return false;
        }
      }
    }
    return true;
    }

    // Driver code
    let a = [0, 4, 3, 2, 1, 5];
    let n = a.length;
    let vp = [];
    vp.push([1, 4]);
    vp.push([2, 3]);
    let p = vp.length;
    if (canBeSorted(n, a, p, vp))
    {
      document.write("Yes");  
    }
    else
    {
      document.write("No");
    }

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)