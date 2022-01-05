# 查询计算由奇数除数组成的数组元素的和

> 原文:[https://www . geeksforgeeks . org/由奇数除数组成的计算数组元素和的查询/](https://www.geeksforgeeks.org/queries-to-calculate-sum-of-array-elements-consisting-of-odd-number-of-divisors/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个由形式为 **{L，R}** 的 **Q** 查询组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**，任务是从范围**【L，R】**中找到所有数组元素的[和，具有奇数个除数](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)**

****示例:****

> *****输入:** arr[] = {2，4，5，6，9}，Q = 3，Query[][] = {{0，2}，{1，3}，{1，4}}*
> ***输出:** 4 4 13*
> ***解释:***
> ***查询 1:** 索引[0，2]中的元素为{2，4，5}。其中，只有 4 个有奇数除数。因此，总和为 4。*
> ***查询 2:** 索引[1，3]中的元素为{4，5，6}。其中，只有 4 个有奇数除数。因此，总和为 4。*
> ***查询 3:** 索引[1，4]中的元素为{4，5，6，9}。其中，只有 4，9 有奇数除数。因此，总和是 13。***
> 
> *****输入:** arr[] = {1，16，5，4，9}，Q = 2，Query[][] = {{1，3}，{0，2}}*
> ***输出:** 20 17***

****天真法:**解决给定问题最简单的方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**在范围**【L，R】**内为每个查询和[找到范围](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)**【L，R】**内具有[奇数除数](https://www.geeksforgeeks.org/program-to-find-count-of-numbers-having-odd-number-of-divisors-in-given-range/)的元素之和，并打印结果之和。**

*****时间复杂度:** O(Q * N *√N)*
***辅助空间:** O(1)***

****高效方法:**上述方法也可以基于以下观察进行优化:**

*   **除数只有奇数[如果数是完美的正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。**
*   **所以，这个问题可以通过将没有奇数除数[的整数](https://www.geeksforgeeks.org/check-if-total-number-of-divisors-are-even-or-odd/)替换为 0 来解决。然后，[构建一个段树，找到范围](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)内元素的总和来回答查询。**

**按照以下步骤解决问题:**

*   **[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，用 **0** 替换非[完美正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)的整数。**
*   **[构建段树，回答区间之间的求和查询。](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)**
*   **遍历所有 **Q** 查询，对于每个查询，从段树中获取特定范围的总和。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to get the middle index
// from the given ranges
int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

// Recursive function to find the sum
// of values in the given range of
// the array
int getSumUtil(int* st, int ss, int se,
               int qs, int qe, int si)
{

    // If segment of this node is a
    // part of given range, then
    // return the sum of the segment
    if (qs <= ss && qe >= se)
        return st[si];

    // If segment of this node is
    // outside the given range
    if (se < qs || ss > qe)
        return 0;

    // If a part of this segment
    // overlaps the given range
    int mid = getMid(ss, se);

    return getSumUtil(st, ss, mid,
                      qs, qe, 2 * si + 1)
           + getSumUtil(st, mid + 1,
                        se, qs, qe,
                        2 * si + 2);
}

// Function to find the sum of elements
// in the range from index qs (query
// start) to qe (query end)
int getSum(int* st, int n, int qs, int qe)
{
    // Invalid ranges
    if (qs < 0 || qe > n - 1 || qs > qe) {
        cout << "Invalid Input";
        return -1;
    }

    return getSumUtil(st, 0, n - 1, qs, qe, 0);
}

// Recursive function to construct the
// Segment Tree for array[ss..se]. si
// is index of current node in tree st
int constructSTUtil(int arr[], int ss,
                    int se, int* st,
                    int si)
{
    // If there is one element
    // in the array
    if (ss == se) {
        st[si] = arr[ss];
        return arr[ss];
    }

    int mid = getMid(ss, se);

    // Recur for left and right
    // subtrees and store the sum
    // of values in this node
    st[si] = constructSTUtil(arr, ss, mid,
                             st, si * 2 + 1)
             + constructSTUtil(arr, mid + 1,
                               se, st,
                               si * 2 + 2);
    return st[si];
}

// Function to construct segment tree
// from the given array
int* constructST(int arr[], int n)
{
    // Allocate memory for the segment
    // tree Height of segment tree
    int x = (int)(ceil(log2(n)));

    // Maximum size of segment tree
    int max_size = 2 * (int)pow(2, x) - 1;

    // Allocate memory
    int* st = new int[max_size];

    // Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, st, 0);

    // Return the constructed
    // segment tree
    return st;
}

// Function to find the sum of elements
// having odd number of divisors in
// index range [L, R] for Q queries
void OddDivisorsSum(int n, int q, int arr[],
                    vector<pair<int, int> > Query)
{
    // Traverse the array, arr[]
    for (int i = 0; i < n; i++) {
        int sq = sqrt(arr[i]);

        // Replace elements that are
        // not perfect squares with 0
        if (sq * sq != arr[i])
            arr[i] = 0;
    }

    // Build segment tree from the
    // given array
    int* st = constructST(arr, n);

    // Iterate through all the queries
    for (int i = 0; i < q; i++) {
        int l = Query[i].first;
        int r = Query[i].second;

        // Print sum of values in
        // array from index l to r
        cout << getSum(st, n, l, r) << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 5, 6, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int Q = 3;
    vector<pair<int, int> > Query
        = { { 0, 2 }, { 1, 3 }, { 1, 4 } };
    OddDivisorsSum(N, Q, arr, Query);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to get the middle index
    // from the given ranges
    static int getMid(int s, int e)
    {
        return s + (e - s) / 2;
    }

    // Recursive function to find the sum
    // of values in the given range of
    // the array
    static int getSumUtil(int st[], int ss, int se, int qs,
                          int qe, int si)
    {

        // If segment of this node is a
        // part of given range, then
        // return the sum of the segment
        if (qs <= ss && qe >= se)
            return st[si];

        // If segment of this node is
        // outside the given range
        if (se < qs || ss > qe)
            return 0;

        // If a part of this segment
        // overlaps the given range
        int mid = getMid(ss, se);

        return getSumUtil(st, ss, mid, qs, qe, 2 * si + 1)
            + getSumUtil(st, mid + 1, se, qs, qe,
                         2 * si + 2);
    }

    // Function to find the sum of elements
    // in the range from index qs (query
    // start) to qe (query end)
    static int getSum(int st[], int n, int qs, int qe)
    {
        // Invalid ranges
        if (qs < 0 || qe > n - 1 || qs > qe) {
            System.out.println("Invalid Input");
            return -1;
        }

        return getSumUtil(st, 0, n - 1, qs, qe, 0);
    }

    // Recursive function to construct the
    // Segment Tree for array[ss..se]. si
    // is index of current node in tree st
    static int constructSTUtil(int arr[], int ss, int se,
                               int st[], int si)
    {
        // If there is one element
        // in the array
        if (ss == se) {
            st[si] = arr[ss];
            return arr[ss];
        }

        int mid = getMid(ss, se);

        // Recur for left and right
        // subtrees and store the sum
        // of values in this node
        st[si]
            = constructSTUtil(arr, ss, mid, st, si * 2 + 1)
              + constructSTUtil(arr, mid + 1, se, st,
                                si * 2 + 2);
        return st[si];
    }

    // Function to construct segment tree
    // from the given array
    static int[] constructST(int arr[], int n)
    {
        // Allocate memory for the segment
        // tree Height of segment tree
        int x = (int)(Math.ceil(Math.log(n) / Math.log(2)));

        // Maximum size of segment tree
        int max_size = 2 * (int)Math.pow(2, x) - 1;

        // Allocate memory
        int st[] = new int[max_size];

        // Fill the allocated memory st
        constructSTUtil(arr, 0, n - 1, st, 0);

        // Return the constructed
        // segment tree
        return st;
    }

    // Function to find the sum of elements
    // having odd number of divisors in
    // index range [L, R] for Q queries
    static void OddDivisorsSum(int n, int q, int arr[],
                               int Query[][])
    {
        // Traverse the array, arr[]
        for (int i = 0; i < n; i++) {
            int sq = (int)Math.sqrt(arr[i]);

            // Replace elements that are
            // not perfect squares with 0
            if (sq * sq != arr[i])
                arr[i] = 0;
        }

        // Build segment tree from the
        // given array
        int st[] = constructST(arr, n);

        // Iterate through all the queries
        for (int i = 0; i < q; i++) {
            int l = Query[i][0];
            int r = Query[i][1];

            // Print sum of values in
            // array from index l to r
            System.out.print(getSum(st, n, l, r) + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        int arr[] = { 2, 4, 5, 6, 9 };
        int N = arr.length;
        int Q = 3;
        int Query[][] = { { 0, 2 }, { 1, 3 }, { 1, 4 } };
        OddDivisorsSum(N, Q, arr, Query);
    }
}

// This code is contributed by Kingash.
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Function to get the middle index
// from the given ranges
function getMid(s,e)
{
    return s + Math.floor((e - s) / 2);
}

// Recursive function to find the sum
// of values in the given range of
// the array
function getSumUtil(st,ss,se,qs,qe,si)
{
    // If segment of this node is a
        // part of given range, then
        // return the sum of the segment
        if (qs <= ss && qe >= se)
            return st[si];

        // If segment of this node is
        // outside the given range
        if (se < qs || ss > qe)
            return 0;

        // If a part of this segment
        // overlaps the given range
        let mid = getMid(ss, se);

        return getSumUtil(st, ss, mid, qs, qe, 2 * si + 1)
            + getSumUtil(st, mid + 1, se, qs, qe,
                         2 * si + 2);
    }

    // Function to find the sum of elements
    // in the range from index qs (query
    // start) to qe (query end)
    function getSum( st,  n,  qs,  qe)
    {
        // Invalid ranges
        if (qs < 0 || qe > n - 1 || qs > qe) {
            document.write("Invalid Input");
            return -1;
        }

        return getSumUtil(st, 0, n - 1, qs, qe, 0);
    }

// Recursive function to construct the
// Segment Tree for array[ss..se]. si
// is index of current node in tree st
function  constructSTUtil(arr,ss,se,st,si)
{
    // If there is one element
        // in the array
        if (ss == se) {
            st[si] = arr[ss];
            return arr[ss];
        }

        let mid = getMid(ss, se);

        // Recur for left and right
        // subtrees and store the sum
        // of values in this node
        st[si]
            = constructSTUtil(arr, ss, mid, st, si * 2 + 1)
              + constructSTUtil(arr, mid + 1, se, st,
                                si * 2 + 2);
        return st[si];
}

// Function to construct segment tree
    // from the given array
function constructST(arr,n)
{
    // Allocate memory for the segment
        // tree Height of segment tree
        let x = (Math.ceil(Math.log(n) / Math.log(2)));

        // Maximum size of segment tree
        let max_size = 2 * Math.pow(2, x) - 1;

        // Allocate memory
        let st = new Array(max_size);

        // Fill the allocated memory st
        constructSTUtil(arr, 0, n - 1, st, 0);

        // Return the constructed
        // segment tree
        return st;
}

// Function to find the sum of elements
    // having odd number of divisors in
    // index range [L, R] for Q queries
function OddDivisorsSum(n,q,arr,Query)
{
    // Traverse the array, arr[]
        for (let i = 0; i < n; i++) {
            let sq = Math.sqrt(arr[i]);

            // Replace elements that are
            // not perfect squares with 0
            if (sq * sq != arr[i])
                arr[i] = 0;
        }

        // Build segment tree from the
        // given array
        let st = constructST(arr, n);

        // Iterate through all the queries
        for (let i = 0; i < q; i++) {
            let l = Query[i][0];
            let r = Query[i][1];

            // Print sum of values in
            // array from index l to r
            document.write(getSum(st, n, l, r) + " ");
        }
}

 // Driver Code
let arr=[2, 4, 5, 6, 9];
let N = arr.length;
let Q = 3;
let Query=[[ 0, 2 ], [ 1, 3 ], [ 1, 4 ]];
OddDivisorsSum(N, Q, arr, Query);

// This code is contributed by avanitrachhadiya2155

</script>
```

****Output:** 

```
4 4 13
```** 

*****时间复杂度:** O(Q * log(N))*
***辅助空间:** O(N)***

****高效方法:**为了优化上述方法，想法是使用辅助数组，该数组存储具有奇数除数的元素的前缀和。按照以下步骤解决问题:**

*   **用 **0** 初始化一个大小为 **N** 的数组 **dp[]** 。**
*   **[使用变量 **i** 和](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)[遍历给定的数组](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/) **arr[]** ，检查是否有任何元素是完美的正方形。如果发现为真，则将 **dp[i]** 的值更新为 **arr[i]** 。**
*   **找到数组 **dp[]** 的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。**
*   **[遍历所有查询](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)，对于**【L，R】**范围内的每个查询，答案将由**(DP[R]–DP[L–1])**给出。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of elements
// having odd number of divisors in
// index range [L, R] for Q queries
void OddDivisorsSum(int n, int q, int a[],
                    vector<pair<int, int> > Query)
{
    // Initialize the dp[] array
    int DP[n] = { 0 };

    // Traverse the array, arr[]
    for (int i = 0; i < n; i++) {
        int x = sqrt(a[i]);

        // If a[i] is a perfect square,
        // then update value of DP[i] to a[i]
        if (x * x == a[i])
            DP[i] = a[i];
    }

    // Find the prefix sum of DP[] array
    for (int i = 1; i < n; i++) {
        DP[i] = DP[i - 1] + DP[i];
    }

    // Iterate through all the queries
    for (int i = 0; i < q; i++) {

        int l = Query[i].first;
        int r = Query[i].second;

        // Find the sum for each query
        if (l == 0) {
            cout << DP[r] << " ";
        }
        else {
            cout << DP[r] - DP[l - 1]
                 << " ";
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 5, 6, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int Q = 3;
    vector<pair<int, int> > Query
        = { { 0, 2 }, { 1, 3 }, { 1, 4 } };
    OddDivisorsSum(N, Q, arr, Query);

    return 0;
}
```

## **蟒蛇 3**

```
# Python3 program for the above approach
from math import sqrt

# Function to find the sum of elements
# having odd number of divisors in
# index range [L, R] for Q queries
def OddDivisorsSum(n, q, a, Query):

    # Initialize the dp[] array
    DP = [0]*n

    # Traverse the array, arr[]
    for i in range(n):
        x = sqrt(a[i])

        # If a[i] is a perfect square,
        # then update value of DP[i] to a[i]
        if (x * x == a[i]):
            DP[i] = a[i]

    # Find the prefix sum of DP[] array
    for i in range(1, n):
        DP[i] = DP[i - 1] + DP[i]

    # Iterate through all the queries
    for i in range(q):
        l = Query[i][0]
        r = Query[i][1]

        # Find the sum for each query
        if (l == 0):
            print(DP[r], end=" ")
        else:
            print(DP[r] - DP[l - 1], end=" ")

# Driver Code
if __name__ == '__main__':
    arr = [2, 4, 5, 6, 9]
    N = len(arr)
    Q = 3
    Query = [ [ 0, 2 ], [ 1, 3 ], [ 1, 4 ] ]
    OddDivisorsSum(N, Q, arr, Query)

    # This code is contributed by mohit kumar 29.
```

## **C#**

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find the sum of elements
    // having odd number of divisors in
    // index range [L, R] for Q queries
    static void OddDivisorsSum(int n, int q, int[] a,
                               int[, ] Query)
    {

        // Initialize the dp[] array
        int[] DP = new int[n];

        // Traverse the array, arr[]
        for (int i = 0; i < n; i++) {
            int x = (int)(Math.Sqrt(a[i]));

            // If a[i] is a perfect square,
            // then update value of DP[i] to a[i]
            if (x * x == a[i])
                DP[i] = a[i];
        }

        // Find the prefix sum of DP[] array
        for (int i = 1; i < n; i++) {
            DP[i] = DP[i - 1] + DP[i];
        }

        // Iterate through all the queries
        for (int i = 0; i < q; i++) {

            int l = Query[i, 0];
            int r = Query[i, 1];

            // Find the sum for each query
            if (l == 0) {
                Console.Write(DP[r] + " ");
            }
            else {
                Console.Write(DP[r] - DP[l - 1] + " ");
            }
        }
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 2, 4, 5, 6, 9 };
        int N = arr.Length;
        int Q = 3;
        int[, ] Query = { { 0, 2 }, { 1, 3 }, { 1, 4 } };
        OddDivisorsSum(N, Q, arr, Query);
    }
}

// This code is contributed by ukasp.
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to find the sum of elements
// having odd number of divisors in
// index range [L, R] for Q queries
function OddDivisorsSum(n, q, a, Query)
{

    // Initialize the dp[] array
    let DP = new Array(n);
     for(let i = 0; i < n; i++)
    {
        DP[i] = 0;
    }

    // Traverse the array, arr[]
    for(let i = 0; i < n; i++)
    {
        let x = Math.floor(Math.sqrt(a[i]));

        // If a[i] is a perfect square,
        // then update value of DP[i] to a[i]
        if (x * x == a[i])
            DP[i] = a[i];
    }

    // Find the prefix sum of DP[] array
    for(let i = 1; i < n; i++)
    {
        DP[i] = DP[i - 1] + DP[i];
    }

    // Iterate through all the queries
    for(let i = 0; i < q; i++)
    {
        let l = Query[i][0];
        let r = Query[i][1];

        // Find the sum for each query
        if (l == 0)
        {
            document.write(DP[r] + " ");
        }
        else
        {
            document.write(DP[r] - DP[l - 1] + " ");
        }
    }
}

// Driver Code
let arr = [ 2, 4, 5, 6, 9 ];
let N = arr.length;
let Q = 3
let Query = [ [ 0, 2 ],
              [ 1, 3 ],
              [ 1, 4 ] ];

OddDivisorsSum(N, Q, arr, Query);

// This code is contributed by patel2127

</script>
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {

    // Function to find the sum of elements
    // having odd number of divisors in
    // index range [L, R] for Q queries
    static void OddDivisorsSum(int n, int q, int[] a,
                               int[][]  Query)
    {

        // Initialize the dp[] array
        int[] DP = new int[n];

        // Traverse the array, arr[]
        for (int i = 0; i < n; i++) {
            int x = (int)(Math.sqrt(a[i]));

            // If a[i] is a perfect square,
            // then update value of DP[i] to a[i]
            if (x * x == a[i])
                DP[i] = a[i];
        }

        // Find the prefix sum of DP[] array
        for (int i = 1; i < n; i++) {
            DP[i] = DP[i - 1] + DP[i];
        }

        // Iterate through all the queries
        for (int i = 0; i < q; i++) {

            int l = Query[i][0];
            int r = Query[i][1];

            // Find the sum for each query
            if (l == 0) {
                System.out.print(DP[r] + " ");
            }
            else {
                System.out.print(DP[r] - DP[l - 1] + " ");
            }
        }
    }

    // Driver Code

    public static void main (String[] args) {

        int[] arr = { 2, 4, 5, 6, 9 };
        int N = arr.length;
        int Q = 3;
        int[][] Query = { { 0, 2 }, { 1, 3 }, { 1, 4 } };
        OddDivisorsSum(N, Q, arr, Query);

    }
}
```

****Output:** 

```
4 4 13
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**