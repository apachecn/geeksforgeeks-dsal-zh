# 给定数组交替加减的范围查询

> 原文:[https://www . geeksforgeeks . org/range-query-for-alternative-加减运算给定数组/](https://www.geeksforgeeks.org/range-queries-for-alternatively-addition-and-subtraction-on-given-array/)

给定一个由 **N** 整数和 **Q** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**查询，其中每行由两个数字 **L 和 R** 组成，表示范围**【L，R】**，任务是找到范围**【L，R】**之间数组元素的交替加减值。

**示例:**

> **输入:** arr[] = {10，13，15，2，45，31，22，3，27}，Q[][] = {{2，5}，{6，8}，{1，7}，{4，8}，{0，5} }
> T3】输出: 27 46 -33 60 24
> **解释:**
> 查询{2，5 }的结果为 27(15–2+45) 7}是-33(13–15+2–45+31–22+3)
> 查询{4，8}的结果是 60(45–31+22–3+27)
> 查询{0，5}的结果是 24(10–13+15–2+45–31)
> 
> **输入:** arr[] = {1，1，1，1，1，1，1}，Q[] = {{2，5}，{6，8}，{1，7}，{4，8}，{0，5}}
> **输出:**0 1 1 1 1 0

**天真方法:**天真的想法是对每个查询从索引 **L 迭代到 R** ，找到数组元素交替加减的值，并在执行操作后打印该值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure to represent a range query
struct Query {
    int L, R;
};

// Function to find the result of
// alternatively adding and subtracting
// elements in the range [L, R]
int findResultUtil(int arr[],
                   int L, int R)
{
    int result = 0;

    // A boolean variable flag to
    // alternatively add and subtract
    bool flag = false;

    // Iterate from [L, R]
    for (int i = L; i <= R; i++) {

        // if flag is false, then
        // add & toggle the flag
        if (flag == false) {
            result = result + arr[i];
            flag = true;
        }

        // if flag is true subtract
        // and toggle the flag
        else {
            result = result - arr[i];
            flag = false;
        }
    }

    // Return the final result
    return result;
}

