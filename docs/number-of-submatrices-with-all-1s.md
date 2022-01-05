# 全 1 的子矩阵数

> 原文:[https://www . geeksforgeeks . org/带有全 1 的子矩阵数量/](https://www.geeksforgeeks.org/number-of-submatrices-with-all-1s/)

给定一个只包含 0 和 1 的 **N*N** 矩阵，任务是计算包含所有 1 的子矩阵的数量。

**示例:**

```
Input : arr[][] = {{1, 1, 1},
                   {1, 1, 1},
                   {1, 1, 1}}
Output : 36
Explanation: All the possible submatrices will have only 1s.
Since, there are 36 submatrices in total, ans = 36

Input : {{1, 1, 1},
                   {1, 0, 1},
                   {1, 1, 1}}
Output : 20 
```

为了简单起见，我们将说一个子矩阵从一个索引(R，C)开始，如果那个特定的索引是它的左上角。
一个**简单的**解决方案是生成所有可能的子矩阵，然后检查其中的所有值是否都是 1。如果对于一个子矩阵，所有元素都是 1，我们将最终答案的值增加 1。上述方法的时间复杂度为 0(n<sup>6</sup>)。

**更好的方法**:为了优化过程，对于矩阵的每个索引，我们将尝试从其中全为 1 的索引开始寻找子矩阵的数量。
我们解决这个问题的第一步是创建一个矩阵‘p _ arr’。
对于每个索引(R，C)，如果 arr[R][C]等于 1，那么在 p_arr[R][C]中，我们将在遇到数组的第一个零或末尾加 1 之前，沿着行‘R’将 1 的数量存储到单元格(R，C)的右侧。
如果 arr[R][C]等于零，p_arr[R][C]也等于零。
为了创建这个矩阵，我们将使用以下递归关系。

```
IF arr[R][C] is not 0
    p_arr[R][C] = p_arr[R][C+1] + 1
ELSE 
    p_arr[R][C] = 0

arr[][] = {{1, 0, 1, 1},
           {0, 1, 0, 1},
           {1, 1, 1, 0},
           {1, 0, 1, 1}}
p_arr[][] for above will look like
          {{1, 0, 2, 1},
           {0, 1, 0, 1},
           {3, 2, 1, 0},
           {1, 0, 2, 1}}
```

一旦我们有了所需的矩阵 **p_arr** ，我们将进入下一步。按列查看矩阵“p_arr”。如果我们正在处理矩阵 p_arr 的第 j <sup>列</sup>列，那么对于该列的每个元素‘I’，我们将尝试找到从单元格 **(i，j)** 开始的所有 1 的子矩阵的数量。
对此，我们可以使用[栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)。

**算法**:

1.  初始化一个堆栈“q”来存储被推入的元素的值以及该堆栈中被推入的元素数量的计数(C <sub>ij</sub> )，其值**严格大于当前元素的值**。我们将使用一对来将这两个数据联系在一起。
    用 0 初始化变量“to_sum”。在每一步，这个变量被更新以存储子矩阵的数量，所有的 1 从在该步被推的元素开始。因此，使用“to_sum”，我们在每一步更新全为 1 的子矩阵的计数。
2.  对于“j”列，在任何步骤“I”中，我们都将准备在堆栈中推送 p_arr[i][j]。让 Q <sub>t</sub> 代表堆栈的最顶层元素，C <sub>t</sub> 代表堆栈中先前推送的元素数量，其值大于堆栈的最顶层元素。在推入堆栈中的元素“p_arr[i][j]”之前，当堆栈不为空或最顶层元素大于要推入的数量时，继续弹出堆栈的最顶层元素，同时将**更新为 _sum** 为**to _ sum+=(C<sub>t</sub>+1)*(Q<sub>t</sub>–p _ arr[I][j])**。让 C <sub>i、</sub>代表比当前元素大的元素的数量，当前元素是之前在这个堆栈中推送的。我们还需要记录 C <sub>i，j</sub> 。因此，在弹出一个元素之前，我们将 C <sub>i，j</sub> 更新为 C <sub>i，j</sub> += C <sub>t</sub> 以及 to_sum。
3.  我们将答案更新为 ans += to_sum。
4.  最后，我们在将该元素与 C <sub>i，j</sub> 配对后，将它推入堆栈。

在 O(n <sup>2</sup> 中创建前缀数组，对于每一列，我们在堆栈中推送一个元素或者只弹出一次。因此，该算法的时间复杂度为 0(n<sup>2</sup>)。

下面是上述方法的实现:

## C++

```
// C++ program to count number of
// sub-matrices with all 1s

#include <iostream>
#include <stack>

using namespace std;

#define n 3

// Function to find required prefix-count for
// each row from right to left
void findPrefixCount(int p_arr[][n], bool arr[][n])
{
    for (int i = 0; i < n; i++) {
        for (int j = n - 1; j >= 0; j--) {

            if (!arr[i][j])
                continue;

            if (j != n - 1)
                p_arr[i][j] += p_arr[i][j + 1];

            p_arr[i][j] += (int)arr[i][j];
        }
    }
}

// Function to count the number of
// sub-matrices with all 1s
int matrixAllOne(bool arr[][n])
{
    // Array to store required prefix count of
    // 1s from right to left for boolean array
    int p_arr[n][n] = { 0 };

    findPrefixCount(p_arr, arr);

    // variable to store the final answer
    int ans = 0;

    /*  Loop to evaluate each column of
        the prefix matrix uniquely.
        For each index of a column we will try to
        determine the number of sub-matrices
        starting from that index
        and has all 1s */
    for (int j = 0; j < n; j++) {

        int i = n - 1;

        /*  Stack to store elements and the count
            of the numbers they popped

            First part of pair will be the
            value of inserted element.
            Second part will be the count
            of the number of elements pushed
            before with a greater value */
        stack<pair<int, int> > q;

        // variable to store the number of
        // submatrices with all 1s
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

            ans += to_sum;

            q.push({ p_arr[i][j], c });

            i--;
        }
    }

    return ans;
}

// Driver Code
int main()
{
    bool arr[][n] = { { 1, 1, 0 },
                      { 1, 0, 1 },
                      { 0, 1, 1 } };

    cout << matrixAllOne(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of
// sub-matrices with all 1s
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

// Function to find required prefix-count for
// each row from right to left
static void findPrefixCount(int p_arr[][],
                            boolean arr[][])
{
    for (int i = 0; i < n; i++)
    {
        for (int j = n - 1; j >= 0; j--)
        {
            if (!arr[i][j])
                continue;

            if (j != n - 1)
                p_arr[i][j] += p_arr[i][j + 1];

            p_arr[i][j] += arr[i][j] == true ? 1 : 0;
        }
    }
}

// Function to count the number of
// sub-matrices with all 1s
static int matrixAllOne(boolean arr[][])
{
    // Array to store required prefix count of
    // 1s from right to left for boolean array
    int [][]p_arr = new int[n][n];

    findPrefixCount(p_arr, arr);

    // variable to store the final answer
    int ans = 0;

    /* Loop to evaluate each column of
        the prefix matrix uniquely.
        For each index of a column we will try to
        determine the number of sub-matrices
        starting from that index
        and has all 1s */
    for (int j = 0; j < n; j++)
    {
        int i = n - 1;

        /* Stack to store elements and the count
            of the numbers they popped

            First part of pair will be the
            value of inserted element.
            Second part will be the count
            of the number of elements pushed
            before with a greater value */
        Stack<pair> q = new Stack<pair>();

        // variable to store the number of
        // submatrices with all 1s
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

            ans += to_sum;

            q.add(new pair(p_arr[i][j], c));

            i--;
        }
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    boolean arr[][] = { { true, true, false },
                        { true, false, true },
                        { false, true, true } };

    System.out.println(matrixAllOne(arr));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to count the number
# of sub-matrices with all 1s

# Function to find required prefix-count
# for each row from right to left
def findPrefixCount(p_arr, arr):

    for i in range(0, n):
        for j in range(n - 1, -1, -1):

            if not arr[i][j]:
                continue

            if j != n - 1:
                p_arr[i][j] += p_arr[i][j + 1]

            p_arr[i][j] += arr[i][j]

# Function to count the number of
# sub-matrices with all 1s
def matrixAllOne(arr):

    # Array to store required prefix count of
    # 1s from right to left for boolean array
    p_arr = [[0 for i in range(n)] for j in range(n)]

    findPrefixCount(p_arr, arr)

    # variable to store the final answer
    ans = 0

    # Loop to evaluate each column of
    # the prefix matrix uniquely.
    # For each index of a column we will try to
    # determine the number of sub-matrices
    # starting from that index and has all 1s
    for j in range(0, n):

        i = n - 1

        # Stack to store elements and the count
        # of the numbers they popped

        # First part of pair will be the
        # value of inserted element.
        # Second part will be the count
        # of the number of elements pushed
        # before with a greater value */
        q = []

        # variable to store the number of
        # submatrices with all 1s
        to_sum = 0

        while i >= 0:

            c = 0
            while len(q) != 0 and q[-1][0] > p_arr[i][j]:

                to_sum -= (q[-1][1] + 1) * \
                            (q[-1][0] - p_arr[i][j])

                c += q[-1][1] + 1
                q.pop()

            to_sum += p_arr[i][j]
            ans += to_sum

            q.append((p_arr[i][j], c))
            i -= 1

    return ans

# Driver Code
if __name__ == "__main__":

    arr = [[1, 1, 0], [1, 0, 1], [0, 1, 1]]

    n = 3
    print(matrixAllOne(arr))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to count number of
// sub-matrices with all 1s
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

// Function to find required prefix-count for
// each row from right to left
static void findPrefixCount(int [,]p_arr,
                            Boolean [,]arr)
{
    for (int i = 0; i < n; i++)
    {
        for (int j = n - 1; j >= 0; j--)
        {
            if (!arr[i, j])
                continue;

            if (j != n - 1)
                p_arr[i, j] += p_arr[i, j + 1];

            p_arr[i, j] += arr[i, j] == true ? 1 : 0;
        }
    }
}

// Function to count the number of
// sub-matrices with all 1s
static int matrixAllOne(Boolean [,]arr)
{
    // Array to store required prefix count of
    // 1s from right to left for boolean array
    int [,]p_arr = new int[n, n];

    findPrefixCount(p_arr, arr);

    // variable to store the final answer
    int ans = 0;

    /*  Loop to evaluate each column of
        the prefix matrix uniquely.
        For each index of a column we will try to
        determine the number of sub-matrices
        starting from that index
        and has all 1s */
    for (int j = 0; j < n; j++)
    {
        int i = n - 1;

        /*  Stack to store elements and the count
            of the numbers they popped

            First part of pair will be the
            value of inserted element.
            Second part will be the count
            of the number of elements pushed
            before with a greater value */
        Stack<pair> q = new Stack<pair>();

        // variable to store the number of
        // submatrices with all 1s
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

            ans += to_sum;

            q.Push(new pair(p_arr[i, j], c));

            i--;
        }
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    Boolean [,]arr = {{ true, true, false },
                      { true, false, true },
                      { false, true, true }};

    Console.WriteLine(matrixAllOne(arr));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to count number of
// sub-matrices with all 1s

var n = 3;

// Function to find required prefix-count for
// each row from right to left
function findPrefixCount(p_arr, arr)
{
    for (var i = 0; i < n; i++) {
        for (var j = n - 1; j >= 0; j--) {

            if (!arr[i][j])
                continue;

            if (j != n - 1)
                p_arr[i][j] += p_arr[i][j + 1];

            p_arr[i][j] += arr[i][j];
        }
    }
}

// Function to count the number of
// sub-matrices with all 1s
function matrixAllOne(arr)
{
    // Array to store required prefix count of
    // 1s from right to left for boolean array
    var p_arr = Array.from(Array(n), ()=>Array(n).fill(0));

    findPrefixCount(p_arr, arr);

    // variable to store the final answer
    var ans = 0;

    /*  Loop to evaluate each column of
        the prefix matrix uniquely.
        For each index of a column we will try to
        determine the number of sub-matrices
        starting from that index
        and has all 1s */
    for (var j = 0; j < n; j++) {

        var i = n - 1;

        /*  Stack to store elements and the count
            of the numbers they popped

            First part of pair will be the
            value of inserted element.
            Second part will be the count
            of the number of elements pushed
            before with a greater value */
        var q = [];

        // variable to store the number of
        // submatrices with all 1s
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

            ans += to_sum;

            q.push([ p_arr[i][j], c ]);

            i--;
        }
    }

    return ans;
}

// Driver Code
var arr = [ [ 1, 1, 0 ],
                  [ 1, 0, 1 ],
                  [ 0, 1, 1 ] ];
document.write( matrixAllOne(arr));

</script>
```

**Output:** 

```
10
```

**时间复杂度**:O(N<sup>2</sup>)
T5】辅助空间: O(N <sup>2</sup>