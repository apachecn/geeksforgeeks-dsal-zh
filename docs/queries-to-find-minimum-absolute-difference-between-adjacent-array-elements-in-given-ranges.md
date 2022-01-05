# 查询给定范围内相邻数组元素之间的最小绝对差

> 原文:[https://www . geeksforgeeks . org/查询查找给定范围内相邻数组元素之间的最小绝对差/](https://www.geeksforgeeks.org/queries-to-find-minimum-absolute-difference-between-adjacent-array-elements-in-given-ranges/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个由形式为 **{L，R}** 个查询组成的数组**查询【】**，每个查询的任务是找到在范围**【L，R】**内相邻元素之间的绝对差的最小值。

**示例:**

> **输入:** arr[] = {2，6，1，8，3，4}，查询[] = {{0，3}，{1，5}，{4，5}}
> **输出:**
> 4
> 1
> 1
> **说明:**
> 以下是执行查询的值:
> 
> 1.  在[0，3]范围内，相邻元素之间的最小绝对差值是最小值(| 2–6 |，| 6–1 |，| 1–8 |)= 4。
> 2.  在[1，5]范围内，相邻元素之间的最小绝对差是最小值(| 6–1 |、| 1–8 |、| 8–3 |、| 3–4 |)= 1。
> 3.  在[4，5]范围内，相邻元素之间的最小绝对差值为最小值(| 3–4 |)= 1。
> 
> 因此，打印 4、1、1 作为给定查询的结果。
> 
> **输入:** arr[] = [10，20，1，1，5 ]，查询[] = [0，1]，[1，4]，[2，3]
> **输出:**
> 10
> 0
> 0

**天真方法:**解决给定问题的最简单方法是创建一个数组 **diff[]** ，该数组存储每个数组元素的相邻元素之间的绝对差异。现在，对于每个查询，[在范围**【L，R–1】**内遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **diff[]** ，并打印范围**【L，R–1】**内所有值的最小值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure for query range
struct Query {
    int L, R;
};

int MAX = 5000;

// Function to find the minimum difference
// between adjacent array element over the
// given range [L, R] for Q Queries
void minDifference(int arr[], int n,
                   Query q[], int m)
{

    // Find the sum of all queries
    for (int i = 0; i < m; i++) {

        // Left and right boundaries
        // of current range
        int L = q[i].L, R = q[i].R;

        int ans = MAX;
        for (int i = L; i < R; i++) {
            ans = min(ans, arr[i]);
        }

        // Print  the sum of the
        // current query range
        cout << ans << '\n';
    }
}

// Function to find the minimum absolute
// difference of adjacent array elements
// for the given range
void minimumDifference(int arr[], Query q[],
                       int N, int m)
{

    // Stores the absolute difference of
    // adjacent elements
    int diff[N];

    for (int i = 0; i < N - 1; i++)
        diff[i] = abs(arr[i] - arr[i + 1]);

    // Find the minimum difference of
    // adjacent elements
    minDifference(diff, N - 1, q, m);
}

// Driver Code
int main()
{
    int arr[] = { 2, 6, 1, 8, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    Query Q[] = { { 0, 3 }, { 1, 5 }, { 4, 5 } };
    int M = sizeof(Q) / sizeof(Q[0]);

    minimumDifference(arr, Q, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Structure for query range
static class Query {
    int L, R;

    public Query(int l, int r) {
        super();
        L = l;
        R = r;
    }

};

static int MAX = 5000;

// Function to find the minimum difference
// between adjacent array element over the
// given range [L, R] for Q Queries
static void minDifference(int arr[], int n,
                   Query q[], int m)
{

    // Find the sum of all queries
    for (int i = 0; i < m; i++) {

        // Left and right boundaries
        // of current range
        int L = q[i].L, R = q[i].R;

        int ans = MAX;
        for (int j = L; j < R; j++) {
            ans = Math.min(ans, arr[j]);
        }

        // Print  the sum of the
        // current query range
        System.out.println(ans);
    }
}

// Function to find the minimum absolute
// difference of adjacent array elements
// for the given range
static void minimumDifference(int arr[], Query q[],
                       int N, int m)
{

    // Stores the absolute difference of
    // adjacent elements
    int []diff = new int[N];

    for (int i = 0; i < N - 1; i++)
        diff[i] = Math.abs(arr[i] - arr[i + 1]);

    // Find the minimum difference of
    // adjacent elements
    minDifference(diff, N - 1, q, m);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 6, 1, 8, 3, 4 };
    int N = arr.length;
    Query Q[] = {new Query( 0, 3 ),new Query( 1, 5 ),new Query( 4, 5 ) };
    int M = Q.length;

    minimumDifference(arr, Q, N, M);

}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach
MAX = 5000;

# Function to find the minimum difference
# between adjacent array element over the
# given range [L, R] for Q Queries
def minDifference(arr, n, q, m) :

    # Find the sum of all queries
    for i in range(m) :

        # Left and right boundaries
        # of current range
        L = q[i][0]; R = q[i][1];

        ans = MAX;
        for i in range(L, R) :
            ans = min(ans, arr[i]);

        # Print  the sum of the
        # current query range
        print(ans);

# Function to find the minimum absolute
# difference of adjacent array elements
# for the given range
def minimumDifference(arr, q, N, m) :

    # Stores the absolute difference of
    # adjacent elements
    diff = [0]*N;

    for i in range(N - 1) :
        diff[i] = abs(arr[i] - arr[i + 1]);

    # Find the minimum difference of
    # adjacent elements
    minDifference(diff, N - 1, q, m);

# Driver Code
if __name__ == "__main__" :

    arr = [ 2, 6, 1, 8, 3, 4 ];
    N = len(arr);
    Q = [ [ 0, 3 ], [ 1, 5 ], [ 4, 5 ] ];
    M = len(Q);

    minimumDifference(arr, Q, N, M);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Structure for query range
class Query {
    public int L, R;

    public Query(int l, int r) {
        this.L = l;
        this.R = r;
    }

};

static int MAX = 5000;

// Function to find the minimum difference
// between adjacent array element over the
// given range [L, R] for Q Queries
static void minDifference(int []arr, int n,
                   Query []q, int m)
{

    // Find the sum of all queries
    for (int i = 0; i < m; i++) {

        // Left and right boundaries
        // of current range
        int L = q[i].L, R = q[i].R;

        int ans = MAX;
        for (int j = L; j < R; j++) {
            ans = Math.Min(ans, arr[j]);
        }

        // Print  the sum of the
        // current query range
        Console.WriteLine(ans);
    }
}

// Function to find the minimum absolute
// difference of adjacent array elements
// for the given range
static void minimumDifference(int []arr, Query []q,
                       int N, int m)
{

    // Stores the absolute difference of
    // adjacent elements
    int []diff = new int[N];

    for (int i = 0; i < N - 1; i++)
        diff[i] = Math.Abs(arr[i] - arr[i + 1]);

    // Find the minimum difference of
    // adjacent elements
    minDifference(diff, N - 1, q, m);
}

// Driver Code
public static void Main()
{
    int []arr = { 2, 6, 1, 8, 3, 4 };
    int N = arr.Length;
    Query []Q = {new Query( 0, 3 ),new Query( 1, 5 ),new Query( 4, 5 ) };
    int M = Q.Length;

    minimumDifference(arr, Q, N, M);

}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach;
        let MAX = 5000;

        // Function to find the minimum difference
        // between adjacent array element over the
        // given range [L, R] for Q Queries
        function minDifference(arr, n, q, m)
        {

            // Find the sum of all queries
            for (let i = 0; i < m; i++) {

                // Left and right boundaries
                // of current range
                let L = q[i][0], R = q[i][1];

                let ans = MAX;
                for (let i = L; i < R; i++) {
                    ans = Math.min(ans, arr[i]);
                }

                // Print  the sum of the
                // current query range
                document.write(ans+'<br>');
            }
        }

        // Function to find the minimum absolute
        // difference of adjacent array elements
        // for the given range
        function minimumDifference(arr, q, N, m) {

            // Stores the absolute difference of
            // adjacent elements
            let diff = new Array(N);

            for (let i = 0; i < N - 1; i++)
                diff[i] = Math.abs(arr[i] - arr[i + 1]);

            // Find the minimum difference of
            // adjacent elements
            minDifference(diff, N - 1, q, m);
        }

        // Driver Code

        let arr = [2, 6, 1, 8, 3, 4];
        let N = arr.length;
        let Q = [[0, 3], [1, 5], [4, 5]];
        let M = Q.length;

        minimumDifference(arr, Q, N, M);

//This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
4
1
1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法也可以通过使用[稀疏表](https://www.geeksforgeeks.org/sparse-table/)进行优化，该稀疏表支持恒定时间内的查询*T5【O(1)*带额外空间*T9【O(N log N)*。不通过原件 **arr[]** 通过 **diff[]** 得到需要的答案。按照以下步骤解决问题:

1.  初始化一个[全局数组](https://www.geeksforgeeks.org/initialization-global-static-variables-c/) **查找[][]** 为稀疏数组。
2.  定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/) **预处理(arr，N)** ，并执行以下操作:
    *   使用变量 **i** 迭代范围**【0，N】**，并将**查找【I】【0】**的值设置为 **i** 。
    *   [嵌套使用变量 **j** 和 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，如果**arr[lookup[I][j-1]]【T9]小于**arr[lookup[I+(1<<(j-1))][j-1]**，则将 **lookup[i][j]** 设置为 **lookup[i][j-1]****
3.  定义函数**查询(int arr[]，int L，int M)** 并执行以下操作:
    *   将变量 **j** 初始化为**(整数)log2(R–L+1)**。
    *   如果 **arr[lookup[L][j]]** 小于或等于**arr[lookup[R –( 1<<j)+1[j]]，**则返回 **arr[lookup[L][j]]，**否则返回**arr[lookup[R –( 1<<j)+1[j]]**。
4.  定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/) **Min_difference(arr，n，q，m)** ，并执行以下操作:
    *   调用函数**预处理(arr，n)** 对稀疏数组进行预处理。
    *   [遍历给定的查询数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**Q[]**，函数**查询(arr，L，R–1)**返回的值给出当前查询的结果。
5.  初始化一个大小为 **N** 的数组 **diff[]** ，并为 **i** 的每个值存储 **arr[i]-arr[i+1]** 的绝对差值。
6.  调用函数 **Min_difference(diff，N-1，q，m)** 求每个查询的最小绝对差。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 500

// Stores the index for the minimum
// value in the subarray arr[i, j]
int lookup[MAX][MAX];

// Structure for query range
struct Query {
    int L, R;
};

// Function to fill the lookup array
// lookup[][] in the bottom up manner
void preprocess(int arr[], int n)
{
    // Initialize M for the intervals
    // with length 1
    for (int i = 0; i < n; i++)
        lookup[i][0] = i;

    // Find the values from smaller
    // to bigger intervals
    for (int j = 1; (1 << j) <= n; j++) {

        // Compute minimum value for
        // all intervals with size 2^j
        for (int i = 0; (i + (1 << j) - 1) < n; i++) {

            // For arr[2][10], compare
            // arr[lookup[0][3]] and
            // arr[lookup[3][3]]
            if (arr[lookup[i][j - 1]]
                < arr[lookup[i + (1 << (j - 1))][j - 1]])
                lookup[i][j] = lookup[i][j - 1];

            // Otherwise
            else
                lookup[i][j]
                    = lookup[i + (1 << (j - 1))][j - 1];
        }
    }
}

// Function find minimum of absolute
// difference of all adjacent element
// in subarray arr[L..R]
int query(int arr[], int L, int R)
{
    // For [2, 10], j = 3
    int j = (int)log2(R - L + 1);

    // For [2, 10], compare arr[lookup[0][3]]
    // and arr[lookup[3][3]],
    if (arr[lookup[L][j]]
        <= arr[lookup[R - (1 << j) + 1][j]])
        return arr[lookup[L][j]];

    else
        return arr[lookup[R - (1 << j) + 1][j]];
}

// Function to find the minimum of the
// ranges for M queries
void Min_difference(int arr[], int n,
                    Query q[], int m)
{
    // Fills table lookup[n][Log n]
    preprocess(arr, n);

    // Compute sum of all queries
    for (int i = 0; i < m; i++) {

        // Left and right boundaries
        // of current range
        int L = q[i].L, R = q[i].R;

        // Print sum of current query range
        cout << query(arr, L, R - 1) << '\n';
    }
}

// Function to find the minimum absolute
// difference in a range
void minimumDifference(int arr[], Query q[],
                       int N, int m)
{

    // diff[] is to stores the absolute
    // difference of adjacent elements
    int diff[N];
    for (int i = 0; i < N - 1; i++)
        diff[i] = abs(arr[i] - arr[i + 1]);

    // Call Min_difference to get minimum
    // difference of adjacent elements
    Min_difference(diff, N - 1, q, m);
}

// Driver Code
int main()
{
    int arr[] = { 2, 6, 1, 8, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    Query Q[] = { { 0, 3 }, { 1, 5 }, { 4, 5 } };
    int M = sizeof(Q) / sizeof(Q[0]);

    minimumDifference(arr, Q, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import javax.management.Query;

class GFG{
static final int MAX = 500;

// Stores the index for the minimum
// value in the subarray arr[i, j]
static int [][]lookup = new int[MAX][MAX];

// Structure for query range
static class Query {
    int L, R;

    public Query(int l, int r) {
        super();
        L = l;
        R = r;
    }
};

// Function to fill the lookup array
// lookup[][] in the bottom up manner
static void preprocess(int arr[], int n)
{
    // Initialize M for the intervals
    // with length 1
    for (int i = 0; i < n; i++)
        lookup[i][0] = i;

    // Find the values from smaller
    // to bigger intervals
    for (int j = 1; (1 << j) <= n; j++) {

        // Compute minimum value for
        // all intervals with size 2^j
        for (int i = 0; (i + (1 << j) - 1) < n; i++) {

            // For arr[2][10], compare
            // arr[lookup[0][3]] and
            // arr[lookup[3][3]]
            if (arr[lookup[i][j - 1]]
                < arr[lookup[i + (1 << (j - 1))][j - 1]])
                lookup[i][j] = lookup[i][j - 1];

            // Otherwise
            else
                lookup[i][j]
                    = lookup[i + (1 << (j - 1))][j - 1];
        }
    }
}

// Function find minimum of absolute
// difference of all adjacent element
// in subarray arr[L..R]
static int query(int arr[], int L, int R)
{
    // For [2, 10], j = 3
    int j = (int)Math.log(R - L + 1);

    // For [2, 10], compare arr[lookup[0][3]]
    // and arr[lookup[3][3]],
    if (arr[lookup[L][j]]
        <= arr[lookup[R - (1 << j) + 1][j]])
        return arr[lookup[L][j]];

    else
        return arr[lookup[R - (1 << j) + 1][j]];
}

// Function to find the minimum of the
// ranges for M queries
static void Min_difference(int arr[], int n,
                    Query q[], int m)
{
    // Fills table lookup[n][Log n]
    preprocess(arr, n);

    // Compute sum of all queries
    for (int i = 0; i < m; i++) {

        // Left and right boundaries
        // of current range
        int L = q[i].L, R = q[i].R;

        // Print sum of current query range
        System.out.println(query(arr, L, R - 1));
    }
}

// Function to find the minimum absolute
// difference in a range
static void minimumDifference(int arr[], Query q[],
                       int N, int m)
{

    // diff[] is to stores the absolute
    // difference of adjacent elements
    int []diff = new int[N];
    for (int i = 0; i < N - 1; i++)
        diff[i] = Math.abs(arr[i] - arr[i + 1]);

    // Call Min_difference to get minimum
    // difference of adjacent elements
    Min_difference(diff, N - 1, q, m);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 6, 1, 8, 3, 4 };
    int N = arr.length;
    Query Q[] = { new Query( 0, 3 ), new Query( 1, 5 ), new Query( 4, 5 ) };
    int M = Q.length;

    minimumDifference(arr, Q, N, M);

}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

public class GFG{
static readonly int MAX = 500;

// Stores the index for the minimum
// value in the subarray arr[i, j]
static int [,]lookup = new int[MAX, MAX];

// Structure for query range
class Query {
    public int L, R;

    public Query(int l, int r) {

        L = l;
        R = r;
    }
};

// Function to fill the lookup array
// lookup[,] in the bottom up manner
static void preprocess(int []arr, int n)
{

    // Initialize M for the intervals
    // with length 1
    for (int i = 0; i < n; i++)
        lookup[i,0] = i;

    // Find the values from smaller
    // to bigger intervals
    for (int j = 1; (1 << j) <= n; j++) {

        // Compute minimum value for
        // all intervals with size 2^j
        for (int i = 0; (i + (1 << j) - 1) < n; i++) {

            // For arr[2,10], compare
            // arr[lookup[0,3]] and
            // arr[lookup[3,3]]
            if (arr[lookup[i,j - 1]]
                < arr[lookup[i + (1 << (j - 1)),j - 1]])
                lookup[i,j] = lookup[i,j - 1];

            // Otherwise
            else
                lookup[i,j]
                    = lookup[i + (1 << (j - 1)),j - 1];
        }
    }
}

// Function find minimum of absolute
// difference of all adjacent element
// in subarray arr[L..R]
static int query(int []arr, int L, int R)
{

    // For [2, 10], j = 3
    int j = (int)Math.Log(R - L + 1);

    // For [2, 10], compare arr[lookup[0,3]]
    // and arr[lookup[3,3]],
    if (arr[lookup[L,j]]
        <= arr[lookup[R - (1 << j) + 1,j]])
        return arr[lookup[L,j]];

    else
        return arr[lookup[R - (1 << j) + 1,j]];
}

// Function to find the minimum of the
// ranges for M queries
static void Min_difference(int []arr, int n,
                    Query []q, int m)
{

    // Fills table lookup[n,Log n]
    preprocess(arr, n);

    // Compute sum of all queries
    for (int i = 0; i < m; i++) {

        // Left and right boundaries
        // of current range
        int L = q[i].L, R = q[i].R;

        // Print sum of current query range
        Console.WriteLine(query(arr, L, R - 1));
    }
}

// Function to find the minimum absolute
// difference in a range
static void minimumDifference(int []arr, Query []q,
                       int N, int m)
{

    // diff[] is to stores the absolute
    // difference of adjacent elements
    int []diff = new int[N];
    for (int i = 0; i < N - 1; i++)
        diff[i] = Math.Abs(arr[i] - arr[i + 1]);

    // Call Min_difference to get minimum
    // difference of adjacent elements
    Min_difference(diff, N - 1, q, m);
} 

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 6, 1, 8, 3, 4 };
    int N = arr.Length;
    Query []Q = { new Query( 0, 3 ), new Query( 1, 5 ), new Query( 4, 5 ) };
    int M = Q.Length;

    minimumDifference(arr, Q, N, M);

}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program for the above approach
let MAX = 500;

// Stores the index for the minimum
// value in the subarray arr[i, j]
let lookup = new Array(MAX).fill(0).map(() => new Array(MAX).fill(0));

// Structure for query range
class Query {
  constructor(l, r) {
    this.L = l;
    this.R = r;
  }
}

// Function to fill the lookup array
// lookup[][] in the bottom up manner
function preprocess(arr, n)
{

  // Initialize M for the intervals
  // with length 1
  for (let i = 0; i < n; i++) lookup[i][0] = i;

  // Find the values from smaller
  // to bigger intervals
  for (let j = 1; 1 << j <= n; j++)
  {

    // Compute minimum value for
    // all intervals with size 2^j
    for (let i = 0; i + (1 << j) - 1 < n; i++)
    {

      // For arr[2][10], compare
      // arr[lookup[0][3]] and
      // arr[lookup[3][3]]
      if (arr[lookup[i][j - 1]] < arr[lookup[i + (1 << (j - 1))][j - 1]])
        lookup[i][j] = lookup[i][j - 1];

      // Otherwise
      else lookup[i][j] = lookup[i + (1 << (j - 1))][j - 1];
    }
  }
}

// Function find minimum of absolute
// difference of all adjacent element
// in subarray arr[L..R]
function query(arr, L, R)
{

  // For [2, 10], j = 3
  let j = Math.floor(Math.log(R - L + 1));

  // For [2, 10], compare arr[lookup[0][3]]
  // and arr[lookup[3][3]],
  if (arr[lookup[L][j]] <= arr[lookup[R - (1 << j) + 1][j]])
    return arr[lookup[L][j]];
  else return arr[lookup[R - (1 << j) + 1][j]];
}

// Function to find the minimum of the
// ranges for M queries
function Min_difference(arr, n, q, m)
{

  // Fills table lookup[n][Log n]
  preprocess(arr, n);

  // Compute sum of all queries
  for (let i = 0; i < m; i++)
  {

    // Left and right boundaries
    // of current range
    let L = q[i].L,
      R = q[i].R;

    // let sum of current query range
    document.write(query(arr, L, R - 1) + "<br>");
  }
}

// Function to find the minimum absolute
// difference in a range
function minimumDifference(arr, q, N, m)
{

  // diff[] is to stores the absolute
  // difference of adjacent elements
  let diff = new Array(N);
  for (let i = 0; i < N - 1; i++) diff[i] = Math.abs(arr[i] - arr[i + 1]);

  // Call Min_difference to get minimum
  // difference of adjacent elements
  Min_difference(diff, N - 1, q, m);
}

// Driver Code

let arr = [2, 6, 1, 8, 3, 4];
let N = arr.length;
let Q = [new Query(0, 3), new Query(1, 5), new Query(4, 5)];
let M = Q.length;

minimumDifference(arr, Q, N, M);

// This code is contributed by _saurabh_jaiswal.

</script>
```

**Output:** 

```
4
1
1
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N*N)*