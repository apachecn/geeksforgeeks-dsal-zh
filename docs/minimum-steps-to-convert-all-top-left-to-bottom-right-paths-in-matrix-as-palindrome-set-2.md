# 将矩阵中所有左上到右下路径转换为回文的最少步骤|设置 2

> 原文:[https://www . geesforgeks . org/最少转换步骤-全部-从左上方到右下方-矩阵中的路径-作为回文-集合-2/](https://www.geeksforgeeks.org/minimum-steps-to-convert-all-top-left-to-bottom-right-paths-in-matrix-as-palindrome-set-2/)

给定一个矩阵**mat【】【】**有 **N** 行和 **M** 列。任务是找到矩阵中所需的最小变化数，使得从左上角到右下角的每条路径都是回文路径。在路径中，从一个单元格到另一个单元格只允许向右和向下移动。

**示例:**

> ***输入:** mat[][] = {{1，2}，{3，1}}*
> ***输出:** 0*
> ***解释:***
> *矩阵中从左上方到右下方的每一条路径都是回文。*
> *路径= > {1，2，1}，{1，3，1}*
> 
> ***输入:** mat[][] = {{1，2}，{3，5}}*
> ***输出:** 1*
> ***解释:***
> *每条路径回文只需要一次修改。*
> *即=>mat[1][1]= 1*
> *path =>{1，2，1}，{ 1，3，1}*

**幼稚做法:**幼稚做法请参考[这篇](https://www.geeksforgeeks.org/minimum-steps-to-convert-all-paths-in-matrix-from-top-left-to-bottom-right-as-palindromic-paths/)帖子。

**高效方法:**想法是放弃使用额外的空间，即使用 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) 。遵循以下步骤:

1.  左上方和右下方的可能距离在 **0 到 N+M–2**的范围内。因此创建一个维度的 2D 数组**【N+M–1】【10】**。
2.  在数组中存储距离的频率，同时将行号(在 0 到 N+M–2 的范围内)视为距离，将列号(0 到 9)视为给定矩阵中的元素。
3.  为了使变化的次数最少，在距离 **X** 处用一个在距离 **X** 处的所有值中具有最高**频率**的值来改变每个单元。
4.  所需的最小步数是每个距离的总频率值和最大频率值之差的总和。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define N 7

// Function for counting minimum
// number of changes
int countChanges(int matrix[][N],
                 int n, int m)
{
    // Distance of elements from (0, 0)
    // will is i range [0, n + m - 2]
    int dist = n + m - 1;

    // Store frequencies of [0, 9]
    // at distance i
    int freq[dist][10];

    // Initialize frequencies as 0
    for (int i = 0; i < dist; i++) {
        for (int j = 0; j < 10; j++)
            freq[i][j] = 0;
    }

    // Count frequencies of [0, 9]
    for (int i = 0; i < n; i++) {

        for (int j = 0; j < m; j++) {

            // Increment frequency of
            // value matrix[i][j]
            // at distance i+j
            freq[i + j][matrix[i][j]]++;
        }
    }

    int min_changes_sum = 0;
    for (int i = 0; i < dist / 2; i++) {

        int maximum = 0;
        int total_values = 0;

        // Find value with max frequency
        // and count total cells at distance i
        // from front end and rear end
        for (int j = 0; j < 10; j++) {

            maximum = max(maximum, freq[i][j]
                    + freq[n + m - 2 - i][j]);

            total_values += (freq[i][j]
                   + freq[n + m - 2 - i][j]);
        }

        // Change all values to the
        // value with max frequency
        min_changes_sum += (total_values
                            - maximum);
    }

    // Return the answer
    return min_changes_sum;
}

// Driver Code
int main()
{
    // Given Matrix
    int mat[][N] = { { 1, 2 }, { 3, 5 } };

    // Function Call
    cout << countChanges(mat, 2, 2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static final int N = 7;

// Function for counting minimum
// number of changes
static int countChanges(int matrix[][],
                        int n, int m)
{

    // Distance of elements from (0, 0)
    // will is i range [0, n + m - 2]
    int dist = n + m - 1;

    // Store frequencies of [0, 9]
    // at distance i
    int [][]freq = new int[dist][10];

    // Initialize frequencies as 0
    for(int i = 0; i < dist; i++)
    {
        for(int j = 0; j < 10; j++)
            freq[i][j] = 0;
    }

    // Count frequencies of [0, 9]
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {

            // Increment frequency of
            // value matrix[i][j]
            // at distance i+j
            freq[i + j][matrix[i][j]]++;
        }
    }

    int min_changes_sum = 0;
    for(int i = 0; i < dist / 2; i++)
    {
        int maximum = 0;
        int total_values = 0;

        // Find value with max frequency
        // and count total cells at distance i
        // from front end and rear end
        for(int j = 0; j < 10; j++)
        {
            maximum = Math.max(maximum, freq[i][j] +
                            freq[n + m - 2 - i][j]);

            total_values += (freq[i][j] +
                             freq[n + m - 2 - i][j]);
        }

        // Change all values to the
        // value with max frequency
        min_changes_sum += (total_values -
                            maximum);
    }

    // Return the answer
    return min_changes_sum;
}

// Driver Code
public static void main(String[] args)
{

    // Given matrix
    int mat[][] = { { 1, 2 }, { 3, 5 } };

    // Function call
    System.out.print(countChanges(mat, 2, 2));
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function for counting minimum
# number of changes
def countChanges(matrix, n, m):

    # Distance of elements from (0, 0)
    # will is i range [0, n + m - 2]
    dist = n + m - 1

    # Store frequencies of [0, 9]
    # at distance i
    # Initialize all with zero
    freq = [[0] * 10 for i in range(dist)]

    # Count frequencies of [0, 9]
    for i in range(n):
        for j in range(m):

            # Increment frequency of
            # value matrix[i][j]
            # at distance i+j
            freq[i + j][matrix[i][j]] += 1

    min_changes_sum = 0

    for i in range(dist // 2):
        maximum = 0
        total_values = 0

        # Find value with max frequency
        # and count total cells at distance i
        # from front end and rear end        
        for j in range(10):
            maximum = max(maximum, freq[i][j] +
                       freq[n + m - 2 - i][j])

            total_values += (freq[i][j] +
                 freq[n + m - 2 - i][j])

        # Change all values to the value
        # with max frequency
        min_changes_sum += (total_values -
                            maximum)

    # Return the answer
    return min_changes_sum

# Driver code
if __name__ == '__main__':

    # Given matrix
    mat = [ [ 1, 2 ], [ 3, 5 ] ]

    # Function call
    print(countChanges(mat, 2, 2))

# This code is contributed by himanshu77
```

## C#

```
// C# program for the above approach
using System;

class GFG{

//static readonly int N = 7;

// Function for counting minimum
// number of changes
static int countChanges(int [,]matrix,
                        int n, int m)
{

    // Distance of elements from (0, 0)
    // will is i range [0, n + m - 2]
    int dist = n + m - 1;

    // Store frequencies of [0, 9]
    // at distance i
    int [,]freq = new int[dist, 10];

    // Initialize frequencies as 0
    for(int i = 0; i < dist; i++)
    {
        for(int j = 0; j < 10; j++)
            freq[i, j] = 0;
    }

    // Count frequencies of [0, 9]
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {

            // Increment frequency of
            // value matrix[i,j]
            // at distance i+j
            freq[i + j, matrix[i, j]]++;
        }
    }

    int min_changes_sum = 0;
    for(int i = 0; i < dist / 2; i++)
    {
        int maximum = 0;
        int total_values = 0;

        // Find value with max frequency
        // and count total cells at distance i
        // from front end and rear end
        for(int j = 0; j < 10; j++)
        {
            maximum = Math.Max(maximum, freq[i, j] +
                            freq[n + m - 2 - i, j]);

            total_values += (freq[i, j] +
                             freq[n + m - 2 - i, j]);
        }

        // Change all values to the
        // value with max frequency
        min_changes_sum += (total_values -
                            maximum);
    }

    // Return the answer
    return min_changes_sum;
}

// Driver Code
public static void Main(String[] args)
{

    // Given matrix
    int [,]mat = { { 1, 2 }, { 3, 5 } };

    // Function call
    Console.Write(countChanges(mat, 2, 2));
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// JavaScript program for the above approach
var N = 7;

// Function for counting minimum
// number of changes
function countChanges(matrix, n, m)
{
    // Distance of elements from (0, 0)
    // will is i range [0, n + m - 2]
    var dist = n + m - 1;

    // Store frequencies of [0, 9]
    // at distance i
    var freq = Array.from(Array(dist), ()=>Array(10));

    // Initialize frequencies as 0
    for (var i = 0; i < dist; i++) {
        for (var j = 0; j < 10; j++)
            freq[i][j] = 0;
    }

    // Count frequencies of [0, 9]
    for (var i = 0; i < n; i++) {

        for (var j = 0; j < m; j++) {

            // Increment frequency of
            // value matrix[i][j]
            // at distance i+j
            freq[i + j][matrix[i][j]]++;
        }
    }

    var min_changes_sum = 0;
    for (var i = 0; i < parseInt(dist / 2); i++) {

        var maximum = 0;
        var total_values = 0;

        // Find value with max frequency
        // and count total cells at distance i
        // from front end and rear end
        for (var j = 0; j < 10; j++) {

            maximum = Math.max(maximum, freq[i][j]
                    + freq[n + m - 2 - i][j]);

            total_values += (freq[i][j]
                   + freq[n + m - 2 - i][j]);
        }

        // Change all values to the
        // value with max frequency
        min_changes_sum += (total_values
                            - maximum);
    }

    // Return the answer
    return min_changes_sum;
}

// Driver Code

// Given Matrix
var mat = [[1, 2], [3, 5 ]];

// Function Call
document.write( countChanges(mat, 2, 2));

</script>
```

**Output:** 

```
1
```

**时间复杂度:***O(N * M)*
T5】辅助空间: *O(N*M)*