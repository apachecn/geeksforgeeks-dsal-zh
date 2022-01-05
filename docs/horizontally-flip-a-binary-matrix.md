# 水平翻转二进制矩阵

> 原文:[https://www . geeksforgeeks . org/水平翻转二进制矩阵/](https://www.geeksforgeeks.org/horizontally-flip-a-binary-matrix/)

给定一个二元矩阵。任务是水平翻转矩阵(找到矩阵的图像)，然后反转它。

**注**:

*   对**来说，水平翻转**矩阵意味着反转矩阵的每一行。例如，水平翻转[1，1，0，0]会产生[0，0，1，1]。
*   对**求逆**矩阵意味着用 1 替换每个 0，反之亦然。例如，反转[0，0，1]会产生[1，1，0]。

**示例**:

```
Input: mat[][] = [[1, 1, 0], 
                  [1, 0, 1], 
                  [0, 0, 0]]
Output: [[1, 0, 0], 
         [0, 1, 0], 
         [1, 1, 1]]
Explanation: 
First reverse each row: [[0, 1, 1], [1, 0, 1], [0, 0, 0]]
Then, invert the image: [[1, 0, 0], [0, 1, 0], [1, 1, 1]]

Input: mat[][] = [[1, 1, 0, 0], 
                  [1, 0, 0, 1], 
                  [0, 1, 1, 1], 
                  [1, 0, 1, 0]]
Output: [[1, 1, 0, 0], 
         [0, 1, 1, 0], 
         [0, 0, 0, 1], 
         [1, 0, 1, 0]]
Explanation: 
First reverse each row: 
[[0, 0, 1, 1], [1, 0, 0, 1], [1, 1, 1, 0], [0, 1, 0, 1]].
Then invert the image:
[[1, 1, 0, 0], [0, 1, 1, 0], [0, 0, 0, 1], [1, 0, 1, 0]]
```

**进场:**我们可以就地进行。仔细观察，可以推断出，在最终矩阵的每一行中，左边的第 I 个值等于输入二进制矩阵右边的第 I 个值的倒数。

因此，我们使用(Column + 1) / 2(带楼层划分)来迭代行前半部分的所有索引![i   ](img/c219860f95052b9f6ddef0ea3ab54389.png "Rendered by QuickLaTeX.com")，包括中心，并相应地更新答案。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 implementation of above approach
# Function to return final Image

def flipped_Invert_Image(mat):

    for row in mat:
        for i in range((len(row) + 1) // 2):

            row[i] = row[len(row) - 1 - i] ^ 1
            row[len(row) - 1 - i] = row[i] ^ 1

    # return Flipped and Inverted image
    return mat

# Driver code
mat = [[1, 1, 0, 0], [1, 0, 0, 1], [0, 1, 1, 1], [1, 0, 1, 0]]

print(flipped_Invert_Image(mat))
```

**Output:** 

```
[[1, 1, 0, 0], [0, 1, 0, 1], [0, 0, 1, 1], [1, 0, 1, 0]]
```

**时间复杂度:** O(N*M)，其中 N 为给定二进制矩阵中的行数，M 为列数。

## C++14

```
//c++ program to flip the binary image horizontally
#include<bits/stdc++.h>
using namespace std;
//function to flip the matrix using two pointer technique
vector<vector<int>> flip_matrix(vector<vector<int>>matrix)
{
    for(int i=0;i<matrix.size();i++)
         { 
             int left = 0;
             int right = matrix[i].size()-1;

             while( left <= right )
             {
                 //conditions executes if compared elements are not equal
                 if(matrix[i][left] == matrix[i][right])
                 {
                     // if element is 0 it becomes 1 if not it becomes 0
                     matrix[i][left] = 1-matrix[i][left];
                     matrix[i][right] = matrix[i][left];
                 }
                 left++;
                 right--;
             }
         }
         //return matrix
        return matrix;
}
//Drive code
int main()
{
    vector<vector<int>>matrix={{1,1,0},{1,0,1},{0,0,0}};
    vector<vector<int>>v=flip_matrix(matrix);
    for(int i=0;i<matrix.size();i++)
    {
        for(int j=0;j<matrix[i].size();j++)
        {
            cout<<v[i][j]<<" ";
        }
        cout<<'\n';
    }
}
```