// Function to find the value
// for each query
void findResult(int arr[], int n,
                Query q[], int m)
{

    // Iterate for each query
    for (int i = 0; i < m; i++) {
        cout << findResultUtil(arr,
                               q[i].L,
                               q[i].R)
             << " ";
    }
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 10, 13, 15, 2, 45,
                  31, 22, 3, 27 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Given Queries
    Query q[] = { { 2, 5 }, { 6, 8 },
                  { 1, 7 }, { 4, 8 },
                  { 0, 5 } };

    int m = sizeof(q) / sizeof(q[0]);

    // Function Call
    findResult(arr, n, q, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Structure to represent a range query
static class Query
{
    int L, R;
    public Query(int l, int r)
    {
        super();
        L = l;
        R = r;
    }
};

// Function to find the result of
// alternatively adding and subtracting
// elements in the range [L, R]
static int findResultUtil(int arr[],
                          int L, int R)
{
    int result = 0;

    // A boolean variable flag to
    // alternatively add and subtract
    boolean flag = false;

    // Iterate from [L, R]
    for(int i = L; i <= R; i++)
    {

        // If flag is false, then
        // add & toggle the flag
        if (flag == false)
        {
            result = result + arr[i];
            flag = true;
        }

        // If flag is true subtract
        // and toggle the flag
        else
        {
            result = result - arr[i];
            flag = false;
        }
    }

    // Return the final result
    return result;
}

// Function to find the value
// for each query
static void findResult(int arr[], int n,
                       Query q[], int m)
{

    // Iterate for each query
    for(int i = 0; i < m; i++)
    {
        System.out.print(findResultUtil(arr,
              q[i].L, q[i].R) + " ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 10, 13, 15, 2, 45,
                  31, 22, 3, 27 };

    int n = arr.length;

    // Given Queries
    Query q[] = { new Query(2, 5), new Query(6, 8),
                  new Query(1, 7), new Query(4, 8),
                  new Query(0, 5) };

    int m = q.length;

    // Function call
    findResult(arr, n, q, m);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the result of
# alternatively adding and subtracting
# elements in the range [L, R]
def findResultUtil(arr, L, R):

    result = 0

    # A boolean variable flag to
    # alternatively add and subtract
    flag = False

    # Iterate from [L, R]
    for i in range(L, R + 1):

        # If flag is False, then
        # add & toggle the flag
        if (flag == False):
            result = result + arr[i]
            flag = True

        # If flag is True subtract
        # and toggle the flag
        else:
            result = result - arr[i]
            flag = False

    # Return the final result
    return result

# Function to find the value
# for each query
def findResult(arr, n, q, m):

    # Iterate for each query
    for i in range(m):
        print(findResultUtil(arr,
                             q[i][0],
                             q[i][1]),
                             end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 10, 13, 15, 2, 45,
            31, 22, 3, 27 ]

    n = len(arr)

    # Given Queries
    q = [ [ 2, 5 ], [ 6, 8 ],
          [ 1, 7 ], [ 4, 8 ],
          [ 0, 5 ] ]

    m = len(q)

    # Function Call
    findResult(arr, n, q, m)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Structure to represent a range query
class Query
{
    public int L, R;
    public Query(int l, int r)
    {
        L = l;
        R = r;
    }
};

// Function to find the result of
// alternatively adding and subtracting
// elements in the range [L, R]
static int findResultUtil(int []arr,
                          int L, int R)
{
    int result = 0;

    // A bool variable flag to
    // alternatively add and subtract
    bool flag = false;

    // Iterate from [L, R]
    for(int i = L; i <= R; i++)
    {

        // If flag is false, then
        // add & toggle the flag
        if (flag == false)
        {
            result = result + arr[i];
            flag = true;
        }

        // If flag is true subtract
        // and toggle the flag
        else
        {
            result = result - arr[i];
            flag = false;
        }
    }

    // Return the readonly result
    return result;
}

// Function to find the value
// for each query
static void findResult(int []arr, int n,
                       Query []q, int m)
{

    // Iterate for each query
    for(int i = 0; i < m; i++)
    {
        Console.Write(findResultUtil(arr,
              q[i].L, q[i].R) + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 10, 13, 15, 2, 45,
                  31, 22, 3, 27 };

    int n = arr.Length;

    // Given Queries
    Query []q = { new Query(2, 5), new Query(6, 8),
                  new Query(1, 7), new Query(4, 8),
                  new Query(0, 5) };

    int m = q.Length;

    // Function call
    findResult(arr, n, q, m);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the result of
// alternatively adding and subtracting
// elements in the range [L, R]
function findResultUtil(arr, L, R)
{
    var result = 0;

    // A boolean variable flag to
    // alternatively add and subtract
    var flag = false;

    // Iterate from [L, R]
    for (var i = L; i <= R; i++) {

        // if flag is false, then
        // add & toggle the flag
        if (flag == false) {
            result = result + arr[i];
            flag = true;
        }

        // if flag is true subtract
        // and toggle the flag
        else {
            result = result - arr[i];
            flag = false;
        }
    }

    // Return the final result
    return result;
}

// Function to find the value
// for each query
function findResult(arr, n, q, m)
{

    // Iterate for each query
    for (var i = 0; i < m; i++) {
        document.write( findResultUtil(arr,
                               q[i][0],
                               q[i][1])
             + " ");
    }
}

// Driver Code
// Given array
var arr = [10, 13, 15, 2, 45,
              31, 22, 3, 27 ];
var n = arr.length;
// Given Queries
var q = [ [ 2, 5 ], [ 6, 8 ],
              [ 1, 7 ], [ 4, 8 ],
              [ 0, 5 ] ];
var m = q.length;
// Function Call
findResult(arr, n, q, m);

</script>
```

**Output:**

```
27 46 -33 60 24
```

**时间复杂度:***O(N * Q)*
T5】辅助空间: *O(1)*

**高效途径:**高效途径是使用[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)解决上述问题。以下是步骤:

1.  将前缀数组的第一个元素(比如 **pre[]** )初始化为 **arr[]** 的第一个元素。
2.  遍历从 **1 到 N-1** 的索引，或者从 pre[i-1]中加减 arr[i]的元素，并将其存储在 pre[i]中，形成前缀数组。
3.  现在，迭代从 **1 到 Q** 的每个查询，并根据以下情况找到结果:
    *   **情况 1:** 如果 L 为零，则**结果为预【R】**。
    *   **情况 2:** 如果 L 为非零，则使用以下等式求出结果:

```
result = Query(L, R) = pre[R] – pre[L - 1]
```

*   如果 L 为奇数，将上述结果乘以 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure to represent a query
struct Query {
    int L, R;
};

// This function fills the Prefix Array
void fillPrefixArray(int arr[], int n,
                    int prefixArray[])
{
    // Initialise the prefix array
    prefixArray[0] = arr[0];

    // Iterate all the element of arr[]
    // and update the prefix array
    for (int i = 1; i < n; i++) {

        // If n is even then, add the
        // previous value of prefix array
        // with the current value of arr
        if (i % 2 == 0) {

            prefixArray[i]
                = prefixArray[i - 1]
                + arr[i];
        }

        // if n is odd, then subtract
        // the previous value of prefix
        // Array from current value
        else {
            prefixArray[i]
                = prefixArray[i - 1]
                - arr[i];
        }
    }
}

// Function to find the result of
// alternatively adding and subtracting
// elements in the range [L< R]
int findResultUtil(int prefixArray[],
                int L, int R)
{
    int result;

    // Case 1 : when L is zero
    if (L == 0) {
        result = prefixArray[R];
    }

    // Case 2 : When L is non zero
    else {
        result = prefixArray[R]
                - prefixArray[L - 1];
    }

    // If L is odd means range starts from
    // odd position multiply result by -1
    if (L & 1) {
        result = result * (-1);
    }

    // Return the final result
    return result;
}

// Function to find the sum of all
// alternative add and subtract
// between ranges [L, R]
void findResult(int arr[], int n,
                Query q[], int m)
{

    // Declare prefix array
    int prefixArray[n];

    // Function Call to fill prefix arr[]
    fillPrefixArray(arr, n, prefixArray);

    // Iterate for each query
    for (int i = 0; i < m; i++) {

        cout << findResultUtil(prefixArray,
                            q[i].L,
                            q[i].R)
            << " ";
    }
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 10, 13, 15, 2, 45,
                31, 22, 3, 27 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Given Queries
    Query q[] = { { 2, 5 }, { 6, 8 },
                { 1, 7 }, { 4, 8 },
                { 0, 5 } };

    int m = sizeof(q) / sizeof(q[0]);

    // Function Call
    findResult(arr, n, q, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Structure to represent a query
static class Query
{
    int L, R;

    public Query(int l, int r)
    {
        super();
        L = l;
        R = r;
    }
};

// This function fills the Prefix Array
static void fillPrefixArray(int arr[], int n,
                            int prefixArray[])
{
    // Initialise the prefix array
    prefixArray[0] = arr[0];

    // Iterate all the element of arr[]
    // and update the prefix array
    for (int i = 1; i < n; i++)
    {

        // If n is even then, add the
        // previous value of prefix array
        // with the current value of arr
        if (i % 2 == 0)
        {
            prefixArray[i] = prefixArray[i - 1] +
                                           arr[i];
        }

        // if n is odd, then subtract
        // the previous value of prefix
        // Array from current value
        else
        {
            prefixArray[i] = prefixArray[i - 1] -
                                           arr[i];
        }
    }
}

// Function to find the result of
// alternatively adding and subtracting
// elements in the range [L< R]
static int findResultUtil(int prefixArray[],
                          int L, int R)
{
    int result;

    // Case 1 : when L is zero
    if (L == 0)
    {
        result = prefixArray[R];
    }

    // Case 2 : When L is non zero
    else
    {
        result = prefixArray[R] -
                   prefixArray[L - 1];
    }

    // If L is odd means range starts from
    // odd position multiply result by -1
    if (L % 2 == 1)
    {
        result = result * (-1);
    }

    // Return the final result
    return result;
}

// Function to find the sum of all
// alternative add and subtract
// between ranges [L, R]
static void findResult(int arr[], int n,
                         Query q[], int m)
{

    // Declare prefix array
    int []prefixArray = new int[n];

    // Function Call to fill prefix arr[]
    fillPrefixArray(arr, n, prefixArray);

    // Iterate for each query
    for (int i = 0; i < m; i++)
    {
        System.out.print(findResultUtil(
                           prefixArray, q[i].L,
                                        q[i].R) + " ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 10, 13, 15, 2, 45,
                31, 22, 3, 27 };

    int n = arr.length;

    // Given Queries
    Query q[] = {new Query( 2, 5 ), new Query( 6, 8 ),
                 new Query( 1, 7 ), new Query( 4, 8 ),
                 new Query( 0, 5 )};

    int m = q.length;

    // Function Call
    findResult(arr, n, q, m);
}
}

// This code is contributed by PrinciRaj1992
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Structure to represent a query
class Query
{
   public  int L, R;

    public Query(int l, int r)
    {
        L = l;
        R = r;
    }
};

// This function fills the Prefix Array
static void fillPrefixArray(int []arr, int n,
                            int []prefixArray)
{
    // Initialise the prefix array
    prefixArray[0] = arr[0];

    // Iterate all the element of []arr
    // and update the prefix array
    for (int i = 1; i < n; i++)
    {

        // If n is even then, add the
        // previous value of prefix array
        // with the current value of arr
        if (i % 2 == 0)
        {
            prefixArray[i] = prefixArray[i - 1] +
                                         arr[i];
        }

        // if n is odd, then subtract
        // the previous value of prefix
        // Array from current value
        else
        {
            prefixArray[i] = prefixArray[i - 1] -
                                         arr[i];
        }
    }
}

// Function to find the result of
// alternatively adding and subtracting
// elements in the range [L< R]
static int findResultUtil(int []prefixArray,
                          int L, int R)
{
    int result;

    // Case 1 : when L is zero
    if (L == 0)
    {
        result = prefixArray[R];
    }

    // Case 2 : When L is non zero
    else
    {
        result = prefixArray[R] -
                 prefixArray[L - 1];
    }

    // If L is odd means range starts from
    // odd position multiply result by -1
    if (L % 2 == 1)
    {
        result = result * (-1);
    }

    // Return the readonly result
    return result;
}

// Function to find the sum of all
// alternative add and subtract
// between ranges [L, R]
static void findResult(int []arr, int n,
                       Query []q, int m)
{

    // Declare prefix array
    int []prefixArray = new int[n];

    // Function Call to fill prefix []arr
    fillPrefixArray(arr, n, prefixArray);

    // Iterate for each query
    for (int i = 0; i < m; i++)
    {
        Console.Write(findResultUtil(
                           prefixArray, q[i].L,
                                        q[i].R) + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 10, 13, 15, 2, 45,
                31, 22, 3, 27 };

    int n = arr.Length;

    // Given Queries
    Query []q = {new Query( 2, 5 ), new Query( 6, 8 ),
                 new Query( 1, 7 ), new Query( 4, 8 ),
                 new Query( 0, 5 )};

    int m = q.Length;

    // Function Call
    findResult(arr, n, q, m);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Structure to represent a query
class Query
{
    constructor(l, r)
    {
        this.L = l;
        this.R = r;
    }
}

// This function fills the Prefix Array
function fillPrefixArray(arr, n, prefixArray)
{

    // Initialise the prefix array
    prefixArray[0] = arr[0];

    // Iterate all the element of arr[]
    // and update the prefix array
    for(let i = 1; i < n; i++)
    {

        // If n is even then, add the
        // previous value of prefix array
        // with the current value of arr
        if (i % 2 == 0)
        {
            prefixArray[i] = prefixArray[i - 1] +
                                           arr[i];
        }

        // if n is odd, then subtract
        // the previous value of prefix
        // Array from current value
        else
        {
            prefixArray[i] = prefixArray[i - 1] -
                                     arr[i];
        }
    }
}

// Function to find the result of
// alternatively adding and subtracting
// elements in the range [L< R]
function findResultUtil(prefixArray, L, R)
{
     let result;

    // Case 1 : when L is zero
    if (L == 0)
    {
        result = prefixArray[R];
    }

    // Case 2 : When L is non zero
    else
    {
        result = prefixArray[R] -
                 prefixArray[L - 1];
    }

    // If L is odd means range starts from
    // odd position multiply result by -1
    if (L % 2 == 1)
    {
        result = result * (-1);
    }

    // Return the final result
    return result;
}

// Function to find the sum of all
// alternative add and subtract
// between ranges [L, R]
function findResult(arr, n, q, m)
{

    // Declare prefix array
    let prefixArray = new Array(n);

    // Function Call to fill prefix arr[]
    fillPrefixArray(arr, n, prefixArray);

    // Iterate for each query
    for(let i = 0; i < m; i++)
    {
        document.write(findResultUtil(
                        prefixArray, q[i].L,
                                     q[i].R) + " ");
    }
}

// Driver Code

// Given array
let arr = [ 10, 13, 15, 2, 45,
            31, 22, 3, 27 ];
let n = arr.length;

// Given Queries
let q = [ new Query(2, 5), new Query(6, 8),
          new Query(1, 7), new Query(4, 8),
          new Query(0, 5)];
let m = q.length;

// Function Call
findResult(arr, n, q, m);

// This code is contributed by unknown2108

</script>
```

**输出:**

```
27 46 -33 60 24
```

**时间复杂度:**O(N+Q)
T3】辅助空间: O(N)