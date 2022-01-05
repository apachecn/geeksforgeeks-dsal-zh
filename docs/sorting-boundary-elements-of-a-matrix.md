# 排序矩阵的边界元素

> 原文:[https://www . geeksforgeeks . org/排序-矩阵的边界元素/](https://www.geeksforgeeks.org/sorting-boundary-elements-of-a-matrix/)

给定一个大小为 **M*N** 的矩阵 **mat[][]** ，任务是只按顺时针方向对矩阵的边框元素进行排序，再次排序后打印矩阵。

**例:**

> **输入:** M = 4，N = 5，下面是给定的矩阵:
> 
> ```
> 1 2 3 4 0 
> 1 1 1 1 2  
> 1 2 2 2 4 
> 1 9 3 1 7
> ```
> 
> **输出:**
> 0 1 1 1 1
> 9 1 1 1 1
> 7 2 2 2 2
> 4 4 3 3 2
> **说明:**
> 对于给定矩阵，边界元素为:
> (1，2，3，4，0，2，4，7，1，3，9，1，1，1)
> 按顺时针顺序排序后:
> (0，1，1，1，1，2，2，3
> 
> **输入:** M = 3，N = 4
> 
> ```
> 4 2 8 0 
> 2 6 9 8 
> 0 3 1 7
> ```
> 
> **输出:**
> 0 0 1 2
> 8 6 9 2
> 8 7 4 3
> **说明:**
> 对于给定矩阵，边框元素为:
> (4，2，8，0，8，7，1，3，0，2)
> 按顺时针顺序排序后:
> (0，0，1，2，3，4，7，8，8)

**方法:**想法是在一个数组中存储[给定矩阵](https://www.geeksforgeeks.org/boundary-elements-matrix/)的所有边界元素，然后[排序](https://www.geeksforgeeks.org/sorting-algorithms/)这个数组，然后简单地使用这个排序的数组作为边界元素打印新的矩阵。

详细步骤如下:

*   遍历给定矩阵，将所有边界元素推到一个数组 **A[]** 。
*   按升序对数组 **A[]** 进行排序。
*   使用数组 **A[]** 的第一个 **N** 元素打印第一行。
*   从第二行到倒数第二行，先从 **A[]** 末尾打印一个单元素，然后从原始矩阵打印 **N-2** 中间元素，最后从 **A[]** 前面打印一个单元素。
*   对于最后一行，以相反的顺序打印从 **A[]** 开始的中间元素，这些元素仍未打印。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
void printMatrix(int grid[][5], int m, int n)
{
  vector<int> A;

  // Appending border elements
  for (int i = 0; i < m; i++)
  {
    for (int j = 0; j < n; j++)
    {
      if (j == n - 1 || (i == m - 1) || j == 0
          || i == 0)
        A.push_back(grid[i][j]);
    }
  }

  // Sorting the list
  sort(A.begin(), A.end());

  // Printing first row with
  // first N elements from A
  for (int i = 0; i < n; i++)
    cout << A[i] << " ";
  cout << endl;
  // print(*A[:n])

  // Printing N-2 rows
  for (int i = 0; i < m - 2; i++)
  {

    // Print elements from last
    cout << A[A.size() - i - 1] << " ";

    // Print middle elements
    // from original matrix
    for (int j = 1; j < n - 1; j++)
      cout << grid[i + 1][j] << " ";

    // Print elements from front
    cout << (A[n + i]) << endl;
  }

  // Printing last row
  reverse(A.begin() + n + m - 2,
          A.begin() + n + m + n - 2);
  for (int i = n + m - 2; i < n + m - 2 + n; i++)
    cout << A[i] << " ";
  //[n + m - 2:n + m - 2 + n] << endl;
}

// Driver Code
int main()
{
  // Dimensions of a Matrix
  int m = 4, n = 5;

  // Given Matrix
  int grid[][5] = { { 1, 2, 3, 4, 0 },
                   { 1, 1, 1, 1, 2 },
                   { 1, 2, 2, 2, 4 },
                   { 1, 9, 3, 1, 7 } };

  // Function Call
  printMatrix(grid, m, n);
  return 0;
}

// This code is contributed by chitranayal.
```

## 蟒蛇 3

```
# Python program for the above approach

def printMatrix(grid, m, n):

    A =[]

    # Appending border elements
    for i in range(m):
        for j in range(n):
            if j == n-1 or (i == m-1
                ) or j == 0 or i == 0:
                A.append(grid[i][j])

    # Sorting the list

    A.sort()

    # Printing first row with
    # first N elements from A
    print(*A[:n])

    # Printing N-2 rows
    for i in range(m-2):

        # Print elements from last
        print(A[len(A)-i-1],
                          end =" ")
        # Print middle elements
        # from original matrix
        for j in range(1, n-1):
            print(grid[i + 1][j],
                          end =" ")

        # Print elements from front
        print(A[n + i])

    # Printing last row
    print(*reversed(A[n + m-2:n + m-2 + n]))

# Driver Code

# Dimensions of a Matrix
m, n = 4, 5

# Given Matrix
grid =[[1, 2, 3, 4, 0],
       [1, 1, 1, 1, 2],
       [1, 2, 2, 2, 4],
       [1, 9, 3, 1, 7]]

# Function Call
printMatrix(grid, m, n)
```

## java 描述语言

```
<script>

// Javascript program for the above approach
function printMatrix(grid, m, n)
{
    let A = [];

    // Appending border elements
    for(let i = 0; i < m; i++)
    {
        for(let j = 0; j < n; j++)
        {
            if (j == n - 1 || (i == m - 1) ||
                j == 0 || i == 0)
                A.push(grid[i][j]);
        }
    }

    // Sorting the list
    A.sort(function(a, b){return a - b;});

    // Printing first row with
    // first N elements from A
    for(let i = 0; i < n; i++)
        document.write(A[i] + " ");

    document.write("<br>")
    // print(*A[:n])

    // Printing N-2 rows
    for(let i = 0; i < m - 2; i++)
    {

        // Print elements from last
        document.write(A[A.length - i - 1] + " ");

        // Print middle elements
        // from original matrix
        for(let j = 1; j < n - 1; j++)
            document.write(grid[i + 1][j] + " ");

        // Print elements from front
        document.write(A[n + i] + "<br>")
    }

    // Printing last row
    document.write(A.slice(
        n + m - 2, n + m - 2 + n).reverse().join(" "));
    //[n + m - 2:n + m - 2 + n] << endl;
}

// Driver Code

// Dimensions of a Matrix
let m = 4, n = 5;

// Given Matrix
let grid = [ [ 1, 2, 3, 4, 0 ],
             [ 1, 1, 1, 1, 2 ],
             [ 1, 2, 2, 2, 4 ],
             [ 1, 9, 3, 1, 7 ] ];

// Function Call
printMatrix(grid, m, n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
0 1 1 1 1
9 1 1 1 1
7 2 2 2 2
4 4 3 3 2
```

***时间复杂度:** O(M*N)*
***辅助空间:** O(M+N)*