# 最多使用 K 次移动打印从给定位置逃出矩阵的所有可能路径

> 原文:[https://www . geeksforgeeks . org/print-从给定位置脱离矩阵的所有可能路径-最多使用 k 个移动/](https://www.geeksforgeeks.org/print-all-possible-paths-to-escape-out-of-a-matrix-from-a-given-position-using-at-most-k-moves/)

给定维度为 **N*M** 的[矩阵](https://www.geeksforgeeks.org/category/data-structures/matrix/)**mat【】【】**，正整数 **K** 和源单元格 **(X，Y)** ，任务是通过在**中最多移动 K 个**的每次移动中向四个方向移动，打印从源单元格 **(X，Y)** 移出矩阵的所有可能路径。

**示例:**

> **输入:** N = 2，M = 2，X = 1，Y = 1，K = 2
> **输出:**
> (1 1)(1 0)
> (1 1)(1 2)(1 3)
> (1 1)(1 2)(0 2)
> (1 1)(0 1)
> (1)(2 1)(2 0)
> (1)(2 1)(3 1)
> 
> **输入:** N = 1，M = 1，X = 1，Y = 1，K = 2
> **输出:**
> (1 1)(1 0)
> (1 1)(1 2)
> (1 1)(0 1)
> (1 1)(2 1)

**方法:**给定的问题可以通过[递归](https://www.geeksforgeeks.org/recursion/)和[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)来解决。按照以下步骤解决给定的问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)，比如说**数组**存储从源单元格到矩阵外的所有移动。
*   定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，比如**打印所有移动(N，M，moves，X，Y，arrayOfMoves)** ，并执行以下步骤:
    *   **基本情况:**
        *   如果**移动**的值为非负数，并且当前单元格 **(X，Y)** 不在矩阵中，则打印存储在**数组**中的所有移动。
        *   如果**移动**的值小于 **0** ，则[从功能](https://www.geeksforgeeks.org/c-function-argument-return-values/)返回。
    *   将当前单元格 **(X，Y)** 插入到数组**中，数组移动[]** 。
    *   通过将**的值递减 **1** 移动**，在当前单元格 **(X，Y)** 的所有四个方向递归调用该函数
    *   如果数组 **的[大小大于 1，则删除为回溯步骤插入的最后一个单元格。](https://www.geeksforgeeks.org/how-to-find-size-of-array-in-cc-without-using-sizeof-operator/)**
*   调用[功能](https://www.geeksforgeeks.org/functions-in-c/) **打印所有移动(N，M，移动，X，Y，arrayOfMoves)** 打印所有可能的移动。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to print all the paths
// that are outside of the matrix
void printAllmoves(
  int n, int m, int x, int y,
  int moves, vector<pair<int,int>> ArrayOfMoves)
{

  // Base Case
  if (x <= 0 || y <= 0 || x >= n + 1
      || y >= m + 1 && moves >= 0) {

    // Add the last position
    ArrayOfMoves.push_back({x, y});

    // Traverse the pairs
    for (auto ob : ArrayOfMoves) {

      // Print all the paths
      cout<<"("<<ob.first<<" "<<ob.second<<")";
    }

    cout<<endl;

    // Backtracking Steps
    if(ArrayOfMoves.size() > 1)
      ArrayOfMoves.pop_back();

    return;
  }

  // If no moves remain
  if (moves <= 0) {
    return;
  }

  // Add the current position
  // in the list
  ArrayOfMoves.push_back({x, y});

  // Recursive function Call
  // in all the four directions
  printAllmoves(n, m, x, y - 1, moves - 1,
                ArrayOfMoves);
  printAllmoves(n, m, x, y + 1, moves - 1,
                ArrayOfMoves);
  printAllmoves(n, m, x - 1, y, moves - 1,
                ArrayOfMoves);
  printAllmoves(n, m, x + 1, y, moves - 1,
                ArrayOfMoves);

  // Backtracking Steps
  if (ArrayOfMoves.size() > 1) {
    ArrayOfMoves.pop_back();
  }
}

// Driver Code
int main()
{
  int N = 2, M = 2;
  int X = 1;
  int Y = 1;
  int K = 2;
  vector<pair<int,int>> ArrayOfMoves;

  // Function Call
  printAllmoves(N, M, X, Y, K,
                ArrayOfMoves);
}

// This code is contributed by ipg2016107.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

public class GFG {

    // Class for the pairs
    static class Pair {
        int a;
        int b;
        Pair(int a, int b)
        {
            this.a = a;
            this.b = b;
        }
    }

    // Function to print all the paths
    // that are outside of the matrix
    static void printAllmoves(
        int n, int m, int x, int y,
        int moves, ArrayList<Pair> ArrayOfMoves)
    {
        // Base Case
        if (x <= 0 || y <= 0 || x >= n + 1
            || y >= m + 1 && moves >= 0) {

            // Add the last position
            ArrayOfMoves.add(new Pair(x, y));

            // Traverse the pairs
            for (Pair ob : ArrayOfMoves) {

                // Print all the paths
                System.out.print("(" + ob.a
                                 + " " + ob.b
                                 + ")");
            }

            System.out.println();

            // Backtracking Steps
            if (ArrayOfMoves.size() > 1)
                ArrayOfMoves.remove(
                    ArrayOfMoves.size() - 1);

            return;
        }

        // If no moves remain
        if (moves <= 0) {
            return;
        }

        // Add the current position
        // in the list
        ArrayOfMoves.add(new Pair(x, y));

        // Recursive function Call
        // in all the four directions
        printAllmoves(n, m, x, y - 1, moves - 1,
                      ArrayOfMoves);
        printAllmoves(n, m, x, y + 1, moves - 1,
                      ArrayOfMoves);
        printAllmoves(n, m, x - 1, y, moves - 1,
                      ArrayOfMoves);
        printAllmoves(n, m, x + 1, y, moves - 1,
                      ArrayOfMoves);

        // Backtracking Steps
        if (ArrayOfMoves.size() > 1) {
            ArrayOfMoves.remove(
                ArrayOfMoves.size() - 1);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 2, M = 2;
        int X = 1;
        int Y = 1;
        int K = 2;
        ArrayList<Pair> ArrayOfMoves
            = new ArrayList<>();

        // Function Call
        printAllmoves(N, M, X, Y, K,
                      ArrayOfMoves);
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to print all the paths
# that are outside of the matrix
def printAllmoves(n,m,x,y, moves,ArrayOfMoves):

  # Base Case
  if (x <= 0 or y <= 0 or x >= n + 1 or y >= m + 1 and moves >= 0):

    # Add the last position
    ArrayOfMoves.append([x, y])

    # Traverse the pairs
    for ob in ArrayOfMoves:

      # Print all the paths
      print("(",ob[0],ob[1],")",end="")

    print("\n",end = "")

    # Backtracking Steps
    if(len(ArrayOfMoves) > 1):
      ArrayOfMoves.pop()

    return

  # If no moves remain
  if (moves <= 0):
    return

  # Add the current position
  # in the list
  ArrayOfMoves.append([x, y])

  # Recursive function Call
  # in all the four directions
  printAllmoves(n, m, x, y - 1, moves - 1,ArrayOfMoves)
  printAllmoves(n, m, x, y + 1, moves - 1,ArrayOfMoves)
  printAllmoves(n, m, x - 1, y, moves - 1,ArrayOfMoves)
  printAllmoves(n, m, x + 1, y, moves - 1,ArrayOfMoves)

  # Backtracking Steps
  if (len(ArrayOfMoves) > 1):
    ArrayOfMoves.pop()

# Driver Code
if __name__ == '__main__':
  N = 2
  M = 2
  X = 1
  Y = 1
  K = 2
  ArrayOfMoves = []

  # Function Call
  printAllmoves(N, M, X, Y, K,ArrayOfMoves)

  # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
using System;
using System.Collections;
public class GFG {
    class Pair {
        public int a;
        public int b;
        public Pair(int a, int b)
        {
            this.a = a;
            this.b = b;
        }
    }

    // Function to print all the paths
    // that are outside of the matrix
    static void printAllmoves(int n, int m, int x, int y,
                              int moves,
                              ArrayList ArrayOfMoves)
    {
        // Base Case
        if (x <= 0 || y <= 0 || x >= n + 1
            || y >= m + 1 && moves >= 0) {

            // Add the last position
            ArrayOfMoves.Add(new Pair(x, y));

            // Traverse the pairs
            foreach (Pair ob in ArrayOfMoves) {

                // Print all the paths
                Console.Write("(" + ob.a + " " + ob.b
                                  + ")");
            }

            Console.WriteLine();

            // Backtracking Steps
            if (ArrayOfMoves.Count > 1)
                ArrayOfMoves.Remove(ArrayOfMoves.Count
                                    - 1);

            return;
        }

        // If no moves remain
        if (moves <= 0) {
            return;
        }

        // Add the current position
        // in the list
        ArrayOfMoves.Add(new Pair(x, y));

        // Recursive function Call
        // in all the four directions
        printAllmoves(n, m, x, y - 1, moves - 1,
                      ArrayOfMoves);
        printAllmoves(n, m, x, y + 1, moves - 1,
                      ArrayOfMoves);
        printAllmoves(n, m, x - 1, y, moves - 1,
                      ArrayOfMoves);
        printAllmoves(n, m, x + 1, y, moves - 1,
                      ArrayOfMoves);

        // Backtracking Steps
        if (ArrayOfMoves.Count > 1) {
            ArrayOfMoves.Remove(ArrayOfMoves.Count - 1);
        }
    }
    static public void Main()
    {
        int N = 2, M = 2;
        int X = 1;
        int Y = 1;
        int K = 2;
        ArrayList ArrayOfMoves = new ArrayList();

        // Function Call
        printAllmoves(N, M, X, Y, K, ArrayOfMoves);
    }
}

// This code is contributed by maddler.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

    // Class for the pairs
     class Pair {

        constructor(a , b) {
            this.a = a;
            this.b = b;
        }
    }
function ob(item)
{

    // Print all the paths
    document.write("(" + item.a + " " + item.b + ")");
}

    // Function to print all the paths
    // that are outside of the matrix
    function printAllmoves(n , m , x , y , moves,  ArrayOfMoves)
    {
        // Base Case
        if (x <= 0 || y <= 0 || x >= n + 1 || y >= m + 1 && moves >= 0) {

            // Add the last position
            ArrayOfMoves.push(new Pair(x, y));

            // Traverse the pairs
            ArrayOfMoves.forEach (ob);

            document.write("<br/>");

            // Backtracking Steps
            if (ArrayOfMoves.length > 1)
                ArrayOfMoves.pop(ArrayOfMoves.length - 1);

            return;
        }

        // If no moves remain
        if (moves <= 0) {
            return;
        }

        // Add the current position
        // in the list
        ArrayOfMoves.push(new Pair(x, y));

        // Recursive function Call
        // in all the four directions
        printAllmoves(n, m, x, y - 1, moves - 1, ArrayOfMoves);
        printAllmoves(n, m, x, y + 1, moves - 1, ArrayOfMoves);
        printAllmoves(n, m, x - 1, y, moves - 1, ArrayOfMoves);
        printAllmoves(n, m, x + 1, y, moves - 1, ArrayOfMoves);

        // Backtracking Steps
        if (ArrayOfMoves.length > 1) {
            ArrayOfMoves.pop(ArrayOfMoves.length - 1);
        }
    }

    // Driver Code
        var N = 2, M = 2;
        var X = 1;
        var Y = 1;
        var K = 2;
        var ArrayOfMoves =new Array();

        // Function Call
        printAllmoves(N, M, X, Y, K, ArrayOfMoves);

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
(1 1)(1 0)
(1 1)(1 2)(1 3)
(1 1)(1 2)(0 2)
(1 1)(0 1)
(1 1)(2 1)(2 0)
(1 1)(2 1)(3 1)
```

***时间复杂度:**O(4<sup>N</sup>)*
***辅助空间:** O(4 <sup>N</sup> )*