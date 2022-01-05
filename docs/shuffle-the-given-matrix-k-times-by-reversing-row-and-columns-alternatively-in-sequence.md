# 通过按顺序交替反转行和列，对给定矩阵进行 K 次洗牌

> 原文:[https://www . geesforgeks . org/shuffle-给定矩阵-k 次-按行和列反转-交替顺序/](https://www.geeksforgeeks.org/shuffle-the-given-matrix-k-times-by-reversing-row-and-columns-alternatively-in-sequence/)

给定一个大小为 **M * N** 的矩阵 **arr[][]** ，其中 **M** 是**行**的数量， **N** 是**列**的数量，以及一个整数 **K** 。任务是在 **K** 步中混洗该矩阵，使得在每一步中，**矩阵的行和列**交替反转，即从反转第一行第一步开始，然后反转第二步中的第一列，然后反转第三步中的第二行，以此类推。

**注意:**如果 **K** 超过 **M** 或 **N** ，则再次从第一行或第一列开始反转。

**示例:**

> **输入:** arr[][] = {{3，4，1，8}，
> {11，23，43，21}，
> {12，17，65，91}，
> {71，56，34，24}}
> K = 4
> **输出:** {{71，56，4，3}，
> {21，17，23，12}，
> 
> **输入:** arr[][] = {{11，23，43，21}，
> {12，17，65，91}，
> {71，56，34，24}}
> K = 8
> **输出:** {{11，43，56，21}，
> {91，65，17，12}，
> {24，34，23，71}

**方法:**只需运行两个循环交替遍历行和列，直到 **K** 变为 0，即可解决问题。最后，打印结果矩阵。遵循以下步骤:

*   运行遍历矩阵的循环。
*   在每次迭代中，反转适当的行和列。
*   做这个操作 K 次。
*   打印最后一个循环。

下面是上述方法的实现

## C++

```
// C++ code to implement the above approach
#include <bits/stdc++.h>
using namespace std;
const int M = 3;
const int N = 4;

// Print matrix elements
void showArray(int arr[][N])
{
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++)
            cout << arr[i][j] << " ";
        cout << endl;
    }
}

// Function to shuffle matrix
void reverseAlternate(int arr[][N], int K)
{
    int turn = 0;
    int row = 0, col = 0;
    while (turn < K) {

        // Reverse the row
        if (turn % 2 == 0) {
            int start = 0, end = N - 1, temp;
            while (start < end) {
                temp = arr[row % M][start];
                arr[row % M][start] = 
                    arr[row % M][end];
                arr[row % M][end] = temp;
                start += 1;
                end -= 1;
            }
            row++;
            turn++;
        }

        // Reverse the column
        else {
            int start = 0, end = M - 1, temp;
            while (start < end) {
                temp = arr[start][col % N];
                arr[start][col % N] = 
                    arr[end][col % N];
                arr[end][col % N] = temp;
                start += 1;
                end -= 1;
            }
            col++;
            turn++;
        }
    }
}

// Driver code
int main()
{

    int matrix[M][N] = { { 11, 23, 43, 21 },
                         { 12, 17, 65, 91 },
                         { 71, 56, 34, 24 } };
    int K = 8;
    reverseAlternate(matrix, K);
    showArray(matrix);
    return 0;
}
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach
       let M = 3;
       let N = 4;

       // Print matrix elements
       function showArray(arr) {
           for (let i = 0; i < M; i++) {
               for (let j = 0; j < N; j++)
                   document.write(arr[i][j] + " ");
               document.write('<br>');
           }
       }

       // Function to shuffle matrix
       function reverseAlternate(arr, K) {
           let turn = 0;
           let row = 0, col = 0;
           while (turn < K) {

               // Reverse the row
               if (turn % 2 == 0) {
                   let start = 0, end = N - 1, temp;
                   while (start < end) {
                       temp = arr[row % M][start];
                       arr[row % M][start] =
                           arr[row % M][end];
                       arr[row % M][end] = temp;
                       start += 1;
                       end -= 1;
                   }
                   row++;
                   turn++;
               }

               // Reverse the column
               else {
                   let start = 0, end = M - 1, temp;
                   while (start < end) {
                       temp = arr[start][col % N];
                       arr[start][col % N] =
                           arr[end][col % N];
                       arr[end][col % N] = temp;
                       start += 1;
                       end -= 1;
                   }
                   col++;
                   turn++;
               }
           }
       }

       // Driver code
       let matrix = [[11, 23, 43, 21],
       [12, 17, 65, 91],
       [71, 56, 34, 24]];
       let K = 8;
       reverseAlternate(matrix, K);
       showArray(matrix);

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
11 43 56 21 
91 65 17 12 
24 34 23 71 
```

***时间复杂度:*** O(K * max(M，N))
***辅助空间:*** O(1)