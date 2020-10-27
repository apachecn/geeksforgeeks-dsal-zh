# 查找所有矩阵元素，这些元素在其行中的最小值在其列中的最大值

给定大小为 **M * N** 的矩阵 **mat [] []** ，任务是找到所有矩阵元素，这些矩阵元素在其各自的行中最小，在其各自的列中最大。 如果不存在此类元素，则打印 **-1** 。

**示例**：

> **输入**：mat [] [] = {{1，10，4}，{9，3，8}，{15，16，17}}
> **输出**：15
> **说明**：
> 15 是唯一在其列{1，3， **15** }中最大而在其行{ **15 [** ，16、17}。
> 
> **输入**：m [] [] = {{10，41}，{3，5}，{16，2}}
> **输出**：-1

**方法**：请按照以下步骤解决问题：

1.  创建 [**无序集**](https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/) ，并存储矩阵每一行的[最小元素。](https://www.geeksforgeeks.org/minimum-element-of-each-row-and-each-column-in-a-matrix/)
2.  [遍历矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)并找到每列的**最大元素**。 对于每一列，检查获得的最大值是否已经存在于 [unordered_set](http://www.geeksforgeeks.org/unorderd_set-stl-uses/) 中。
3.  如果发现是真的，请打印该号码。 如果找不到这样的矩阵元素，则打印 **-1** 。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Functionto find all the matrix elements
// which are minimum in its row and maximum
// in its column
vector<int> minmaxNumbers(vector<vector<int> >& matrix,
                          vector<int>& res)
{

    // Initialize unordered set
    unordered_set<int> set;

    // Traverse the matrix
    for (int i = 0; i < matrix.size(); i++) {
        int minr = INT_MAX;
        for (int j = 0; j < matrix[i].size(); j++) {

            // Update the minimum
            // element of current row
            minr = min(minr, matrix[i][j]);
        }

        // Insert the minimum
        // element of the row
        set.insert(minr);
    }

    for (int j = 0; j < matrix[0].size(); j++) {
        int maxc = INT_MIN;

        for (int i = 0; i < matrix.size(); i++) {

            // Update the maximum
            // element of current column
            maxc = max(maxc, matrix[i][j]);
        }

        // Checking if it is already present
        // in the unordered_set or not
        if (set.find(maxc) != set.end()) {
            res.push_back(maxc);
        }
    }

    return res;
}

// Driver Code
int main()
{
    vector<vector<int> > mat
        = { { 1, 10, 4 }, 
            { 9, 3, 8 }, 
            { 15, 16, 17 } };

    vector<int> ans;

    // Function call
    minmaxNumbers(mat, ans);

    // If no such matrix
    // element is found
    if (ans.size() == 0)
        cout << "-1" << endl;

    for (int i = 0; i < ans.size(); i++)
        cout << ans[i] << endl;

    return 0;
}

```

## Java

```java

// Java program for the above approach
import java.util.*; 

class GFG{

// Functionto find all the matrix elements 
// which are minimum in its row and maximum 
// in its column 
public static Vector<Integer>minmaxNumbers(int[][] matrix,
              Vector<Integer> res)         
{ 

    // Initialize unordered set
    Set<Integer> set = new HashSet<Integer>(); 

    // Traverse the matrix 
    for(int i = 0; i < matrix.length; i++)
    { 
        int minr = Integer.MAX_VALUE; 
        for(int j = 0; j < matrix[i].length; j++)
        { 

            // Update the minimum 
            // element of current row 
            minr = Math.min(minr, matrix[i][j]); 
        } 

        // Insert the minimum 
        // element of the row 
        set.add(minr); 
    } 

    for(int j = 0; j < matrix[0].length; j++) 
    { 
        int maxc = Integer.MIN_VALUE; 
        for(int i = 0; i < matrix.length; i++)
        { 

            // Update the maximum 
            // element of current column 
            maxc = Math.max(maxc, matrix[i][j]); 
        } 

        // Checking if it is already present 
        // in the unordered_set or not 
        if (set.contains(maxc))
        { 
            res.add(maxc); 
        } 
    } 
    return res; 
} 

// Driver code
public static void main(String[] args) 
{
    int[][] mat = { { 1, 10, 4 },  
                    { 9, 3, 8 },  
                    { 15, 16, 17 } }; 

    Vector<Integer> ans = new Vector<Integer>(); 

    // Function call 
    ans = minmaxNumbers(mat, ans); 

    // If no such matrix 
    // element is found 
    if (ans.size() == 0) 
        System.out.println("-1");

    for(int i = 0; i < ans.size(); i++) 
        System.out.println(ans.get(i));
}
}

// This code is contributed by divyeshrabadiya07

```

## Python3

```py

# Python3 program for the above approach
import sys

# Functionto find all the matrix elements
# which are minimum in its row and maximum
# in its column
def minmaxNumbers(matrix, res):

    # Initialize unordered set
    s = set()

    # Traverse the matrix
    for i in range(0, len(matrix), 1):
        minr = sys.maxsize
        for j in range(0, len(matrix[i]), 1):

            # Update the minimum
            # element of current row
            minr = min(minr, matrix[i][j])

        # Insert the minimum
        # element of the row
        s.add(minr)

    for j in range(0, len(matrix[0]), 1):
        maxc = -sys.maxsize - 1

        for i in range(0, len(matrix), 1):

            # Update the maximum
            # element of current column
            maxc = max(maxc, matrix[i][j])

        # Checking if it is already present
        # in the unordered_set or not
        if (maxc in s):
            res.append(maxc)

    return res

# Driver Code
if __name__ == '__main__':

    mat = [ [ 1, 10, 4 ], 
            [ 9, 3, 8 ], 
            [ 15, 16, 17 ] ]

    ans = []

    # Function call
    minmaxNumbers(mat, ans)

    # If no such matrix
    # element is found
    if (len(ans) == 0):
        print("-1")

    for i in range(len(ans)):
        print(ans[i])

# This code is contributed by SURENDRA_GANGWAR

```

## C#

```cs

// C# program for 
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Functionto find all 
// the matrix elements 
// which are minimum 
// in its row and
//  maximum in its column 
public static List<int> minmaxNumbers(int[,] matrix, 
                                      List<int> res)         
{     
  // Initialize unordered set
  HashSet<int> set = new HashSet<int>(); 

  // Traverse the matrix 
  for(int i = 0; i < matrix.GetLength(0); i++)
  { 
    int minr = int.MaxValue; 
    for(int j = 0; j < matrix.GetLength(1); j++)
    { 
      // Update the minimum 
      // element of current row 
      minr = Math.Min(minr, matrix[i, j]); 
    } 

    // Insert the minimum 
    // element of the row 
    set.Add(minr); 
  } 

  for(int j = 0; j < matrix.GetLength(0); j++) 
  { 
    int maxc = int.MinValue; 
    for(int i = 0; i < matrix.GetLength(1); i++)
    { 
      // Update the maximum 
      // element of current column 
      maxc = Math.Max(maxc, matrix[i, j]); 
    } 

    // Checking if it is already present 
    // in the unordered_set or not 
    if (set.Contains(maxc))
    { 
      res.Add(maxc); 
    } 
  } 
  return res; 
} 

// Driver code
public static void Main(String[] args) 
{
  int[,] mat = {{1, 10, 4},  
                {9, 3, 8},  
                {15, 16, 17}}; 

  List<int> ans = new List<int>(); 

  // Function call 
  ans = minmaxNumbers(mat, ans); 

  // If no such matrix 
  // element is found 
  if (ans.Count == 0) 
    Console.WriteLine("-1");

  for(int i = 0; i < ans.Count; i++) 
    Console.WriteLine(ans[i]);
}
}

// This code is contributed by 29AjayKumar

```

**Output:** 

```
15

```

***时间复杂度**：O（M * N）*
***辅助空间**：O（M + N）*



* * *

* * *



