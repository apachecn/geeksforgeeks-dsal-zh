# 从给定的相邻元素对中生成一个数组

> 原文:[https://www . geeksforgeeks . org/从给定的相邻元素对生成数组/](https://www.geeksforgeeks.org/generate-an-array-from-given-pairs-of-adjacent-elements/)

给定一个由 **N** 对整数组成的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/) **arr[][]** ，每行中的两个元素表示它们是原始数组中的相邻元素。任务是用给定的相邻元素对**arr【】**构建一个数组。

**示例**

> **输入:** arr[] = {{5，1 }，{3，4 }，{3，5}}
> **输出:** 4 3 5 1
> **解释:**可以使用以下操作构建数组:
> 操作 1:元素 4 和 1 有一个邻居。因此，它们可以是原始数组中的第一个或最后一个元素。考虑到 4 是原始数组中的第一个元素， **A[]** = {4}。
> 操作 2:将 3 放在 4 的旁边。因此， **A[]** = {4，3}
> 操作 3:将 5 放置在 3 附近。因此， **A[]** = {4，3，5}。
> 操作 4:将 1 作为数组中的最后一个元素。因此， **A[]** = {4，3，5，1}。
> 
> **输入:** arr[] = {{8，11}，{-3，6}，{-3，8 } }
> T3】输出: 6 -3 8 11

