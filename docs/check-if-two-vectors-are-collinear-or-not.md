# 检查两个矢量是否共线

> 原文:[https://www . geeksforgeeks . org/check-如果两个向量共线或不共线/](https://www.geeksforgeeks.org/check-if-two-vectors-are-collinear-or-not/)

给定代表两个向量的 **x** 、 **y** 和 **z** 坐标的六个整数，任务是检查两个给定向量是否[共线](https://www.geeksforgeeks.org/program-check-three-points-collinear/)。

**示例:**

> **输入:** x1 = 4，y1 = 8，z1 = 12，x2 = 8，y2 = 16，z2 = 24
> **输出:**是
> **说明:**给定向量:4i + 8j + 12k 和 8i + 16j + 24k 共线。
> 
> **输入:** x1 = 2，y1 = 8，z1 = -4，x2 = 4，y2 = 16，z2 = 8
> **输出:**否
> **说明:**给定向量:2i+8j–4k 和 4i + 16j + 8k 不共线。

**方法:**如果满足以下任一条件，则可以基于两个向量共线的思想来解决问题:

*   如果存在数字 **n** ，则两个向量 **A** 和 **B** 共线，使得 **A** = **n** **b.**
*   如果两个向量的坐标关系相等，则两个向量共线，即 **x1 / x2 = y1 / y2 = z1 / z2** 。
    ***注:**如果向量的一个分量为零，则该条件无效。*
*   如果两个向量的[叉积](https://www.geeksforgeeks.org/program-dot-product-cross-product-two-vector/)等于 [*零向量*](https://en.wikipedia.org/wiki/Null_vector) ，则两个向量共线。

因此，解决问题的思路是检查两个给定向量的[叉积是否等于](https://www.geeksforgeeks.org/program-dot-product-cross-product-two-vector/) [*空向量*](https://en.wikipedia.org/wiki/Null_vector) 。如果发现为真，则打印**是**。否则，打印**否**。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate cross
// product of two vectors
void crossProduct(int vect_A[],
                  int vect_B[],
                  int cross_P[])
{
    // Update cross_P[0]
    cross_P[0]
        = vect_A[1] * vect_B[2]
          - vect_A[2] * vect_B[1];

    // Update cross_P[1]
    cross_P[1]
        = vect_A[2] * vect_B[0]
          - vect_A[0] * vect_B[2];

    // Update cross_P[2]
    cross_P[2]
        = vect_A[0] * vect_B[1]
          - vect_A[1] * vect_B[0];
}

// Function to check if two given
// vectors are collinear or not
void checkCollinearity(int x1, int y1,
                       int z1, int x2,
                       int y2, int z2)
{
    // Store the first and second vectors
    int A[3] = { x1, y1, z1 };
    int B[3] = { x2, y2, z2 };

    // Store their cross product
    int cross_P[3];

    // Calculate their cross product
    crossProduct(A, B, cross_P);

    // Check if their cross product
    // is a NULL Vector or not
    if (cross_P[0] == 0 && cross_P[1] == 0
        && cross_P[2] == 0)
        cout << "Yes";
    else
        cout << "No";
}

// Driver Code
int main()
{
    // Given coordinates
    // of the two vectors
    int x1 = 4, y1 = 8, z1 = 12;
    int x2 = 8, y2 = 16, z2 = 24;

    checkCollinearity(x1, y1, z1,
                      x2, y2, z2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to calculate cross
// product of two vectors
static void crossProduct(int vect_A[],
                         int vect_B[],
                         int cross_P[])
{

    // Update cross_P[0]
    cross_P[0] = vect_A[1] * vect_B[2] -
                 vect_A[2] * vect_B[1];

    // Update cross_P[1]
    cross_P[1] = vect_A[2] * vect_B[0] -
                 vect_A[0] * vect_B[2];

    // Update cross_P[2]
    cross_P[2] = vect_A[0] * vect_B[1] -
                 vect_A[1] * vect_B[0];
}

// Function to check if two given
// vectors are collinear or not
static void checkCollinearity(int x1, int y1,
                              int z1, int x2,
                              int y2, int z2)
{

    // Store the first and second vectors
    int A[] = { x1, y1, z1 };
    int B[] = { x2, y2, z2 };

    // Store their cross product
    int cross_P[] = new int[3];

    // Calculate their cross product
    crossProduct(A, B, cross_P);

    // Check if their cross product
    // is a NULL Vector or not
    if (cross_P[0] == 0 && cross_P[1] == 0 &&
        cross_P[2] == 0)
        System.out.print("Yes");
    else
        System.out.print("No");
}

// Driver Code
public static void main (String[] args)
{

    // Given coordinates
    // of the two vectors
    int x1 = 4, y1 = 8, z1 = 12;
    int x2 = 8, y2 = 16, z2 = 24;

    checkCollinearity(x1, y1, z1,
                      x2, y2, z2);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate cross
# product of two vectors
def crossProduct(vect_A, vect_B, cross_P):
    # Update cross_P[0]
    cross_P[0] = (vect_A[1] * vect_B[2] -
                  vect_A[2] * vect_B[1])

    # Update cross_P[1]
    cross_P[1] = (vect_A[2] * vect_B[0] -
                  vect_A[0] * vect_B[2])

    # Update cross_P[2]
    cross_P[2] = (vect_A[0] * vect_B[1] -
                  vect_A[1] * vect_B[0])

# Function to check if two given
# vectors are collinear or not
def checkCollinearity(x1, y1, z1, x2, y2, z2):

    # Store the first and second vectors
    A = [x1, y1, z1]
    B = [x2, y2, z2]

    # Store their cross product
    cross_P = [0 for i in range(3)]

    # Calculate their cross product
    crossProduct(A, B, cross_P)

    # Check if their cross product
    # is a NULL Vector or not
    if (cross_P[0] == 0 and
        cross_P[1] == 0 and
        cross_P[2] == 0):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    # Given coordinates
    # of the two vectors
    x1 = 4
    y1 = 8
    z1 = 12
    x2 = 8
    y2 = 16
    z2 = 24

    checkCollinearity(x1, y1, z1, x2, y2, z2)

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate cross
// product of two vectors
static void crossProduct(int []vect_A,
                         int []vect_B,
                         int []cross_P)
{

    // Update cross_P[0]
    cross_P[0] = vect_A[1] * vect_B[2] -
                 vect_A[2] * vect_B[1];

    // Update cross_P[1]
    cross_P[1] = vect_A[2] * vect_B[0] -
                 vect_A[0] * vect_B[2];

    // Update cross_P[2]
    cross_P[2] = vect_A[0] * vect_B[1] -
                 vect_A[1] * vect_B[0];
}

// Function to check if two given
// vectors are collinear or not
static void checkCollinearity(int x1, int y1,
                              int z1, int x2,
                              int y2, int z2)
{

    // Store the first and second vectors
    int []A = { x1, y1, z1 };
    int []B = { x2, y2, z2 };

    // Store their cross product
    int []cross_P = new int[3];

    // Calculate their cross product
    crossProduct(A, B, cross_P);

    // Check if their cross product
    // is a NULL Vector or not
    if (cross_P[0] == 0 && cross_P[1] == 0 &&
        cross_P[2] == 0)
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver Code
public static void Main (string[] args)
{

    // Given coordinates
    // of the two vectors
    int x1 = 4, y1 = 8, z1 = 12;
    int x2 = 8, y2 = 16, z2 = 24;

    checkCollinearity(x1, y1, z1,
                      x2, y2, z2);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

        // Javascript program for the
        // above approach

        // Function to calculate cross
        // product of two vectors
        function crossProduct(vect_A,
            vect_B,
            cross_P) {
            // Update cross_P[0]
            cross_P[0]
                = vect_A[1] * vect_B[2]
                - vect_A[2] * vect_B[1];

            // Update cross_P[1]
            cross_P[1]
                = vect_A[2] * vect_B[0]
                - vect_A[0] * vect_B[2];

            // Update cross_P[2]
            cross_P[2]
                = vect_A[0] * vect_B[1]
                - vect_A[1] * vect_B[0];
        }

        // Function to check if two given
        // vectors are collinear or not
        function checkCollinearity(x1, y1,
            z1, x2,
            y2, z2) {
            // Store the first and second vectors
            let A = [x1, y1, z1];
            let B = [x2, y2, z2];

            // Store their cross product
            let cross_P = [];

            // Calculate their cross product
            crossProduct(A, B, cross_P);

            // Check if their cross product
            // is a NULL Vector or not
            if (cross_P[0] == 0 && cross_P[1] == 0
                && cross_P[2] == 0)
                document.write("Yes")
            else
                document.write("No")
        }

        // Driver Code

        // Given coordinates
        // of the two vectors
        let x1 = 4, y1 = 8, z1 = 12;
        let x2 = 8, y2 = 16, z2 = 24;

        checkCollinearity(x1, y1, z1,
            x2, y2, z2);

        // This code is contributed by Hritik

 </script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)