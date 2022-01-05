# 在矩阵中找到最大和的行

> 原文:[https://www . geesforgeks . org/find-row-带最大矩阵求和/](https://www.geeksforgeeks.org/find-row-with-maximum-sum-in-a-matrix/)

给定一个 N*N 矩阵。任务是找到具有最大和的行的索引。这是元素总和最大的行。
**例** :

```
Input : mat[][] = {
        { 1, 2, 3, 4, 5 },
        { 5, 3, 1, 4, 2 },
        { 5, 6, 7, 8, 9 },
        { 0, 6, 3, 4, 12 },
        { 9, 7, 12, 4, 3 },
    };
Output : Row 3 has max sum 35

Input : mat[][] = {
        { 1, 2, 3 },
        { 4, 2, 1 },
        { 5, 6, 7 },
    };
Output : Row 3 has max sum 18
```

其思想是[逐行遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)找到每行元素的和，检查每行当前和是否大于当前行之前获得的最大和，并相应更新 maximum_sum。
以下是上述办法的实施情况:

## C++

```
// C++ program to find row with
// max sum in a matrix
#include <bits/stdc++.h>
using namespace std;

#define N 5 // No of rows and column

// Function to find the row with max sum
pair<int, int> colMaxSum(int mat[N][N])
{
    // Variable to store index of row
    // with maximum
    int idx = -1;

    // Variable to store max sum
    int maxSum = INT_MIN;

    // Traverse matrix row wise
    for (int i = 0; i < N; i++) {
        int sum = 0;

        // calculate sum of row
        for (int j = 0; j < N; j++) {
            sum += mat[i][j];
        }

        // Update maxSum if it is less than
        // current sum
        if (sum > maxSum) {
            maxSum = sum;

            // store index
            idx = i;
        }
    }

    pair<int, int> res;

    res = make_pair(idx, maxSum);

    // return result
    return res;
}

// Driver code
int main()
{

    int mat[N][N] = {
        { 1, 2, 3, 4, 5 },
        { 5, 3, 1, 4, 2 },
        { 5, 6, 7, 8, 9 },
        { 0, 6, 3, 4, 12 },
        { 9, 7, 12, 4, 3 },
    };

    pair<int, int> ans = colMaxSum(mat);

    cout << "Row " << ans.first + 1 << " has max sum "
         << ans.second;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find row with
// max sum in a matrix
import java.util.ArrayList;

class MaxSum
{
    public static int N;

    static ArrayList<Integer> colMaxSum(int mat[][])
    {
        // Variable to store index of row
        // with maximum
        int idx = -1;

        // Variable to store maximum sum
        int maxSum = Integer.MIN_VALUE;

        // Traverse the matrix row wise
        for (int i = 0; i < N; i++)
        {
            int sum = 0;
            for (int j = 0; j < N; j++)
            {
                sum += mat[i][j];
            }

            // Update maxSum if it is less than
            // current row sum
            if (maxSum < sum)
            {
                maxSum = sum;

                // store index
                idx = i;
            }
        }

        // Arraylist to store values of index
        // of maximum sum and the maximum sum together
        ArrayList<Integer> res = new ArrayList<>();
        res.add(idx);
        res.add(maxSum);

        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        N = 5;
        int[][] mat = {
            { 1, 2, 3, 4, 5 },
            { 5, 3, 1, 4, 2 },
            { 5, 6, 7, 8, 9 },
            { 0, 6, 3, 4, 12 },
            { 9, 7, 12, 4, 3 },
        };
        ArrayList<Integer> ans = colMaxSum(mat);
        System.out.println("Row "+ (ans.get(0)+1)+ " has max sum "
        + ans.get(1));
    }
}

// This code is contributed by Vivekkumar Singh
```

## 蟒蛇 3

```
# Python3 program to find row with
# max sum in a matrix
import sys

N = 5 # No of rows and column

# Function to find the row with max sum
def colMaxSum(mat):

    # Variable to store index of row
    # with maximum
    idx = -1

    # Variable to store max sum
    maxSum = -sys.maxsize

    # Traverse matrix row wise
    for i in range(0, N):
        sum = 0

        # calculate sum of row
        for j in range(0, N):
            sum += mat[i][j]

        # Update maxSum if it is less than
        # current sum
        if (sum > maxSum):
            maxSum = sum

            # store index
            idx = i

    res = [idx, maxSum]

    # return result
    return res

# Driver code
mat = [[ 1, 2, 3, 4, 5],
       [ 5, 3, 1, 4, 2],
       [ 5, 6, 7, 8, 9],
       [ 0, 6, 3, 4, 12],
       [ 9, 7, 12, 4, 3]]

ans = colMaxSum(mat)
print("Row", ans[0] + 1, "has max sum", ans[1])

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program to find row with
// max sum in a matrix
using System;
using System.Collections.Generic;

public class MaxSum
{
    public static int N;

    static List<int> colMaxSum(int [,]mat)
    {
        // Variable to store index of row
        // with maximum
        int idx = -1;

        // Variable to store maximum sum
        int maxSum = int.MinValue;

        // Traverse the matrix row wise
        for (int i = 0; i < N; i++)
        {
            int sum = 0;
            for (int j = 0; j < N; j++)
            {
                sum += mat[i, j];
            }

            // Update maxSum if it is less than
            // current row sum
            if (maxSum < sum)
            {
                maxSum = sum;

                // store index
                idx = i;
            }
        }

        // Arraylist to store values of index
        // of maximum sum and the maximum sum together
        List<int> res = new List<int>();
        res.Add(idx);
        res.Add(maxSum);

        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        N = 5;
        int[,] mat = {
            { 1, 2, 3, 4, 5 },
            { 5, 3, 1, 4, 2 },
            { 5, 6, 7, 8, 9 },
            { 0, 6, 3, 4, 12 },
            { 9, 7, 12, 4, 3 },
        };
        List<int> ans = colMaxSum(mat);
        Console.WriteLine("Row "+ (ans[0]+1)+ " has max sum "
        + ans[1]);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find row with
// max sum in a matrix
var N;
function colMaxSum(mat)
{
    // Variable to store index of row
    // with maximum
    var idx = -1;
    // Variable to store maximum sum
    var maxSum = -1000000000;
    // Traverse the matrix row wise
    for (var i = 0; i < N; i++)
    {
        var sum = 0;
        for (var j = 0; j < N; j++)
        {
            sum += mat[i][j];
        }
        // Update maxSum if it is less than
        // current row sum
        if (maxSum < sum)
        {
            maxSum = sum;
            // store index
            idx = i;
        }
    }

    // Arraylist to store values of index
    // of maximum sum and the maximum sum together
    var res = [];
    res.push(idx);
    res.push(maxSum);
    return res;
}
// Driver code
N = 5;
var mat = [
    [ 1, 2, 3, 4, 5 ],
    [ 5, 3, 1, 4, 2 ],
    [ 5, 6, 7, 8, 9 ],
    [ 0, 6, 3, 4, 12],
    [ 9, 7, 12, 4, 3]];
var ans = colMaxSum(mat);
document.write("Row "+ (ans[0]+1)+ " has max sum "
+ ans[1]);

</script>
```

**Output:** 

```
Row 3 has max sum 35
```