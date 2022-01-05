# 检查矩阵是否包含以 0 为边界元素的正方形子矩阵

> 原文:[https://www . geesforgeks . org/check-if-a-matrix-contains-a-square-submatrix-以 0 为边界元素/](https://www.geeksforgeeks.org/check-if-a-matrix-contains-a-square-submatrix-with-0-as-boundary-element/)

给定一个 **N*N** 二进制矩阵 **arr[][]** ，任务是检查该矩阵是否包含一个至少大小为**2×2**的正方形，其边界仅由 **0** s 组成。

**示例:**

> **输入:**
> arr[][] = {
> {1，1，0，1，0}，
> {0，0，0，0，0，1}，
> {0，1，1，1，0，1}，
> {0，0，0，1，0，1，0，1}，
> {0，1，1，0，0，1}，
> {0，0，0，0，0，1}
> }
> 
> {
> {，，，，}，
> {0，0，0，0，}，
> {0、、、0、}，
> {0、、、0、}，
> {0、、、0、}，
> {0，0，0，0，0，}
> }
> 
> **输入:**
> arr[][] = {
> {1，1，0，1，0}，
> {0，0，0，0，0，1}，
> {0，1，1，1，0，1}，
> {0，0，0，1，1，1，1}，
> {0，1，1，0，1，0，1}，
> {0，0，0，0，0，1}
> }

**进场:**

1.  正方形由其最上面和最下面的行以及最左边和最右边的列来定义。
2.  给定一对行和一对列组成一个有效的正方形，您可以很容易地确定相关的正方形是否是一个带有两个 for 循环的零的正方形。
3.  需要迭代输入矩阵中的每个有效的正方形，arr[][]。
4.  我们可以从最外面的正方形开始迭代，并在矩阵中递归向内。
5.  向内移动时，从(r1，c1)和(r2，c2)我们有 5 个选项，将生成方形矩阵:-
    a) (r1 + 1，c1 + 1)，(r2–1，C2–1)
    b)(R1，c1 + 1)，(r2–1，c2)
    c) (r1 + 1，c1)，(R2，C2–1)
    d)(R1+1，c1 + 1)，(R2，c2)
    e) (r1，c1)，(R2–1，C2–1)
6.  由于该问题有许多[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)，因此我们需要使用[缓存/记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)来避免重复计算。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

bool hasSquareOfZeroes(
    vector<vector<int> >& matrix,
    int r1, int c1, int r2, int c2,
    unordered_map<string, bool>& cache);

bool isSquareOfZeroes(
    vector<vector<int> >& matrix,
    int r1, int c1,
    int r2, int c2);

// Function checks if square
// with all 0's in boundary
// exists in the matrix
bool squareOfZeroes(
    vector<vector<int> > matrix)
{
    int lastIdx = matrix.size() - 1;
    unordered_map<string, bool> cache;
    return hasSquareOfZeroes(
        matrix,
        0, 0,
        lastIdx,
        lastIdx,
        cache);
}

// Function iterate inward in
// the matrix and checks the
// square obtained and memoize/cache
// the result to avoid duplicate computation

// r1 is the top row,
// c1 is the left col
// r2 is the bottom row,
// c2 is the right
bool hasSquareOfZeroes(
    vector<vector<int> >& matrix,
    int r1, int c1, int r2, int c2,
    unordered_map<string, bool>& cache)
{
    if (r1 >= r2 || c1 >= c2)
        return false;
    string key = to_string(r1) + '-'
                 + to_string(c1) + '-'
                 + to_string(r2) + '-'
                 + to_string(c2);

    if (cache.find(key) != cache.end())
        return cache[key];

    cache[key]
        = isSquareOfZeroes(
              matrix, r1, c1, r2, c2)
          || hasSquareOfZeroes(
                 matrix, r1 + 1, c1 + 1,
                 r2 - 1, c2 - 1, cache)
          || hasSquareOfZeroes(
                 matrix, r1, c1 + 1,
                 r2 - 1, c2, cache)
          || hasSquareOfZeroes(
                 matrix, r1 + 1, c1,
                 r2, c2 - 1, cache)
          || hasSquareOfZeroes(
                 matrix, r1 + 1, c1 + 1,
                 r2, c2, cache)
          || hasSquareOfZeroes(
                 matrix, r1, c1,
                 r2 - 1, c2 - 1, cache);

    return cache[key];
}

