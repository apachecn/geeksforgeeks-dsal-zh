# 查询返回第 L 个最小数和第 R 个最小数的绝对差

> 原文:[https://www . geesforgeks . org/query-to-return-l-th-最小数和-r-th-最小数的绝对差/](https://www.geeksforgeeks.org/queries-to-return-the-absolute-difference-between-l-th-smallest-number-and-the-r-th-smallest-number/)

给定一个由 **N** 独特元素和 **Q** 查询组成的数组**。每个查询由两个整数 **L** 和 **R** 组成。任务是打印 **L <sup>th</sup> 最小**和 **R <sup>th</sup> 最小**元素的指数之间的绝对差值。**

**示例:**

> **输入:** arr[] = {1，5，4，2，8，6，7}，
> que[] = {{2，5}，{1，3}，{1，5}，{3，6 } }
> T4】输出:T6】2
> 2
> 5
> 4
> 对于第一个查询，第二个最小的数字是 2，位于索引 3
> 处，第五个最小的数字是 6，位于索引 5 处。因此
> 这两个指数之间的绝对差值为 2。
> 
> **输入:** arr[] = {1，2，3，4}，
> 比[] = {{1，1}，{2，3 } }
> T4】输出:
> 0
> 1

**方法:**可以按照以下步骤解决上述问题。

*   将元素及其索引存储在一对数组中。
*   根据第一个元素对数组进行排序。
*   对于每个查询，答案都是**ABS(arr[l–1])。第二个-arr[r-1]。第二)**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the result
// for a particular query
int answerQuery(pair<int, int> arr[], int l, int r)
{
    // Get the difference between the indices of
    // L-th and the R-th smallest element
    int answer = abs(arr[l - 1].second - arr[r - 1].second);

    // Return the answer
    return answer;
}

// Function that performs all the queries
void solveQueries(int a[], int n, int q[][2], int m)
{

    // Store the array numbers
    // and their indices
    pair<int, int> arr[n];
    for (int i = 0; i < n; i++) {
        arr[i].first = a[i];
        arr[i].second = i;
    }

    // Sort the array elements
    sort(arr, arr + n);

    // Answer all the queries
    for (int i = 0; i < m; i++)
        cout << answerQuery(arr, q[i][0], q[i][1]) << endl;
}

// Driver code
int main()
{
    int a[] = { 1, 5, 4, 2, 8, 6, 7 };
    int n = sizeof(a) / sizeof(a[0]);
    int q[][2] = { { 2, 5 }, { 1, 3 }, { 1, 5 }, { 3, 6 } };
    int m = sizeof(q) / sizeof(q[0]);
    solveQueries(a, n, q, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.util.Comparator;

class GFG
{

// pair class
static class pair
{
    int first,second;
    pair(int f, int s)
    {
        first = f;
        second = s;
    }
}

// Function to return the result
// for a particular query
static int answerQuery(pair arr[], int l, int r)
{
    // Get the difference between the indices of
    // L-th and the R-th smallest element
    int answer = Math.abs(arr[l - 1].second -
                        arr[r - 1].second);

    // Return the answer
    return answer;
}

// Function that performs all the queries
static void solveQueries(int a[], int n,
                        int q[][], int m)
{

    // Store the array numbers
    // and their indices
    pair arr[] = new pair[n];
    for (int i = 0; i < n; i++)
    {
        arr[i] = new pair(0, 0);
        arr[i].first = a[i];
        arr[i].second = i;
    }
        // Sort pair
        Comparator<pair> comp = new Comparator<pair>()
        {

            public int compare(pair e1, pair e2)
            {
                if(e1.first < e2.first)
                {
                    return -1;
                }
                else if (e1.first > e2.first)
                {
                    return 1;
                }
                else
                {
                    return 0;
                }
            }
        };

    // Sort the array elements
    Arrays.sort(arr,comp);

    // Answer all the queries
    for (int i = 0; i < m; i++)
        System.out.println( answerQuery(arr, q[i][0], q[i][1]));
}

// Driver code
public static void main(String args[])
{
    int a[] = { 1, 5, 4, 2, 8, 6, 7 };
    int n = a.length;
    int q[][] = { { 2, 5 }, { 1, 3 }, { 1, 5 }, { 3, 6 } };
    int m = q.length;
    solveQueries(a, n, q, m);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the result
# for a particular query
def answerQuery(arr, l, r):

    # Get the difference between the indices
    # of L-th and the R-th smallest element
    answer = abs(arr[l - 1][1] -
                 arr[r - 1][1])

    # Return the answer
    return answer

# Function that performs all the queries
def solveQueries(a, n, q, m):

    # Store the array numbers
    # and their indices
    arr = [[0 for i in range(n)]
              for j in range(n)]
    for i in range(n):
        arr[i][0] = a[i]
        arr[i][1] = i

    # Sort the array elements
    arr.sort(reverse = False)

    # Answer all the queries
    for i in range(m):
        print(answerQuery(arr, q[i][0],
                               q[i][1]))

# Driver code
if __name__ == '__main__':
    a = [1, 5, 4, 2, 8, 6, 7]
    n = len(a)
    q = [[2, 5], [1, 3],
         [1, 5], [3, 6]]
    m = len(q)
    solveQueries(a, n, q, m)

# This code is contributed by
# Surendra_Gangwar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the result
// for a particular query
function answerQuery(arr, l, r)
{
    // Get the difference between the indices of
    // L-th and the R-th smallest element
    let answer = Math.abs(arr[l - 1][1] - arr[r - 1][1]);

    // Return the answer
    return answer;
}

// Function that performs all the queries
function solveQueries(a, n, q, m)
{

    // Store the array numbers
    // and their indices
    let arr = new Array(n);

    for(let i = 0; i < n; i++){
        arr[i] = new Array(n).fill(0)
    }

    for (let i = 0; i < n; i++) {
        arr[i][0] = a[i];
        arr[i][1] = i;
    }

    // Sort the array elements
    arr.sort((a, b) => a[0] - b[0]);

    // Answer all the queries
    for (let i = 0; i < m; i++)
        document.write(answerQuery(arr, q[i][0], q[i][1]) +
        "<br>");
}

// Driver code

    let a = [ 1, 5, 4, 2, 8, 6, 7 ];
    let n = a.length;
    let q = [ [ 2, 5 ], [ 1, 3 ], [ 1, 5 ], [ 3, 6 ] ];
    let m = q.length;
    solveQueries(a, n, q, m);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
2
2
5
4
```