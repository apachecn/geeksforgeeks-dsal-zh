# 找到 1 的最大矩形，并允许交换列

> 原文： [https://www.geeksforgeeks.org/find-the-largest-rectangle-of-1s-with-swapping-of-columns-allowed/](https://www.geeksforgeeks.org/find-the-largest-rectangle-of-1s-with-swapping-of-columns-allowed/)

给定具有 0 和 1 的矩阵，请找到矩阵中所有 1 的最大矩形。 可以通过交换给定矩阵的任何一对列来形成矩形。

**示例**：

```
Input: bool mat[][] = { {0, 1, 0, 1, 0},
                        {0, 1, 0, 1, 1},
                        {1, 1, 0, 1, 0}
                      };
Output: 6
The largest rectangle's area is 6\. The rectangle 
can be formed by swapping column 2 with 3
The matrix after swapping will be
     0 0 1 1 0
     0 0 1 1 1
     1 0 1 1 0

Input: bool mat[R][C] = { {0, 1, 0, 1, 0},
                         {0, 1, 1, 1, 1},
                         {1, 1, 1, 0, 1},
                         {1, 1, 1, 1, 1}
                      };
Output: 9

```



想法是使用辅助矩阵存储每列中连续 1 的计数。 一旦有了这些计数，便以非递增的计数顺序对辅助矩阵的所有行进行排序。 最后遍历排序的行以找到最大面积。

注意：形成辅助矩阵后，每一行都变得独立，因此我们可以独立地交换或排序每一行。这是因为我们只能交换列，因此我们使每一行独立，并找到了矩形的最大面积 行和列。

以下是上述第一个示例的详细步骤。

**步骤 1**：首先，计算编号。 每列中的连续 1 个。 辅助数组`hist[][]`用于存储连续 1 的计数。 因此，对于上述第一个示例，`hist[R][C]`的内容为：

```
    0 1 0 1 0
    0 2 0 2 1
    1 3 0 3 0
```

此步骤的时间复杂度为`O(R * C)`。

**步骤 2**：以非递增方式对列进行排序。 排序步骤后，矩阵`hist[][]`将为：

```
    1 1 0 0 0
    2 2 1 0 0
    3 3 1 0 0
```

此步骤可以在`O(R *(R + C))`中完成。 因为我们知道值的范围是 0 到`R`，所以我们可以对每一行使用计数排序。

排序实际上是列的交换。 如果我们看步骤 2 的第三行：`3 3 1 0 0`。

排序的行对应于交换列，以便将具有最高可能矩形的列放在最前面，然后是 第二高的矩形，依此类推。 因此，在该示例中，有 2 列可以形成一个高度 3 的矩形。这使面积为`3 * 2 = 6`。 如果我们尝试使矩形变宽，则高度会降低到 1，因为没有剩余的列允许在第三行上有更高的矩形。

**步骤 3**：遍历`hist[][]`的每一行并检查最大面积。 由于每一行都按 1 的计数排序，因此可以通过将列数乘以`hist[i][j]`中的值来计算当前区域。 此步骤还需要`O(R * C)`时间。

下面是基于以上思想的实现。

## C++ 

```cpp

// C++ program to find the largest rectangle of 1's with swapping 
// of columns allowed. 
#include <bits/stdc++.h> 
#define R 3 
#define C 5 

using namespace std; 

// Returns area of the largest rectangle of 1's 
int maxArea(bool mat[R][C]) 
{ 
    // An auxiliary array to store count of consecutive 1's 
    // in every column. 
    int hist[R + 1][C + 1]; 

    // Step 1: Fill the auxiliary array hist[][] 
    for (int i = 0; i < C; i++) { 
        // First row in hist[][] is copy of first row in mat[][] 
        hist[0][i] = mat[0][i]; 

        // Fill remaining rows of hist[][] 
        for (int j = 1; j < R; j++) 
            hist[j][i] = (mat[j][i] == 0) ? 0 : hist[j - 1][i] + 1; 
    } 

    // Step 2: Sort columns of hist[][] in non-increasing order 
    for (int i = 0; i < R; i++) { 
        int count[R + 1] = { 0 }; 

        // counting occurrence 
        for (int j = 0; j < C; j++) 
            count[hist[i][j]]++; 

        // Traverse the count array from right side 
        int col_no = 0; 
        for (int j = R; j >= 0; j--) { 
            if (count[j] > 0) { 
                for (int k = 0; k < count[j]; k++) { 
                    hist[i][col_no] = j; 
                    col_no++; 
                } 
            } 
        } 
    } 

    // Step 3: Traverse the sorted hist[][] to find maximum area 
    int curr_area, max_area = 0; 
    for (int i = 0; i < R; i++) { 
        for (int j = 0; j < C; j++) { 
            // Since values are in decreasing order, 
            // The area ending with cell (i, j) can 
            // be obtained by multiplying column number 
            // with value of hist[i][j] 
            curr_area = (j + 1) * hist[i][j]; 
            if (curr_area > max_area) 
                max_area = curr_area; 
        } 
    } 
    return max_area; 
} 

// Driver program 
int main() 
{ 
    bool mat[R][C] = { { 0, 1, 0, 1, 0 }, 
                       { 0, 1, 0, 1, 1 }, 
                       { 1, 1, 0, 1, 0 } }; 
    cout << "Area of the largest rectangle is " << maxArea(mat); 
    return 0; 
} 

```