**方法:**使用 [**哈希**](https://www.geeksforgeeks.org/hashing-data-structure/) 和 [**DFS**](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 可以解决问题。按照以下步骤解决问题:

1.  使用[地图](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)，比如**地图**初始化[邻接表](https://www.geeksforgeeks.org/graph-and-its-representations/)，以存储分配给每个元素的相邻元素。
2.  初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如说 **res** ，来存储数组中的原始元素。
3.  从角元素开始创建原始数组。因此，找到只有一个邻居的元素。这可以是原始阵列的第一个**元素**或最后一个**元素**。
4.  将获得的元素插入 **res** 。
5.  遍历邻接表中的每个元素，检查它的邻居是否被访问过。
6.  在向量 **res** 中插入未访问的邻居，并遍历该元素的所有邻居。重复**步骤 5** 直到访问完所有元素。
7.  返回**静止**。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to find original array
void find_original_array(vector<pair<int, int> >& A)
{

    // Map to store all neighbors for each element
    unordered_map<int, vector<int> > mp;

    // Vector to store original elements
    vector<int> res;

    // Stotrs which array elements are visited
    unordered_map<int, bool> visited;

    // Adjacency list to store neighbors
    // of each array element
    for (auto& it : A) {

        mp[it.first].push_back(it.second);
        mp[it.second].push_back(it.first);
    }

    auto it = mp.begin();

    // Find the first corner element
    for (; it != mp.end(); it++) {
        if (it->second.size() == 1) {
            break;
        }
    }

    // Stores first element of
    // the original array
    int adjacent = it->first;

    // Push it into the original array
    res.push_back(it->first);

    // Mark as visited
    visited[it->first] = true;

    // Traversing the neighbors and check
    // if the elements are visited or not
    while (res.size() != A.size() + 1) {

        // Traverse adjacent elements
        for (auto& elements : mp[adjacent]) {

            // If element is not visited
            if (!visited[elements]) {

                // Push it into res
                res.push_back(elements);

                // Mark as visited
                visited[elements] = true;

                // Update the next adjacent
                adjacent = elements;
            }
        }
    }

    // Print original array
    for (auto it : res) {
        cout << it << " ";
    }
}

// Driver Code
int main()
{

    // Given pairs of adjacent elements
    vector<pair<int, int> > A
        = { { 5, 1 }, { 3, 4 }, { 3, 5 } };

    find_original_array(A);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.io.*;
import java.util.*;

class Pair {
    int first, second;
    Pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

class GFG {
    // Utility function to find original array
    static void find_original_array(List<Pair> A)
    {

        // Map to store all neighbors for each element
        @SuppressWarnings("unchecked")
        Map<Integer, List<Integer> > mp = new HashMap();

        // Vector to store original elements
        List<Integer> res = new ArrayList<Integer>();

        // Stotrs which array elements are visited
        @SuppressWarnings("unchecked")
        Map<Integer, Boolean> visited = new HashMap();

        // Adjacency list to store neighbors
        // of each array element
        for (Pair it : A) {
            List<Integer> temp;
            temp = (mp.containsKey(it.first))
                       ? mp.get(it.first)
                       : new ArrayList<Integer>();
            temp.add(it.second);
            mp.put(it.first, temp);

            temp = (mp.containsKey(it.second))
                       ? mp.get(it.second)
                       : new ArrayList<Integer>();
            temp.add(it.first);
            mp.put(it.second, temp);
        }

        int it = 0;

        // Find the first corner element
        for (Map.Entry<Integer, List<Integer> > entry :
             mp.entrySet()) {
            if (entry.getValue().size() == 1) {
                it = entry.getKey();
            }
        }

        // Stores first element of
        // the original array
        int adjacent = it;

        // Push it into the original array
        res.add(it);

        // Mark as visited
        visited.put(it, true);

        // Traversing the neighbors and check
        // if the elements are visited or not
        while (res.size() != A.size() + 1) {

            // Traverse adjacent elements
            for (int elements : mp.get(adjacent)) {

                // If element is not visited
                if (!visited.containsKey(elements)) {

                    // Push it into res
                    res.add(elements);

                    // Mark as visited
                    visited.put(elements, true);

                    // Update the next adjacent
                    adjacent = elements;
                }
            }
        }

        // Print original array
        for (int val : res) {
            System.out.print(val + " ");
        }
    }
    // Driver Code
    public static void main(String[] args)
    {
        @SuppressWarnings("unchecked")
        List<Pair> A = new ArrayList();
        A.add(new Pair(5, 1));
        A.add(new Pair(3, 4));
        A.add(new Pair(3, 5));

        find_original_array(A);
    }
}

// This code is contributed by jithin.
```

## 蟒蛇 3

```
# Python3 program of the above approach

# Utility function to find original array
def find_original_array(A):

    # Map to store all neighbors for each element
    mp = [[] for i in range(6)]

    # Vector to store original elements
    res = []

    # Stotrs which array elements are visited
    visited = {}

    # A djacency list to store neighbors
    # of each array element
    for it in A:
        mp[it[0]].append(it[1])
        mp[it[1]].append(it[0])

    start = 0

    # Find the first corner element
    for it in range(6):
        if (len(mp[it]) == 1):
            start = it + 3
            break

    # Stores first element of
    # the original array  
    adjacent = start

    # Push it into the original array
    res.append(start)

    # Mark as visited
    visited[start] = True

    # Traversing the neighbors and check
    # if the elements are visited or not
    while (len(res) != len(A) + 1):

        # Traverse adjacent elements
        for elements in mp[adjacent]:

            # If element is not visited
            if (elements not in visited):

                # Push it into res
                res.append(elements)

                # Mark as visited
                visited[elements] = True

                # Update the next adjacent
                adjacent = elements

    # Print original array
    print(*res)

# Driver Code
if __name__ == '__main__':

    # Given pairs of adjacent elements
    A = [[5, 1],[ 3, 4],[ 3, 5]]

    find_original_array(A)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program of the above approach
using System;
using System.Collections.Generic;

public class Pair
{
  public int first, second;
  public Pair(int first, int second)
  {
    this.first = first;
    this.second = second;
  }
}

public class GFG
{

  // Utility function to find original array
  static void find_original_array(List<Pair> A)
  {

    // Map to store all neighbors for each element
    Dictionary<int,List<int>> mp = new Dictionary<int,List<int>>();

    // Vector to store original elements
    List<int> res = new List<int>();

    // Stotrs which array elements are visited
    Dictionary<int,bool> visited = new Dictionary<int,bool>();

    // Adjacency list to store neighbors
    // of each array element
    foreach (Pair it in A)
    {
      List<int> temp;
      temp = (mp.ContainsKey(it.first))
        ? mp[it.first]
        : new List<int>();

      temp.Add(it.second);
      if(!mp.ContainsKey(it.first))
        mp.Add(it.first, temp);
      else
        mp[it.first] = temp;

      temp = (mp.ContainsKey(it.second))
        ? mp[it.second]
        : new List<int>();
      temp.Add(it.first);
      if(!mp.ContainsKey(it.second))
        mp.Add(it.second, temp);
      else
        mp[it.second] = temp;

    }

    int It = 0;

    // Find the first corner element
    foreach (int key in mp.Keys)
    {
      if(mp[key].Count == 1)
      {
        It=key;
      }
    }

    // Stores first element of
    // the original array
    int adjacent = It;

    // Push it into the original array
    res.Add(It);

    // Mark as visited
    visited.Add(It, true);

    // Traversing the neighbors and check
    // if the elements are visited or not
    while (res.Count != A.Count + 1)
    {

      // Traverse adjacent elements
      foreach (int elements in mp[adjacent])
      {

        // If element is not visited
        if (!visited.ContainsKey(elements))
        {

          // Push it into res
          res.Add(elements);

          // Mark as visited
          visited.Add(elements, true);

          // Update the next adjacent
          adjacent = elements;
        }
      }
    }

    // Print original array
    foreach (int val in res)
    {
      Console.Write(val + " ");
    }
  }

  // Driver Code
  static public void Main (){
    List<Pair> A = new List<Pair>();
    A.Add(new Pair(5, 1));
    A.Add(new Pair(3, 4));
    A.Add(new Pair(3, 5));

    find_original_array(A);
  }
}

// This code is contributed by avanitrachhadiya2155
```

**Output:** 

```
4 3 5 1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*