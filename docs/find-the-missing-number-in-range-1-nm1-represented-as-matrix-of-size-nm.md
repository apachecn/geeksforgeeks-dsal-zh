# 查找范围[1，N*M+1]内的缺失数，表示为大小为 N*M 的矩阵

> 原文:[https://www . geesforgeks . org/find-范围内缺失数字-1-nm1-表示为尺寸矩阵-nm/](https://www.geeksforgeeks.org/find-the-missing-number-in-range-1-nm1-represented-as-matrix-of-size-nm/)

给定一个 **N x M** 矩阵 **mat[][]** ，其中所有元素都是从 1 开始的自然数，并且除了一个元素之外都是连续的，找到那个元素。

**示例**:

> **输入** : mat[][] = {{1，2，3，4}，
> {5，6，7，8}，
> {9，11，12，13}}
> N = 3，M = 4
> **输出** : 10
> **说明**:第 3 行缺号为 10。
> 
> **输入** : mat[][] = {{1，2，3}，
> {5，6，7}，
> {8，9，10}}
> N = 3，M = 3
> **输出** : 4

**逼近**:这个问题可以通过检查矩阵每行最后一个元素的 M 的倍数来解决，如果不匹配，那么丢失的元素就在那一行。应用线性搜索并找到它。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;
#define Max 1000

// Function to return Missing
// Element from matrix Mat
int check(int Mat[][Max], int N, int M)
{
    // Edge Case
    if (Mat[0][0] != 1)
        return 1;

    // Initialize last element of
    // first row
    int X = Mat[0][0] + M - 1;

    for (int i = 0; i < N; i++) {

        // If last element of respective row
        // matches respective multiples of X
        if (Mat[i][M - 1] == X)
            X = X + M;

        // Else missing element
        // is in that row
        else {

            // Initializing first element
            //  of the row
            int Y = X - M + 1;

            // Initializing column index
            int j = 0;

            // Linear Search
            while (Y <= X) {
                if (Mat[i][j] == Y) {
                    Y++;
                    j++;
                }
                else
                    return Y;
            }
        }
    }
}

// Driver Code
int main()
{
    int N = 3;
    int M = 4;

    int Mat[][Max] = { { 1, 2, 3, 4 },
                       { 5, 6, 7, 8 },
                       {  9, 11, 12, 13 } };

    cout << check(Mat, N, M);
    return 0;
}
```

**Output**

```
10
```

***时间复杂度*** : O(N + M)
***辅助空间*** : O(1)

**有效方法**:有效方法是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)算法检查行中最后一个元素的倍数。如果不匹配，则丢失的元素在该行或其前几行中，如果匹配，则丢失的元素在下几行中。首先，使用二分搜索法查找该行，然后以查找列的相同方式在该行中应用二分搜索法。

下面是上述方法的实现:

## C++

```
// C++ program to implement the above approach
#include <bits/stdc++.h>
using namespace std;
#define Max 1000

// Function to return Missing
// Element from matrix MAt
int check(int Mat[][Max], int N, int M)
{

    // Edge Case
    if (Mat[0][0] != 1)
        return 1;

    // Initialize last element of
    // first row
    int X = Mat[0][0] + M - 1;
    int m, l = 0, h = N - 1;

    // Checking for row
    while (l < h) {

        // Avoiding overflow
        m = l + (h - l) / 2;

        if (Mat[m][M - 1] == X * (m + 1))
            l = m + 1;
        else
            h = m;
    }

    // Set the required row index and
    // last element of previous row
    int R = h;
    X = X * h;
    l = 0, h = M - 1;

    // Checking for column
    while (l < h) {

        // Avoiding overflow
        m = l + (h - l) / 2;

        if (Mat[R][m] == X + (m + 1))
            l = m + 1;
        else
            h = m;
    }

    // Returning Missing Element
    return X + h + 1;
}

// Driver Code
int main()
{
    int N = 3;
    int M = 4;
    int Mat[][Max] = { { 1, 2, 3, 4 },
                       { 5, 6, 7, 8 },
                       { 9, 11, 12, 13 } };
    cout << check(Mat, N, M);
    return 0;
}
```

**Output**

```
10
```

***时间复杂度***:O(log N+log M)
***辅助空间*** : O(1)