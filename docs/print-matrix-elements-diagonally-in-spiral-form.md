# 以螺旋形式对角打印矩阵元素

> 原文:[https://www . geesforgeks . org/print-matrix-elements-以螺旋形式对角排列/](https://www.geeksforgeeks.org/print-matrix-elements-diagonally-in-spiral-form/)

给定一个尺寸为 **N * M** 的[矩阵](https://www.geeksforgeeks.org/matrix/)**arr【】【】**和一个整数 **K** ，任务是以螺旋形式对角打印矩阵中从左上角元素到 **K** 的所有元素。

**示例:**

> **输入:** N=5，M=6，K=15，arr[][]={{1，2，3，4，5，6}，
> {7，8，9，10，11，12}，
> {13，14，15，16，17，18}，
> {19，20，21，22，23，24}，
> {25，26，27，28，29，30}
> 
> | one | Two | three | four | five | six |
> | seven | eight | nine | Ten | Eleven | Twelve |
> | Thirteen | Fourteen | Fifteen | Sixteen | Seventeen | Eighteen |
> | Nineteen | Twenty | Twenty-one | Twenty-two | Twenty-three | Twenty-four |
> | Twenty-five | Twenty-six | Twenty-seven | Twenty-eight | Twenty-nine | Thirty |
> 
> 1 <sup>st</sup> 对角印花:{1}
> 2 <sup>nd</sup> 对角印花:{2，7}
> 3 <sup>rd</sup> 对角印花:{13，8，3}
> ……
> 5 <sup>th</sup> 对角印花{25，20，15}。
> 由于遇到 15，因此不再打印矩阵元素。
> 
> **输入:** N = 4，M = 3，K = 69，arr[][]={{4，87，24}，
> {17，1，18}，
> {25，69，97}，
> {19，27，85}}
> **输出:** 4，87，17，25，1，24，18，69

**方法:**按照以下步骤解决问题:

1.  矩阵中的对角线总数为**N+M–1**。
2.  以螺旋方式逐个穿过对角线。
3.  对于遍历的每个元素，检查是否等于 **K** 。如果发现是真的，打印该元素并终止。
4.  否则，打印元素并计算要遍历的下一个索引。如果 **i** 和 **j** 是当前指数:
    *   沿对角线向上移动**时，i** 将减少，而 **j** 将增加。
    *   对角向下移动**时，i** 将增加，而 **j** 将减少。
5.  如果下一个索引不是有效的索引，则移动到下一个对角线。
6.  否则，将当前位置更新到下一个位置。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the
// indices are valid or not
bool isValid(int i, int j,
            int N, int M)
{
    return (i >= 0 && i < N
            && j >= 0 && j < M);
}

// Function to evaluate the next
// index while moving diagonally up
pair<int, int> up(int i, int j,
                int N, int M)
{
    if (isValid(i - 1, j + 1, N, M))
        return { i - 1, j + 1 };
    else
        return { -1, -1 };
}

// Function to evaluate the next
// index while moving diagonally down
pair<int, int> down(int i, int j,
                    int N, int M)
{
    if (isValid(i + 1, j - 1, N, M))
        return { i + 1, j - 1 };
    else
        return { -1, -1 };
}

// Function to print matrix elements
// diagonally in Spiral Form
void SpiralDiagonal(int N, int M, int K,
                    vector<vector<int> > a)
{
    int i = 0, j = 0;

    // Total Number of Diagonals
    // = N + M - 1
    for (int diagonal = 0;
        diagonal < N + M - 1;
        diagonal++) {

        while (1) {

            // Stop when K is
            // encountered
            if (a[i][j] == K) {

                cout << K;
                return;
            }

            // Print the integer
            cout << a[i][j] << ", ";

            // Store the next index
            pair<int, int> next;
            if (diagonal & 1) {

                next = down(i, j, N, M);
            }
            else {

                next = up(i, j, N, M);
            }

            // If current index is invalid
            if (next.first == next.second
                && next.first == -1) {

                // Move to the next diagonal
                if (diagonal & 1) {

                    (i + 1 < N) ? ++i : ++j;
                }
                else {

                    (j + 1 < M) ? ++j : ++i;
                }
                break;
            }

            // Otherwise move to the
            // next valid index
            else {

                i = next.first;
                j = next.second;
            }
        }
    }
}

// Driver Code
int main()
{

    int N = 5, M = 6, K = 15;
    vector<vector<int> > arr
        = { { 1, 2, 3, 4, 5, 6 },
            { 7, 8, 9, 10, 11, 12 },
            { 13, 14, 15, 16, 17, 18 },
            { 19, 20, 21, 22, 23, 24 },
            { 25, 26, 27, 28, 29, 30 } };

    // Function Call
    SpiralDiagonal(N, M, K, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
import java.lang.*;

class GFG{
static class pair
{
    int first, second;
    pair(int f, int s)
    {
        this.first = f;
        this.second = s;
    }
}

// Function to check if the
// indices are valid or not
static boolean isValid(int i, int j,
                       int N, int M)
{
    return (i >= 0 && i < N &&
            j >= 0 && j < M);
}

// Function to evaluate the next
// index while moving diagonally up
static int[] up(int i, int j,
                int N, int M)
{
    if (isValid(i - 1, j + 1, N, M))
        return new int[]{ i - 1, j + 1 };
    else
        return new int[]{ -1, -1 };
}

// Function to evaluate the next
// index while moving diagonally down
static int[] down(int i, int j,
                  int N, int M)
{
    if (isValid(i + 1, j - 1, N, M))
        return new int[]{ i + 1, j - 1 };
    else
        return new int[]{ -1, -1 };
}

// Function to print matrix elements
// diagonally in Spiral Form
static void SpiralDiagonal(int N, int M,
                           int K, int[][] a)
{
    int i = 0, j = 0;

    // Total Number of Diagonals
    // = N + M - 1
    for(int diagonal = 0;
            diagonal < N + M - 1;
            diagonal++)
    {
        while (true)
        {

            // Stop when K is
            // encountered
            if (a[i][j] == K)
            {
                System.out.print(K);
                return;
            }

            // Print the integer
            System.out.print(a[i][j] + ", ");

            // Store the next index
            int[] next;

            if ((diagonal & 1) == 1)
            {
                next = down(i, j, N, M);
            }
            else
            {
                next = up(i, j, N, M);
            }

            // If current index is invalid
            if (next[0] == next[1] &&
                next[1] == -1)
            {

                // Move to the next diagonal
                if ((diagonal & 1) == 1)
                {
                    if (i + 1 < N)
                        ++i;
                    else
                        ++j;
                }
                else
                {
                    if (j + 1 < M)
                        ++j;
                    else
                        ++i;
                }
                break;
            }

            // Otherwise move to the
            // next valid index
            else
            {
                i = next[0];
                j = next[1];
            }
        }
    }
}

// Driver code
public static void main (String[] args)
{
    int N = 5, M = 6, K = 15;
    int[][] arr = { { 1, 2, 3, 4, 5, 6 },
                    { 7, 8, 9, 10, 11, 12 },
                    { 13, 14, 15, 16, 17, 18 },
                    { 19, 20, 21, 22, 23, 24 },
                    { 25, 26, 27, 28, 29, 30 } };

    // Function Call
    SpiralDiagonal(N, M, K, arr);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to check if the
# indices are valid or not
def isValid(i, j, N, M):
    return (i >= 0 and i < N and j >= 0 and j < M)

# Function to evaluate the next
# index while moving diagonally up
def up(i, j, N, M):
    if(isValid(i - 1, j + 1, N, M)):
        return [i - 1, j + 1 ]
    else:
        return [-1, -1]

# Function to evaluate the next
# index while moving diagonally down
def down(i, j, N, M):
    if(isValid(i + 1, j - 1, N, M)):
        return [i + 1, j - 1 ]
    else:
        return [-1, -1]

# Function to print matrix elements
# diagonally in Spiral Form
def SpiralDiagonal(N, M, K, a):
    i = 0
    j = 0

    # Total Number of Diagonals
    # = N + M - 1
    for diagonal in range(N + M - 1):

        while(True):

            # Stop when K is
            # encountered
            if(a[i][j] == K):
                print(K, end = "")
                return

            # Print the integer
            print(a[i][j], ", ", end="", sep="")

            # Store the next index
            next = []
            if((diagonal & 1) == 1):
                next = down(i, j, N, M)
            else:
                next = up(i, j, N, M)

            # If current index is invalid
            if(next[0] == next[1] and next[1] == -1):

                # Move to the next diagonal
                if((diagonal & 1) == 1):
                    if(i + 1 < N):
                        i += 1
                    else:
                        j += 1
                else:
                    if(j + 1 < M):
                        j += 1
                    else:
                        i += 1
                break

            # Otherwise move to the
            # next valid index
            else:
                i = next[0]
                j = next[1]

# Driver code
N = 5
M = 6
K = 15
arr = [[1, 2, 3, 4, 5, 6 ],
       [ 7, 8, 9, 10, 11, 12],
       [13, 14, 15, 16, 17, 18 ],
       [19, 20, 21, 22, 23, 24],
       [25, 26, 27, 28, 29, 30]]

# Function Call
SpiralDiagonal(N, M, K, arr);

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the
// above approach
using System;

class GFG{

// Function to check if the
// indices are valid or not
static bool isValid(int i, int j,
                    int N, int M)
{
    return (i >= 0 && i < N &&
            j >= 0 && j < M);
}

// Function to evaluate the next
// index while moving diagonally up
static int[] up(int i, int j, int N, int M)
{
    if (isValid(i - 1, j + 1, N, M))
        return new int[]{ i - 1, j + 1 };
    else
        return new int[]{ -1, -1 };
}

// Function to evaluate the next
// index while moving diagonally down
static int[] down(int i, int j, int N, int M)
{
    if (isValid(i + 1, j - 1, N, M))
        return new int[]{ i + 1, j - 1 };
    else
        return new int[]{ -1, -1 };
}

// Function to print matrix elements
// diagonally in Spiral Form
static void SpiralDiagonal(int N, int M, int K,
                           int[, ] a)
{
    int i = 0, j = 0;

    // Total Number of Diagonals
    // = N + M - 1
    for(int diagonal = 0;
            diagonal < N + M - 1;
            diagonal++)
    {
        while (true)
        {

            // Stop when K is
            // encountered
            if (a[i, j] == K)
            {
                Console.Write(K);
                return;
            }

            // Print the integer
            Console.Write(a[i, j] + ", ");

            // Store the next index
            int[] next;

            if ((diagonal & 1) == 1)
            {
                next = down(i, j, N, M);
            }
            else
            {
                next = up(i, j, N, M);
            }

            // If current index is invalid
            if (next[0] == next[1] &&
                next[1] == -1)
            {

                // Move to the next diagonal
                if ((diagonal & 1) == 1)
                {
                    if (i + 1 < N)
                        ++i;
                    else
                        ++j;
                }
                else
                {
                    if (j + 1 < M)
                        ++j;
                    else
                        ++i;
                }
                break;
            }

            // Otherwise move to the
            // next valid index
            else
            {
                i = next[0];
                j = next[1];
            }
        }
    }
}

// Driver code
public static void Main(string[] args)
{
    int N = 5, M = 6, K = 15;
    int[, ] arr = { { 1, 2, 3, 4, 5, 6 },
                    { 7, 8, 9, 10, 11, 12 },
                    { 13, 14, 15, 16, 17, 18 },
                    { 19, 20, 21, 22, 23, 24 },
                    { 25, 26, 27, 28, 29, 30 } };

    // Function Call
    SpiralDiagonal(N, M, K, arr);
}
}

// This code is contributed by grand_master
```

## java 描述语言

```
<script>

// JavaScript implementation for the above approach

// Function to check if the
// indices are valid or not
function isValid(i, j, N, M)
{
    return (i >= 0 && i < N
            && j >= 0 && j < M);
}

// Function to evaluate the next
// index while moving diagonally up
function up( i, j, N, M)
{
    if (isValid(i - 1, j + 1, N, M))
        return [ i - 1, j + 1 ];
    else
        return [ -1, -1 ];
}

// Function to evaluate the next
// index while moving diagonally down
function down( i, j, N, M)
{
    if (isValid(i + 1, j - 1, N, M))
        return [ i + 1, j - 1 ];
    else
        return [ -1, -1 ];
}

// Function to print matrix elements
// diagonally in Spiral Form
function SpiralDiagonal(N,M,K,a)
{
    var i = 0, j = 0;

    // Total Number of Diagonals
    // = N + M - 1
    for (var diagonal = 0;
        diagonal < N + M - 1;
        diagonal++) {

        while (1) {

            // Stop when K is
            // encountered
            if (a[i][j] == K) {

                document.write(K);
                return;
            }

            // Print the integer
            document.write(a[i][j], ", ");

            // Store the next index
            var next = new Array(2);
            if (diagonal & 1) {

                next = down(i, j, N, M);
            }
            else {

                next = up(i, j, N, M);
            }

            // If current index is invalid
            if (next[0] == next[1]
                && next[0] == -1) {

                // Move to the next diagonal
                if (diagonal & 1) {

                    (i + 1 < N) ? ++i : ++j;
                }
                else {

                    (j + 1 < M) ? ++j : ++i;
                }
                break;
            }

            // Otherwise move to the
            // next valid index
            else {

                i = next[0];
                j = next[1];
            }
        }
    }
}

// Driver Code
var N = 5, M = 6, K = 15;
var arr = [[1, 2, 3, 4, 5, 6 ],
       [ 7, 8, 9, 10, 11, 12],
       [13, 14, 15, 16, 17, 18 ],
       [19, 20, 21, 22, 23, 24],
       [25, 26, 27, 28, 29, 30]];

// Function Call
SpiralDiagonal(N, M, K, arr);

// This code is contributed by Shubham Singh

</script>
```

**输出:**

```
1, 2, 7, 13, 8, 3, 4, 9, 14, 19, 25, 20, 15
```

***时间复杂度:** O(N*M)*
***辅助** **空间:** O(1)*