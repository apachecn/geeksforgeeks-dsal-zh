# 打印给定矩阵中按零计数排序的列的索引

> 原文:[https://www . geesforgeks . org/print-列索引-按给定矩阵中的零计数排序/](https://www.geeksforgeeks.org/print-index-of-columns-sorted-by-count-of-zeroes-in-the-given-matrix/)

给定一个有 N 行 M 列的矩阵。任务是根据每列中不断增加的零数打印给定矩阵的列索引。
例如，如果第一列包含 2 个零，第二列包含 1 个零，第三列不包含任何零。那么输出将是 3，2，1。

**注**:矩阵被认为具有基于 1 的索引。

**示例:**

```
Input : mat[N][M] ={{0, 0, 0},
                    {0, 2, 0},
                    {0, 1, 1},
                    {1, 1, 1}};
Output : 2 3 1 
No. of zeroes in first col: 3
No. of zeroes in second col: 1
No of zeroes in third col: 2
Therefore, sorted order of count is 1 2 3
and their corresponding column numbers are, 2 3 1

Input: mat[N][M] ={{0, 0, 0},
                    {0, 0, 3},
                    {0, 1, 1}};
Output : 3 2 1 
```

**接近**:

1.  创建一个向量对来存储每列中的零计数。其中对的第一个元素是计数，对的第二个元素是对应的列索引。
2.  按列遍历矩阵。
3.  在成对向量中插入每列的零计数。
4.  根据零的计数对向量进行排序。
5.  打印该对中的第二个元素，该元素包含根据零的计数排序的列的索引。

下面是上述方法的实现:

## C++

```
// C++ Program to print the index of columns
// of the given matrix based on the
// increasing number of zeroes in each column

#include <bits/stdc++.h>

using namespace std;

#define N 4 // rows
#define M 3 // columns

// Function to print the index of columns
// of the given matrix based on the
// increasing number of zeroes in each column
void printColumnSorted(int mat[N][M])
{
    // Vector of pair to store count of zeroes
    // in each column.
    // First element of pair is count
    // Second element of pair is column index
    vector<pair<int, int> > colZeroCount;

    // Traverse the matrix column wise
    for (int i = 0; i < M; i++) {
        int count = 0;

        for (int j = 0; j < N; j++) {
            if (mat[j][i] == 0)
                count++;
        }

        // Insert the count of zeroes for each column
        // in the vector of pair
        colZeroCount.push_back(make_pair(count, i));
    }

    // Sort the vector of pair according to the
    // count of zeroes
    sort(colZeroCount.begin(), colZeroCount.end());

    // Print the second element of the pair which
    // contain indexes of the sorted vector of pair
    for (int i = 0; i < M; i++)
        cout << colZeroCount[i].second + 1 << " ";
}

// Driver Code
int main()
{
    int mat[N][M] = { { 0, 0, 0 },
                      { 0, 2, 0 },
                      { 0, 1, 1 },
                      { 1, 1, 1 } };

    printColumnSorted(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the index of columns
// of the given matrix based on the increasing
// number of zeroes in each column
import java.io.*;
import java.util.*;

class GFG{

static int N = 4;
static int M = 3;

// Function to print the index of columns
// of the given matrix based on the increasing
// number of zeroes in each column
static void printColumnSorted(int[][] mat)
{

    // Vector of pair to store count of zeroes
    // in each column.First element of pair is
    // count.Second element of pair is column index
    ArrayList<
    ArrayList<Integer>> colZeroCount = new ArrayList<
                                           ArrayList<Integer>>();

    // Traverse the matrix column wise
    for(int i = 0; i < M; i++)
    {
        int count = 0;
        for(int j = 0; j < N; j++)
        {
            if (mat[j][i] == 0)
            {
                count++;
            }
        }

        // Insert the count of zeroes for
        // each column in the vector of pair
        colZeroCount.add(new ArrayList<Integer>(
            Arrays.asList(count,i)));
    }

    // Sort the vector of pair according to the
    // count of zeroes
    Collections.sort(colZeroCount,
                     new Comparator<ArrayList<Integer>>()
    {   
        @Override
        public int compare(ArrayList<Integer> o1,
                           ArrayList<Integer> o2)
        {
            return o1.get(0).compareTo(o2.get(0));
        }              
    });

    // Print the second element of the pair which
    // contain indexes of the sorted vector of pair
    for(int i = 0; i < M; i++)
    {
        System.out.print(
            (colZeroCount.get(i).get(1) + 1) + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int[][] mat = { { 0, 0, 0 }, { 0, 2, 0 },
                    { 0, 1, 1 }, { 1, 1, 1 } };

    printColumnSorted(mat);
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program to print the index of
# columns of the given matrix based
# on the increasing number of zeroes
# in each column

# Rows
N = 4

# Columns
M = 3

# Function to print the index of columns
# of the given matrix based on the
# increasing number of zeroes in
# each column
def printColumnSorted(mat):

    # Vector of pair to store count
    # of zeroes in each column.
    # First element of pair is count
    # Second element of pair is column index
    colZeroCount = []

    # Traverse the matrix column wise
    for i in range(M):
        count = 0

        for j in range(N):
            if (mat[j][i] == 0):
                count += 1

        # Insert the count of zeroes for
        # each column in the vector of pair
        colZeroCount.append((count, i))

    # Sort the vector of pair according
    # to the count of zeroes
    colZeroCount = sorted(colZeroCount)

    # Print the second element of the
    # pair which contain indexes of the
    # sorted vector of pair
    for i in range(M):
        print(colZeroCount[i][1] + 1, end = " ")

# Driver Code
if __name__ == '__main__':

    mat = [ [ 0, 0, 0 ],
            [ 0, 2, 0 ],
            [ 0, 1, 1 ],
            [ 1, 1, 1 ] ]

    printColumnSorted(mat)

# This code is contributed mohit kumar 29
```

## java 描述语言

```
<script>
// Javascript program to print the index of columns
// of the given matrix based on the increasing
// number of zeroes in each column

let N = 4;
let M = 3;

// Function to print the index of columns
// of the given matrix based on the increasing
// number of zeroes in each column
function printColumnSorted(mat)
{
    // Vector of pair to store count of zeroes
    // in each column.First element of pair is
    // count.Second element of pair is column index
    let colZeroCount = [];

    // Traverse the matrix column wise
    for(let i = 0; i < M; i++)
    {
        let count = 0;
        for(let j = 0; j < N; j++)
        {
            if (mat[j][i] == 0)
            {
                count++;
            }
        }

        // Insert the count of zeroes for
        // each column in the vector of pair
        colZeroCount.push([count,i]);
    }

    // Sort the vector of pair according to the
    // count of zeroes
    colZeroCount.sort(function(a,b){return a[0]-b[0];});

    // Print the second element of the pair which
    // contain indexes of the sorted vector of pair
    for(let i = 0; i < M; i++)
    {
        document.write(
            (colZeroCount[i][1] + 1) + " ");
    }
}

// Driver Code
let mat = [ [ 0, 0, 0 ],
            [ 0, 2, 0 ],
            [ 0, 1, 1 ],
            [ 1, 1, 1 ] ];

printColumnSorted(mat);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
2 3 1
```