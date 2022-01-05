# 对网格中的单元格进行计数，通过 K 次垂直或水平跳转可以达到单元格的最大数量

> 原文:[https://www . geesforgeks . org/count-cells-in-a-grid-by-k-vertical-or-horizontal-jumps-to-count-cells-in-a-grid-in-a-grid-a-count-cells-in-a-count-count-in-a-grid-count-count-cells-in-a-](https://www.geeksforgeeks.org/count-cells-in-a-grid-from-which-maximum-number-of-cells-can-be-reached-by-k-vertical-or-horizontal-jumps/)

给定尺寸为 **N*M** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**mat【】【】**和正整数 **K** ，任务是找出网格中的单元数量，通过 **K** 在垂直或水平方向上的跳跃，可以达到最大单元数量。

**示例:**

> **输入:** N = 3，M = 3，K = 2
> **输出:** 4
> **说明:**
> 表示为 **X** 的细胞是 K (= 2)跳可达到最大细胞数的细胞:
> **X O X**
> T15】O O O
> T18】X O X
> 
> **输入:** N = 5，M = 5，K = 2
> T3】输出: 9

**方法:**给定的问题可以通过基于以下观察分别计算行和列的可能单元的数量来解决:

*   考虑任意一行，说 **i** 这样 **i < = K** ，那么从 **i** 使用 **K** 的跳转可以到达的行数是**(N–I)/K+1**。
*   如果这些行说 **i** 是 **i > K** ，那么这些单元被连接到某一行 **X** ，其中 **X < = K** ，因此它们已经被考虑。

因此，从上面的观察来看，想法是找到连接到一个变量中最大行数的行数，比如 **count_R** 。类似地，对于列，在一个变量中找到与最大列数相连的列数，比如 **count_C** 。

现在，网格中的单元数量由 **(count_R)*(count_C)** 给出，使得在垂直或水平方向上跳跃 **K** 就可以从该单元到达最大单元。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of cells
// in the grid such that maximum cell is
// reachable with a jump of K
long long countCells(int n, int m, int s)
{
    // Maximum reachable rows
    // from the current row
    int mx1 = -1;

    // Stores the count of cell that are
    // reachable from the current row
    int cont1 = 0;

    for (int i = 0; i < s && i < n; ++i) {

        // Count of reachable rows
        int aux = (n - (i + 1)) / s + 1;

        // Update the maximum value
        if (aux > mx1) {
            mx1 = cont1 = aux;
        }

        // Add it to the count
        else if (aux == mx1)
            cont1 += aux;
    }

    // Maximum reachable columns from
    // the current column
    int mx2 = -1;

    // Stores the count of cell that are
    // reachable from the current column
    int cont2 = 0;

    for (int i = 0; i < s && i < m; ++i) {

        // Count of rechable columns
        int aux = (m - (i + 1)) / s + 1;

        // Update the maximum value
        if (aux > mx2)
            mx2 = cont2 = aux;

        // Add it to the count
        else if (aux == mx2)
            cont2 += aux;
    }

    // Return the total count of cells
    return (long long)(cont1 * cont2);
}

// Driver Code
int main()
{
    int N = 5, M = 5, K = 2;
    cout << countCells(N, M, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

  // Function to count the number of cells
  // in the grid such that maximum cell is
  // reachable with a jump of K
  public static long countCells(int n, int m, int s)
  {

    // Maximum reachable rows
    // from the current row
    int mx1 = -1;

    // Stores the count of cell that are
    // reachable from the current row
    int cont1 = 0;

    for (int i = 0; i < s && i < n; ++i) {

      // Count of reachable rows
      int aux = (n - (i + 1)) / s + 1;

      // Update the maximum value
      if (aux > mx1) {
        mx1 = cont1 = aux;
      }

      // Add it to the count
      else if (aux == mx1)
        cont1 += aux;
    }

    // Maximum reachable columns from
    // the current column
    int mx2 = -1;

    // Stores the count of cell that are
    // reachable from the current column
    int cont2 = 0;

    for (int i = 0; i < s && i < m; ++i) {

      // Count of rechable columns
      int aux = (m - (i + 1)) / s + 1;

      // Update the maximum value
      if (aux > mx2)
        mx2 = cont2 = aux;

      // Add it to the count
      else if (aux == mx2)
        cont2 += aux;
    }

    // Return the total count of cells
    return (long) (cont1 * cont2);
  }

  // Driver Code
  public static void main(String args[]) {
    int N = 5, M = 5, K = 2;
    System.out.println(countCells(N, M, K));

  }

}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to count the number of cells
# in the grid such that maximum cell is
# reachable with a jump of K
def countCells(n, m, s):
    # Maximum reachable rows
    # from the current row
    mx1 = -1

    # Stores the count of cell that are
    # reachable from the current row
    cont1 = 0
    i = 0
    while(i < s and i < n):
        # Count of reachable rows
        aux = (n - (i + 1)) // s + 1

        # Update the maximum value
        if (aux > mx1):
            mx1 = cont1 = aux

        # Add it to the count
        elif(aux == mx1):
            cont1 += aux
        i += 1

    # Maximum reachable columns from
    # the current column
    mx2 = -1

    # Stores the count of cell that are
    # reachable from the current column
    cont2 = 0

    i = 0
    while(i < s and i < m):
        # Count of rechable columns
        aux = (m - (i + 1)) // s + 1

        # Update the maximum value
        if (aux > mx2):
            mx2 = cont2 = aux

        # Add it to the count
        elif(aux == mx2):
            cont2 += aux
        i += 1

    # Return the total count of cells
    return cont1 * cont2

# Driver Code
if __name__ == '__main__':
    N = 5
    M = 5
    K = 2
    print(countCells(N, M, K))

    # This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count the number of cells
// in the grid such that maximum cell is
// reachable with a jump of K
static int countCells(int n, int m, int s)
{

    // Maximum reachable rows
    // from the current row
    int mx1 = -1;

    // Stores the count of cell that are
    // reachable from the current row
    int cont1 = 0;

    for (int i = 0; i < s && i < n; ++i) {

        // Count of reachable rows
        int aux = (n - (i + 1)) / s + 1;

        // Update the maximum value
        if (aux > mx1) {
            mx1 = cont1 = aux;
        }

        // Add it to the count
        else if (aux == mx1)
            cont1 += aux;
    }

    // Maximum reachable columns from
    // the current column
    int mx2 = -1;

    // Stores the count of cell that are
    // reachable from the current column
    int cont2 = 0;

    for (int i = 0; i < s && i < m; ++i) {

        // Count of rechable columns
        int aux = (m - (i + 1)) / s + 1;

        // Update the maximum value
        if (aux > mx2)
            mx2 = cont2 = aux;

        // Add it to the count
        else if (aux == mx2)
            cont2 += aux;
    }

    // Return the total count of cells
    return (cont1 * cont2);
}

// Driver Code
public static void Main()
{
    int N = 5, M = 5, K = 2;
    Console.Write(countCells(N, M, K));
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count the number of cells
// in the grid such that maximum cell is
// reachable with a jump of K
function countCells(n, m, s)
{

  // Maximum reachable rows
  // from the current row
  let mx1 = -1;

  // Stores the count of cell that are
  // reachable from the current row
  let cont1 = 0;

  for (let i = 0; i < s && i < n; ++i) {
    // Count of reachable rows
    let aux = Math.floor((n - (i + 1)) / s + 1);

    // Update the maximum value
    if (aux > mx1) {
      mx1 = cont1 = aux;
    }

    // Add it to the count
    else if (aux == mx1) cont1 += aux;
  }

  // Maximum reachable columns from
  // the current column
  let mx2 = -1;

  // Stores the count of cell that are
  // reachable from the current column
  let cont2 = 0;

  for (let i = 0; i < s && i < m; ++i) {
    // Count of rechable columns
    let aux = Math.floor((m - (i + 1)) / s + 1);

    // Update the maximum value
    if (aux > mx2) mx2 = cont2 = aux;
    // Add it to the count
    else if (aux == mx2) cont2 += aux;
  }

  // Return the total count of cells
  return cont1 * cont2;
}

// Driver Code

let N = 5,
  M = 5,
  K = 2;
document.write(countCells(N, M, K));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
9
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(1)*