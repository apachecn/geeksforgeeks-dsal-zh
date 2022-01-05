# 检查矩阵的所有对角线是否回文

> 原文:[https://www . geeksforgeeks . org/check-如果矩阵的所有对角线都是回文或非回文/](https://www.geeksforgeeks.org/check-if-all-the-diagonals-of-the-matrix-are-palindromic-or-not/)

给定尺寸为 **N*M** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**mat【】【】【】**，任务是检查矩阵的所有[对角线(从右上到左下)是否回文。如果发现**为真**，则打印**是**。否则，打印**否**。](https://www.geeksforgeeks.org/program-to-print-the-diagonals-of-a-matrix/)

**示例:**

> **输入:** mat[][] = [[1，0，0，0，0]，[0，1，1，1]，[0，1，0，1]，[0，1，1，0]]
> **输出:**是
> T6】解释:T8】矩阵 mat[][]的所有对角线由下式给出:
> 
> *   {1}
> *   {0, 0}
> *   {0, 1, 0}
> *   {0, 1, 1, 0}
> *   {1, 0, 1}
> *   {1, 1}
> *   {0}
> 
> 因为上面所有的对角线都是回文。因此，打印“是”。
> 
> **输入:** mat[][] = [[1，0，0，0]，[1，1，0，1]，[1，0，1，1]，[0，1，0，1]]
> **输出:**否

**方法:**给定的问题可以通过[执行矩阵的对角遍历](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix)并针对每个对角遍历检查元素是否回文来解决。如果存在非回文的对角线，则打印**是**。否则，打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

#define N 5

// Function to check if the matrix is
// palindrome or not
string isbinaryMatrixPalindrome(
    int mat[N][N])
{

    // Traverse the matrix and check if
    // top right and bottom left elements
    // have same value
    for (int i = 0; i < N - 1; i++) {
        for (int j = N - 1; j > i; j--) {

            // If top right element is not
            // equal to the bottom left
            // element return false
            if (mat[i][j] != mat[j][i]) {
                return "Np";
            }
        }
    }

    return "Yes";
}

// Driver Code
int main()
{
    int mat[N][N] = { { 1, 0, 0, 1, 1 },
                      { 0, 1, 0, 1, 0 },
                      { 0, 0, 1, 1, 1 },
                      { 1, 1, 1, 0, 1 },
                      { 1, 0, 1, 1, 0 } };

    cout << isbinaryMatrixPalindrome(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

public class GFG {

    final static int N = 5;

    // Function to check if the matrix is
    // palindrome or not
    static String isbinaryMatrixPalindrome(int mat[][])
    {

        // Traverse the matrix and check if
        // top right and bottom left elements
        // have same value
        for (int i = 0; i < N - 1; i++) {
            for (int j = N - 1; j > i; j--) {

                // If top right element is not
                // equal to the bottom left
                // element return false
                if (mat[i][j] != mat[j][i]) {
                    return "Np";
                }
            }
        }

        return "Yes";
    }

    // Driver Code
    public static void main (String[] args) {

        int mat[][] = { { 1, 0, 0, 1, 1 },
                          { 0, 1, 0, 1, 0 },
                          { 0, 0, 1, 1, 1 },
                          { 1, 1, 1, 0, 1 },
                          { 1, 0, 1, 1, 0 } };

        System.out.println(isbinaryMatrixPalindrome(mat));
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# python program for the above approach
N = 5

# Function to check if the matrix is
# palindrome or not
def isbinaryMatrixPalindrome(mat):

    # Traverse the matrix and check if
    # top right and bottom left elements
    # have same value
    for i in range(0, N - 1):
        for j in range(N - 1, i, -1):

            # If top right element is not
            # equal to the bottom left
            # element return false
            if (mat[i][j] != mat[j][i]):
                return "No"

    return "Yes"

# Driver Code
if __name__ == "__main__":

    mat = [[1, 0, 0, 1, 1],
           [0, 1, 0, 1, 0],
           [0, 0, 1, 1, 1],
           [1, 1, 1, 0, 1],
           [1, 0, 1, 1, 0]]
    print(isbinaryMatrixPalindrome(mat))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
public class GFG {

    static int N = 5;

    // Function to check if the matrix is
    // palindrome or not
    static string isbinaryMatrixPalindrome(int [,]mat)
    {

        // Traverse the matrix and check if
        // top right and bottom left elements
        // have same value
        for (int i = 0; i < N - 1; i++) {
            for (int j = N - 1; j > i; j--) {

                // If top right element is not
                // equal to the bottom left
                // element return false
                if (mat[i, j] != mat[j, i]) {
                    return "Np";
                }
            }
        }

        return "Yes";
    }

    // Driver Code
    public static void Main (string[] args) {

        int [,]mat = { { 1, 0, 0, 1, 1 },
                          { 0, 1, 0, 1, 0 },
                          { 0, 0, 1, 1, 1 },
                          { 1, 1, 1, 0, 1 },
                          { 1, 0, 1, 1, 0 } };

        Console.WriteLine(isbinaryMatrixPalindrome(mat));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

let N = 5;

// Function to check if the matrix is
// palindrome or not
function isbinaryMatrixPalindrome(mat)
{

  // Traverse the matrix and check if
  // top right and bottom left elements
  // have same value
  for (let i = 0; i < N - 1; i++)
  {
    for (let j = N - 1; j > i; j--)
    {

      // If top right element is not
      // equal to the bottom left
      // element return false
      if (mat[i][j] != mat[j][i]) {
        return "Np";
      }
    }
  }

  return "Yes";
}

// Driver Code

let mat = [
  [1, 0, 0, 1, 1],
  [0, 1, 0, 1, 0],
  [0, 0, 1, 1, 1],
  [1, 1, 1, 0, 1],
  [1, 0, 1, 1, 0],
];

document.write(isbinaryMatrixPalindrome(mat));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*