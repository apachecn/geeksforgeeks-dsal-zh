# 1 和 0 个数相等的最大面积矩形子矩阵

> 原文:[https://www . geesforgeks . org/最大面积-矩形-子矩阵-等数-1s-0s/](https://www.geeksforgeeks.org/largest-area-rectangular-sub-matrix-equal-number-1s-0s/)

给定一个二元矩阵。问题是寻找 1 和 0 相等的面积最大的矩形子矩阵。

示例:

```
Input : mat[][] = { {0, 0, 1, 1},
                    {0, 1, 1, 0},
                    {1, 1, 1, 0},
                    {1, 0, 0, 1} }
Output : 8 sq. units
(Top, left): (0, 0)
(Bottom, right): (3, 1)

Input : mat[][] = { {0, 0, 1, 1},
                    {0, 1, 1, 1} }            
Output : 6 sq. units

```

这个问题的**天真的解决方案**是通过计算给定 2D 阵列中 1 和 0 的总数来检查该矩形中的每个可能的矩形。该解决方案需要 4 个嵌套循环，并且该解决方案的时间复杂度是 O(n^4).

一个**有效的解决方案**基于[最大的矩形子矩阵，其和为 0](https://www.geeksforgeeks.org/largest-rectangular-sub-matrix-whose-sum-0/) ,这降低了 O(n^3).的时间复杂度首先，将矩阵中的每一个“0”视为“-1”。现在的想法是把问题简化为一维数组。我们一个接一个地固定左列和右列，并为每个左列和右列对找到具有 0 个总和连续行的最大子阵列。我们基本上为每个固定的左右列对找到顶部和底部的行号(它们的和为零)。要查找上下行号，请从左到右计算每行中元素的总和，并将这些总和存储在一个数组中，比如 temp[]。所以 temp[i]表示第 I 行从左到右元素的和，如果我们在 temp[]中找到和为 0 的最大子阵，就可以得到和等于 0(即 1 和 0 的个数相等)的矩形子阵的索引位置。通过这个过程，我们可以找到和等于 0(即 1 和 0 的个数相等)的面积最大的矩形子矩阵。我们可以利用哈希技术在一维数组中找到和等于 0 的最大长度子数组。

```
// C++ implementation to find largest area rectangular
// submatrix with equal number of 1's and 0's
#include <bits/stdc++.h>

using namespace std;

#define MAX_ROW 10
#define MAX_COL 10

// This function basically finds largest 0
// sum subarray in arr[0..n-1]. If 0 sum
// does't exist, then it returns false. Else
// it returns true and sets starting and
// ending indexes as start and end.
bool subArrWithSumZero(int arr[], int &start, 
                              int &end, int n)
{
    // to store cumulative sum
    int sum[n];

    // Initialize all elements of sum[] to 0
    memset(sum, 0, sizeof(sum));

    // map to store the indexes of sum
    unordered_map<int, int> um;

    // build up the cumulative sum[] array
    sum[0] = arr[0];
    for (int i=1; i<n; i++)
        sum[i] = sum[i-1] + arr[i];

    // to store the maximum length subarray
    // with sum equal to 0
    int maxLen = 0;

    // traverse to the sum[] array
    for (int i=0; i<n; i++)    
    {
        // if true, then there is a subarray
        // with sum equal to 0 from the
        // beginning up to index 'i'
        if (sum[i] == 0)
        {
            // update the required variables
            start = 0; 
            end = i;
            maxLen = (i+1);
        }

        // else if true, then sum[i] has not 
        // seen before in 'um'
        else if (um.find(sum[i]) == um.end())
            um[sum[i]] = i;

        // sum[i] has been seen before in the
        // unordered_map 'um'    
        else
        {
            // if previous subarray length is smaller
            // than the current subarray length, then
            // update the required variables
            if (maxLen < (i-um[sum[i]]))
            {
                maxLen = (i-um[sum[i]]);
                start = um[sum[i]] + 1;
                end = i;
            }
        }    
    }    

    // if true, then there is no
    // subarray with sum equal to 0
    if (maxLen == 0)
        return false;

    // else return true    
    return true;    
}

// function to find largest area rectangular
// submatrix with equal number of 1's and 0's
void maxAreaRectWithSumZero(int mat[MAX_ROW][MAX_COL], 
                                    int row, int col)
{
    // to store intermediate values
    int temp[row], startRow, endRow;

    // to store the final outputs
    int finalLeft, finalRight, finalTop, finalBottom;
    finalLeft = finalRight = finalTop = finalBottom = -1;
    int maxArea = 0;

    // Set the left column    
    for (int left = 0; left < col; left++)
    {
        // Initialize all elements of temp as 0
        memset(temp, 0, sizeof(temp));

        // Set the right column for the left column
        // set by outer loop
        for (int right = left; right < col; right++)
        {
            // Calculate sum between current left
            // and right for every row 'i'
            // consider value '1' as '1' and
            // value '0' as '-1'
            for (int i=0; i<row; i++)
                temp[i] += mat[i][right] ? 1 : -1;

            // Find largest subarray with 0 sum in
            // temp[]. The subArrWithSumZero() function 
            // also sets values of finalTop, finalBottom,
            // finalLeft and finalRight if there exists
            // a subarray with sum 0 in temp
            if (subArrWithSumZero(temp, startRow, endRow, row))
            {
                int area = (right - left + 1) * 
                                       (endRow - startRow + 1);

                // Compare current 'area' with previous area
                // and accodingly update final values
                if (maxArea < area)
                {
                    finalTop = startRow;
                    finalBottom = endRow;
                    finalLeft = left;
                    finalRight = right;                    
                    maxArea = area;
                }
            }
        }
    }

    // if true then there is no rectangular submatrix
    // with equal number of 1's and 0's
    if (maxArea == 0)
        cout << "No such rectangular submatrix exists:";

    // displaying the top left and bottom right boundaries
    // with the area of the rectangular submatrix    
    else
    {
        cout << "(Top, Left): " 
             << "(" << finalTop << ", " << finalLeft
             << ")" << endl; 

        cout << "(Bottom, Right): " 
             << "(" << finalBottom << ", " << finalRight 
             << ")" << endl;      

        cout << "Area: " << maxArea << " sq.units";     
    }
}

// Driver program to test above
int main()
{
    int mat[MAX_ROW][MAX_COL] = { {0, 0, 1, 1},
                                    {0, 1, 1, 0},
                                    {1, 1, 1, 0},
                                  {1, 0, 0, 1} };    
    int row = 4, col = 4;
    maxAreaRectWithSumZero(mat, row, col);
    return 0;                      

} 
```

输出:

```
(Top, Left): (0, 0)
(Bottom, Right): (3, 1)
Area: 8 sq.units

```

时间复杂度:O(n <sup>3</sup> )
辅助空间:O(n)

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。