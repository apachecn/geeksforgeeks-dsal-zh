# 检查矩阵的两个元素是否在同一对角线上

> 原文:[https://www . geeksforgeeks . org/check-如果矩阵的两个元素在同一个对角线上或不在同一对角线上/](https://www.geeksforgeeks.org/check-if-two-elements-of-a-matrix-are-on-the-same-diagonal-or-not/)

给定一个矩阵 **mat[][]** ，两个整数 **X** 和 **Y** ，任务是检查 **X** 和 **Y** 是否在给定矩阵的同一对角线上。

**示例:**

> **输入:** mat[][]= {{1，2}。{3，4}}，X = 1，Y = 4
> **输出:**是
> **说明:**
> X 和 Y 位于同一对角线上。
> 
> **输入:** mat[][]= {{1，2}。{3，4}}，X = 2，Y = 4
> T3】输出:否

**方法:**解决问题的关键观察是，矩阵的两个元素只有在元素的指数之和或指数的绝对差相等时才在同一对角线上。按照以下步骤解决问题:

*   [遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)找到矩阵元素的索引。
*   检查元素是否在同一对角线上。
    设矩阵元素的指数为(P，Q)和(X，Y)，则两个元素在同一对角线上的条件由下式给出:

> P–Q = = X–Y 或 P + Q == X + Y

*   如果满足上述条件，则打印“是”。否则，打印“否”。

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if two
// integers are on the same
// diagonal of the matrix
void checkSameDiag(int li[6][5], int x,
                   int y, int m, int n)
{
  // Storing indexes of x in I, J
  int I = 0, J = 0;

  // Storing Indexes of y in P, Q
  int P = 0, Q = 0;

  for(int i = 0; i < m; i++)
  {
    for(int j = 0; j < n; j++)
    {
      if (li[i][j] == x)
      {
        I = i;
        J = j;
      }
      if (li[i][j] == y)
      {
        P = i;
        Q = j;
      }
    }
  }

  // Condition to check if the
  // both the elements are in
  // same diagonal of a matrix
  if (P - Q == I - J ||
      P + Q == I + J)
  {
    cout << "YES";
  }
  else
    cout << "NO";
}

// Driver code
int main()
{
  // Dimensions of Matrix
  int m = 6;
  int n = 5;

  // Given Matrix
  int li[6][5] = {{32, 94, 99, 26, 82},
                  {51, 69, 52, 63, 17},
                  {90, 36, 88, 55, 33},
                  {93, 42, 73, 39, 28},
                  {81, 31, 83, 53, 10},
                  {12, 29, 85, 80, 87}};

  // Elements to be checked
  int x = 42;
  int y = 80;

  // Function call
  checkSameDiag(li, x, y, m, n);
  return 0;
}

//This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
class GFG{

// Function to check if two
// integers are on the same
// diagonal of the matrix
static void checkSameDiag(int li[][], int x,
                          int y, int m, int n)
{

    // Storing indexes of x in I, J
    int I = 0, J = 0;

    // Storing Indexes of y in P, Q
    int P = 0, Q = 0;

    for(int i = 0; i < m; i++)
    {
        for(int j = 0; j < n; j++)
        {
            if (li[i][j] == x)
            {
                I = i;
                J = j;
            }
            if (li[i][j] == y)
            {
                P = i;
                Q = j;
            }
        }
    }

    // Condition to check if the
    // both the elements are in
    // same diagonal of a matrix
    if (P - Q == I - J ||
        P + Q == I + J)
    {
        System.out.println("YES");
    }
    else
        System.out.println("NO");
}

// Driver Code
public static void main(String[] args)
{

    // Dimensions of Matrix
    int m = 6;
    int n = 5;

    // Given Matrix
    int[][] li = { { 32, 94, 99, 26, 82 },
                   { 51, 69, 52, 63, 17 },
                   { 90, 36, 88, 55, 33 },
                   { 93, 42, 73, 39, 28 },
                   { 81, 31, 83, 53, 10 },
                   { 12, 29, 85, 80, 87 } };

    // Elements to be checked
    int x = 42;
    int y = 80;

    // Function call
    checkSameDiag(li, x, y, m, n);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to check if two
# integers are on the same
# diagonal of the matrix
def checkSameDiag(x, y):

    # Storing indexes of x in I, J
    # Storing Indexes of y in P, Q
    for i in range(m):
        for j in range(n):
            if li[i][j] == x:
                I, J = i, j
            if li[i][j] == y:
                P, Q = i, j

    # Condition to check if the
    # both the elements are in
    # same diagonal of a matrix
    if P-Q == I-J or P + Q == I + J:
        print("YES")
    else:
        print("NO")

# Driver Code
if __name__ == "__main__":

    # Dimensions of Matrix
    m, n = 6, 5

    # Given Matrix
    li = [[32, 94, 99, 26, 82],
        [51, 69, 52, 63, 17],
        [90, 36, 88, 55, 33],
        [93, 42, 73, 39, 28],
        [81, 31, 83, 53, 10],
        [12, 29, 85, 80, 87]]

    # elements to be checked
    x, y = 42, 80

    # Function Call
    checkSameDiag(x, y)
```

## C#

```
// C# implementation of the
// above approach
using System;
class GFG{

// Function to check if two
// integers are on the same
// diagonal of the matrix
static void checkSameDiag(int [,]li, int x,
                          int y, int m, int n)
{
  // Storing indexes of x in I, J
  int I = 0, J = 0;

  // Storing Indexes of y in P, Q
  int P = 0, Q = 0;

  for(int i = 0; i < m; i++)
  {
    for(int j = 0; j < n; j++)
    {
      if (li[i, j] == x)
      {
        I = i;
        J = j;
      }
      if (li[i, j] == y)
      {
        P = i;
        Q = j;
      }
    }
  }

  // Condition to check if the
  // both the elements are in
  // same diagonal of a matrix
  if (P - Q == I - J ||
                         P + Q == I + J)
  {
    Console.WriteLine("YES");
  }
  else
    Console.WriteLine("NO");
}

// Driver Code
public static void Main(String[] args)
{
  // Dimensions of Matrix
  int m = 6;
  int n = 5;

  // Given Matrix
  int [,]li = {{32, 94, 99, 26, 82},
               {51, 69, 52, 63, 17},
               {90, 36, 88, 55, 33},
               {93, 42, 73, 39, 28},
               {81, 31, 83, 53, 10},
               {12, 29, 85, 80, 87}};

  // Elements to be checked
  int x = 42;
  int y = 80;

  // Function call
  checkSameDiag(li, x, y, m, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

// Function to check if two
// integers are on the same
// diagonal of the matrix
function checkSameDiag(li, x,
                          y, m, n)
{

    // Storing indexes of x in I, J
    let I = 0, J = 0;

    // Storing Indexes of y in P, Q
    let P = 0, Q = 0;

    for(let i = 0; i < m; i++)
    {
        for(let j = 0; j < n; j++)
        {
            if (li[i][j] == x)
            {
                I = i;
                J = j;
            }
            if (li[i][j] == y)
            {
                P = i;
                Q = j;
            }
        }
    }

    // Condition to check if the
    // both the elements are in
    // same diagonal of a matrix
    if (P - Q == I - J ||
        P + Q == I + J)
    {
        document.write("YES");
    }
    else
        document.write("NO");
}

// Driver code

    // Dimensions of Matrix
    let m = 6;
    let n = 5;

    // Given Matrix
    let li = [[ 32, 94, 99, 26, 82 ],
                   [ 51, 69, 52, 63, 17 ],
                   [ 90, 36, 88, 55, 33 ],
                   [ 93, 42, 73, 39, 28 ],
                   [ 81, 31, 83, 53, 10 ],
                   [ 12, 29, 85, 80, 87 ]];

    // Elements to be checked
    let x = 42;
    let y = 80;

    // Function call
    checkSameDiag(li, x, y, m, n);

    // This code is contributed by splevel62.
</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*