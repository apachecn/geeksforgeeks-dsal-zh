# 查询数组中从给定索引到最后一个索引的不同元素的数量

> 原文:[https://www . geesforgeks . org/query-for-number-of-distinct-elements-from-a-给定索引-直到数组中的最后一个索引/](https://www.geeksforgeeks.org/queries-for-number-of-distinct-elements-from-a-given-index-till-last-index-in-an-array/)

给定大小为 n 的数组“a[]”和查询数 q。每个查询可以用一个整数 m 来表示。您的任务是打印从索引 m 到 n 的不同整数的数目，即直到数组的最后一个元素。
**例:**

> **输入:** arr[] = {1，2，3，1，2，3，4，5}，q[] = {1，4，6，8}
> **输出:** 5 5 3 1
> 在查询 1 中，a[0…7]中的不同整数
> 的数量为 5 (1，2，3，4，5)
> 在查询 2 中，a[3…7]中的不同整数
> 的数量为 5 (1，2，3，4，5)

**进场:**

*   取一个数组**检查[]** ，检查当前元素是否被访问过。如果已经访问过，将其标记为 **1** 否则为 **0** 。
*   取一个数组 **idx[]** ，它将存储从当前索引到最后一个索引的不同元素的数量。
*   从最后一个循环开始，如果当前元素尚未被访问，将其检查标记为 **1** ，将当前计数器存储在 **idx** 中，并将其递增，否则只需将当前计数器存储在 **idx** 中。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 100001

// Function to perform queries to find
// number of distinct elements from
// a given index till last index in an array
void find_distinct(int a[], int n, int q, int queries[])
{
    int check[MAX] = { 0 };
    int idx[MAX];
    int cnt = 1;
    for (int i = n - 1; i >= 0; i--) {
        // Check if current element
        // already visited or not
        if (check[a[i]] == 0) {

            // If not visited store current counter
            // and increment it and mark check as 1
            idx[i] = cnt;
            check[a[i]] = 1;
            cnt++;
        }
        else {

            // Otherwise if visited simply
            // store current counter
            idx[i] = cnt - 1;
        }
    }

    // Perform queries
    for (int i = 0; i < q; i++) {
        int m = queries[i];
        cout << idx[m] << " ";
    }
}

// Driver code
int main()
{
    int a[] = { 1, 2, 3, 1, 2, 3, 4, 5 };
    int n = sizeof(a) / sizeof(int);
    int queries[] = { 0, 3, 5, 7 };
    int q = sizeof(queries) / sizeof(int);
    find_distinct(a, n, q, queries);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int MAX =100001;

// Function to perform queries to find
// number of distinct elements from
// a given index till last index in an array
static void find_distinct(int a[], int n, int q, int queries[])
{
    int []check = new int[MAX];
    int []idx = new int[MAX];
    int cnt = 1;
    for (int i = n - 1; i >= 0; i--)
    {
        // Check if current element
        // already visited or not
        if (check[a[i]] == 0)
        {

            // If not visited store current counter
            // and increment it and mark check as 1
            idx[i] = cnt;
            check[a[i]] = 1;
            cnt++;
        }
        else
        {

            // Otherwise if visited simply
            // store current counter
            idx[i] = cnt - 1;
        }
    }

    // Perform queries
    for (int i = 0; i < q; i++)
    {
            int m = queries[i];
            System.out.print(idx[m] + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 1, 2, 3, 1, 2, 3, 4, 5 };
    int n = a.length;
    int queries[] = { 0, 3, 5, 7 };
    int q = queries.length;
    find_distinct(a, n, q, queries);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python implementation of the approach
MAX = 100001;

# Function to perform queries to find
# number of distinct elements from
# a given index till last index in an array
def find_distinct(a, n, q, queries):
    check = [0] * MAX;
    idx = [0] * MAX;
    cnt = 1;
    for i in range(n - 1, -1, -1):

        # Check if current element
        # already visited or not
        if (check[a[i]] == 0):

            # If not visited store current counter
            # and increment it and mark check as 1
            idx[i] = cnt;
            check[a[i]] = 1;
            cnt += 1;
        else:

            # Otherwise if visited simply
            # store current counter
            idx[i] = cnt - 1;

    # Perform queries
    for i in range(0, q):
        m = queries[i];
        print(idx[m], end = " ");

# Driver code
a = [ 1, 2, 3, 1, 2, 3, 4, 5 ];
n = len(a);
queries = [ 0, 3, 5, 7 ];
q = len(queries);
find_distinct(a, n, q, queries);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int MAX =100001;

// Function to perform queries to find
// number of distinct elements from
// a given index till last index in an array
static void find_distinct(int []a, int n, int q, int []queries)
{
    int []check = new int[MAX];
    int []idx = new int[MAX];
    int cnt = 1;
    for (int i = n - 1; i >= 0; i--)
    {
        // Check if current element
        // already visited or not
        if (check[a[i]] == 0)
        {

            // If not visited store current counter
            // and increment it and mark check as 1
            idx[i] = cnt;
            check[a[i]] = 1;
            cnt++;
        }
        else
        {

            // Otherwise if visited simply
            // store current counter
            idx[i] = cnt - 1;
        }
    }

    // Perform queries
    for (int i = 0; i < q; i++)
    {
            int m = queries[i];
            Console.Write(idx[m] + " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 1, 2, 3, 1, 2, 3, 4, 5 };
    int n = a.Length;
    int []queries = { 0, 3, 5, 7 };
    int q = queries.Length;
    find_distinct(a, n, q, queries);
}
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to perform queries to find
// number of distinct elements from
// a given index till last index in an array
function find_distinct(a, n, q, queries)
{
    let MAX =100001;
    let check = new Array(MAX).fill(0);
    let idx = new Array(MAX).fill(0);
    let cnt = 1;

    let i=n-1;

    while (i>=0) {
     // Check if current element
        // already visited or not
        if (check[a[i]] == 0)
        {

            // If not visited store current counter
            // and increment it and mark check as 1
            idx[i] = cnt;
            check[a[i]] = 1;
            cnt++;
        }
        else
        {

            // Otherwise if visited simply
            // store current counter
            idx[i] = cnt - 1;
        }
    i--;
    }

    // Perform queries
    for (let i = 0; i < q; i++)
    {
            let m = queries[i];
            document.write(idx[m] + " ");
    }

}

// Driver code

let a = [1, 2, 3, 1, 2, 3, 4, 5 ];
let n = a.length;
let queries = [0, 3, 5, 7];
let q = queries.length;
find_distinct(a, n, q, queries);

</script>
```

**Output:** 

```
5 5 3 1
```

**时间复杂度:**O(MAX+N)
T3】辅助空间: O(MAX)