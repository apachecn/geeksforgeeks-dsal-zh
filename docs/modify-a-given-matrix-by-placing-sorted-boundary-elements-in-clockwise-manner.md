# 通过顺时针放置排序的边界元素修改给定矩阵

> 原文:[https://www . geesforgeks . org/modify-a-给定矩阵-按放置-排序-边界-元素-以顺时针方式/](https://www.geeksforgeeks.org/modify-a-given-matrix-by-placing-sorted-boundary-elements-in-clockwise-manner/)

给定一个正方形[矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**A[][]****N * N，**的任务是从最外面到最里面的边界开始对矩阵的边界元素进行排序，并以顺时针方式放置它们。

**示例:**

> **输入:** A[][] = {{9，7，4，5}，{1，6，2，-6}，{12，20，2，0}，{-5，-6，7，-2}}
> **输出:**{-6，-6，-5，-2}，{12，2，2，0}，{9，20，6，1}，{7，7，5，4}}
> 解释:
> 最外边界
> 边界元素的排序顺序为{-6，-6，-5，-2，0，1，4，5，7，7，9，12}。
> 将这些排序后的元素序列以顺时针方式放回矩阵中，从左上角开始将 A[][]修改为{{-6，-6，-5，-2}，{12，6，2，0}，{9，20，2，1}，{7，7，5，4}}
> 下一级边界元素为{6，2，2，20}。
> 这些元素的排序顺序为{2，2，6，20}。
> 将这些排序后的元素序列以顺时针方式放回到矩阵中，从左上角开始将 A[][]修改为{{-6，-6，-5，-2}，{12，2，2，0}，{9，20，6，1}，{7，7，5，4}}
> 
> **输入:** A[][] = {{4，3，}，{1，2}}
> **输出:** {{1，2，}，{4，3}}

**方法:**思路是利用[边界变量获取当前边界元素](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/)并存储在数组中。然后，[按升序对数组进行排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)并将排序后的元素按顺时针方向放回矩阵中。
按照以下步骤解决问题:

*   初始化变量，比如 **k，m，l** ，和 **n** ，代表起始行索引，终止行索引，起始列索引和终止列索引。
*   迭代直到所有的循环方块都被访问。
    *   在每次外循环遍历中，以顺时针方式将正方形的元素存储在一个数组中，比如 **V** 。
    *   按下 **V** 中的顶行，即将 **k <sup>第</sup>T5】行的元素从列索引 **l** 推至 **n** 。增加 **k** 的计数。**
    *   按下 **V** 中的右栏，即将**n–1<sup>第</sup>T5】栏的元素从行索引 **k** 推到 **m** 。减少 **n** 的计数。**
    *   推下一行，即如果 **k < m** ，则将 **m-1 <sup>第</sup>T5】行的元素从列索引**n–1**推至 **l** 。减少 **m** 的计数。**
    *   推左列，即如果 **l < n** ，则从行索引**m–1**到 **k** 推第 **l <sup>第</sup>T5】列的元素。增加 **l** 的计数。**
    *   [按照升序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对数组 **V** 进行排序。
    *   重复上述步骤，用从**到**的排序元素更新矩阵的元素。
*   完成矩阵遍历后，打印修改后的矩阵 **A** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the elements
// of the matrix in row-wise manner
void printMatrix(vector<vector<int> > a)
{
    for (auto x : a) {
        for (auto y : x) {
            cout << y << " ";
        }
        cout << "\n";
    }
}

// Function to sort boundary elements
// of a matrix starting from the outermost
// to the innermost boundary and place them
// in a clockwise manner
void sortBoundaryWise(vector<vector<int> > a)
{
    /*  k - starting row index
        m - ending row index
        l - starting column index
        n - ending column index
        i - iterator
      */
    int i, k = 0, l = 0;
    int m = a.size(), n = a[0].size();
    int n_i, n_k = 0, n_l = 0, n_m = m, n_n = n;

    while (k < m && l < n) {

        // Stores the current
        // boundary elements
        vector<int> boundary;

        // Push the first row
        for (i = l; i < n; ++i) {
            boundary.push_back(a[k][i]);
        }
        k++;

        // Push the last column
        for (i = k; i < m; ++i) {
            boundary.push_back(a[i][n - 1]);
        }
        n--;

        // Push the last row
        if (k < m) {
            for (i = n - 1; i >= l; --i) {
                boundary.push_back(a[m - 1][i]);
            }
            m--;
        }

        // Push the first column
        if (l < n) {
            for (i = m - 1; i >= k; --i) {
                boundary.push_back(a[i][l]);
            }
            l++;
        }

        // Sort the boundary elements
        sort(boundary.begin(), boundary.end());
        int ind = 0;

        // Update the current boundary
        // with sorted elements

        // Update the first row
        for (i = n_l; i < n_n; ++i) {
            a[n_k][i] = boundary[ind++];
        }
        n_k++;

        // Update the last column
        for (i = n_k; i < n_m; ++i) {
            a[i][n_n - 1] = boundary[ind++];
        }
        n_n--;

        // Update the last row
        if (n_k < n_m) {
            for (i = n_n - 1; i >= n_l; --i) {
                a[n_m - 1][i] = boundary[ind++];
            }
            n_m--;
        }

        // Update the first column
        if (n_l < n_n) {
            for (i = n_m - 1; i >= n_k; --i) {
                a[i][n_l] = boundary[ind++];
            }
            n_l++;
        }
    }

    // Print the resultant matrix
    printMatrix(a);
}

// Driver Code
int main()
{
    // Given matrix
    vector<vector<int> > matrix = { { 9, 7, 4, 5 },
                                    { 1, 6, 2, -6 },
                                    { 12, 20, 2, 0 },
                                    { -5, -6, 7, -2 } };

    sortBoundaryWise(matrix);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print the elements
// of the matrix in row-wise manner
static void printMatrix(ArrayList<ArrayList<Integer>> a)
{
    for(int i = 0; i < a.size(); i++)
    {
        for(int j = 0; j < a.get(i).size(); j++)
        {
            System.out.print(a.get(i).get(j) + " ");
        }
        System.out.println();
    }
}

// Function to sort boundary elements
// of a matrix starting from the outermost
// to the innermost boundary and place them
// in a clockwise manner
static void sortBoundaryWise(ArrayList<ArrayList<Integer>> a)
{
    /*  k - starting row index
        m - ending row index
        l - starting column index
        n - ending column index
        i - iterator
      */
    int i, k = 0, l = 0;
    int m = a.size(), n = a.get(0).size();
    int n_i, n_k = 0, n_l = 0, n_m = m, n_n = n;

    while (k < m && l < n)
    {

        // Stores the current
        // boundary elements
        ArrayList<Integer> boundary = new ArrayList<Integer>();

        // Push the first row
        for(i = l; i < n; ++i)
        {
            boundary.add(a.get(k).get(i));
        }
        k++;

        // Push the last column
        for(i = k; i < m; ++i)
        {
            boundary.add(a.get(i).get(n - 1));
        }
        n--;

        // Push the last row
        if (k < m)
        {
            for(i = n - 1; i >= l; --i)
            {
                boundary.add(a.get(m - 1).get(i));
            }
            m--;
        }

        // Push the first column
        if (l < n)
        {
            for(i = m - 1; i >= k; --i)
            {
                boundary.add(a.get(i).get(l));
            }
            l++;
        }

        // Sort the boundary elements
        Collections.sort(boundary);  
        int ind = 0;

        // Update the current boundary
        // with sorted elements

        // Update the first row
        for(i = n_l; i < n_n; ++i)
        {
            a.get(n_k).set(i, boundary.get(ind));
            ind++;
        }
        n_k += 1;

        // Update the last column
        for(i = n_k; i < n_m; ++i)
        {
            a.get(i).set(n_n - 1, boundary.get(ind));
             ind++;
        }
        n_n--;

        // Update the last row
        if (n_k < n_m)
        {
            for(i = n_n - 1; i >= n_l; --i)
            {
                a.get(n_m - 1).set(i, boundary.get(ind));
                ind++;
            }
            n_m--;
        }

        // Update the first column
        if (n_l < n_n)
        {
            for(i = n_m - 1; i >= n_k; --i)
            {
                a.get(i).set(n_l, boundary.get(ind));
                ind++;
            }
            n_l++;
        }
    }

    // Print the resultant matrix
    printMatrix(a);
}

// Driver Code
public static void main(String args[])
{

    // Given matrix
    ArrayList<
    ArrayList<Integer>> matrix = new ArrayList<
                                     ArrayList<Integer>>();
    ArrayList<Integer> list1 = new ArrayList<Integer>(
        Arrays.asList(9, 7, 4, 5));
    ArrayList<Integer> list2 = new ArrayList<Integer>(
        Arrays.asList(1, 6, 2, -6));
    ArrayList<Integer> list3 = new ArrayList<Integer>(
        Arrays.asList(12, 20, 2, 0));
    ArrayList<Integer> list4 = new ArrayList<Integer>(
        Arrays.asList(-5, -6, 7, -2));

    matrix.add(list1);
    matrix.add(list2);
    matrix.add(list3);
    matrix.add(list4);

    sortBoundaryWise(matrix);
}
}

// This code is contributed by ipg2016107
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the elements
# of the matrix in row-wise manner
def printMatrix(a):
    for x in a:
        for y in x:
            print(y, end = " ")

        print()

# Function to sort boundary elements
# of a matrix starting from the outermost
# to the innermost boundary and place them
# in a clockwise manner
def sortBoundaryWise(a):

    '''  k - starting row index
        m - ending row index
        l - starting column index
        n - ending column index
        i - iterator
      '''
    k = 0
    l = 0
    m = len(a)
    n = len(a[0])
    n_k = 0
    n_l = 0
    n_m = m
    n_n = n

    while (k < m and l < n):

        # Stores the current
        # boundary elements
        boundary = []

        # Push the first row
        for i in range(l, n):
            boundary.append(a[k][i])
        k += 1

        # Push the last column
        for i in range(k, m):
            boundary.append(a[i][n - 1])
        n -= 1

        # Push the last row
        if (k < m):
            for i in range(n - 1,  l - 1, -1):
                boundary.append(a[m - 1][i])
            m -= 1

        # Push the first column
        if (l < n):
            for i in range(m - 1, k - 1, -1):
                boundary.append(a[i][l])
            l += 1

        # Sort the boundary elements
        boundary.sort()
        ind = 0

        # Update the current boundary
        # with sorted elements

        # Update the first row
        for i in range(n_l, n_n):
            a[n_k][i] = boundary[ind]
            ind += 1

        n_k += 1

        # Update the last column
        for i in range(n_k, n_m):
            a[i][n_n - 1] = boundary[ind]
            ind += 1
        n_n -= 1

        # Update the last row
        if (n_k < n_m):
            for i in range(n_n - 1, n_l - 1, -1):
                a[n_m - 1][i] = boundary[ind]
                ind += 1

            n_m -= 1

        # Update the first column
        if (n_l < n_n):
            for i in range(n_m - 1, n_k - 1, -1):
                a[i][n_l] = boundary[ind]
                ind += 1
            n_l += 1

    # Print the resultant matrix
    printMatrix(a)

# Driver Code
if __name__ == "__main__":

    # Given matrix
    matrix = [[9, 7, 4, 5],
              [1, 6, 2, -6],
              [12, 20, 2, 0],
              [-5, -6, 7, -2]]

    sortBoundaryWise(matrix)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

  // Function to print the elements
  // of the matrix in row-wise manner
  static void printMatrix(List<List<int>> a)
  {
    foreach(List<int> x in a) {
      foreach(int y in x) {
        Console.Write(y + " ");
      }
      Console.WriteLine();
    }
  }

  // Function to sort boundary elements
  // of a matrix starting from the outermost
  // to the innermost boundary and place them
  // in a clockwise manner
  static void sortBoundaryWise(List<List<int>> a)
  {
    /*  k - starting row index
            m - ending row index
            l - starting column index
            n - ending column index
            i - iterator
          */
    int i, k = 0, l = 0;
    int m = a.Count, n = a[0].Count;
    int n_k = 0, n_l = 0, n_m = m, n_n = n;

    while (k < m && l < n) {

      // Stores the current
      // boundary elements
      List<int> boundary = new List<int>();

      // Push the first row
      for (i = l; i < n; ++i) {
        boundary.Add(a[k][i]);
      }
      k++;

      // Push the last column
      for (i = k; i < m; ++i) {
        boundary.Add(a[i][n - 1]);
      }
      n--;

      // Push the last row
      if (k < m) {
        for (i = n - 1; i >= l; --i) {
          boundary.Add(a[m - 1][i]);
        }
        m--;
      }

      // Push the first column
      if (l < n) {
        for (i = m - 1; i >= k; --i) {
          boundary.Add(a[i][l]);
        }
        l++;
      }

      // Sort the boundary elements
      boundary.Sort();
      int ind = 0;

      // Update the current boundary
      // with sorted elements

      // Update the first row
      for (i = n_l; i < n_n; ++i) {
        a[n_k][i] = boundary[ind++];
      }
      n_k++;

      // Update the last column
      for (i = n_k; i < n_m; ++i) {
        a[i][n_n - 1] = boundary[ind++];
      }
      n_n--;

      // Update the last row
      if (n_k < n_m) {
        for (i = n_n - 1; i >= n_l; --i) {
          a[n_m - 1][i] = boundary[ind++];
        }
        n_m--;
      }

      // Update the first column
      if (n_l < n_n) {
        for (i = n_m - 1; i >= n_k; --i) {
          a[i][n_l] = boundary[ind++];
        }
        n_l++;
      }
    }

    // Print the resultant matrix
    printMatrix(a);
  }

  // Driver code
  static void Main()
  {
    // Given matrix
    List<List<int>> matrix = new List<List<int>>();
    matrix.Add(new List<int>(new int[]{9, 7, 4, 5}));
    matrix.Add(new List<int>(new int[]{1, 6, 2, -6}));
    matrix.Add(new List<int>(new int[]{12, 20, 2, 0}));
    matrix.Add(new List<int>(new int[]{-5, -6, 7, -2}));

    sortBoundaryWise(matrix);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print the elements
// of the matrix in row-wise manner
function printMatrix(a)
{
    for(let i = 0; i < a.length; i++)
    {
        for(let j = 0; j < a[i].length; j++)
        {
            document.write(a[i][j] + " ");
        }
        document.write("<br>");
    }
}

// Function to sort boundary elements
// of a matrix starting from the outermost
// to the innermost boundary and place them
// in a clockwise manner
function sortBoundaryWise(a)
{
    /*  k - starting row index
        m - ending row index
        l - starting column index
        n - ending column index
        i - iterator
      */
    let i, k = 0, l = 0;
    let m = a.length, n = a[0].length;
    let n_i, n_k = 0, n_l = 0, n_m = m, n_n = n;

    while (k < m && l < n)
    {

        // Stores the current
        // boundary elements
        let boundary = [];

        // Push the first row
        for(i = l; i < n; ++i)
        {
            boundary.push(a[k][i]);
        }
        k++;

        // Push the last column
        for(i = k; i < m; ++i)
        {
            boundary.push(a[i][n - 1]);
        }
        n--;

        // Push the last row
        if (k < m)
        {
            for(i = n - 1; i >= l; --i)
            {
                boundary.push(a[m - 1][i]);
            }
            m--;
        }

        // Push the first column
        if (l < n)
        {
            for(i = m - 1; i >= k; --i)
            {
                boundary.push(a[i][l]);
            }
            l++;
        }

        // Sort the boundary elements
        boundary.sort(function(a,b){return a-b;}); 
        let ind = 0;

        // Update the current boundary
        // with sorted elements

        // Update the first row
        for(i = n_l; i < n_n; ++i)
        {
            a[n_k][i] = boundary[ind];
            ind++;
        }
        n_k += 1;

        // Update the last column
        for(i = n_k; i < n_m; ++i)
        {
            a[i][n_n - 1] = boundary[ind];
             ind++;
        }
        n_n--;

        // Update the last row
        if (n_k < n_m)
        {
            for(i = n_n - 1; i >= n_l; --i)
            {
                a[n_m - 1][i] = boundary[ind];
                ind++;
            }
            n_m--;
        }

        // Update the first column
        if (n_l < n_n)
        {
            for(i = n_m - 1; i >= n_k; --i)
            {
                a[i][n_l] = boundary[ind];
                ind++;
            }
            n_l++;
        }
    }

    // Print the resultant matrix
    printMatrix(a);
}

// Driver Code
 // Given matrix
let matrix = [];
let list1 = [9, 7, 4, 5];
let list2=[1, 6, 2, -6];

let list3=[12, 20, 2, 0];
let list4=[-5, -6, 7, -2];

matrix.push(list1);
matrix.push(list2);
matrix.push(list3);
matrix.push(list4);

sortBoundaryWise(matrix);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
-6 -6 -5 -2 
12 2 2 0 
9 20 6 1 
7 7 5 4 
```

***时间复杂度:**O(N<sup>3</sup>* log(N))*
***辅助空间:** O(N <sup>2</sup> )*