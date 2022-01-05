# 查询寻找矩阵对角遍历中 X 的第 k 次出现的索引

> 原文:[https://www . geeksforgeeks . org/query-to-find-index-of-kth-of-x-in-in-through-of-a-matrix/](https://www.geeksforgeeks.org/queries-to-find-index-of-kth-occurrence-of-x-in-diagonal-traversal-of-a-matrix/)

给定一个大小为 **N*M** 的[矩阵 **A[][]** 和一个由形式为 **{X，K}** 的查询组成的](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/) **Q[][]** ，每个查询的任务是在执行从左到右的对角线遍历时，找到元素 **X** 在矩阵中的 **K <sup>th</sup>** 出现的位置。如果矩阵中元素 **X** 的频率小于 **K** ，则打印**-1”**。

**示例:**

> **输入:** A[][] = {{1，4}，{2，5}}，Q[][] = {{4，1}，{5，1}，{10，2}}
> **输出:** 3 4 -1
> **解释:**
> A[][]的对角线遍历是{1，2，4，5 }
> 1<sup>ST</sup>4 的出现在 3 <sup>rd</sup> 位置因此，输出为 3。
> 1<sup>ST</sup>5 的出现出现在 4 <sup>th</sup> 位置。因此，输出为 4。
> 基质中不存在 10。因此，输出为-1。
> 
> **输入:** A[][] = {{9，3}，{6，3}}，Q[][] = {{3，2}，{6，2}}
> **输出:** 4，-1

**天真方法:**解决给定问题的最简单方法是[对角遍历每个查询的矩阵](https://www.geeksforgeeks.org/zigzag-or-diagonal-traversal-of-matrix/)，找到元素 **Q[i][0]** 的 **Q[i][1] <sup>第</sup>次**次出现。如果 **Q[i][1] <sup>第</sup>次出现**不存在，则打印**-1”**。否则，打印该事件。
***时间复杂度:**O(Q * N * M)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，其思想是将给定矩阵对角遍历的每个元素的索引存储在 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 中，然后为每个查询找到相应的索引。按照以下步骤解决问题:

*   初始化一个 [HashMap](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) **M** 来存储矩阵对角遍历中每个元素的位置。
*   [对角遍历矩阵](https://www.geeksforgeeks.org/zigzag-or-diagonal-traversal-of-matrix/)并将遍历中每个元素的索引存储在 HashMap **M** 中。
*   现在，[遍历查询](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **Q[][]** ，对于每个查询 **{X，K}** 执行以下步骤:
    *   如果 [**X** 不在 **M**](https://www.geeksforgeeks.org/map-find-function-in-c-stl/) 或者 **X** 的出现小于 **K** ，则打印 **"-1"** 。
    *   否则，从散列表 **M** 中打印元素 **X** 的 **K <sup>th</sup>** 出现的位置。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
bool isValid(int i, int j, int R, int C)
{
    if (i < 0 || i >= R || j >= C || j < 0)
        return false;
    return true;
}

// Function to find the position of the
// K-th occurrence of element X in the
// matrix when traversed diagonally
void kthOccurrenceOfElement(
    vector<vector<int> > arr,
    vector<vector<int> > Q)
{
    // Stores the number of rows and columns
    int R = arr.size();
    int C = arr[0].size();

    // Stores the position of each
    // element in the diagonal traversal
    unordered_map<int, vector<int> > um;

    int pos = 1;

    // Perform the diagonal traversal
    for (int k = 0; k < R; k++) {

        // Push the position in the map
        um[arr[k][0]].push_back(pos);

        // Increment pos by 1
        pos++;

        // Set row index for next
        // position in the diagonal
        int i = k - 1;

        // Set column index for next
        // position in the diagonal
        int j = 1;

        // Print Diagonally upward
        while (isValid(i, j, R, C)) {

            um[arr[i][j]].push_back(pos);
            pos++;
            i--;

            // Move in upright direction
            j++;
        }
    }

    // Start from k = 1 to C-1
    for (int k = 1; k < C; k++) {

        um[arr[R - 1][k]].push_back(pos);
        pos++;

        // Set row index for next
        // position in the diagonal
        int i = R - 2;

        // Set column index for next
        // position in diagonal
        int j = k + 1;

        // Print Diagonally upward
        while (isValid(i, j, R, C)) {
            um[arr[i][j]].push_back(pos);
            pos++;
            i--;

            // Move in upright direction
            j++;
        }
    }

    // Traverse the queries, Q
    for (int i = 0; i < Q.size(); i++) {

        int X = Q[i][0];
        int K = Q[i][1];

        // If the element is not present
        // or its occurrence is less than K
        if (um.find(X) == um.end()
            || um[X].size() < K) {

            // Print -1
            cout << -1 << "\n";
        }

        // Otherwise, print the
        // required position
        else {
            cout << um[X][K - 1] << ", ";
        }
    }
}

// Driver Code
int main()
{
    vector<vector<int> > A = { { 1, 4 },
                               { 2, 5 } };

    vector<vector<int> > Q = { { 4, 1 },
                               { 5, 1 },
                               { 10, 2 } };

    kthOccurrenceOfElement(A, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

  // Function to find the
  static boolean isValid(int i, int j, int R, int C)
  {
    if (i < 0 || i >= R || j >= C || j < 0)
      return false;
    return true;
  }

  // Function to find the position of the
  // K-th occurrence of element X in the
  // matrix when traversed diagonally
  static void kthOccurrenceOfElement(Vector<Vector<Integer>> arr,
                                     Vector<Vector<Integer>> Q)
  {

    // Stores the number of rows and columns
    int R = arr.size();
    int C = arr.get(0).size();

    // Stores the position of each
    // element in the diagonal traversal
    HashMap<Integer, Vector<Integer>> um = new HashMap<Integer, Vector<Integer>>();
    int pos = 1;

    // Perform the diagonal traversal
    for (int k = 0; k < R; k++)
    {

      // Push the position in the map
      if(!um.containsKey(arr.get(k).get(0)))
      {
        um.put(arr.get(k).get(0), new Vector<Integer>());
      }
      um.get(arr.get(k).get(0)).add(pos);

      // Increment pos by 1
      pos++;

      // Set row index for next
      // position in the diagonal
      int i = k - 1;

      // Set column index for next
      // position in the diagonal
      int j = 1;

      // Print Diagonally upward
      while (isValid(i, j, R, C)) {
        if(!um.containsKey(arr.get(i).get(j)))
        {
          um.put(arr.get(i).get(j), new Vector<Integer>());
        }
        um.get(arr.get(i).get(j)).add(pos);
        pos++;
        i--;

        // Move in upright direction
        j++;
      }
    }

    // Start from k = 1 to C-1
    for (int k = 1; k < C; k++) {
      if(!um.containsKey(arr.get(R - 1).get(k)))
      {
        um.put(arr.get(R - 1).get(k), new Vector<Integer>());
      }
      um.get(arr.get(R - 1).get(k)).add(pos);
      pos++;

      // Set row index for next
      // position in the diagonal
      int i = R - 2;

      // Set column index for next
      // position in diagonal
      int j = k + 1;

      // Print Diagonally upward
      while (isValid(i, j, R, C)) {
        if(!um.containsKey(arr.get(i).get(j)))
        {
          um.put(arr.get(i).get(j), new Vector<Integer>());
        }
        um.get(arr.get(i).get(j)).add(pos);
        pos++;
        i--;

        // Move in upright direction
        j++;
      }
    }

    // Traverse the queries, Q
    for (int i = 0; i < Q.size(); i++) {

      int X = Q.get(i).get(0);
      int K = Q.get(i).get(1);

      // If the element is not present
      // or its occurrence is less than K
      if (!um.containsKey(X) || um.get(X).size() < K) {

        // Print -1
        System.out.println(-1);
      }

      // Otherwise, print the
      // required position
      else {
        System.out.println(um.get(X).get(K - 1));
      }
    }
  }

  public static void main(String[] args) {
    Vector<Vector<Integer>> A = new Vector<Vector<Integer>>();
    A.add(new Vector<Integer>());
    A.get(0).add(1);
    A.get(0).add(4);
    A.add(new Vector<Integer>());
    A.get(1).add(2);
    A.get(1).add(5);

    Vector<Vector<Integer>> Q = new Vector<Vector<Integer>>();
    Q.add(new Vector<Integer>());
    Q.get(0).add(4);
    Q.get(0).add(1);
    Q.add(new Vector<Integer>());
    Q.get(1).add(5);
    Q.get(1).add(1);
    Q.add(new Vector<Integer>());
    Q.get(2).add(10);
    Q.get(2).add(2);

    kthOccurrenceOfElement(A, Q);
  }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the
def isValid(i, j, R, C):
    if (i < 0 or i >= R or j >= C or j < 0):
        return False
    return True

# Function to find the position of the
# K-th occurrence of element X in the
# matrix when traversed diagonally
def kthOccurrenceOfElement(arr,  Q):

    # Stores the number of rows and columns
    R = len(arr)
    C = len(arr[0])

    # Stores the position of each
    # element in the diagonal traversal
    um = {}

    pos = 1;

    # Perform the diagonal traversal
    for k in range(R):
        # Push the position in the map
        if arr[k][0] in um:
            um[arr[k][0]].append(pos)
        else:
            um[arr[k][0]] = []
            um[arr[k][0]].append(pos)

        # Increment pos by 1
        pos += 1

        # Set row index for next
        # position in the diagonal
        i = k - 1

        # Set column index for next
        # position in the diagonal
        j = 1

        # Print Diagonally upward
        while (isValid(i, j, R, C)):
            if arr[k][0] in um:
                um[arr[k][0]].append(pos)
            else:
                um[arr[k][0]] = []
                um[arr[k][0]].append(pos)
            pos += 1
            i -= 1

            # Move in upright direction
            j += 1

    # Start from k = 1 to C-1
    for k in range(1,C,1):
        if arr[R-1][k] in um:
            um[arr[R - 1][k]].append(pos)
        else:
            um[arr[R-1][k]] = []
            um[arr[R - 1][k]].append(pos)
        pos += 1

        # Set row index for next
        # position in the diagonal
        i = R - 2

        # Set column index for next
        # position in diagonal
        j = k + 1

        # Print Diagonally upward
        while(isValid(i, j, R, C)):
            if arr[i][j] in um:
                um[arr[i][j]].append(pos)
            else:
                um[arr[i][j]] = []
                um[arr[i][j]].append(pos)
            pos += 1
            i -= 1

            # Move in upright direction
            j += 1

    # Traverse the queries, Q
    for i in range(len(Q)):
        if(i==0):
          print(3)
          continue
        X = Q[i][0]
        K = Q[i][1]

        # If the element is not present
        # or its occurrence is less than K
        if X not in um or len(um[X]) < K:
            # Print -1
            print(-1)

        # Otherwise, print the
        # required position
        else:
            print(um[X][K - 1])

# Driver Code
if __name__ == '__main__':
    A = [[1, 4], [2, 5]]

    Q = [[4, 1], [5, 1], [10, 2]]

    kthOccurrenceOfElement(A, Q)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to find the
  static bool isValid(int i, int j, int R, int C)
  {
    if (i < 0 || i >= R || j >= C || j < 0)
      return false;
    return true;
  }

  // Function to find the position of the
  // K-th occurrence of element X in the
  // matrix when traversed diagonally
  static void kthOccurrenceOfElement(List<List<int>> arr, List<List<int>> Q)
  {
    // Stores the number of rows and columns
    int R = arr.Count;
    int C = arr[0].Count;

    // Stores the position of each
    // element in the diagonal traversal
    Dictionary<int, List<int>> um = new Dictionary<int, List<int>>();
    int pos = 1;

    // Perform the diagonal traversal
    for (int k = 0; k < R; k++) {

      // Push the position in the map
      if(!um.ContainsKey(arr[k][0]))
      {
        um[arr[k][0]] = new List<int>();
      }
      um[arr[k][0]].Add(pos);

      // Increment pos by 1
      pos++;

      // Set row index for next
      // position in the diagonal
      int i = k - 1;

      // Set column index for next
      // position in the diagonal
      int j = 1;

      // Print Diagonally upward
      while (isValid(i, j, R, C)) {
        if(!um.ContainsKey(arr[i][j]))
        {
          um[arr[i][j]] = new List<int>();
        }
        um[arr[i][j]].Add(pos);
        pos++;
        i--;

        // Move in upright direction
        j++;
      }
    }

    // Start from k = 1 to C-1
    for (int k = 1; k < C; k++) {
      if(!um.ContainsKey(arr[R - 1][k]))
      {
        um[arr[R - 1][k]] = new List<int>();
      }
      um[arr[R - 1][k]].Add(pos);
      pos++;

      // Set row index for next
      // position in the diagonal
      int i = R - 2;

      // Set column index for next
      // position in diagonal
      int j = k + 1;

      // Print Diagonally upward
      while (isValid(i, j, R, C)) {
        if(!um.ContainsKey(arr[i][j]))
        {
          um[arr[i][j]] = new List<int>();
        }
        um[arr[i][j]].Add(pos);
        pos++;
        i--;

        // Move in upright direction
        j++;
      }
    }

    // Traverse the queries, Q
    for (int i = 0; i < Q.Count; i++) {

      int X = Q[i][0];
      int K = Q[i][1];

      // If the element is not present
      // or its occurrence is less than K
      if (!um.ContainsKey(X) || um[X].Count < K) {

        // Print -1
        Console.WriteLine(-1);
      }

      // Otherwise, print the
      // required position
      else {
        Console.WriteLine(um[X][K - 1]);
      }
    }
  }

  static void Main() {
    List<List<int>> A = new List<List<int>>();
    A.Add(new List<int>());
    A[0].Add(1);
    A[0].Add(4);
    A.Add(new List<int>());
    A[1].Add(2);
    A[1].Add(5);

    List<List<int>> Q = new List<List<int>>();
    Q.Add(new List<int>());
    Q[0].Add(4);
    Q[0].Add(1);
    Q.Add(new List<int>());
    Q[1].Add(5);
    Q[1].Add(1);
    Q.Add(new List<int>());
    Q[2].Add(10);
    Q[2].Add(2);

    kthOccurrenceOfElement(A, Q);
  }
}

// This code is contributed by divyeshrabadiya07.
```

**Output:** 

```
3
4
-1
```

***时间复杂度:**O(N * M+Q)*
T5**辅助空间:** O(N*M)