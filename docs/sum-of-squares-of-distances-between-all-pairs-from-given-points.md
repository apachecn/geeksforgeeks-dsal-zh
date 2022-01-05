# 给定点所有对之间距离的平方和

> 原文:[https://www . geeksforgeeks . org/所有给定点对之间距离的平方和/](https://www.geeksforgeeks.org/sum-of-squares-of-distances-between-all-pairs-from-given-points/)

给定一个由 **XY 平面**上的 **N** 点的坐标组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是找出所有对点之间的平方距离之和，即**(X<sub>I</sub>–X<sub>j</sub>)<sup>2</sup>+(Y<sub>I</sub>–Y<sub>j</sub>)<sup>2</sup>**

**示例:**

> **输入:** arr[][] = {{1，1}，{-1，-1}，{1，-1}，{-1，1}}
> **输出:** 32
> **说明:**
> 距离第 1 <sup>st</sup> 点(1，1)距离第 2 <sup>nd</sup> ，第 3 <sup>rd</sup> 和第 4 <sup>th</sup> 点分别为 8、4 和 4。
> 第 2 <sup>点与第 3 <sup>点</sup>和第 4 <sup>点</sup>点的距离分别为 4 和 4。
> 3<sup>第</sup>点与 4 <sup>第</sup>点的距离为 8。
> 因此，总距离= (8 + 4 + 4) + (4 + 4) + (8) = 32</sup>
> 
> **输入:** arr[][] = {{1，1}，{1，1}，{0，0}}
> **输出:** 4
> **说明:**
> 1<sup>ST</sup>点到 2 <sup>nd</sup> 和 3 <sup>rd</sup> 点的距离分别为 0 和 2。
> 第二<sup>点与第三<sup>点的距离为 2。
> 因此，总距离= (0 + 2) + (2) = 4</sup></sup>

**天真方法:**解决问题最简单的方法是[生成给定数组的所有可能的不同对](https://www.geeksforgeeks.org/number-of-unique-pairs-in-an-array/)**arr【】【】**并计算所有对点(X <sub>i</sub> 、Y <sub>j</sub> )和(X <sub>j</sub> 、Y <sub>j</sub> )之间距离的平方和，即(X<sub>I</sub>–X<sub>j</sub>)

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**对上述方法进行优化，思路是将距离平方和重新分组，拆分为两个和。按照以下步骤解决问题:

*   初始化变量，比如 **xq** 、 **yq** 、 **xs** 和 **ys** 。
*   初始化一个变量，比如说 **res** ，用 **zero** 来存储结果和。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个点 **{x，y}** ，执行以下步骤:
    *   将变量 **res** 中**(I * x<sup>2</sup>+I * y<sup>2</sup>)**的值相加，对应平方距离的相加。
    *   将**(xq–2 * xs * a)**和**(yq–2 * ys * b)**加到 **res** 上，以抵消**(a–b)<sup>2</sup>**扩展中 2 * X * Y 的效果。
    *   将值**a<sup>2</sup>T3】和**b<sup>2</sup>T7】分别添加到变量 **xq** 和 **yq** 中。****
    *   将值 **a** 和 **b** 分别添加到变量 **xs** 和 **ys** 中。
    *   将数值 **xs** 和 **yq** 分别加到变量**a<sup>2</sup>T7】和**b<sup>2</sup>T11】中。****
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of squares
// of distance between all distinct pairs
void findSquareSum(
    int Coordinates[][2], int N)
{
    long long xq = 0, yq = 0;
    long long xs = 0, ys = 0;

    // Stores final answer
    long long res = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        int a, b;

        a = Coordinates[i][0];
        b = Coordinates[i][1];

        res += xq;
        res -= 2 * xs * a;

        // Adding the effect of this
        // point for all the previous
        // x - points
        res += i * (long long)(a * a);

        // Temporarily add the
        // square of x-coordinate
        xq += a * a;
        xs += a;
        res += yq;
        res -= 2 * ys * b;
        res += i * (long long)b * b;

        // Add the effect of this point
        // for all the previous y - points
        yq += b * b;
        ys += b;
    }

    // Print the desired answer
    cout << res;
}

// Driver Code
int main()
{
    int arr[][2] = { { 1, 1 },
                     { -1, -1 },
                     { 1, -1 },
                     { -1, 1 } };
    int N = sizeof(arr) / sizeof(arr[0]);
    findSquareSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

  // Function to find the sum of squares
  // of distance between all distinct pairs
  static void findSquareSum(
    int Coordinates[][], int N)
  {
    long xq = 0, yq = 0;
    long xs = 0, ys = 0;

    // Stores final answer
    long res = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {
      int a, b;

      a = Coordinates[i][0];
      b = Coordinates[i][1];

      res += xq;
      res -= 2 * xs * a;

      // Adding the effect of this
      // point for all the previous
      // x - points
      res += i * (long)(a * a);

      // Temporarily add the
      // square of x-coordinate
      xq += a * a;
      xs += a;
      res += yq;
      res -= 2 * ys * b;
      res += i * (long)b * b;

      // Add the effect of this point
      // for all the previous y - points
      yq += b * b;
      ys += b;
    }

    // Print the desired answer
    System.out.println(res);
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[][] = { { 1, 1 },
                   { -1, -1 },
                   { 1, -1 },
                   { -1, 1 } };
    int N = arr.length;
    findSquareSum(arr, N);
  }
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the sum of squares
# of distance between all distinct pairs
def findSquareSum(Coordinates, N):
    xq , yq = 0, 0
    xs , ys = 0, 0

    # Stores final answer
    res = 0

    # Traverse the array
    for i in range(N):

        a = Coordinates[i][0]
        b = Coordinates[i][1]

        res += xq
        res -= 2 * xs * a

        # Adding the effect of this
        # point for all the previous
        # x - points
        res += i * (a * a)

        # Temporarily add the
        # square of x-coordinate
        xq += a * a
        xs += a
        res += yq
        res -= 2 * ys * b
        res += i * b * b

        # Add the effect of this point
        # for all the previous y - points
        yq += b * b
        ys += b

    # Print the desired answer
    print (res)

# Driver Code
if __name__ == '__main__':
    arr = [ [ 1, 1 ],
         [ -1, -1 ],
         [ 1, -1 ],
         [ -1, 1 ] ]

    N = len(arr)

    findSquareSum(arr, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the sum of squares
// of distance between all distinct pairs
static void findSquareSum(int[,] Coordinates, int N)
{
    long xq = 0, yq = 0;
    long xs = 0, ys = 0;

    // Stores final answer
    long res = 0;

    // Traverse the array
    for(int i = 0; i < N ; i++)
    {
        int a, b;

        a = Coordinates[i, 0];
        b = Coordinates[i, 1];

        res += xq;
        res -= 2 * xs * a;

        // Adding the effect of this
        // point for all the previous

        // x - points
        res += i * (long)(a * a);

        // Temporarily add the
        // square of x-coordinate
        xq += a * a;
        xs += a;
        res += yq;
        res -= 2 * ys * b;
        res += i * (long)b * b;

        // Add the effect of this point
        // for all the previous y - points
        yq += b * b;
        ys += b;
    }

    // Print the desired answer
    Console.Write(res);
}

// Driver code
static void Main()
{
    int[,] arr = { { 1, 1 },
                   { -1, -1 },
                   { 1, -1 },
                   { -1, 1 } };
    int N = arr.GetLength(0);

    findSquareSum(arr, N);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// Javascript program for the above approach

  // Function to find the sum of squares
  // of distance between all distinct pairs
  function findSquareSum(
    Coordinates, N)
  {
    let xq = 0, yq = 0;
    let xs = 0, ys = 0;

    // Stores final answer
    let res = 0;

    // Traverse the array
    for (let i = 0; i < N; i++) {
      let a, b;

      a = Coordinates[i][0];
      b = Coordinates[i][1];

      res += xq;
      res -= 2 * xs * a;

      // Adding the effect of this
      // point for all the previous
      // x - points
      res += i * (a * a);

      // Temporarily add the
      // square of x-coordinate
      xq += a * a;
      xs += a;
      res += yq;
      res -= 2 * ys * b;
      res += i * b * b;

      // Add the effect of this point
      // for all the previous y - points
      yq += b * b;
      ys += b;
    }

    // Print the desired answer
    document.write(res);
  }

// Driver code

    let arr = [[ 1, 1 ],
               [ -1, -1 ],
               [ 1, -1 ],
               [ -1, 1 ]];
    let N = arr.length;
    findSquareSum(arr, N);

</script>
```

**Output:** 

```
32
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)