# 使用地图数据结构对 2D 矢量进行对角排序

> 原文:[https://www . geesforgeks . org/sort-a-2d-vector-对角使用-map-data-structure/](https://www.geeksforgeeks.org/sort-a-2d-vector-diagonally-using-map-data-structure/)

给定整数的 2D 向量**mat[][]**。任务是按照从左上方到右下方的递增顺序对向量的元素进行对角排序。
**例:**

```
Input: mat[][] = 
{{9, 4, 2}, 
 {7, 4, 6},
 {2, 3, 3}}     
Output: 
3 4 2
3 4 6
2 7 9
Explanation:
There are 5 diagonals in this matrix:
1\. {2} - No need to sort
2\. {7, 3} - Sort - {3, 7}
3\. {9, 4, 3} - Sort - {3, 4, 9}
4\. {4, 6} - Already sorted
5\. {2} - No need to sort

Input: mat[][] =  
{{ 4, 3, 2, 1 }, 
 { 3, 2, 1, 0 }, 
 { 2, 1, 1, 0 }, 
 { 0, 1, 2, 3 }}
Output: 
1 0 0 1 
1 2 1 2 
1 2 3 3 
0 2 3 4 
```

**进场:**

1.  同一对角线上的所有元素具有相同的索引差异**I–j**，其中 I 是行号，j 是列号。因此，我们可以使用地图来存储索引 I–j .
    的每一条对角线
2.  现在，我们可以使用内置函数对地图的每个索引进行排序。

3.  现在在原始矩阵中，我们可以插入存储在 map 中的矩阵的每一条对角线。

4.  最后，我们可以打印矩阵。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation to sort the
// diagonals of the matrix

#include <bits/stdc++.h>
using namespace std;

// Function to sort the
// diagonal of the matrix
void SortDiagonal(int mat[4][4],
                  int m, int n)
{
    // Map to store every diagonal
    // in different indices here
    // elements of same diagonal
    // will be stored in same index
    unordered_map<int, vector<int> > mp;

    for (int i = 0; i < m; i++)
    {
        for (int j = 0; j < n; j++)
        {
            // Storing diagonal elements
            // in map
            mp[i - j].push_back(mat[i][j]);
        }
    }

    // To sort each diagonal in
    // ascending order
    for (int k = -(n - 1); k < m; k++)
    {
        sort(mp[k].begin(),
             mp[k].end());
    }

    // Loop to store every diagonal
    // in ascending order
    for (int i = m - 1; i >= 0; i--)
    {
        for (int j = n - 1; j >= 0; j--)
        {
            mat[i][j] = mp[i - j].back();
            mp[i - j].pop_back();
        }
    }

    // Loop to print the matrix
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++)
            cout << mat[i][j] << " ";
        cout << endl;
    }
}

// Driven Code
int main()
{
    int arr[4][4] = { { 4, 3, 2, 1 },
                    { 3, 2, 1, 0 },
                    { 2, 1, 1, 0 },
                    { 0, 1, 2, 3 } };

    // Sort the Diagonals
    SortDiagonal(arr, 4, 4);

    return 0;
}
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to sort the
// diagonal of the matrix
function SortDiagonal(mat, m, n)
{
    // Map to store every diagonal
    // in different indices here
    // elements of same diagonal
    // will be stored in same index
    var mp = {};
    for (var i = 0; i < m; i++)
    {
        for (var j = 0; j < n; j++)
        {
            mp[i - j] = [];
        }
     }

    for (var i = 0; i < m; i++)
    {
        for (var j = 0; j < n; j++)
        {
            // Storing diagonal elements
            // in map
            mp[i - j].push(mat[i][j]);
        }
    }

    // To sort each diagonal in
    // ascending order
    for (var k = -(n - 1); k < m; k++)
    {
        mp[k].sort();
    }

    // Loop to store every diagonal
    // in ascending order
    for (var i = m - 1; i >= 0; i--)
    {
        for (var j = n - 1; j >= 0; j--)
        {
            mat[i][j] = mp[i - j].pop();
        }
    }

    // Loop to print the matrix
    for (var i = 0; i < m; i++) {
        for (var j = 0; j < n; j++)
            document.write(mat[i][j] + " " );
        document.write("<br>");
    }
}

// Driver Code
var arr = [[ 4, 3, 2, 1 ],
    [ 3, 2, 1, 0 ],
    [ 2, 1, 1, 0 ],
    [ 0, 1, 2, 3 ]];

// Sort the Diagonals
SortDiagonal(arr, 4, 4);
</script>
```

**Output:** 

```
1 0 0 1 
1 2 1 2 
1 2 3 3 
0 2 3 4 
```