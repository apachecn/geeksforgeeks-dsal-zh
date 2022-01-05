# 给定范围内所有无序对与更新查询的乘积之和

> 原文:[https://www . geeksforgeeks . org/带有更新查询的给定范围内所有无序对的乘积之和/](https://www.geeksforgeeks.org/sum-of-product-of-all-unordered-pairs-in-given-range-with-update-queries/)

给定一个由以下类型的 **N** 整数和 **Q** 查询组成的数组 **A[]** ，任务是打印所有更新查询的输出。

*   **(1，L，R):** 第一种类型的查询，用于查找数组中从索引 **L** 到 **R** 的所有无序对的乘积的[和，其中 **1 < = L < = R < = N** 。](https://www.geeksforgeeks.org/sum-product-pairs-array-elements/)
*   **(2，P，X):** 第二种类型的查询，用于将数组的第 **P <sup>第</sup>T5】个整数的值更改为新值 **X** 。**

**示例:**

> **输入:** A[] = {5 7 2 3 1}，Q = 3，查询[] = [ [1，1，3]，[2，2，5]，[1，2，5]]
> 
> **输出:**
> 59
> 41
> T5】解释:
> 查询 1:在第一次查询中，给定范围内可能的对是(5，7)、(5，2)和(7，2)。所以两两乘积和将是(5*7) + (5*2) + (7*2) = 35 + 10 + 14 = 59。
> 查询 2:在第 2 次查询中，将第 2 个整数更新为 5，使数组为[5，5，2，3，1]。
> 查询 3:在第三个查询中，范围[2，5]中可能的对是(5，2)，(5，3)，(5，1)，(2，3)，(2，1)和(3，1)。这些对的乘积之和是 41。
> 
> **输入:** A[] = {7 3 2 1 4 5 8}，Q = 5，query[]=[[1，1，6]，[2，2，4]，[1，2，5]，[2，3，8]，[1，4，7]]
> 
> **输出:** 59
> 41
> 6

**天真方法:**解决这个问题的简单方法是，对于第一类查询，生成给定查询范围内的所有无序对，并打印这些对的乘积之和。对于第二种类型的查询，根据给定值更新数组元素。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the Pairwise
// Product Sum in range from L to R
void pairwiseProductSum(int a[], int l, int r)
{
    int sum = 0;

    // Loop to iterate over all possible
    // pairs from L to R
    for (int j = l - 1; j <= r - 1; j++) {
        for (int k = j + 1; k <= r - 1; k++) {
            sum += (a[j] * a[k]);
        }
    }

    // Print answer
    cout << sum << endl;
}

// Function to update the Array
// element at index P to X
void updateArray(int* a, int p, int x)
{
    // Update the value at Pth
    // index in the array
    a[p - 1] = x;
}

// Function to solve Q queries
void solveQueries(
    int* a, int n,
    int Q, int query[][3])
{

    for (int i = 0; i < Q; i++) {

        // If Query is of type 1
        if (query[i][0] == 1)
            pairwiseProductSum(
                a, query[i][1], query[i][2]);

        // If Query is of type 2
        else
            updateArray(
                a, query[i][1], query[i][2]);
    }
}

// Driver Code
int main()
{
    int A[] = { 5, 7, 2, 3, 1 };
    int N = sizeof(A) / sizeof(int);
    int Q = 3;
    int query[Q][3] = { { 1, 1, 3 },
                        { 2, 2, 5 },
                        { 1, 2, 5 } };

    solveQueries(A, N, Q, query);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.util.*;

class GFG{

// Function to calculate the Pairwise
// Product Sum in range from L to R
static void pairwiseProductSum(int a[], int l, int r)
{
    int sum = 0;

    // Loop to iterate over all possible
    // pairs from L to R
    for (int j = l - 1; j <= r - 1; j++) {
        for (int k = j + 1; k <= r - 1; k++) {
            sum += (a[j] * a[k]);
        }
    }

    // Print answer
    System.out.print(sum +"\n");
}

// Function to update the Array
// element at index P to X
static void updateArray(int[] a, int p, int x)
{
    // Update the value at Pth
    // index in the array
    a[p - 1] = x;
}

// Function to solve Q queries
static void solveQueries(
    int[] a, int n,
    int Q,
    int query[][])
{

    for (int i = 0; i < Q; i++) {

        // If Query is of type 1
        if (query[i][0] == 1)
            pairwiseProductSum(
                a, query[i][1], query[i][2]);

        // If Query is of type 2
        else
            updateArray(
                a, query[i][1], query[i][2]);
    }
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 5, 7, 2, 3, 1 };
    int N = A.length;
    int Q = 3;
    int query[][] = { { 1, 1, 3 },
                        { 2, 2, 5 },
                        { 1, 2, 5 } };

    solveQueries(A, N, Q, query);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 Program for the above approach

# Function to calculate the Pairwise
# Product Sum in range from L to R
def pairwiseProductSum(a, l, r):
    sum = 0

    # Loop to iterate over all possible
    # pairs from L to R
    for j in range(l - 1,r,1):
        for k in range(j + 1,r,1):
            sum += (a[j] * a[k]);

    # Print answer
    print(sum)

# Function to update the Array
# element at index P to X
def updateArray(a, p, x):
    # Update the value at Pth
    # index in the array
    a[p - 1] = x

# Function to solve Q queries
def solveQueries(a,n,Q,query):
    for i in range(Q):
        # If Query is of type 1
        if (query[i][0] == 1):
            pairwiseProductSum(a, query[i][1], query[i][2])

        # If Query is of type 2
        else:
            updateArray(a, query[i][1], query[i][2])

# Driver Code
if __name__ == '__main__':
    A = [5, 7, 2, 3, 1]
    N = len(A)
    Q = 3
    query = [[1, 1, 3],[2, 2, 5],[1, 2, 5]]

    solveQueries(A, N, Q, query)

    # This code is contributed by ipg2016107
```

## C#

```
//C# code for the above approach
using System;

public class GFG{
// Function to calculate the Pairwise
// Product Sum in range from L to R
static void pairwiseProductSum(int[] a, int l, int r)
{
    int sum = 0;

    // Loop to iterate over all possible
    // pairs from L to R
    for (int j = l - 1; j <= r - 1; j++) {
        for (int k = j + 1; k <= r - 1; k++) {
            sum += (a[j] * a[k]);
        }
    }

    // Print answer
    Console.Write(sum +"\n");
}

// Function to update the Array
// element at index P to X
static void updateArray(int[] a, int p, int x)
{
    // Update the value at Pth
    // index in the array
    a[p - 1] = x;
}

// Function to solve Q queries
static void solveQueries(
    int[] a, int n,
    int Q,
    int[][] query)
{

    for (int i = 0; i < Q; i++) {

        // If Query is of type 1
        if (query[i][0] == 1)
            pairwiseProductSum(
                a, query[i][1], query[i][2]);

        // If Query is of type 2
        else
            updateArray(
                a, query[i][1], query[i][2]);
    }
}

// Driver Code
    static public void Main (){

        // Code
      int[] A = { 5, 7, 2, 3, 1 };
    int N = A.Length;
    int Q = 3;
        int[][] query = {
                            new int[3]{ 1, 1, 3 },
                            new int[3]{ 2, 2, 5 },
                            new int[3] { 1, 2, 5 }
                           };

    solveQueries(A, N, Q, query);
    }
}
// This code is contributed by Potta Lokesh
```

## java 描述语言

```
<script>
// Javascript Program for the above approach

// Function to calculate the Pairwise
// Product Sum in range from L to R
function pairwiseProductSum(a, l, r)
{
  let sum = 0;

  // Loop to iterate over all possible
  // pairs from L to R
  for (let j = l - 1; j <= r - 1; j++) {
    for (let k = j + 1; k <= r - 1; k++) {
      sum += a[j] * a[k];
    }
  }

  // Print answer
  document.write(sum + "<br>");
}

// Function to update the Array
// element at index P to X
function updateArray(a, p, x)
{

  // Update the value at Pth
  // index in the array
  a[p - 1] = x;
}

// Function to solve Q queries
function solveQueries(a, n, Q, query)
{
  for (let i = 0; i < Q; i++)
  {

    // If Query is of type 1
    if (query[i][0] == 1) pairwiseProductSum(a, query[i][1], query[i][2]);

    // If Query is of type 2
    else updateArray(a, query[i][1], query[i][2]);
  }
}

// Driver Code
let A = [5, 7, 2, 3, 1];
let N = A.length;
let Q = 3;
let query = [
  [1, 1, 3],
  [2, 2, 5],
  [1, 2, 5],
];

solveQueries(A, N, Q, query);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
59
41
```

**时间复杂度:** *O(N <sup>2</sup> )* 为成对积和查询， *O(1)* 为更新查询。
**空间复杂度:** *O(N)*

**有效方法:**使用这里讨论的[前缀求和技术](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，每个查询的复杂度可以降低到 *O(N)* 。

**更好的方法:**进一步降低复杂性的更好方法是基于以下观察结果使用[芬威克树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/):

> 鉴于
> (a+b+ c)<sup>2</sup>= a<sup>2</sup>+b<sup>2</sup>+c<sup>2</sup>+2 *(a * b+ b * c+c * a)
> 让所需的成对乘积和为 P
> 让 E =(a1+a2+a3+a4……+an)<sup>2</sup>
> =>E = a1<sup>2</sup>+a2【)
> =>E = a1<sup>2</sup>+a2<sup>2</sup>+…+an<sup>2</sup>+2 *(P)
> =>P =(E –( a1<sup>2</sup>+a2<sup>2</sup>+…。+an<sup>2</sup>)/2
> 所以，P =(E–Q)/2 其中 Q =(a1<sup>2</sup>+a2<sup>2</sup>+…。+ an <sup>2</sup>

根据以上观察，我们可以养护两株芬威克树。

*   首先，Fenwick 树将通过更新查询跟踪给定范围内的[元素的总和。这可用于计算任何给定范围的 **E** 。](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)
*   同样，第二个芬威克树将通过更新查询跟踪给定范围内元素的平方和。这可用于计算任何给定范围的 **Q** 。此后， **P** 可以很容易地计算为**P =(E–Q)/2**。

下面是上述方法的实现:

## C++

```
<script>
// javascript Program for the above approach
var MAXN = 100000;

// Vector to store fenwick tree
// of the 1st type
var bit1 = Array.from({length: MAXN}, (_, i) => 0);

// Vector to store fenwick tree
// of the 2nd type
var bit2 = Array.from({length: MAXN}, (_, i) => 0);

// Function to update the value
// at idx index in fenwick tree
function update(idx , val , bit)
{
    while (idx < bit.length) {
        bit[idx] += val;
        idx += idx & (-idx);
    }
}

// Function to return the sum of values
// stored from O to idx index in the
// array using Fenwick Tree
function Query(idx , bit)
{
    var res = 0;
    while (idx > 0) {
        res += bit[idx];
        idx -= idx & (-idx);
    }
    return res;
}

// Function to build the Fenwick
// tree from the a Array
function buildFenwickTree(a , n)
{
    for (var i = 1; i <= n; i++) {

        // Function call to update
        // the ith element in the
        // first Fenwick Tree
        update(i, a[i - 1], bit1);

        // Function call to update
        // the ith element in the
        // first Fenwick Tree
        update(i, a[i - 1] * a[i - 1], bit2);
    }
}

// Function to find the Pairwise
// Product Sum in the range L to R
function pairwiseProductSum(a , l , r)
{
    var sum, e, q;

    // Function call to calculate E
    // in the given range
    e = Query(r, bit1) - Query(l - 1, bit1);
    e = e * e;

    // Function call to calculate E
    // in the given range
    q = Query(r, bit2) - Query(l - 1, bit2);
    sum = (e - q) / 2;

    // Print Answer
    document.write(sum +"<br>");
}

// Function to update the Fenwick
// tree and the array element at
// index P to the new value X
function updateArray(a , p , x)
{
    // Function call to update the
    // value in 1st Fenwick Tree
    update(p, -a[p - 1], bit1);
    update(p, x, bit1);

    // Function call to update the
    // value in 2nd Fenwick Tree
    update(p, -a[p - 1] * a[p - 1], bit2);
    update(p, x * x, bit2);

    a[p - 1] = x;
}

// Function to solve Q queries
function solveQueries(
    a , n,
    Q , query)
{
    // Function Call to build the
    // Fenwick Tree
    buildFenwickTree(a, n);

    for (var i = 0; i < Q; i++) {

        // If Query is of type 1
        if (query[i][0] == 1)
            pairwiseProductSum(
                a, query[i][1], query[i][2]);

        // If Query is of type 2
        else
            updateArray(
                a, query[i][1], query[i][2]);
    }
}

// Driver Code

    var A = [ 5, 7, 2, 3, 1 ];
    var N = A.length;
    var Q = 3;
    var query = [ [ 1, 1, 3 ],
                        [ 2, 2, 5 ],
                        [ 1, 2, 5 ] ];

    solveQueries(A, N, Q, query);

// This code is contributed by 29AjayKumar
</script>
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach

class GFG{

static final int MAXN = 100000;

// Vector to store fenwick tree
// of the 1st type
static int []bit1 = new int[MAXN];

// Vector to store fenwick tree
// of the 2nd type
static int []bit2 = new int[MAXN];

// Function to update the value
// at idx index in fenwick tree
static void update(int idx, int val, int []bit)
{
    while (idx < bit.length) {
        bit[idx] += val;
        idx += idx & (-idx);
    }
}

// Function to return the sum of values
// stored from O to idx index in the
// array using Fenwick Tree
static int query(int idx, int []bit)
{
    int res = 0;
    while (idx > 0) {
        res += bit[idx];
        idx -= idx & (-idx);
    }
    return res;
}

// Function to build the Fenwick
// tree from the a[] Array
static void buildFenwickTree(int a[], int n)
{
    for (int i = 1; i <= n; i++) {

        // Function call to update
        // the ith element in the
        // first Fenwick Tree
        update(i, a[i - 1], bit1);

        // Function call to update
        // the ith element in the
        // first Fenwick Tree
        update(i, a[i - 1] * a[i - 1], bit2);
    }
}

// Function to find the Pairwise
// Product Sum in the range L to R
static void pairwiseProductSum(int a[], int l, int r)
{
    int sum, e, q;

    // Function call to calculate E
    // in the given range
    e = query(r, bit1) - query(l - 1, bit1);
    e = e * e;

    // Function call to calculate E
    // in the given range
    q = query(r, bit2) - query(l - 1, bit2);
    sum = (e - q) / 2;

    // Print Answer
    System.out.print(sum +"\n");
}

// Function to update the Fenwick
// tree and the array element at
// index P to the new value X
static void updateArray(int[] a, int p, int x)
{
    // Function call to update the
    // value in 1st Fenwick Tree
    update(p, -a[p - 1], bit1);
    update(p, x, bit1);

    // Function call to update the
    // value in 2nd Fenwick Tree
    update(p, -a[p - 1] * a[p - 1], bit2);
    update(p, x * x, bit2);

    a[p - 1] = x;
}

// Function to solve Q queries
static void solveQueries(
    int[] a, int n,
    int Q, int query[][])
{
    // Function Call to build the
    // Fenwick Tree
    buildFenwickTree(a, n);

    for (int i = 0; i < Q; i++) {

        // If Query is of type 1
        if (query[i][0] == 1)
            pairwiseProductSum(
                a, query[i][1], query[i][2]);

        // If Query is of type 2
        else
            updateArray(
                a, query[i][1], query[i][2]);
    }
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 5, 7, 2, 3, 1 };
    int N = A.length;
    int Q = 3;
    int query[][] = { { 1, 1, 3 },
                        { 2, 2, 5 },
                        { 1, 2, 5 } };

    solveQueries(A, N, Q, query);

}
}

// This code is contributed by Princi Singh
```

## C#

```
// C# Program for the above approach
using System;
class GFG {

    static int MAXN = 100000;

    // Vector to store fenwick tree
    // of the 1st type
    static int[] bit1 = new int[MAXN];

    // Vector to store fenwick tree
    // of the 2nd type
    static int[] bit2 = new int[MAXN];

    // Function to update the value
    // at idx index in fenwick tree
    static void update(int idx, int val, int[] bit)
    {
        while (idx < bit.Length) {
            bit[idx] += val;
            idx += idx & (-idx);
        }
    }

    // Function to return the sum of values
    // stored from O to idx index in the
    // array using Fenwick Tree
    static int query(int idx, int[] bit)
    {
        int res = 0;
        while (idx > 0) {
            res += bit[idx];
            idx -= idx & (-idx);
        }
        return res;
    }

    // Function to build the Fenwick
    // tree from the a[] Array
    static void buildFenwickTree(int[] a, int n)
    {
        for (int i = 1; i <= n; i++) {

            // Function call to update
            // the ith element in the
            // first Fenwick Tree
            update(i, a[i - 1], bit1);

            // Function call to update
            // the ith element in the
            // first Fenwick Tree
            update(i, a[i - 1] * a[i - 1], bit2);
        }
    }

    // Function to find the Pairwise
    // Product Sum in the range L to R
    static void pairwiseProductSum(int[] a, int l, int r)
    {
        int sum, e, q;

        // Function call to calculate E
        // in the given range
        e = query(r, bit1) - query(l - 1, bit1);
        e = e * e;

        // Function call to calculate E
        // in the given range
        q = query(r, bit2) - query(l - 1, bit2);
        sum = (e - q) / 2;

        // Print Answer
        Console.WriteLine(sum);
    }

    // Function to update the Fenwick
    // tree and the array element at
    // index P to the new value X
    static void updateArray(int[] a, int p, int x)
    {
        // Function call to update the
        // value in 1st Fenwick Tree
        update(p, -a[p - 1], bit1);
        update(p, x, bit1);

        // Function call to update the
        // value in 2nd Fenwick Tree
        update(p, -a[p - 1] * a[p - 1], bit2);
        update(p, x * x, bit2);

        a[p - 1] = x;
    }

    // Function to solve Q queries
    static void solveQueries(int[] a, int n, int Q,
                             int[, ] query)
    {
        // Function Call to build the
        // Fenwick Tree
        buildFenwickTree(a, n);

        for (int i = 0; i < Q; i++) {

            // If Query is of type 1
            if (query[i, 0] == 1)
                pairwiseProductSum(a, query[i, 1],
                                   query[i, 2]);

            // If Query is of type 2
            else
                updateArray(a, query[i, 1], query[i, 2]);
        }
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] A = { 5, 7, 2, 3, 1 };
        int N = A.Length;
        int Q = 3;
        int[, ] query
            = { { 1, 1, 3 }, { 2, 2, 5 }, { 1, 2, 5 } };

        solveQueries(A, N, Q, query);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// javascript Program for the above approach
var MAXN = 100000;

// Vector to store fenwick tree
// of the 1st type
var bit1 = Array.from({length: MAXN}, (_, i) => 0);

// Vector to store fenwick tree
// of the 2nd type
var bit2 = Array.from({length: MAXN}, (_, i) => 0);

// Function to update the value
// at idx index in fenwick tree
function update(idx , val , bit)
{
    while (idx < bit.length) {
        bit[idx] += val;
        idx += idx & (-idx);
    }
}

// Function to return the sum of values
// stored from O to idx index in the
// array using Fenwick Tree
function Query(idx , bit)
{
    var res = 0;
    while (idx > 0) {
        res += bit[idx];
        idx -= idx & (-idx);
    }
    return res;
}

// Function to build the Fenwick
// tree from the a Array
function buildFenwickTree(a , n)
{
    for (var i = 1; i <= n; i++) {

        // Function call to update
        // the ith element in the
        // first Fenwick Tree
        update(i, a[i - 1], bit1);

        // Function call to update
        // the ith element in the
        // first Fenwick Tree
        update(i, a[i - 1] * a[i - 1], bit2);
    }
}

// Function to find the Pairwise
// Product Sum in the range L to R
function pairwiseProductSum(a , l , r)
{
    var sum, e, q;

    // Function call to calculate E
    // in the given range
    e = Query(r, bit1) - Query(l - 1, bit1);
    e = e * e;

    // Function call to calculate E
    // in the given range
    q = Query(r, bit2) - Query(l - 1, bit2);
    sum = (e - q) / 2;

    // Print Answer
    document.write(sum );
}

// Function to update the Fenwick
// tree and the array element at
// index P to the new value X
function updateArray(a, p, x)
{

    // Function call to update the
    // value in 1st Fenwick Tree
    update(p, -a[p - 1], bit1);
    update(p, x, bit1);

    // Function call to update the
    // value in 2nd Fenwick Tree
    update(p, -a[p - 1] * a[p - 1], bit2);
    update(p, x * x, bit2);

    a[p - 1] = x;
}

// Function to solve Q queries
function solveQueries(
    a , n,
    Q , query)
{
    // Function Call to build the
    // Fenwick Tree
    buildFenwickTree(a, n);

    for (var i = 0; i < Q; i++) {

        // If Query is of type 1
        if (query[i][0] == 1)
            pairwiseProductSum(
                a, query[i][1], query[i][2]);

        // If Query is of type 2
        else
            updateArray(
                a, query[i][1], query[i][2]);
    }
}

// Driver Code
    var A = [ 5, 7, 2, 3, 1 ];
    var N = A.length;
    var Q = 3;
    var query = [ [ 1, 1, 3 ],
                        [ 2, 2, 5 ],
                        [ 1, 2, 5 ] ];

    solveQueries(A, N, Q, query);

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
59
41
```

**时间复杂度:** *O(N*log N)* 为分威克树的构建
T5】O(log N)为成对积和查询
T8】O(log N)为更新查询。
**辅助空间:** *O(N)*