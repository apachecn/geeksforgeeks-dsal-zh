# 计算正方形矩阵中主对角线与包含重复值的行数和列数之和

> 原文:[https://www . geeksforgeeks . org/compute-sum-main-对角线-行数和列数-包含重复值的方阵/](https://www.geeksforgeeks.org/calculate-sum-of-the-main-diagonal-and-the-number-of-rows-and-columns-containing-repeated-values-in-a-square-matrix/)

给定维度为 **N * N、**的[矩阵](http://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/) **M[][]** ，该矩阵仅由范围从 **1** 到 **N** 的整数组成，任务是计算主对角线中存在的矩阵元素之和，即包含重复值的行数和列数。

**示例:**

> **输入:** N = 4，M[][] = {{1，2，3，4}，{2，1，4，3}，{3，4，1，2}，{4，3，2，1}}
> **输出:** 4 0 0
> **解释:**
> 对角线之和= M[0][0]+M[1][1]+M[2][2]+M[3][3]= 4。
> 没有一行或一列由重复的元素组成。
> 因此，要求的总和为 4
> 
> **输入:** N = 3，M[][] = {{2，1，3}，{1，3，2}，{1，2，3}}
> **输出:** 8 0 2
> **说明:**
> 对角线之和= M[0][0]+M[1][1]+M[2][2] = 8。
> 没有一行由重复的元素组成。
> 1 <sup>st</sup> 和 3 <sup>rd</sup> 列由重复的元素组成。

**方法:**方法是简单地[遍历矩阵的所有元素](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)和[找到对角线的和](https://www.geeksforgeeks.org/efficiently-compute-sums-of-diagonals-of-a-matrix/)以及具有重复值的行数和列数。按照以下步骤解决给定的问题:

*   初始化变量**跟踪**、**行重复**和**列重复**分别存储包含重复矩阵元素的主对角线、行数和列数之和。
*   [遍历矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)**M【I】【j】**中的每个元素，如果 **i** 等于 **j** ，则增加**轨迹**的总和。
*   若要查找包含重复值的行，请一次迭代一行，比较值，并检查是否存在重复值。获得第一对重复元素后，将**行重复**增加 **1** 和[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   对矩阵的每一行重复上述步骤。
*   对所有列重复相同的过程，其中**列重复**增加 **1** ，如果值匹配。
*   完成所有迭代后，打印**轨迹**、**行重复**和**列重复**的值作为结果。

下面是上述方法的实现:

## C++14

```
// C++14 program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate trace of
// a matrix and number of rows and
// columns with repeated elements
void vestigium(int N, int M[4][4])
{

    // Stores the trace, number of
    // rows and columns consisting
    // of repeated matrix elements
    int trace = 0, row_repeat = 0;
    int column_repeat = 0;

    // Iterate over the matrix
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // If current element is
            // present in the main diagonal
            if (i == j)
            {

                // Update trace
                trace += M[i][j];
            }
        }

        int flag1 = 0;

        // Iterate over each row
        // and increment row_repeat
        // if repeated values exists
        for(int j = 0; j < N; j++)
        {
            for(int k = 0; k < N; k++)
            {

                // For each valid range
                if (j != k && M[i][j] == M[i][k])
                {
                    row_repeat++;
                    flag1 = 1;
                    break;
                }
            }

            if (flag1 == 1)
            {
                break;
            }
        }

        int flag2 = 0;

        // Iterate over each column and
        // increment column_repeat if
        // repeated values are encountered
        for(int j = 0; j < N; j++)
        {
            for(int k = 0; k < N; k++)
            {

                // For each valid range
                if (j != k && M[j][i] == M[k][i])
                {
                    column_repeat++;
                    flag2 = 1;
                    break;
                }
            }

            if (flag2 == 1)
            {
                break;
            }
        }
    }

    // Answer
    cout << trace << " "
         << row_repeat << " "
         << column_repeat ;
}

// Driver Code
int main()
{
    int M[4][4] = { { 1, 2, 3, 4 },
                    { 2, 1, 4, 3 },
                    { 3, 4, 1, 2 },
                    { 4, 3, 2, 1 } };

    int N = sizeof(M) / sizeof(M[0]);

    vestigium(N, M);
}

// This code is contributed by sanjoy_62
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    // Function to calculate trace of
    // a matrix and number of rows and
    // columns with repeated elements
    public static String vestigium(
        int N, int M[][])
    {
        // Stores the trace, number of
        // rows and columns consisting
        // of repeated matrix elements
        int trace = 0, row_repeat = 0;
        int column_repeat = 0;

        // Iterate over the matrix
        for (int i = 0; i < N; i++) {

            for (int j = 0; j < N; j++) {

                // If current element is
                // present in the main diagonal
                if (i == j) {

                    // Update trace
                    trace += M[i][j];
                }
            }

            int flag1 = 0;

            // Iterate over each row
            // and increment row_repeat
            // if repeated values exists
            for (int j = 0; j < N; j++) {
                for (int k = 0; k < N; k++) {

                    // For each valid range
                    if (j != k
                        && M[i][j] == M[i][k]) {
                        row_repeat++;
                        flag1 = 1;
                        break;
                    }
                }

                if (flag1 == 1) {

                    break;
                }
            }

            int flag2 = 0;

            // Iterate over each column and
            // increment column_repeat if
            // repeated values are encountered
            for (int j = 0; j < N; j++) {
                for (int k = 0; k < N; k++) {

                    // For each valid range
                    if (j != k
                        && M[j][i] == M[k][i]) {

                        column_repeat++;
                        flag2 = 1;
                        break;
                    }
                }

                if (flag2 == 1) {

                    break;
                }
            }
        }

        // Answer
        String output = trace + " "
                        + row_repeat + " "
                        + column_repeat + "\n";

        // Return answer
        return output;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int M[][] = { { 1, 2, 3, 4 },
                      { 2, 1, 4, 3 },
                      { 3, 4, 1, 2 },
                      { 4, 3, 2, 1 } };
        int N = M.length;

        String output = vestigium(N, M);

        // Print the output
        System.out.print(output);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate trace of
# a matrix and number of rows and
# columns with repeated elements
def vestigium(N, M) :

    # Stores the trace, number of
    # rows and columns consisting
    # of repeated matrix elements
    trace = 0
    row_repeat = 0
    column_repeat = 0

    # Iterate over the matrix
    for i in range(N) :
        for j in range(N) :

            # If current element is
            # present in the main diagonal
            if (i == j):

                # Update trace
                trace += M[i][j]
        flag1 = 0

        # Iterate over each row
        # and increment row_repeat
        # if repeated values exists
        for j in range(N) :
            for k in range(N) :

                # For each valid range
                if (j != k and M[i][j] == M[i][k]) :
                    row_repeat += 1
                    flag1 = 1
                    break
            if (flag1 == 1) :
                break
        flag2 = 0

        # Iterate over each column and
        # increment column_repeat if
        # repeated values are encountered
        for j in range(N) :
            for k in range(N) :

                # For each valid range
                if (j != k and M[j][i] == M[k][i]) :
                    column_repeat += 1
                    flag2 = 1
                    break

            if (flag2 == 1) :
                break

    # Answer
    print(trace, row_repeat, column_repeat)

# Driver Code
M = [[ 1, 2, 3, 4 ],
    [ 2, 1, 4, 3 ],
    [ 3, 4, 1, 2 ],
    [ 4, 3, 2, 1 ]]           
N = len(M)
vestigium(N, M)

# This code is contributed by avijitmonald1998.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate trace of
// a matrix and number of rows and
// columns with repeated elements
public static String vestigium(int N, int[,] M)
{

    // Stores the trace, number of
    // rows and columns consisting
    // of repeated matrix elements
    int trace = 0, row_repeat = 0;
    int column_repeat = 0;

    // Iterate over the matrix
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // If current element is
            // present in the main diagonal
            if (i == j)
            {

                // Update trace
                trace += M[i, j];
            }
        }

        int flag1 = 0;

        // Iterate over each row
        // and increment row_repeat
        // if repeated values exists
        for(int j = 0; j < N; j++)
        {
            for(int k = 0; k < N; k++)
            {

                // For each valid range
                if (j != k && M[i, j] == M[i, k])
                {
                    row_repeat++;
                    flag1 = 1;
                    break;
                }
            }

            if (flag1 == 1)
            {
                break;
            }
        }

        int flag2 = 0;

        // Iterate over each column and
        // increment column_repeat if
        // repeated values are encountered
        for(int j = 0; j < N; j++)
        {
            for(int k = 0; k < N; k++)
            {

                // For each valid range
                if (j != k && M[j, i] == M[k, i])
                {
                    column_repeat++;
                    flag2 = 1;
                    break;
                }
            }

            if (flag2 == 1)
            {
                break;
            }
        }
    }

    // Answer
    string output = trace + " " + row_repeat + " " +
                    column_repeat + "\n";

    // Return answer
    return output;
}

// Driver Code
public static void Main(string[] args)
{
    int[, ] M = { { 1, 2, 3, 4 },
                  { 2, 1, 4, 3 },
                  { 3, 4, 1, 2 },
                  { 4, 3, 2, 1 } };
    int N = M.GetLength(0);

    string output = vestigium(N, M);

    // Print the output
    Console.Write(output);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function to calculate trace of
// a matrix and number of rows and
// columns with repeated elements
function vestigium( N , M)
{
    // Stores the trace, number of
    // rows and columns consisting
    // of repeated matrix elements
    var trace = 0, row_repeat = 0;
    var column_repeat = 0;

    // Iterate over the matrix
    for (i = 0; i < N; i++) {

        for (j = 0; j < N; j++) {

            // If current element is
            // present in the main diagonal
            if (i == j) {

                // Update trace
                trace += M[i][j];
            }
        }

        var flag1 = 0;

        // Iterate over each row
        // and increment row_repeat
        // if repeated values exists
        for (j = 0; j < N; j++) {
            for (k = 0; k < N; k++) {

                // For each valid range
                if (j != k
                    && M[i][j] == M[i][k]) {
                    row_repeat++;
                    flag1 = 1;
                    break;
                }
            }

            if (flag1 == 1) {

                break;
            }
        }

        var flag2 = 0;

        // Iterate over each column and
        // increment column_repeat if
        // repeated values are encountered
        for (j = 0; j < N; j++) {
            for (k = 0; k < N; k++) {

                // For each valid range
                if (j != k
                    && M[j][i] == M[k][i]) {

                    column_repeat++;
                    flag2 = 1;
                    break;
                }
            }

            if (flag2 == 1) {

                break;
            }
        }
    }

    // Answer
    var output = trace + " "
                    + row_repeat + " "
                    + column_repeat + "\n";

    // Return answer
    return output;
}

// Driver Code
    var M = [ [ 1, 2, 3, 4 ],
                  [ 2, 1, 4, 3 ],
                  [ 3, 4, 1, 2 ],
                  [ 4, 3, 2, 1 ] ];
    var N = M.length;

    var output = vestigium(N, M);

    // Print the output
    document.write(output);

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
4 0 0
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>2</sup> )*