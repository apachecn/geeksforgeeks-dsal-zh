# 通过更新来查找没有相似相邻元素的最长子序列的查询

> 原文:[https://www . geesforgeks . org/query-to-find-最长-子序列-无相似-相邻-元素-带更新/](https://www.geeksforgeeks.org/queries-to-find-longest-subsequence-having-no-similar-adjacent-elements-with-updates/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个查询数组**【】【】**，每个查询的形式为 **{x，y}** 。对于每个查询，任务是将索引 **x** ( *基于 1 的索引*)处的元素替换为 **y** ，并找到没有相似相邻元素的最长[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的长度。

**示例:**

> **输入:** arr[] = {1，1，2，5，2}，Q = 2，query[][]= { {1，3}，{4，2}}
> **输出:** 5 3
> **解释:**
> 最初数组是{ 1，1，2，5，2}。
> **查询 1:** 修改索引 1 到 3 处的值，数组修改为{3，1，2，5，2}。
> 因此，没有相似相邻元素的最长子序列是{3，1，2，5，2}，长度为 5。
> 因此，打印 5 作为答案。
> **查询 2:** 将索引 4 处的值修改为 2，数组将修改为{3，1，2，2，2}。
> 因此，没有相似相邻元素的最长子序列是{3，1，2}，长度为 3。
> 因此，打印 2 作为答案。
> 
> **输入:** arr[] = {1，1，2，5，2}，Q = 1，query[][]= { { 2，2}}
> **输出:** 4
> **解释:**
> 最初数组是{1，1，2，5，2}。
> **查询 1:** 将索引 2 处的值修改为 2，数组修改为{1，2，2，5，2}。
> 因此，没有相似相邻元素的最长子序列是{1，2，5，2}，长度为 4。
> 因此，将该值打印为 4。

**天真方法:**按照以下步骤，用最简单的方法解决问题:

1.  仅当元素不等于子序列的前一个元素时，才将其添加到子序列中。
2.  对于每个查询 **{x，y}** ，将索引 **x** 处的元素替换为 **y** 。
3.  通过变量**计数**跟踪在任意点找到的最长子序列。
4.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，每当序列的当前元素不等于序列的前一个元素时，将**计数**变量增加 **1** 。
5.  迭代一次序列后，**计数**包含最长所需子序列的长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the
// longest subsequence such that no
// two adjacent elements are equal
void longestSubsequence(int N, int Q,
                        int arr[],
                        int Queries[][2])
{
    for (int i = 0; i < Q; i++) {

        // Replace element at
        // index x with y
        int x = Queries[i][0];
        int y = Queries[i][1];

        // Since x is 1-indexed,
        // decrement x by 1
        arr[x - 1] = y;

        // Keep track of number of
        // elements in subsequence
        int count = 1;

        for (int j = 1; j < N; j++) {

            // If previous element is not
            // same as current element
            if (arr[j] != arr[j - 1]) {
                count += 1;
            }
        }

        // Print the desired count
        cout << count << ' ';
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 2, 5, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int Q = 2;
    int Queries[Q][2] = { { 1, 3 }, { 4, 2 } };

    // Function Call
    longestSubsequence(N, Q, arr, Queries);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to find the length of the
// longest subsequence such that no
// two adjacent elements are equal
static void longestSubsequence(int N, int Q,
                        int arr[],
                        int Queries[][])
{
    for (int i = 0; i < Q; i++)
    {

        // Replace element at
        // index x with y
        int x = Queries[i][0];
        int y = Queries[i][1];

        // Since x is 1-indexed,
        // decrement x by 1
        arr[x - 1] = y;

        // Keep track of number of
        // elements in subsequence
        int count = 1;

        for (int j = 1; j < N; j++)
        {

            // If previous element is not
            // same as current element
            if (arr[j] != arr[j - 1])
            {
                count += 1;
            }
        }

        // Print the desired count
        System.out.print(count +" ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 1, 2, 5, 2 };
    int N = arr.length;
    int Q = 2;
    int Queries[][] = { { 1, 3 }, { 4, 2 } };

    // Function Call
    longestSubsequence(N, Q, arr, Queries);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the length of the
# longest subsequence such that no
# two adjacent elements are equal
def longestSubsequence(N, Q, arr, Queries):

    for i in range(Q):

        # Replace element at
        # index x with y
        x = Queries[i][0]
        y = Queries[i][1]

        # Since x is 1-indexed,
        # decrement x by 1
        arr[x - 1] = y

        # Keep track of number of
        # elements in subsequence
        count = 1

        for j in range(1, N):

            # If previous element is not
            # same as current element
            if (arr[j] != arr[j - 1]):
                count += 1

        # Print the desired count
        print(count, end = ' ')

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 1, 2, 5, 2 ]
    N = len(arr)
    Q = 2
    Queries = [ [ 1, 3 ], [ 4, 2 ] ]

    # Function Call
    longestSubsequence(N, Q, arr, Queries)

# This code is contributed by chitranayal
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the length of the
// longest subsequence such that no
// two adjacent elements are equal
static void longestSubsequence(int N, int Q,
                               int []arr,
                               int [,]Queries)
{
    for(int i = 0; i < Q; i++)
    {

        // Replace element at
        // index x with y
        int x = Queries[i, 0];
        int y = Queries[i, 1];

        // Since x is 1-indexed,
        // decrement x by 1
        arr[x - 1] = y;

        // Keep track of number of
        // elements in subsequence
        int count = 1;

        for(int j = 1; j < N; j++)
        {

            // If previous element is not
            // same as current element
            if (arr[j] != arr[j - 1])
            {
                count += 1;
            }
        }

        // Print the desired count
        Console.Write(count +" ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 1, 2, 5, 2 };
    int N = arr.Length;
    int Q = 2;
    int[,]Queries = { { 1, 3 }, { 4, 2 } };

    // Function Call
    longestSubsequence(N, Q, arr, Queries);
}
}

// This code is contributed by jana_sayantan
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to find the length of the
// longest subsequence such that no
// two adjacent elements are equal
function longestSubsequence(N, Q,
                        arr, Queries)
{
    for (let i = 0; i < Q; i++)
    {

        // Replace element at
        // index x with y
        let x = Queries[i][0];
        let y = Queries[i][1];

        // Since x is 1-indexed,
        // decrement x by 1
        arr[x - 1] = y;

        // Keep track of number of
        // elements in subsequence
        let count = 1;

        for (let j = 1; j < N; j++)
        {

            // If previous element is not
            // same as current element
            if (arr[j] != arr[j - 1])
            {
                count += 1;
            }
        }

        // Print the desired count
        document.write(count +" ");
    }
}

// Driver code

    let arr = [ 1, 1, 2, 5, 2 ];
    let N = arr.length;
    let Q = 2;
    let Queries = [[ 1, 3 ], [ 4, 2 ]];

    // Function Call
    longestSubsequence(N, Q, arr, Queries);

 // This code is contributed by code_hunt.
</script>
```

**Output:** 

```
5 3
```

***时间复杂度:** O(N*Q)*
***辅助空间:** O(N)*

**有效方法:**为了优化上述方法，观察发现所需子序列中元素的存在仅取决于其先前的元素，如下所示:

*   在最终答案中，替换索引 **x** 处的元素只会影响索引 **x** 和 **x + 1** 处元素的贡献。
*   因此，从变量**计数**中减去这两个指数的贡献，重新计算这两个指数的贡献，将在恒定时间内给出所需的答案。

按照以下步骤解决问题:

*   初始化一个变量，比如**计数**，来存储子序列的计数。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并计算那些不同于数组前一个元素的元素，并将其存储在变量**计数**中。
*   现在遍历每个查询 **{x，y}** ，并执行以下操作:
    *   如果索引**(x–1)**处的元素与索引 **x** 处的元素不同，则按 **1** 递减**计数**。
    *   如果索引**(x–1)**处的元素不同于元素 **y** ，则按 **1** 递增**计数**。
    *   同样，如果索引 **(x + 1)** 处的元素与索引 **x** 处的元素不同，则以 **1** 递减**计数**。
    *   如果索引 **(x + 1)** 处的元素与元素 **y** 不同，则按 **1** 递增**计数**。
    *   打印每次查询后**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

void longestSubsequence(int N, int Q,
                        int arr[],
                        int Queries[][2])
{
    int count = 1;

    // Traverse the array arr[]
    for (int i = 1; i < N; i++) {

        // If previous element is not
        // same as current element
        if (arr[i] != arr[i - 1]) {
            count += 1;
        }
    }

    // Traverse the queries
    for (int i = 0; i < Q; i++) {

        // Replace element at
        // index x with y
        int x = Queries[i][0];
        int y = Queries[i][1];

        // Recalculate for index x
        if (x > 1) {

            // Subtract contribution
            // of element at index x
            if (arr[x - 1] != arr[x - 2]) {
                count -= 1;
            }

            // Add contribution of y
            if (arr[x - 2] != y) {
                count += 1;
            }
        }

        // Recalculate for index x + 1
        if (x < N) {

            // Subtract contribution of
            // element at index x + 1
            if (arr[x] != arr[x - 1]) {
                count -= 1;
            }

            // Adds contribution of y
            if (y != arr[x]) {
                count += 1;
            }
        }
        cout << count << ' ';

        // Replace the element
        arr[x - 1] = y;
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 2, 5, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int Q = 2;
    int Queries[Q][2] = { { 1, 3 }, { 4, 2 } };

    // Function Call
    longestSubsequence(N, Q, arr, Queries);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static void longestSubsequence(int N, int Q,
                               int arr[],
                               int Queries[][])
{
    int count = 1;

    // Traverse the array arr[]
    for(int i = 1; i < N; i++)
    {

        // If previous element is not
        // same as current element
        if (arr[i] != arr[i - 1])
        {
            count += 1;
        }
    }

    // Traverse the queries
    for(int i = 0; i < Q; i++)
    {

        // Replace element at
        // index x with y
        int x = Queries[i][0];
        int y = Queries[i][1];

        // Recalculate for index x
        if (x > 1)
        {

            // Subtract contribution
            // of element at index x
            if (arr[x - 1] != arr[x - 2])
            {
                count -= 1;
            }

            // Add contribution of y
            if (arr[x - 2] != y)
            {
                count += 1;
            }
        }

        // Recalculate for index x + 1
        if (x < N)
        {

            // Subtract contribution of
            // element at index x + 1
            if (arr[x] != arr[x - 1])
            {
                count -= 1;
            }

            // Adds contribution of y
            if (y != arr[x])
            {
                count += 1;
            }
        }
        System.out.print(count + " ");

        // Replace the element
        arr[x - 1] = y;
    }
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 1, 1, 2, 5, 2 };
    int N = arr.length;
    int Q = 2;
    int Queries[][] = { { 1, 3 }, { 4, 2 } };

    // Function Call
    longestSubsequence(N, Q, arr, Queries);
}
}

// This code is contributed by jana_sayantan
```

## 蟒蛇 3

```
# Python3 program for the above approach
def longestSubsequence(N, Q, arr, Queries):

    count = 1

    # Traverse the array arr[]
    for i in range(1, N):

        # If previous element is not
        # same as current element
        if (arr[i] != arr[i - 1]):
            count += 1

    # Traverse the queries
    for i in range(Q):

        # Replace element at
        # index x with y
        x = Queries[i][0]
        y = Queries[i][1]

        # Recalculate for index x
        if (x > 1):

            # Subtract contribution
            # of element at index x
            if (arr[x - 1] != arr[x - 2]):
                count -= 1

            # Add contribution of y
            if (arr[x - 2] != y):
                count += 1

        # Recalculate for index x + 1
        if (x < N):

            # Subtract contribution of
            # element at index x + 1
            if (arr[x] != arr[x - 1]):
                count -= 1

            # Adds contribution of y
            if (y != arr[x]):
                count += 1

        print(count, end = ' ')

        # Replace the element
        arr[x - 1] = y

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 1, 2, 5, 2 ]
    N = len(arr)
    Q = 2
    Queries = [ [ 1, 3 ], [ 4, 2 ] ]

    # Function Call
    longestSubsequence(N, Q, arr, Queries)

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static void longestSubsequence(int N, int Q,
                               int []arr,
                               int [,]Queries)
{
    int count = 1;

    // Traverse the array arr[]
    for(int i = 1; i < N; i++)
    {

        // If previous element is not
        // same as current element
        if (arr[i] != arr[i - 1])
        {
            count += 1;
        }
    }

    // Traverse the queries
    for(int i = 0; i < Q; i++)
    {

        // Replace element at
        // index x with y
        int x = Queries[i, 0];
        int y = Queries[i, 1];

        // Recalculate for index x
        if (x > 1)
        {

            // Subtract contribution
            // of element at index x
            if (arr[x - 1] != arr[x - 2])
            {
                count -= 1;
            }

            // Add contribution of y
            if (arr[x - 2] != y)
            {
                count += 1;
            }
        }

        // Recalculate for index x + 1
        if (x < N)
        {

            // Subtract contribution of
            // element at index x + 1
            if (arr[x] != arr[x - 1])
            {
                count -= 1;
            }

            // Adds contribution of y
            if (y != arr[x])
            {
                count += 1;
            }
        }
        Console.Write(count + " ");

        // Replace the element
        arr[x - 1] = y;
    }
}

// Driver Code
public static void Main(string []args)
{
    int []arr = { 1, 1, 2, 5, 2 };
    int N = arr.Length;
    int Q = 2;
    int [,]Queries = { { 1, 3 }, { 4, 2 } };

    // Function Call
    longestSubsequence(N, Q, arr, Queries);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// javascript program for the above approach

    function longestSubsequence( N , Q , arr , Queries) {
        var count = 1;

        // Traverse the array arr
        for (var i = 1; i < N; i++) {

            // If previous element is not
            // same as current element
            if (arr[i] != arr[i - 1]) {
                count += 1;
            }
        }

        // Traverse the queries
        for (var i = 0; i < Q; i++) {

            // Replace element at
            // index x with y
            var x = Queries[i][0];
            var y = Queries[i][1];

            // Recalculate for index x
            if (x > 1) {

                // Subtract contribution
                // of element at index x
                if (arr[x - 1] != arr[x - 2]) {
                    count -= 1;
                }

                // Add contribution of y
                if (arr[x - 2] != y) {
                    count += 1;
                }
            }

            // Recalculate for index x + 1
            if (x < N) {

                // Subtract contribution of
                // element at index x + 1
                if (arr[x] != arr[x - 1]) {
                    count -= 1;
                }

                // Adds contribution of y
                if (y != arr[x]) {
                    count += 1;
                }
            }
            document.write(count + " ");

            // Replace the element
            arr[x - 1] = y;
        }
    }

    // Driver Code

        var arr = [ 1, 1, 2, 5, 2 ];
        var N = arr.length;
        var Q = 2;
        var Queries = [ [ 1, 3 ], [ 4, 2 ] ];

        // Function Call
        longestSubsequence(N, Q, arr, Queries);

// This code contributed by Princi Singh
</script>
```

**Output:** 

```
5 3
```

***时间复杂度:** O(N + Q)*
***辅助空间:** O(N)*