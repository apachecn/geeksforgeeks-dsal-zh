# 在 2D 阵列中找到一个峰值元素

> 原文:[https://www.geeksforgeeks.org/find-peak-element-2d-array/](https://www.geeksforgeeks.org/find-peak-element-2d-array/)

如果一个元素大于或等于它的四个相邻元素，即左、右、上和下，则它是一个峰值元素。例如，A[i][j]的邻居是 A[i-1][j]、A[i+1][j]、A[i][j-1]和 A[i][j+1]。对于角元素，缺少的邻居被认为是负无穷大值。
**例:**

```
Input : 10 20 15
        21 30 14
        7  16 32 
Output : 30
30 is a peak element because all its 
neighbors are smaller or equal to it. 
32 can also be picked as a peak.

Input : 10 7
        11 17
Output : 17
```

以下是关于这个问题的一些事实:
1:对角线相邻不被认为是邻居。
2:一个峰元素不一定是最大元素。
3:可以存在不止一种这样的元素。
4:总有峰元素。我们可以通过使用笔和纸创建一些矩阵来看到这个属性。
**方法一:(蛮力)**
迭代矩阵的所有元素，检查它是否大于/等于它的所有邻居。如果是，返回元素。
时间复杂度:O(行*列)
辅助空间:O(1)
**方法二:(高效)**
这个问题主要是[在 1D 阵](https://www.geeksforgeeks.org/find-a-peak-in-a-given-array/)中找峰元素的一个延伸。我们在此应用类似的基于二分搜索法的解决方案。

1.  考虑中柱，并在其中找到最大元素。
2.  让中间列的索引为“中间”，中间列中最大元素的值为“最大”，最大元素位于“mat[max_index][mid]”。

3.  如果最大值> = A[索引][中间 1] &最大值> = A[索引][选择+1]，则最大值为峰值，返回最大值。
4.  如果 max < mat[max_index][mid-1]，则对矩阵的左半部分重复。
5.  如果 max < mat[max_index][mid+1]，则对矩阵的右半部分重复。

以下是上述算法的实现:

## C++

```
// Finding peak element in a 2D Array.
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;

// Function to find the maximum in column 'mid'
// 'rows' is number of rows.
int findMax(int arr[][MAX], int rows, int mid, int& max)
{
    int max_index = 0;
    for (int i = 0; i < rows; i++) {
        if (max < arr[i][mid]) {
            // Saving global maximum and its index
            // to check its neighbours
            max = arr[i][mid];
            max_index = i;
        }
    }
    return max_index;
}

// Function to find a peak element
int findPeakRec(int arr[][MAX], int rows, int columns,
                int mid)
{
    // Evaluating maximum of mid column. Note max is
    // passed by reference.
    int max = 0;
    int max_index = findMax(arr, rows, mid, max);

    // If we are on the first or last column,
    // max is a peak
    if (mid == 0 || mid == columns - 1)
        return max;

    // If mid column maximum is also peak
    if (max >= arr[max_index][mid - 1] && max >= arr[max_index][mid + 1])
        return max;

    // If max is less than its left
    if (max < arr[max_index][mid - 1])
        return findPeakRec(arr, rows, columns, mid - ceil((double)mid / 2));

    // If max is less than its left
    // if (max < arr[max_index][mid+1])
    return findPeakRec(arr, rows, columns, mid + ceil((double)mid / 2));
}

// A wrapper over findPeakRec()
int findPeak(int arr[][MAX], int rows, int columns)
{
    return findPeakRec(arr, rows, columns, columns / 2);
}

// Driver Code
int main()
{
    int arr[][MAX] = { { 10, 8, 10, 10 },
                       { 14, 13, 12, 11 },
                       { 15, 9, 11, 21 },
                       { 16, 17, 19, 20 } };

    // Number of Columns
    int rows = 4, columns = 4;
    cout << findPeak(arr, rows, columns);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Finding peak element in a 2D Array.
class GFG
{
    static int MAX = 100;

    // Function to find the maximum in column
    // 'mid', 'rows' is number of rows.
    static int findMax(int[][] arr, int rows,
                       int mid, int max)
    {
        int max_index = 0;
        for (int i = 0; i < rows; i++)
        {
            if (max < arr[i][mid])
            {

                // Saving global maximum and its index
                // to check its neighbours
                max = arr[i][mid];
                max_index = i;
            }
        }
        return max_index;
    }

    // Function to change the value of [max]
    static int Max(int[][] arr, int rows,
                   int mid, int max)
    {
        for (int i = 0; i < rows; i++)
        {
            if (max < arr[i][mid])
            {

                // Saving global maximum and its index
                // to check its neighbours
                max = arr[i][mid];
            }
        }
        return max;
    }

    // Function to find a peak element
    static int findPeakRec(int[][] arr, int rows,
                           int columns, int mid)
    {
        // Evaluating maximum of mid column.
        // Note max is passed by reference.
        int max = 0;
        int max_index = findMax(arr, rows, mid, max);
        max = Max(arr, rows, mid, max);

        // If we are on the first or last column,
        // max is a peak
        if (mid == 0 || mid == columns - 1)
            return max;

        // If mid column maximum is also peak
        if (max >= arr[max_index][mid - 1] &&
            max >= arr[max_index][mid + 1])
            return max;

        // If max is less than its left
        if (max < arr[max_index][mid - 1])
            return findPeakRec(arr, rows, columns,
                         (int)(mid - Math.ceil((double) mid / 2)));

        // If max is less than its left
        // if (max < arr[max_index][mid+1])
        return findPeakRec(arr, rows, columns,
                     (int)(mid + Math.ceil((double) mid / 2)));
    }

    // A wrapper over findPeakRec()
    static int findPeak(int[][] arr, int rows, int columns)
    {
        return findPeakRec(arr, rows, columns, columns / 2);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[][] arr = {{ 10, 8, 10, 10 },
                       { 14, 13, 12, 11 },
                       { 15, 9, 11, 21 },
                       { 16, 17, 19, 20 }};

        // Number of Columns
        int rows = 4, columns = 4;
        System.out.println(findPeak(arr, rows, columns));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Finding peak element in a 2D Array.
MAX = 100
from math import ceil

# Function to find the maximum in column 'mid'
# 'rows' is number of rows.
def findMax(arr, rows, mid,max):

    max_index = 0
    for i in range(rows):
        if (max < arr[i][mid]):

            # Saving global maximum and its index
            # to check its neighbours
            max = arr[i][mid]
            max_index = i
    #print(max_index)

    return max,max_index

# Function to find a peak element
def findPeakRec(arr, rows, columns,mid):

    # Evaluating maximum of mid column.
    # Note max is passed by reference.
    max = 0
    max, max_index = findMax(arr, rows, mid, max)

    # If we are on the first or last column,
    # max is a peak
    if (mid == 0 or mid == columns - 1):
        return max

    # If mid column maximum is also peak
    if (max >= arr[max_index][mid - 1] and
        max >= arr[max_index][mid + 1]):
        return max

    # If max is less than its left
    if (max < arr[max_index][mid - 1]):
        return findPeakRec(arr, rows, columns,
                           mid - ceil(mid / 2.0))

    # If max is less than its left
    # if (max < arr[max_index][mid+1])
    return findPeakRec(arr, rows, columns,
                       mid + ceil(mid / 2.0))

# A wrapper over findPeakRec()
def findPeak(arr, rows, columns):
    return findPeakRec(arr, rows,
                       columns, columns // 2)

# Driver Code
arr = [ [ 10, 8, 10, 10 ],
        [ 14, 13, 12, 11 ],
        [ 15, 9, 11, 21 ],
        [ 16, 17, 19, 20 ] ]

# Number of Columns
rows = 4
columns = 4
print(findPeak(arr, rows, columns))

# This code is contributed by Mohit Kumar
```

## C#

```
// Finding peak element in a 2D Array.
using System;

class GFG
{

    // Function to find the maximum in column
    // 'mid', 'rows' is number of rows.
    static int findMax(int[,] arr, int rows,
                       int mid, int max)
    {
        int max_index = 0;
        for (int i = 0; i < rows; i++)
        {
            if (max < arr[i,mid])
            {

                // Saving global maximum and its
                // index to check its neighbours
                max = arr[i,mid];
                max_index = i;
            }
        }
        return max_index;
    }

    // Function to change the value of [max]
    static int Max(int[,] arr, int rows,
                   int mid, int max)
    {
        for (int i = 0; i < rows; i++)
        {
            if (max < arr[i, mid])
            {

                // Saving global maximum and its
                // index to check its neighbours
                max = arr[i, mid];
            }
        }
        return max;
    }

    // Function to find a peak element
    static int findPeakRec(int[,] arr, int rows,
                           int columns, int mid)
    {
        // Evaluating maximum of mid column.
        // Note max is passed by reference.
        int max = 0;
        int max_index = findMax(arr, rows, mid, max);
        max = Max(arr, rows, mid, max);

        // If we are on the first or last column,
        // max is a peak
        if (mid == 0 || mid == columns - 1)
            return max;

        // If mid column maximum is also peak
        if (max >= arr[max_index, mid - 1] &&
            max >= arr[max_index, mid + 1])
            return max;

        // If max is less than its left
        if (max < arr[max_index,mid - 1])
            return findPeakRec(arr, rows, columns,
                   (int)(mid - Math.Ceiling((double) mid / 2)));

        // If max is less than its left
        // if (max < arr[max_index][mid+1])
        return findPeakRec(arr, rows, columns,
               (int)(mid + Math.Ceiling((double) mid / 2)));
    }

    // A wrapper over findPeakRec()
    static int findPeak(int[,] arr,
                        int rows, int columns)
    {
        return findPeakRec(arr, rows, columns,
                                      columns / 2);
    }

    // Driver Code
    static public void Main ()
    {
        int[,] arr = {{ 10, 8, 10, 10 },
                      { 14, 13, 12, 11 },
                      { 15, 9, 11, 21 },
                      { 16, 17, 19, 20 }};

        // Number of Columns
        int rows = 4, columns = 4;
        Console.Write(findPeak(arr, rows, columns));
    }
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>
    // Finding peak element in a 2D Array.

    let MAX = 100;

    // Function to find the maximum in column
    // 'mid', 'rows' is number of rows.
    function findMax(arr, rows, mid, max)
    {
        let max_index = 0;
        for (let i = 0; i < rows; i++)
        {
            if (max < arr[i][mid])
            {

                // Saving global maximum and its index
                // to check its neighbours
                max = arr[i][mid];
                max_index = i;
            }
        }
        return max_index;
    }

    // Function to change the value of [max]
    function Max(arr, rows, mid, max)
    {
        for (let i = 0; i < rows; i++)
        {
            if (max < arr[i][mid])
            {

                // Saving global maximum and its index
                // to check its neighbours
                max = arr[i][mid];
            }
        }
        return max;
    }

    // Function to find a peak element
    function findPeakRec(arr, rows, columns, mid)
    {
        // Evaluating maximum of mid column.
        // Note max is passed by reference.
        let max = 0;
        let max_index = findMax(arr, rows, mid, max);
        max = Max(arr, rows, mid, max);

        // If we are on the first or last column,
        // max is a peak
        if (mid == 0 || mid == columns - 1)
            return max;

        // If mid column maximum is also peak
        if (max >= arr[max_index][mid - 1] &&
            max >= arr[max_index][mid + 1])
            return max;

        // If max is less than its left
        if (max < arr[max_index][mid - 1])
            return findPeakRec(arr, rows, columns, (mid - Math.ceil(mid / 2)));

        // If max is less than its left
        // if (max < arr[max_index][mid+1])
        return findPeakRec(arr, rows, columns, (mid + Math.ceil(mid / 2)));
    }

    // A wrapper over findPeakRec()
    function findPeak(arr, rows, columns)
    {
        return findPeakRec(arr, rows, columns, parseInt(columns / 2, 10));
    }

    let arr = [[ 10, 8, 10, 10 ],
                [ 14, 13, 12, 11 ],
                [ 15, 9, 11, 21 ],
                [ 16, 17, 19, 20 ]];

    // Number of Columns
    let rows = 4, columns = 4;
    document.write(findPeak(arr, rows, columns));

</script>
```

**输出:**

```
21
```

时间复杂度:O(行*日志(列))。我们重复了一半的列数。在每次递归调用中，我们线性搜索当前中间列中的最大值。
辅助空间:O(列/2)为递归调用栈
**来源:**
[https://OCW . MIT . edu/courses/electric-engineering-and-computer-science/6-006-算法导论-fall-2011/讲座-视频/MIT6_006F11_lec01.pdf](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-006-introduction-to-algorithms-fall-2011/lecture-videos/MIT6_006F11_lec01.pdf)

本文由 **Rohit Thapliyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。