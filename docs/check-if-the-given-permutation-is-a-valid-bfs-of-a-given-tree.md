# 检查给定的排列是否是给定树的有效 BFS

> 原文:[https://www . geesforgeks . org/check-如果给定置换是给定树的有效 bfs/](https://www.geeksforgeeks.org/check-if-the-given-permutation-is-a-valid-bfs-of-a-given-tree/)

给定一棵树，其节点编号为从 **1 到 N** 以及从 **1 到 N** 的编号排列。通过在给定的树上应用 [BFS(广度优先遍历)](https://www.geeksforgeeks.org/bfs-vs-dfs-binary-tree/)，检查是否有可能获得给定的置换数组。
**注意:**遍历永远从 1 开始。
**示例:**

> **输入:** arr[] = { 1 5 2 3 4 6 }
> 给定树的边:
> 1–2
> 1–5
> 2–3
> 2–4
> 5–6
> T9】输出:否
> **解释:**
> 不存在与给定排列相同的遍历。有效的遍历是:
> 1 2 5 3 4 6
> 1 2 5 4 3 6
> 1 5 2 6 3 4
> 1 5 2 6 4 3
> T20】输入: arr[] = { 1 2 3 }
> 给定树的边:
> 1–2
> 2–3
> **输出:**是
> **解释:**
> 给定的排列是

**方法:**要解决上述问题，我们必须遵循以下步骤:

*   在 BFS，我们访问当前节点的所有邻居，并按顺序将他们的孩子推入[](https://www.geeksforgeeks.org/queue-data-structure/)**队列中，并重复此过程，直到队列不为空。**
*   **假设根的**有两个孩子**:A 和 b，我们可以自由选择先去拜访他们中的哪一个。假设我们先访问 A，但是现在我们将不得不把 A 的孩子推到队列中，并且我们不能在 A 之前访问 B 的孩子。**
*   **因此，基本上我们可以以任何顺序访问特定节点的子节点，但是应该访问两个不同节点的子节点的顺序是固定的，即如果 A 在 B 之前被访问，那么 A 的所有子节点应该在 B 的所有子节点之前被访问**
*   **我们也会这样做。我们将**组成一个集合**的队列，在每个集合中，我们将推特定节点的子节点，并沿着排列进行遍历。如果在队列顶部的集合中找到**排列的当前元素**，那么我们将继续，否则我们将返回 false。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ implementation to check if the
// given permutation is a valid
// BFS of a given tree
#include <bits/stdc++.h>
using namespace std;

// map for storing the tree
map<int, vector<int> > tree;

// map for marking
// the nodes visited
map<int, int> vis;

// Function to check if
// permutation is valid
bool valid_bfs(vector<int>& v)
{
    int n = (int)v.size();
    queue<set<int> > q;
    set<int> s;
    s.insert(1);

    /*inserting the root in
     the front of queue.*/
    q.push(s);
    int i = 0;

    while (!q.empty() && i < n)
    {

        // If the current node
        // in a permutation
        // is already visited
        // then return false
        if (vis.count(v[i]))
        {
            return 0;
        }
        vis[v[i]] = 1;

        // if all the children of previous
        // nodes are visited then pop the
        // front element of queue.
        if (q.front().size() == 0)
        {
            q.pop();
        }

        // if the current element of the
        // permutation is not found
        // in the set at the top of queue
        // then return false
        if (q.front().find(v[i])
            == q.front().end()) {
            return 0;
        }
        s.clear();

        // push all the children of current
        // node in a set and then push
        // the set in the queue.
        for (auto j : tree[v[i]]) {
            if (vis.count(j)) {
                continue;
            }
            s.insert(j);
        }
        if (s.size() > 0) {
            set<int> temp = s;
            q.push(temp);
        }
        s.clear();

        // erase the current node from
        // the set at the top of queue
        q.front().erase(v[i]);

        // increment the index
        // of permutation
        i++;
    }

    return 1;
}

// Driver code
int main()
{
    tree[1].push_back(2);
    tree[2].push_back(1);
    tree[1].push_back(5);
    tree[5].push_back(1);
    tree[2].push_back(3);
    tree[3].push_back(2);
    tree[2].push_back(4);
    tree[4].push_back(2);
    tree[5].push_back(6);
    tree[6].push_back(5);

    vector<int> arr
        = { 1, 5, 2, 3, 4, 6 };

    if (valid_bfs(arr))
        cout << "Yes" << endl;

    else
        cout << "No" << endl;

    return 0;
}

// This code is contributed by rutvik_56
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation to check if the
// given permutation is a valid
// BFS of a given tree
import java.util.*;
class GFG{

// Map for storing the tree
static HashMap<Integer,
       Vector<Integer> > tree =
                         new HashMap<>();

// Map for marking
// the nodes visited
static HashMap<Integer,
               Integer> vis =
                        new HashMap<>();

// Function to check if
// permutation is valid
static boolean valid_bfs(List<Integer> v)
{
  int n = (int)v.size();
  Queue<HashSet<Integer> > q =
                new LinkedList<>();
  HashSet<Integer> s = new HashSet<>();
  s.add(1);

  // Inserting the root in
  // the front of queue.
  q.add(s);
  int i = 0;

  while (!q.isEmpty() && i < n)
  {
    // If the current node
    // in a permutation
    // is already visited
    // then return false
    if (vis.containsKey(v.get(i)))
    {
      return false;
    }

    vis.put(v.get(i), 1);

    // If all the children of previous
    // nodes are visited then pop the
    // front element of queue.
    if (q.peek().size() == 0)
    {
      q.remove();
    }

    // If the current element of the
    // permutation is not found
    // in the set at the top of queue
    // then return false
    if (!q.peek().contains(v.get(i)))
    {
      return false;
    }
    s.clear();

    // Push all the children of current
    // node in a set and then push
    // the set in the queue.
    for (int j : tree.get(v.get(i)))
    {
      if (vis.containsKey(j))
      {
        continue;
      }
      s.add(j);
    }
    if (s.size() > 0)
    {
      HashSet<Integer> temp = s;
      q.add(temp);
    }
    s.clear();

    // Erase the current node from
    // the set at the top of queue
    q.peek().remove(v.get(i));

    // Increment the index
    // of permutation
    i++;
  }
  return true;
}

// Driver code
public static void main(String[] args)
{
  for (int i = 1; i <= 6; i++)
  {
    tree.put(i, new Vector<Integer>());
  }

  tree.get(1).add(2);
  tree.get(2).add(1);
  tree.get(1).add(5);
  tree.get(5).add(1);
  tree.get(2).add(3);
  tree.get(3).add(2);
  tree.get(2).add(4);
  tree.get(4).add(2);
  tree.get(5).add(6);
  tree.get(6).add(5);

  Integer []arr1 = {1, 5, 2, 3, 4, 6};
  List<Integer> arr = Arrays.asList(arr1);

  if (valid_bfs(arr))
    System.out.print("Yes" + "\n");
  else
    System.out.print("No" + "\n");
}
}

// This code is contributed by Princi Singh
```

## **蟒蛇 3**

```
# Python3 implementation to check if the
# given permutation is a valid
# BFS of a given tree

# map for storing the tree
tree=dict()

# map for marking
# the nodes visited
vis=dict()

# Function to check if
# permutation is valid
def valid_bfs( v):

    n = len(v)

    q=[]
    s=set()
    s.add(1);

    '''inserting the root in
     the front of queue.'''
    q.append(s);
    i = 0;

    while (len(q)!=0 and i < n):

        # If the current node
        # in a permutation
        # is already visited
        # then return false
        if (v[i] in vis):
            return 0;

        vis[v[i]] = 1;

        # if all the children of previous
        # nodes are visited then pop the
        # front element of queue.
        if (len(q[0])== 0):
            q.pop(0);

        # if the current element of the
        # permutation is not found
        # in the set at the top of queue
        # then return false
        if (v[i] not in q[0]):
            return 0;

        s.clear();

        # append all the children of current
        # node in a set and then append
        # the set in the queue.
        for j in tree[v[i]]:

            if (j in vis):
                continue;

            s.add(j);

        if (len(s) > 0):

            temp = s;
            q.append(temp);

        s.clear();

        # erase the current node from
        # the set at the top of queue
        q[0].discard(v[i]);

        # increment the index
        # of permutation
        i+=1

    return 1;

# Driver code
if __name__=="__main__":

    tree[1]=[]
    tree[2]=[]
    tree[5]=[]
    tree[3]=[]
    tree[2]=[]
    tree[4]=[]
    tree[6]=[]
    tree[1].append(2);
    tree[2].append(1);
    tree[1].append(5);
    tree[5].append(1);
    tree[2].append(3);
    tree[3].append(2);
    tree[2].append(4);
    tree[4].append(2);
    tree[5].append(6);
    tree[6].append(5);

    arr = [ 1, 5, 2, 3, 4, 6 ]

    if (valid_bfs(arr)):
        print("Yes")
    else:
        print("No")
```

## **C#**

```
// C# implementation to check
// if the given permutation
// is a valid BFS of a given tree
using System;
using System.Collections.Generic;
class GFG{

// Map for storing the tree
static Dictionary<int,
       List<int>> tree = new Dictionary<int,
                              List<int>>();

// Map for marking
// the nodes visited
static Dictionary<int,
                  int> vis = new Dictionary<int,
                                            int>();

// Function to check if
// permutation is valid
static bool valid_bfs(List<int> v)
{
  int n = (int)v.Count;
  Queue<HashSet<int>> q =
        new Queue<HashSet<int>>();
  HashSet<int> s = new HashSet<int>();
  s.Add(1);

  // Inserting the root in
  // the front of queue.
  q.Enqueue(s);
  int i = 0;

  while (q.Count != 0 && i < n)
  {
    // If the current node
    // in a permutation
    // is already visited
    // then return false
    if (vis.ContainsKey(v[i]))
    {
      return false;
    }

    vis.Add(v[i], 1);

    // If all the children of previous
    // nodes are visited then pop the
    // front element of queue.
    if (q.Peek().Count == 0)
    {
      q.Dequeue();
    }

    // If the current element of the
    // permutation is not found
    // in the set at the top of queue
    // then return false
    if (!q.Peek().Contains(v[i]))
    {
      return false;
    }

    s.Clear();

    // Push all the children of current
    // node in a set and then push
    // the set in the queue.
    foreach (int j in tree[v[i]])
    {
      if (vis.ContainsKey(j))
      {
        continue;
      }
      s.Add(j);
    }
    if (s.Count > 0)
    {
      HashSet<int> temp = s;
      q.Enqueue(temp);
    }
    s.Clear();

    // Erase the current node from
    // the set at the top of queue
    q.Peek().Remove(v[i]);

    // Increment the index
    // of permutation
    i++;
  }
  return true;
}

// Driver code
public static void Main(String[] args)
{
  for (int i = 1; i <= 6; i++)
  {
    tree.Add(i, new List<int>());
  }

  tree[1].Add(2);
  tree[2].Add(1);
  tree[1].Add(5);
  tree[5].Add(1);
  tree[2].Add(3);
  tree[3].Add(2);
  tree[2].Add(4);
  tree[4].Add(2);
  tree[5].Add(6);
  tree[6].Add(5);

  int []arr1 = {1, 5, 2, 3, 4, 6};
  List<int> arr = new List<int>();
  arr.AddRange(arr1);

  if (valid_bfs(arr))
    Console.Write("Yes" + "\n");
  else
    Console.Write("No" + "\n");
}
}

// This code is contributed by Princi Singh
```

## **java 描述语言**

```
<script>
    // Javascript implementation to check if the
    // given permutation is a valid
    // BFS of a given tree

    // Map for storing the tree
    let tree = new Map();

    // Map for marking
    // the nodes visited
    let vis = new Map();

    // Function to check if
    // permutation is valid
    function valid_bfs(v)
    {
      let n = v.length;
      let q = [];
      let s = new Set();
      s.add(1);

      // Inserting the root in
      // the front of queue.
      q.push(s);
      let i = 0;

      while (q.length > 0 && i < n)
      {
        // If the current node
        // in a permutation
        // is already visited
        // then return false
        if (vis.has(v[i]))
        {
          return false;
        }

        vis.set(v[i], 1);

        // If all the children of previous
        // nodes are visited then pop the
        // front element of queue.
        if (q[0].length == 0)
        {
          q.shift();
        }

        // If the current element of the
        // permutation is not found
        // in the set at the top of queue
        // then return false
        if (!q[0].has(v[i]))
        {
          return false;
        }
        s.clear();

        // Push all the children of current
        // node in a set and then push
        // the set in the queue.
        for (let j = 0; j < (tree.get(v[i])).length; j++)
        {
          if (vis.has((tree.get(v[i]))[j]))
          {
            continue;
          }
          s.add((tree.get(v[i]))[j]);
        }
        if (s.size > 0)
        {
          let temp = s;
          q.push(temp);
        }
        s.clear();

        // Erase the current node from
        // the set at the top of queue
        q[0].delete(v[i]);

        // Increment the index
        // of permutation
        i++;
      }
      return true;
    }

    for (let i = 1; i <= 6; i++)
    {
      tree.set(i, []);
    }

    tree.get(1).push(2);
    tree.get(2).push(1);
    tree.get(1).push(5);
    tree.get(5).push(1);
    tree.get(2).push(3);
    tree.get(3).push(2);
    tree.get(2).push(4);
    tree.get(4).push(2);
    tree.get(5).push(6);
    tree.get(6).push(5);

    let arr1 = [1, 5, 2, 3, 4, 6];
    let arr = arr1;

    if (valid_bfs(arr))
      document.write("Yes");
    else
      document.write("No");

  // This code is contributed by divyeshrabadiya07.
</script>
```

****Output:** 

```
No
```** 

*****时间复杂度:**O(N * log N)*
T5】类似文章: [检查给定的排列是否是图的有效 DFS](https://www.geeksforgeeks.org/check-given-permutation-valid-dfs-graph/)**