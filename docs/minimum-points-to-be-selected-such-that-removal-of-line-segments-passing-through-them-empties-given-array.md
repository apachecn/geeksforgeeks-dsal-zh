# 要选择的最小点，使得通过它们的线段的移除清空给定的阵列

> 原文:[https://www . geesforgeks . org/最小待选点-这样-删除线段-通过它们-清空-给定数组/](https://www.geeksforgeeks.org/minimum-points-to-be-selected-such-that-removal-of-line-segments-passing-through-them-empties-given-array/)

给定一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**arr【】【】**，其中每一行都是**{开始，结束}** 的形式，表示 **X** 轴上每个线段的开始和结束点。一步，在 **X** 轴上选择一个点，删除所有通过该点的线段。任务是找到删除[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)所有线段需要选择的此类点的最小个数。

**示例:**

> **输入:** arr[][]= { {9，15}、{3，8}、{1，6}、{7，12}、{5，10} }
> **输出:** 2
> **解释:**
> 在 **X-** 轴上选择点 arr[2][1](= (6，0)并删除第二(= arr[1])、第三(= arr[2])和第五(= arr[4])线段
> 选择 X 轴上的点 arr[3][1](= (12，0))，删除第一条(=arr[0])和第四条(=arr[3])线段。
> 因此，要求计数为 2。
> 
> **输入:** arr[][]={ {1，4}，{5，7}，{9，13} }
> **输出:** 3

**方法:**使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   初始化一个变量，说 **cntSteps** 来计算删除所有线段所需的步骤总数。
*   [根据线段](https://www.geeksforgeeks.org/sorting-2d-vector-in-c-set-1-by-row-and-column/)的端点对数组 **arr[][]** 进行排序。
*   初始化一个变量，说**点= arr[0][1]** 来存储 **X** 轴的点。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查**arr【I】【0】**的值是否大于**点**。如果发现为真，则将值**增加**步数 **1** 并更新**点= arr[i][1]** 的值。
*   最后，打印 **cntSteps** 的值。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Comparator function
bool comp(vector<int> &x, vector<int> y)
{
    return x[1] < y[1];
}

// Function to count the minimum number of
// steps required to delete all the segments
int cntMinSteps(vector<vector<int> > &arr,
                                   int N)
{

    // Stores count of steps required
    // to delete all the line segments
    int cntSteps = 1;

    // Sort the array based on end points
    // of line segments
    sort(arr.begin(), arr.end(), comp);

    // Stores point on X-axis
    int Points = arr[0][1];

    // Traverse the array
    for(int i = 0; i < N; i++) {

        // If arr[1][0] is
        // greater than Points
        if(arr[i][0] > Points) {

            // Update cntSteps
            cntSteps++;

            // Update Points
            Points = arr[i][1];
        }
    }

    return cntSteps;

}

// Driver Code
int main() {

    vector<vector<int> > arr
       = { { 9, 15 }, { 3, 8 },
            { 1, 6 }, { 7, 12 },
                      { 5, 10 } };

    int N = arr.size();

    cout<< cntMinSteps(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to sort by column
public static void sortbyColumn(int arr[][],
                                int col)
{

    // Using built-in sort function Arrays.sort
    Arrays.sort(arr, new Comparator<int[]>()
    {
        @Override

        // Compare values according to columns
        public int compare(final int[] entry1, 
                           final int[] entry2)
        {

            // To sort in descending order revert 
            // the '>' Operator
            if (entry1[col] > entry2[col])
                return 1;
            else
                return -1;
        }
    });  // End of function call sort().
}

// Function to count the minimum number of
// steps required to delete all the segments
static int cntMinSteps(int[][] arr, int N)
{

    // Stores count of steps required
    // to delete all the line segments
    int cntSteps = 1;

    // Sort the array based on end points
    // of line segments
    sortbyColumn(arr, 1);

    // Stores point on X-axis
    int Points = arr[0][1];

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If arr[1][0] is
        // greater than Points
        if(arr[i][0] > Points)
        {

            // Update cntSteps
            cntSteps++;

            // Update Points
            Points = arr[i][1];
        }
    }
    return cntSteps;
}

// Driver Code
public static void main(String[] args)
{
    int[][] arr = { { 9, 15 }, { 3, 8 },
                    { 1, 6 }, { 7, 12 },
                    { 5, 10 } };

    int N = arr.length;

    System.out.print(cntMinSteps(arr, N));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Comparator function
def comp(x, y):
    return x[1] < y[1]

# Function to count the
# minimum number of steps
# required to delete all
# the segments
def cntMinSteps(arr, N):

    # Stores count of steps
    # required to delete all
    # the line segments
    cntSteps = 1

    # Sort the array based
    # on end points of line
    # segments
    arr.sort(reverse = False)   

    # Stores point on X-axis
    Points = arr[0][1]   

    # Traverse the array
    for i in range(N):

        # If arr[1][0] is
        # greater than Points
        if(arr[i][0] > Points):

            # Update cntSteps
            cntSteps += 1

            # Update Points
            Points = arr[i][1]

    return cntSteps

# Driver Code
if __name__ == '__main__':

    arr = [[9, 15], [3, 8],
           [1, 6], [7, 12],
           [5, 10]]           
    N = len(arr)
    print(cntMinSteps(arr, N))

# This code is contributed by bgangwar59
```

**Output:** 

```
2
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*