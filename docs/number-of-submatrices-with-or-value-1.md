# 或值为 1 的子矩阵数量

> 原文:[https://www . geeksforgeeks . org/带-or-value-1 的子矩阵数/](https://www.geeksforgeeks.org/number-of-submatrices-with-or-value-1/)

给定一个 **N*N** 二进制矩阵，任务是求 OR 值为 1 的矩形子矩阵的个数。

**示例:**

```
Input : arr[][] = {{0, 0, 0},
                   {0, 0, 0},
                   {0, 0, 0}}
Output : 0
Explanation: All the submatrices will have an OR value 0.
Thus, ans = 0.

Input : arr[][] = {{0, 0, 0},
                  {0, 1, 0},
                  {0, 0, 0}}
Output : 16 
```

一个**简单的解决方案**是生成所有可能的子矩阵，然后检查其中是否有任何值为 1。如果对于一个子矩阵，至少有一个元素是 1，我们将最终答案的值增加 1。上述方法的时间复杂度为 0(n<sup>6</sup>)。

**更好的做法**:换个角度来看这个问题。我们现在将试图找到全为 0 的子矩阵的数量。对于最终的答案，我们将从子矩阵的总数中减去这个值。
为了优化该过程，对于矩阵的每个索引，我们将尝试从其中全为 0 的索引开始寻找子矩阵的数量。
我们解决这个问题的第一步是创建一个矩阵‘p _ arr’。

*   对于每个索引(R，C)，如果 arr[R][C]等于 0，那么在 p_arr[R][C]中，我们将在遇到“1”或数组末尾加 1 之前，沿着行“R”存储单元格(R，C)右侧的 0 数。
*   如果 arr[R][C]等于 1，p_arr[R][C]等于零。

为了创建这个矩阵，我们将使用以下递归关系。

```
IF arr[R][C] is 0
    p_arr[R][C] = p_arr[R][C+1] + 1
ELSE 
    p_arr[R][C] = 0

arr[][] = {{1, 0, 0, 0},
           {0, 1, 0, 1},
           {0, 1, 0, 0},
           {0, 0, 0, 0}}

p_arr[][] for above will look like
          {{0, 3, 2, 1},
           {1, 0, 1, 0},
           {1, 0, 2, 1},
           {4, 3, 2, 1}}
```

一旦我们有了所需的矩阵 **p_arr** ，我们将开始逐列处理矩阵‘p _ arr’。如果我们正在处理矩阵“p_arr”的 j <sup>第</sup>列，那么对于该列的每个元素“I”，我们将尝试从单元格 **(i，j)** 开始查找子矩阵的数量，所有这些都是 0。
对此，我们可以使用栈数据结构。

**算法**:

1.  初始化一个堆栈“q”来存储被推入的元素的值以及堆栈中被推入的元素数量的计数(C <sub>ij</sub> )，其值**严格大于当前元素的值**。我们将使用配对将两个数据联系在一起。
    用 0 初始化变量为 _sum。在每一步，这个变量被更新以存储从在该步被推的元素开始的全 0 的子矩阵的数量。因此，使用“to_sum”，我们在每一步更新全为 0 的子矩阵的计数。
2.  对于“j”列，在任何步骤“I”中，我们都将准备在堆栈中推送 p_arr[i][j]。让 Q <sub>t</sub> 代表堆栈的最顶层元素，C <sub>t</sub> 代表堆栈中先前推送的元素数量，其值大于堆栈的最顶层元素。在推入堆栈中的元素“p_arr[i][j]”之前，当堆栈不为空或最顶层元素大于要推入的数量时，继续弹出堆栈的最顶层元素，同时将**更新为 _sum** 为**to _ sum+=(C<sub>t</sub>+1)*(Q<sub>t</sub>–p _ arr[I][j])**。让 C <sub>i，j</sub> 代表大于当前元素的元素数量，当前元素是先前在此堆栈中推送的。我们还需要记录 C <sub>i，j</sub> 。因此，在弹出一个元素之前，我们将 C <sub>i，j</sub> 更新为 C <sub>i，j</sub> += C <sub>t</sub> 以及 to_sum。
3.  我们将全零的子矩阵数更新为 count _ zero _ 矩阵+= to_sum。
4.  最后，我们在将该元素与 C <sub>i，j</sub> 配对后，将它推入堆栈。

N*N 矩阵中子矩阵的总数等于:

```
(N2 * (N + 1)2)/4
```

因此，最终答案将是:

```
ans = (N2 * (N + 1)2)/4 - count_zero_submatrices 
```

我们在 O(N <sup>2</sup> 中创建前缀数组，对于每一列，我们在堆栈中推送一个元素或者只弹出一次。因此，该算法的时间复杂度为 0(N<sup>2</sup>)。

下面是上述方法的实现:

## C++

```
// C++ program to count number of submatrices
// with OR value 1

#include <iostream>
#include <stack>
#define n 3
using namespace std;

// Function to find required prefix-count for each row
// from right to left
void findPrefixCount(int p_arr[][n], bool arr[][n])
{
    for (int i = 0; i < n; i++)
        for (int j = n - 1; j >= 0; j--) {

            if (arr[i][j])
                continue;
            if (j != n - 1)
                p_arr[i][j] += p_arr[i][j + 1];

            p_arr[i][j] += (int)(!arr[i][j]);
        }
}

// Function to find the count of submatrices
// with OR value 1
int matrixOrValueOne(bool arr[][n])
{
    // Array to store prefix count of zeros from
    // right to left for boolean array
    int p_arr[n][n] = { 0 };

    findPrefixCount(p_arr, arr);

    // Variable to store the count of
    // submatrices with OR value 0
    int count_zero_submatrices = 0;

    // Loop to evaluate each column of
    // the prefix matrix uniquely.
    // For each index of a column we will try to
    // determine the number of sub-matrices
    // starting from that index
    // and has all 1s
    for (int j = 0; j < n; j++) {

        int i = n - 1;

        // stack to store elements and the count
        // of the numbers they popped

        // First part of pair will be the
        // value of inserted element.
        // Second part will be the count
        // of the number of elements pushed
        // before with a greater value
        stack<pair<int, int> > q;

        // Variable to store the number of submatrices
        // with all 0s
        int to_sum = 0;

        while (i >= 0) {

            int c = 0;

            while (q.size() != 0 and q.top().first > p_arr[i][j]) {

                to_sum -= (q.top().second + 1) *
                             (q.top().first - p_arr[i][j]);

                c += q.top().second + 1;

                q.pop();
            }

            to_sum += p_arr[i][j];

            count_zero_submatrices += to_sum;

            q.push({ p_arr[i][j], c });

            i--;
        }
    }

    // Return the final answer
    return (n * (n + 1) * n * (n + 1)) / 4
           - count_zero_submatrices;
}

// Driver Code
int main()
{
    bool arr[][n] = { { 0, 0, 0 },
                      { 0, 1, 0 },
                      { 0, 0, 0 } };

    cout << matrixOrValueOne(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of submatrices
// with OR value 1
import java.util.*;

class GFG
{
static int n = 3;
static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find required prefix-count
// for each row from right to left
static void findPrefixCount(int p_arr[][],
                            boolean arr[][])
{
    for (int i = 0; i < n; i++)
        for (int j = n - 1; j >= 0; j--)
        {
            if (arr[i][j])
                continue;
            if (j != n - 1)
                p_arr[i][j] += p_arr[i][j + 1];

            p_arr[i][j] += (arr[i][j] == false ? 1 : 0);
        }
}

// Function to find the count of submatrices
// with OR value 1
static int matrixOrValueOne(boolean arr[][])
{
    // Array to store prefix count of zeros from
    // right to left for boolean array
    int [][]p_arr = new int[n][n];

    findPrefixCount(p_arr, arr);

    // Variable to store the count of
    // submatrices with OR value 0
    int count_zero_submatrices = 0;

    // Loop to evaluate each column of
    // the prefix matrix uniquely.
    // For each index of a column we will try to
    // determine the number of sub-matrices
    // starting from that index
    // and has all 1s
    for (int j = 0; j < n; j++)
    {
        int i = n - 1;

        // stack to store elements and the count
        // of the numbers they popped

        // First part of pair will be the
        // value of inserted element.
        // Second part will be the count
        // of the number of elements pushed
        // before with a greater value
        Stack<pair> q = new Stack<pair>();

        // Variable to store the number of submatrices
        // with all 0s
        int to_sum = 0;

        while (i >= 0)
        {
            int c = 0;

            while (q.size() != 0 &&
                   q.peek().first > p_arr[i][j])
            {

                to_sum -= (q.peek().second + 1) *
                          (q.peek().first - p_arr[i][j]);

                c += q.peek().second + 1;

                q.pop();
            }

            to_sum += p_arr[i][j];

            count_zero_submatrices += to_sum;

            q.add(new pair(p_arr[i][j], c ));

            i--;
        }
    }

    // Return the final answer
    return (n * (n + 1) * n * (n + 1)) / 4
        - count_zero_submatrices;
}

// Driver Code
public static void main(String[] args)
{
    boolean arr[][] = { { false, false, false },
                        { false, true, false },
                        { false, false, false } };

    System.out.println(matrixOrValueOne(arr));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to count number
# of submatrices with OR value 1

# Function to find required prefix-count
# for each row from right to left
def findPrefixCount(p_arr, arr):

    for i in range(0, n):
        for j in range(n - 1, -1, -1):

            if arr[i][j]:
                continue
            if j != n - 1:
                p_arr[i][j] += p_arr[i][j + 1]

            p_arr[i][j] += int(not arr[i][j])

# Function to find the count
# of submatrices with OR value 1
def matrixOrValueOne(arr):

    # Array to store prefix count of zeros
    # from right to left for boolean array
    p_arr = [[0 for i in range(n)]     
                for j in range(n)]

    findPrefixCount(p_arr, arr)

    # Variable to store the count of
    # submatrices with OR value 0
    count_zero_submatrices = 0

    # Loop to evaluate each column of
    # the prefix matrix uniquely.
    # For each index of a column we will try
    # to determine the number of sub-matrices
    # starting from that index and has all 1s
    for j in range(0, n):

        i = n - 1

        # stack to store elements and the
        # count of the numbers they popped

        # First part of pair will be the
        # value of inserted element.
        # Second part will be the count
        # of the number of elements pushed
        # before with a greater value
        q = []

        # Variable to store the number
        # of submatrices with all 0s
        to_sum = 0

        while i >= 0:

            c = 0
            while (len(q) != 0 and
                   q[-1][0] > p_arr[i][j]):

                to_sum -= ((q[-1][1] + 1) *
                           (q[-1][0] - p_arr[i][j]))

                c += q.pop()[1] + 1

            to_sum += p_arr[i][j]
            count_zero_submatrices += to_sum

            q.append((p_arr[i][j], c))
            i -= 1

    # Return the final answer
    return ((n * (n + 1) * n * (n + 1)) //
             4 - count_zero_submatrices)

# Driver Code
if __name__ == "__main__":

    n = 3
    arr = [[0, 0, 0],
           [0, 1, 0],
           [0, 0, 0]]

    print(matrixOrValueOne(arr))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to count number of submatrices
// with OR value 1
using System;
using System.Collections.Generic;

class GFG
{
static int n = 3;
class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find required prefix-count
// for each row from right to left
static void findPrefixCount(int [,]p_arr,
                            bool [,]arr)
{
    for (int i = 0; i < n; i++)
        for (int j = n - 1; j >= 0; j--)
        {
            if (arr[i, j])
                continue;
            if (j != n - 1)
                p_arr[i, j] += p_arr[i, j + 1];

            p_arr[i, j] += (arr[i, j] == false ? 1 : 0);
        }
}

// Function to find the count of submatrices
// with OR value 1
static int matrixOrValueOne(bool [,]arr)
{
    // Array to store prefix count of zeros from
    // right to left for bool array
    int [,]p_arr = new int[n, n];

    findPrefixCount(p_arr, arr);

    // Variable to store the count of
    // submatrices with OR value 0
    int count_zero_submatrices = 0;

    // Loop to evaluate each column of
    // the prefix matrix uniquely.
    // For each index of a column we will try to
    // determine the number of sub-matrices
    // starting from that index
    // and has all 1s
    for (int j = 0; j < n; j++)
    {
        int i = n - 1;

        // stack to store elements and the count
        // of the numbers they.Popped

        // First part of pair will be the
        // value of inserted element.
        // Second part will be the count
        // of the number of elements.Pushed
        // before with a greater value
        Stack<pair> q = new Stack<pair>();

        // Variable to store the number of
        // submatrices with all 0s
        int to_sum = 0;

        while (i >= 0)
        {
            int c = 0;

            while (q.Count != 0 &&
                   q.Peek().first > p_arr[i, j])
            {

                to_sum -= (q.Peek().second + 1) *
                          (q.Peek().first - p_arr[i, j]);

                c += q.Peek().second + 1;

                q.Pop();
            }

            to_sum += p_arr[i, j];

            count_zero_submatrices += to_sum;

            q.Push(new pair(p_arr[i, j], c));

            i--;
        }
    }

    // Return the final answer
    return (n * (n + 1) * n * (n + 1)) / 4 -
                     count_zero_submatrices;
}

// Driver Code
public static void Main(String[] args)
{
    bool [,]arr = { { false, false, false },
                    { false, true, false },
                    { false, false, false } };

    Console.WriteLine(matrixOrValueOne(arr));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to count number of submatrices
// with OR value 1

var n = 3

// Function to find required prefix-count for each row
// from right to left
function findPrefixCount(p_arr, arr)
{
    for (var i = 0; i < n; i++)
        for (var j = n - 1; j >= 0; j--) {

            if (arr[i][j])
                continue;
            if (j != n - 1)
                p_arr[i][j] += p_arr[i][j + 1];

            p_arr[i][j] += (!arr[i][j]);
        }
}

// Function to find the count of submatrices
// with OR value 1
function matrixOrValueOne(arr)
{
    // Array to store prefix count of zeros from
    // right to left for boolean array
    var p_arr = Array.from(Array(n), ()=> Array(n).fill(0));

    findPrefixCount(p_arr, arr);

    // Variable to store the count of
    // submatrices with OR value 0
    var count_zero_submatrices = 0;

    // Loop to evaluate each column of
    // the prefix matrix uniquely.
    // For each index of a column we will try to
    // determine the number of sub-matrices
    // starting from that index
    // and has all 1s
    for (var j = 0; j < n; j++) {

        var i = n - 1;

        // stack to store elements and the count
        // of the numbers they popped

        // First part of pair will be the
        // value of inserted element.
        // Second part will be the count
        // of the number of elements pushed
        // before with a greater value
        var q = [];

        // Variable to store the number of submatrices
        // with all 0s
        var to_sum = 0;

        while (i >= 0) {

            var c = 0;

            while (q.length != 0 && q[q.length-1][0] > p_arr[i][j]) {

                to_sum -= (q[q.length-1][1] + 1) *
                             (q[q.length-1][0] - p_arr[i][j]);

                c += q[q.length-1][1] + 1;

                q.pop();
            }

            to_sum += p_arr[i][j];

            count_zero_submatrices += to_sum;

            q.push([p_arr[i][j], c]);

            i--;
        }
    }

    // Return the final answer
    return (n * (n + 1) * n * (n + 1)) / 4
           - count_zero_submatrices;
}

// Driver Code
var arr = [ [ 0, 0, 0 ],
                  [ 0, 1, 0 ],
                  [ 0, 0, 0 ] ];
document.write( matrixOrValueOne(arr));

</script>
```

**Output:** 

```
16
```