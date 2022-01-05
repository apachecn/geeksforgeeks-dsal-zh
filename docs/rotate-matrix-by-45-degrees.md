# 将矩阵旋转 45 度

> 原文:[https://www.geeksforgeeks.org/rotate-matrix-by-45-degrees/](https://www.geeksforgeeks.org/rotate-matrix-by-45-degrees/)

给定大小为 **N*N、**的矩阵 **mat[][]** ，任务是将矩阵旋转 **45 度**并打印矩阵。

**示例:**

> **输入:** N = 6，
> 【mat[]={ { 3，4，5，1，5，9，5}，
> 【6，9，8，7，2，5，2}，
> 【1，5，2】 3}}
> **【输出:**
>  **6 4
> 【t19 5】
> 4 5 8 1
> 4 7 9 7 5
> 4 5 8 7 8 7 2**
> 
> ****输入:** N = 4，
> 【mat[]={ { 2，5，7，2}，
> 【9，1，4，3}，【5，8，2，3}，**
> 
>  ****输出:**T2 2
> 9 5
> 5 1 7
> 6 8 4 2
> 4 2 3
> 6 3
> 3**

****方法:**按照下面给出的步骤解决问题:**

1.  **使用计数器变量将[对角线元素存储在列表](https://www.geeksforgeeks.org/python-print-diagonals-of-2d-list/)中。**
2.  **打印使输出看起来像所需图案所需的空格数。**
3.  **[反转列表后打印列表元素](https://www.geeksforgeeks.org/python-reversing-list/)。**
4.  **[仅遍历对角线元素](https://www.geeksforgeeks.org/zigzag-or-diagonal-traversal-of-matrix/)以优化操作所花费的时间。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to rotate matrix by 45 degree
void matrix(int n, int m, vector<vector<int>> li)
{

    // Counter Variable
    int ctr = 0;

    while (ctr < 2 * n - 1)
    {
        for(int i = 0;
                i < abs(n - ctr - 1);
                i++)
        {
            cout << " ";
        }

        vector<int> lst;

        // Iterate [0, m]
        for(int i = 0; i < m; i++)
        {

            // Iterate [0, n]
            for(int j = 0; j < n; j++)
            {

                // Diagonal Elements
                // Condition
                if (i + j == ctr)
                {

                    // Appending the
                    // Diagonal Elements
                    lst.push_back(li[i][j]);
                }
            }
        }

        // Printing reversed Diagonal
        // Elements
        for(int i = lst.size() - 1; i >= 0; i--)
        {
            cout << lst[i] << " ";
        }
        cout << endl;
        ctr += 1;
    }
}

// Driver code   
int main()
{

    // Dimensions of Matrix
    int n = 8;
    int m = n;

    // Given matrix
    vector<vector<int>> li{
        { 4, 5, 6, 9, 8, 7, 1, 4 },
        { 1, 5, 9, 7, 5, 3, 1, 6 },
        { 7, 5, 3, 1, 5, 9, 8, 0 },
        { 6, 5, 4, 7, 8, 9, 3, 7 },
        { 3, 5, 6, 4, 8, 9, 2, 1 },
        { 3, 1, 6, 4, 7, 9, 5, 0 },
        { 8, 0, 7, 2, 3, 1, 0, 8 },
        { 7, 5, 3, 1, 5, 9, 8, 5 } };

    // Function call
    matrix(n, m, li);

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for
// the above approach
import java.util.*;
class GFG{

// Function to rotate
// matrix by 45 degree
static void matrix(int n, int m,
                   int [][]li)
{
  // Counter Variable
  int ctr = 0;

  while (ctr < 2 * n - 1)
  {
    for(int i = 0; i < Math.abs(n - ctr - 1);
            i++)
    {
      System.out.print(" ");
    }

    Vector<Integer> lst = new Vector<Integer>();

    // Iterate [0, m]
    for(int i = 0; i < m; i++)
    {
      // Iterate [0, n]
      for(int j = 0; j < n; j++)
      {
        // Diagonal Elements
        // Condition
        if (i + j == ctr)
        {
          // Appending the
          // Diagonal Elements
          lst.add(li[i][j]);
        }
      }
    }

    // Printing reversed Diagonal
    // Elements
    for(int i = lst.size() - 1; i >= 0; i--)
    {
      System.out.print(lst.get(i) + " ");
    }

    System.out.println();
    ctr += 1;
  }
}

// Driver code   
public static void main(String[] args)
{   
  // Dimensions of Matrix
  int n = 8;
  int m = n;

  // Given matrix
  int[][] li = {{4, 5, 6, 9, 8, 7, 1, 4},
                {1, 5, 9, 7, 5, 3, 1, 6},
                {7, 5, 3, 1, 5, 9, 8, 0},
                {6, 5, 4, 7, 8, 9, 3, 7},
                {3, 5, 6, 4, 8, 9, 2, 1},
                {3, 1, 6, 4, 7, 9, 5, 0},
                {8, 0, 7, 2, 3, 1, 0, 8},
                {7, 5, 3, 1, 5, 9, 8, 5}};

  // Function call
  matrix(n, m, li);
}
}

// This code is contributed by Princi Singh
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to rotate matrix by 45 degree

def matrix(n, m, li):

    # Counter Variable
    ctr = 0
    while(ctr < 2 * n-1):
        print(" "*abs(n-ctr-1), end ="")
        lst = []

        # Iterate [0, m]
        for i in range(m):

                # Iterate [0, n]
            for j in range(n):

                # Diagonal Elements
                # Condition
                if i + j == ctr:

                    # Appending the
                    # Diagonal Elements
                    lst.append(li[i][j])

        # Printing reversed Diagonal
        # Elements
        lst.reverse()
        print(*lst)
        ctr += 1

# Driver Code

# Dimensions of Matrix
n = 8
m = n

# Given matrix
li = [[4, 5, 6, 9, 8, 7, 1, 4],
      [1, 5, 9, 7, 5, 3, 1, 6],
      [7, 5, 3, 1, 5, 9, 8, 0],
      [6, 5, 4, 7, 8, 9, 3, 7],
      [3, 5, 6, 4, 8, 9, 2, 1],
      [3, 1, 6, 4, 7, 9, 5, 0],
      [8, 0, 7, 2, 3, 1, 0, 8],
      [7, 5, 3, 1, 5, 9, 8, 5]]

# Function Call
matrix(n, m, li)
```

## **C#**

```
// C# program for
// the above approach
using System;
using System.Collections;
class GFG{

// Function to rotate
// matrix by 45 degree
static void matrix(int n, int m,
                   int [,]li)
{
  // Counter Variable
  int ctr = 0;

  while (ctr < 2 * n - 1)
  {
    for(int i = 0;
            i < Math.Abs(n - ctr - 1);
            i++)
    {
      Console.Write(" ");
    }

    ArrayList lst = new ArrayList();

    // Iterate [0, m]
    for(int i = 0; i < m; i++)
    {
      // Iterate [0, n]
      for(int j = 0; j < n; j++)
      {
        // Diagonal Elements
        // Condition
        if (i + j == ctr)
        {
          // Appending the
          // Diagonal Elements
          lst.Add(li[i, j]);
        }
      }
    }

    // Printing reversed Diagonal
    // Elements
    for(int i = lst.Count - 1;
            i >= 0; i--)
    {
      Console.Write((int)lst[i] + " ");
    }

    Console.Write("\n");
    ctr += 1;
  }
}

// Driver code   
public static void Main(string[] args)
{   
  // Dimensions of Matrix
  int n = 8;
  int m = n;

  // Given matrix
  int[,] li = {{4, 5, 6, 9, 8, 7, 1, 4},
               {1, 5, 9, 7, 5, 3, 1, 6},
               {7, 5, 3, 1, 5, 9, 8, 0},
               {6, 5, 4, 7, 8, 9, 3, 7},
               {3, 5, 6, 4, 8, 9, 2, 1},
               {3, 1, 6, 4, 7, 9, 5, 0},
               {8, 0, 7, 2, 3, 1, 0, 8},
               {7, 5, 3, 1, 5, 9, 8, 5}};

  // Function call
  matrix(n, m, li);
}
}

// This code is contributed by Rutvik_56
```

****Output:** 

```
       4
      1 5
     7 5 6
    6 5 9 9
   3 5 3 7 8
  3 5 4 1 5 7
 8 1 6 7 5 3 1
7 0 6 4 8 9 1 4
 5 7 4 8 9 8 6
  3 2 7 9 3 0
   1 3 9 2 7
    5 1 5 1
     9 0 0
      8 8
       5

```** 

*****时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)***