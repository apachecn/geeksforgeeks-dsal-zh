# 使用维护对象算法查询给定范围内偶数和元素的计数

> 原文:[https://www . geeksforgeeks . org/query-for-count-of-偶数位数-sum-elements-in-给定范围-use-mos-algorithm/](https://www.geeksforgeeks.org/queries-for-count-of-even-digit-sum-elements-in-given-range-using-mos-algorithm/)

给定一个由 **N** 元素组成的数组 **arr[]** ，任务是回答 Q 个查询，每个查询有两个整数 **L** 和 **R** 。对于每个查询，任务是在数字和为偶数的子阵列**arr【L…R】**中找到元素的数量。

**示例:**

> **输入:** arr[] = {7，3，19，13，5，4}
> 查询= { {1，5}，{0，1} }
> **输出:** 3
> **解释:**
> 查询 1:元素 19，13 和 4 在子数组中有偶数的和:{3，9，13，5，4}。
> 查询 2:子数组中没有偶数和的元素:{7，3}
> 
> **输入:** arr[] = {0，1，2，3，4，5，6，7}
> 查询= { 3，5 }
> T4】输出: 1

我们已经讨论过这种方法:[使用段树](https://www.geeksforgeeks.org/queries-for-the-count-of-even-digit-sum-elements-in-the-given-range-using-segment-tree/)查询给定范围内偶数和元素的计数

**方法:(使用** [**MO 的算法**](https://www.geeksforgeeks.org/mos-algorithm-query-square-root-decomposition-set-1-introduction/) **)**
想法是对所有查询进行预处理，以便一个查询的结果可以用于下一个查询。

1.  对所有查询进行排序，将 L 值从 **0 到√n–1**的查询放在一起，然后是从 **√n 到 2×√n–1**的查询，依此类推。一个块中的所有查询都按照 R 值的递增顺序进行排序。
2.  逐个处理所有查询，增加偶数和元素的数量，并将结果存储在结构中。
    *   让 **count_even** 存储上一次查询中偶数个数求和元素的个数。
    *   移除先前查询的额外元素，并为当前查询添加新元素。例如，如果以前的查询是[0，8]，而当前的查询是[3，9]，那么删除元素 arr[0]，arr[1]和 arr[2]并添加 arr[9]。
3.  为了显示结果，请按照提供的顺序对查询进行排序。

> 辅助功能:
> **添加元素()**
> 
> *   如果当前元素有偶数位数和，则增加**计数 _ 偶数**的计数。
> 
> **去除元素()**
> 
> *   如果当前元素具有偶数位数和，则减少**计数 _ 偶数**的计数。

下面的代码是上述方法的实现:

## C++

```
// C++ program to count of even
// digit sum elements in the given
// range using MO's algorithm

#include <bits/stdc++.h>
using namespace std;

#define MAX 100000

// Variable to represent block size.
// This is made global so compare()
// of sort can use it.
int block;

// Structure to represent a query range
struct Query {

    // Starting index
    int L;

    // Ending index
    int R;

    // Index of query
    int index;

    // Count of even
    // even digit sum
    int even;
};

// To store the count of
// even digit sum
int count_even;

// Function used to sort all queries so that
// all queries of the same block are arranged
// together and within a block, queries are
// sorted in increasing order of R values.
bool compare(Query x, Query y)
{
    // Different blocks, sort by block.
    if (x.L / block != y.L / block)
        return x.L / block < y.L / block;

    // Same block, sort by R value
    return x.R < y.R;
}

// Function used to sort all queries
// in order of their index value so that
// results of queries can be printed
// in same order as of input
bool compare1(Query x, Query y)
{
    return x.index < y.index;
}

// Function to find the digit sum
// for a number
int digitSum(int num)
{
    int sum = 0;
    while (num) {
        sum += (num % 10);
        num /= 10;
    }

    return sum;
}

// Function to Add elements
// of current range
void add(int currL, int a[])
{
    // If digit sum of a[currL]
    // is even then increment
    if (digitSum(a[currL]) % 2 == 0)
        count_even++;
}

// Function to remove elements
// of previous range
void remove(int currR, int a[])
{

    // If digit sum of a[currL]
    // is even then decrement
    if (digitSum(a[currR]) % 2 == 0)
        count_even--;
}

// Function to generate
// the result of queries
void queryResults(int a[], int n,
                  Query q[], int m)
{

    // Initialize number of
    // even digit sum to 0
    count_even = 0;

    // Find block size
    block = (int)sqrt(n);

    // Sort all queries so that queries of
    // same blocks are arranged together.
    sort(q, q + m, compare);

    // Initialize current L, current R and
    // current result
    int currL = 0, currR = 0;

    for (int i = 0; i < m; i++) {
        // L and R values of current range
        int L = q[i].L, R = q[i].R;

        // Add Elements of current range
        while (currR <= R) {
            add(currR, a);
            currR++;
        }
        while (currL > L) {
            add(currL - 1, a);
            currL--;
        }

        // Remove element of previous range
        while (currR > R + 1)

        {
            remove(currR - 1, a);
            currR--;
        }
        while (currL < L) {
            remove(currL, a);
            currL++;
        }

        q[i].even = count_even;
    }
}
// Function to display the results of
// queries in their initial order
void printResults(Query q[], int m)
{
    sort(q, q + m, compare1);
    for (int i = 0; i < m; i++) {
        cout << q[i].even << endl;
    }
}

// Driver Code
int main()
{

    int arr[] = { 5, 2, 3, 1, 4, 8, 10, 12 };
    int n = sizeof(arr) / sizeof(arr[0]);

    Query q[] = { { 1, 3, 0, 0 },
                  { 0, 4, 1, 0 },
                  { 4, 7, 2, 0 } };

    int m = sizeof(q) / sizeof(q[0]);

    queryResults(arr, n, q, m);

    printResults(q, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count of even
// digit sum elements in the given
// range using MO's algorithm
import java.util.Arrays;
import java.util.Collections;
import java.util.Comparator;

class GFG{

static int MAX = 100000;

// Variable to represent block size.
// This is made global so compare()
// of sort can use it.
static int block;

// Structure to represent a query range
static class Query
{

    // Starting index
    int L;

    // Ending index
    int R;

    // Index of query
    int index;

    // Count of even
    // even digit sum
    int even;

    public Query(int l, int r,
                 int index, int even)
    {
        this.L = l;
        this.R = r;
        this.index = index;
        this.even = even;
    }
};

// To store the count of
// even digit sum
static int count_even;

// Function to find the digit sum
// for a number
static int digitSum(int num)
{
    int sum = 0;
    while (num > 0)
    {
        sum += (num % 10);
        num /= 10;
    }
    return sum;
}

// Function to Add elements
// of current range
static void add(int currL, int a[])
{

    // If digit sum of a[currL]
    // is even then increment
    if (digitSum(a[currL]) % 2 == 0)
        count_even++;
}

// Function to remove elements
// of previous range
static void remove(int currR, int a[])
{

    // If digit sum of a[currL]
    // is even then decrement
    if (digitSum(a[currR]) % 2 == 0)
        count_even--;
}

// Function to generate
// the result of queries
static void queryResults(int a[], int n,
                       Query q[], int m)
{

    // Initialize number of
    // even digit sum to 0
    count_even = 0;

    // Find block size
    block = (int) Math.sqrt(n);

    // Sort all queries so that queries of
    // same blocks are arranged together.
    Collections.sort(Arrays.asList(q),
                     new Comparator<Query>()
    {

        // Function used to sort all queries so that
        // all queries of the same block are arranged
        // together and within a block, queries are
        // sorted in increasing order of R values.
        public int compare(Query x, Query y)
        {

            // Different blocks, sort by block.
            if (x.L / block != y.L / block)
                return x.L / block - y.L / block;

            // Same block, sort by R value
            return x.R - y.R;
        }
    });

    // Initialize current L, current R and
    // current result
    int currL = 0, currR = 0;

    for(int i = 0; i < m; i++)
    {

        // L and R values of current range
        int L = q[i].L, R = q[i].R;

        // Add Elements of current range
        while (currR <= R)
        {
            add(currR, a);
            currR++;
        }
        while (currL > L)
        {
            add(currL - 1, a);
            currL--;
        }

        // Remove element of previous range
        while (currR > R + 1)
        {
            remove(currR - 1, a);
            currR--;
        }
        while (currL < L)
        {
            remove(currL, a);
            currL++;
        }
        q[i].even = count_even;
    }
}

// Function to display the results of
// queries in their initial order
static void printResults(Query q[], int m)
{
    Collections.sort(Arrays.asList(q),
             new Comparator<Query>()
    {

        // Function used to sort all queries
        // in order of their index value so that
        // results of queries can be printed
        // in same order as of input
        public int compare(Query x, Query y)
        {
            return x.index - y.index;
        }
    });
    for(int i = 0; i < m; i++)
    {
        System.out.println(q[i].even);
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, 2, 3, 1, 4, 8, 10, 12 };
    int n = arr.length;

    Query q[] = { new Query(1, 3, 0, 0),
                  new Query(0, 4, 1, 0),
                  new Query(4, 7, 2, 0) };

    int m = q.length;

    queryResults(arr, n, q, m);

    printResults(q, m);
}
}

// This code is contributed by sanjeev2552
```

**Output:** 

```
1
2
2

```

***时间复杂度:**O(Q x√N)*T4】