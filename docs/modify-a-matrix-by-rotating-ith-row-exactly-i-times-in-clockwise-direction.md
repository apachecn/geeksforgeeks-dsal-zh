# 通过顺时针方向旋转第一行正好 I 次来修改矩阵

> 原文:[https://www . geesforgeks . org/通过顺时针方向旋转一行精确 I 次来修改矩阵/](https://www.geeksforgeeks.org/modify-a-matrix-by-rotating-ith-row-exactly-i-times-in-clockwise-direction/)

给定一个尺寸为 **M * N** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**mat【】【】【】**，任务是将矩阵 **i** 每顺时针旋转**I<sup>th</sup>T9】次后得到的矩阵打印出来。**

**示例:**

> **输入:** mat[][] = {{1，2，3}，{4，5，6}，{7，8，9}}
> **输出:**
> 1 2 3
> 6 4 5
> 8 9 7
> **说明:**
> 第 0<sup>行旋转 0 次。因此，第 0<sup>行保持与{1，2，3}相同。
> 1<sup>ST</sup>排旋转 1 次。因此，1 <sup>st</sup> 行修改为{6，4，5}。
> 第 2 排<sup>旋转 2 次。因此，第 2<sup>行修改为{8，9，7}。
> 完成上述操作后，给定矩阵修改为{{1，2，3}，{6，4，5}，{8，9，7}}。</sup></sup></sup></sup>
> 
> **输入:** mat[][] = {{1，2，3，4}，{4，5，6，7}，{7，8，9，8}，{7，8，9，8}}
> **输出:**
> 1 2 3 4
> 7 4 5 6
> 9 8 7 8
> 8 9 8 7

**方法:**按照以下步骤解决问题:

*   [以逐行方式遍历给定矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)，对于每一个 **i <sup>第</sup>行**，执行以下步骤:
    *   [反转矩阵的当前行](https://www.geeksforgeeks.org/program-to-reverse-the-rows-in-a-2d-array/)。
    *   反转当前行的第一个 **i** 柠檬。
    *   反转当前行的最后一个**(N–I)**元素，其中 **N** 是当前行的大小。
*   完成以上步骤后，[打印矩阵](https://www.geeksforgeeks.org/print-2-d-array-matrix-java/) **mat[][]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to rotate every i-th
// row of the matrix i times
void rotateMatrix(vector<vector<int> >& mat)
{
    int i = 0;

    // Traverse the matrix row-wise
    for (auto& it : mat) {

        // Reverse the current row
        reverse(it.begin(), it.end());

        // Reverse the first i elements
        reverse(it.begin(), it.begin() + i);

        // Reverse the last (N - i) elements
        reverse(it.begin() + i, it.end());

        // Increment count
        i++;
    }

    // Print final matrix
    for (auto rows : mat) {
        for (auto cols : rows) {
            cout << cols << " ";
        }
        cout << "\n";
    }
}

// Driver Code
int main()
{
    vector<vector<int> > mat
        = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };
    rotateMatrix(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Function to reverse arr[] from start to end
  static void reverse(int arr[], int start, int end)
  {
    while (start < end) {
      int temp = arr[start];
      arr[start] = arr[end];
      arr[end] = temp;
      start++;
      end--;
    }
  }

  // Function to rotate every i-th
  // row of the matrix i times
  static void rotateMatrix(int mat[][])
  {
    int i = 0;

    // Traverse the matrix row-wise
    for (int rows[] : mat) {

      // Reverse the current row
      reverse(rows, 0, rows.length - 1);

      // Reverse the first i elements
      reverse(rows, 0, i - 1);

      // Reverse the last (N - i) elements
      reverse(rows, i, rows.length - 1);

      // Increment count
      i++;
    }

    // Print final matrix
    for (int rows[] : mat) {
      for (int cols : rows) {
        System.out.print(cols + " ");
      }
      System.out.println();
    }
  }

  // Driver Code
  public static void main(String[] args)
  {

    int mat[][] = { { 1, 2, 3 },
                   { 4, 5, 6 },
                   { 7, 8, 9 } };

    rotateMatrix(mat);
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to rotate every i-th
# row of the matrix i times
def rotateMatrix(mat):

    i = 0
    mat1 = []

    # Traverse the matrix row-wise
    for it in mat:

        # Reverse the current row
        it.reverse()

        # Reverse the first i elements
        it1 = it[:i]
        it1.reverse()

        # Reverse the last (N - i) elements
        it2 = it[i:]
        it2.reverse()

        # Increment count
        i += 1
        mat1.append(it1 + it2)

    # Print final matrix
    for rows in mat1:
        for cols in rows:
            print(cols, end = " ")

        print()

# Driver Code
if __name__ == "__main__":

    mat = [ [ 1, 2, 3 ], [ 4, 5, 6 ], [ 7, 8, 9 ] ]

    rotateMatrix(mat)

# This code is contributed by ukasp
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function to reverse arr[] from start to end
function  reverse(arr,start,end)
{
    while (start < end) {
      let temp = arr[start];
      arr[start] = arr[end];
      arr[end] = temp;
      start++;
      end--;
    }
}

 // Function to rotate every i-th
  // row of the matrix i times
function rotateMatrix(mat)
{
    let i = 0;

    // Traverse the matrix row-wise
    for (let rows=0;rows<mat.length;rows++) {

      // Reverse the current row
      reverse(mat[rows], 0, mat[rows].length - 1);

      // Reverse the first i elements
      reverse(mat[rows], 0, i - 1);

      // Reverse the last (N - i) elements
      reverse(mat[rows], i, mat[rows].length - 1);

      // Increment count
      i++;
    }

    // Print final matrix
    for (let rows=0;rows< mat.length;rows++) {
      for (let cols=0;cols< mat[rows].length;cols++) {
        document.write(mat[rows][cols] + " ");
      }
      document.write("<br>");
    }
}

// Driver Code
let mat=[[ 1, 2, 3 ],
                   [ 4, 5, 6 ],
                   [ 7, 8, 9 ]];
rotateMatrix(mat);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
1 2 3 
6 4 5 
8 9 7
```

***时间复杂度:** O(M * N)*
***辅助空间:** O(1)*