// Function checks if the
// boundary of the square
// consists of 0's
bool isSquareOfZeroes(
    vector<vector<int> >& matrix,
    int r1, int c1,
    int r2, int c2)
{
    for (int row = r1; row < r2 + 1; row++) {
        if (matrix[row][c1] != 0
            || matrix[row][c2] != 0)
            return false;
    }
    for (int col = c1; col < c2 + 1; col++) {
        if (matrix[r1][col] != 0
            || matrix[r2][col] != 0)
            return false;
    }
    return true;
}

// Driver Code
int main()
{
    vector<vector<int> > matrix{
        { 1, 1, 1, 0, 1, 0 },
        { 0, 0, 0, 0, 0, 1 },
        { 0, 1, 1, 1, 0, 1 },
        { 0, 0, 0, 1, 0, 1 },
        { 0, 1, 1, 1, 0, 1 },
        { 0, 0, 0, 0, 0, 1 }
    };
    int ans;
    ans = squareOfZeroes(matrix);

    if (ans == 1) {
        cout << "True" << endl;
    }
    else {
        cout << "False" << endl;
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;
import java.util.*;

class GFG
{

    // Function checks if square
    // with all 0's in boundary
    // exists in the matrix
    static int squareOfZeroes(int[][] matrix)
    {
        int lastIdx = matrix.length - 1;
        Map<String, Boolean> cache
            = new HashMap<String, Boolean>();
        return (hasSquareOfZeroes(matrix, 0, 0, lastIdx,
                                 lastIdx, cache)) ? 1 : 0;
    }

    // Function iterate inward in
    // the matrix and checks the
    // square obtained and memoize/cache
    // the result to avoid duplicate computation

    // r1 is the top row,
    // c1 is the left col
    // r2 is the bottom row,
    // c2 is the right
    static boolean hasSquareOfZeroes(int[][] matrix, int r1, int c1,
                                     int r2, int c2,
                                     Map<String, Boolean> cache)
    {
        if (r1 >= r2 || c1 >= c2)
            return false;
        String key = r1 + "-" + c1 +
          "-" + r2 + "-" + c2;

        if (cache.containsKey(key))
            return cache.get(key);

        cache.put(
            key,
            isSquareOfZeroes(matrix, r1, c1, r2, c2)
                || hasSquareOfZeroes(matrix, r1 + 1, c1 + 1,
                                     r2 - 1, c2 - 1, cache)
                || hasSquareOfZeroes(matrix, r1, c1 + 1,
                                     r2 - 1, c2, cache)
                || hasSquareOfZeroes(matrix, r1 + 1, c1, r2,
                                     c2 - 1, cache)
                || hasSquareOfZeroes(matrix, r1 + 1, c1 + 1,
                                     r2, c2, cache)
                || hasSquareOfZeroes(matrix, r1, c1, r2 - 1,
                                     c2 - 1, cache));

        return cache.get(key);
    }

    // Function checks if the
    // boundary of the square
    // consists of 0's
    static boolean isSquareOfZeroes(int[][] matrix,
                                    int r1, int c1,
                                    int r2, int c2)
    {
        for (int row = r1; row < r2 + 1; row++)
        {
            if (matrix[row][c1] != 0
                || matrix[row][c2] != 0)
                return false;
        }
        for (int col = c1; col < c2 + 1; col++)
        {
            if (matrix[r1][col] != 0
                || matrix[r2][col] != 0)
                return false;
        }
        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[][] matrix = {
            { 1, 1, 1, 0, 1, 0 }, { 0, 0, 0, 0, 0, 1 },
            { 0, 1, 1, 1, 0, 1 }, { 0, 0, 0, 1, 0, 1 },
            { 0, 1, 1, 1, 0, 1 }, { 0, 0, 0, 0, 0, 1 }
        };
        int ans;
        ans = squareOfZeroes(matrix);

        if (ans == 1)
        {
            System.out.println("True");
        }
        else
        {
            System.out.println("False");
        }
    }
}

// This code is contributed by jitin
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function checks if square
# with all 0's in boundary
# exists in the matrix
def squareOfZeroes():

    global matrix, cache
    lastIdx = len(matrix) - 1

    return hasSquareOfZeroes(0, 0, lastIdx,
                                   lastIdx)

# Function iterate inward in
# the matrix and checks the
# square obtained and memoize/cache
# the result to avoid duplicate computation

# r1 is the top row,
# c1 is the left col
# r2 is the bottom row,
# c2 is the right
def hasSquareOfZeroes(r1, c1, r2, c2):

    global matrix, cache

    if (r1 >= r2 or c1 >= c2):
        return False

    key = (str(r1) + '-' + str(c1) + '-' +
           str(r2) + '-' + str(c2))

    if (key in cache):
        return cache[key]

    cache[key] = (isSquareOfZeroes(r1, c1, r2, c2) or
                 hasSquareOfZeroes(r1 + 1, c1 + 1,
                                   r2 - 1, c2 - 1))
    cache[key] = (cache[key] or
                  hasSquareOfZeroes(r1, c1 + 1,
                                        r2 - 1, c2) or
                  hasSquareOfZeroes(r1 + 1, c1,
                                r2, c2 - 1))
    cache[key] = (cache[key] or
                  hasSquareOfZeroes(r1 + 1, c1 + 1,
                                    r2, c2) or
                  hasSquareOfZeroes(r1, c1, r2 - 1,
                                            c2 - 1))

    return cache[key]

# Function checks if the
# boundary of the square
# consists of 0's
def isSquareOfZeroes(r1, c1, r2, c2):

    global matrix

    for row in range(r1, r2 + 1):
        if (matrix[row][c1] != 0 or
            matrix[row][c2] != 0):
            return False

    for col in range(c1, c2 + 1):
        if (matrix[r1][col] != 0 or
            matrix[r2][col] != 0):
            return False

    return True

# Driver Code
if __name__ == '__main__':

    cache = {}
    matrix = [ [ 1, 1, 1, 0, 1, 0 ],
               [ 0, 0, 0, 0, 0, 1 ],
               [ 0, 1, 1, 1, 0, 1 ],
               [ 0, 0, 0, 1, 0, 1 ],
               [ 0, 1, 1, 1, 0, 1 ],
               [ 0, 0, 0, 0, 0, 1 ] ]

    ans = squareOfZeroes()

    if (ans == 1):
        print("True")
    else:
        print("False")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function checks if square
  // with all 0's in boundary
  // exists in the matrix
  static int squareOfZeroes(int[,] matrix)
  {
    int lastIdx = matrix.GetLength(0) - 1;
    Dictionary<string, bool> cache = new Dictionary<string, bool>();
    if(hasSquareOfZeroes(matrix, 0, 0, lastIdx,lastIdx, cache))
    {
      return 1;
    }
    else
    {
      return 0;
    }
  }

  // Function iterate inward in
  // the matrix and checks the
  // square obtained and memoize/cache
  // the result to avoid duplicate computation

  // r1 is the top row,
  // c1 is the left col
  // r2 is the bottom row,
  // c2 is the right
  static bool hasSquareOfZeroes(int[,] matrix, int r1,
                                int c1,int r2, int c2,
                                Dictionary<string, bool> cache)
  {
    if (r1 >= r2 || c1 >= c2)
    {
      return false;
    }
    string key = r1 + "-" + c1 + "-" + r2 + "-" + c2;
    if (cache.ContainsKey(key))
    {
      return cache[key];
    }
    cache[key] = (isSquareOfZeroes(matrix, r1, c1, r2, c2) ||
                  hasSquareOfZeroes(matrix, r1 + 1, c1 + 1,
                                    r2 - 1, c2 - 1, cache) ||
                  hasSquareOfZeroes(matrix, r1, c1 + 1,r2 - 1,
                                    c2, cache) ||
                  hasSquareOfZeroes(matrix, r1 + 1, c1, r2,
                                    c2 - 1, cache) ||
                  hasSquareOfZeroes(matrix, r1 + 1, c1 + 1,
                                    r2, c2, cache) ||
                  hasSquareOfZeroes(matrix, r1, c1, r2 - 1,
                                    c2 - 1, cache));
    return cache[key];
  }

  // Function checks if the
  // boundary of the square
  // consists of 0's
  static bool isSquareOfZeroes(int[,] matrix, int r1,
                               int c1,int r2, int c2)
  {
    for (int row = r1; row < r2 + 1; row++)
    {
      if (matrix[row,c1] != 0 || matrix[row,c2] != 0)
      {
        return false;
      }

    }
    for (int col = c1; col < c2 + 1; col++)
    {
      if (matrix[r1,col] != 0 || matrix[r2,col] != 0)
      {
        return false;
      }
    }
    return true;
  }

  // Driver Code
  static public void Main ()
  {
    int[,] matrix = {{ 1, 1, 1, 0, 1, 0 },
                     { 0, 0, 0, 0, 0, 1 },
                     { 0, 1, 1, 1, 0, 1 },
                     { 0, 0, 0, 1, 0, 1 },
                     { 0, 1, 1, 1, 0, 1 },
                     { 0, 0, 0, 0, 0, 1 }};
    int ans;
    ans = squareOfZeroes(matrix);
    if(ans == 1)
    {
      Console.WriteLine("True");

    }
    else
    {
      Console.WriteLine("False");
    }
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function checks if square
// with all 0's in boundary
// exists in the matrix
function squareOfZeroes( matrix)
{
    var lastIdx = matrix.length - 1;
    var cache = new Map();
    return hasSquareOfZeroes(
        matrix,
        0, 0,
        lastIdx,
        lastIdx,
        cache);
}

// Function iterate inward in
// the matrix and checks the
// square obtained and memoize/cache
// the result to avoid duplicate computation

// r1 is the top row,
// c1 is the left col
// r2 is the bottom row,
// c2 is the right
function hasSquareOfZeroes(matrix, r1, c1, r2, c2, cache)
{
    if (r1 >= r2 || c1 >= c2)
        return false;
    var key = (r1.toString()) + '-'
                 + (c1.toString()) + '-'
                 + (r2.toString()) + '-'
                 + (c2.toString());

    if (cache.has(key))
        return cache.get(key);

    cache[key]
        = isSquareOfZeroes(
              matrix, r1, c1, r2, c2)
          || hasSquareOfZeroes(
                 matrix, r1 + 1, c1 + 1,
                 r2 - 1, c2 - 1, cache)
          || hasSquareOfZeroes(
                 matrix, r1, c1 + 1,
                 r2 - 1, c2, cache)
          || hasSquareOfZeroes(
                 matrix, r1 + 1, c1,
                 r2, c2 - 1, cache)
          || hasSquareOfZeroes(
                 matrix, r1 + 1, c1 + 1,
                 r2, c2, cache)
          || hasSquareOfZeroes(
                 matrix, r1, c1,
                 r2 - 1, c2 - 1, cache);

    return cache[key];
}

// Function checks if the
// boundary of the square
// consists of 0's
function isSquareOfZeroes(matrix, r1, c1, r2, c2)
{
    for (var row = r1; row < r2 + 1; row++) {
        if (matrix[row][c1] != 0
            || matrix[row][c2] != 0)
            return false;
    }
    for (var col = c1; col < c2 + 1; col++) {
        if (matrix[r1][col] != 0
            || matrix[r2][col] != 0)
            return false;
    }
    return true;
}

// Driver Code
var matrix = [
    [ 1, 1, 1, 0, 1, 0 ],
    [ 0, 0, 0, 0, 0, 1 ],
    [ 0, 1, 1, 1, 0, 1 ],
    [ 0, 0, 0, 1, 0, 1 ],
    [ 0, 1, 1, 1, 0, 1 ],
    [ 0, 0, 0, 0, 0, 1 ]
];
var ans;
ans = squareOfZeroes(matrix);
if (ans == 1) {
    document.write( "True");
}
else {
    document.write( "False" );
}

</script>
```

**Output:** 

```
True
```

***时间复杂度:** O(N^4)*
***空间复杂度:** O(N^3)*

**高效方法:**为了优化上述方法，我们需要遵循以下步骤:

1.  我们需要为矩阵中的每个元素预先计算两个值:每个元素右边的 0 数(包括元素本身)和每个元素下面的 0 数(包括元素本身)。
2.  我们可以通过从右下角开始迭代矩阵，然后从右向左遍历每一行来计算这些值。
3.  一旦我们计算了矩阵，那么我们就可以检查正方形的边界是否由常数时间内的所有 0 组成。
4.  为了检查正方形的边界，我们只需要查看任何正方形的两个顶角下方的 0 的数量以及同一个正方形的两个左角右侧的 0 的数量。