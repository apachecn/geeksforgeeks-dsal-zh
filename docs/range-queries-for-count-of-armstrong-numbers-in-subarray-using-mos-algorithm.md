# 使用 MO 算法对子阵列中阿姆斯特朗数计数的范围查询

> 原文:[https://www . geeksforgeeks . org/range-query-for-count-of-Armstrong-in-subarray-numbers-use-mos-algorithm/](https://www.geeksforgeeks.org/range-queries-for-count-of-armstrong-numbers-in-subarray-using-mos-algorithm/)

给定一个由表示范围的 L 和 R 表示的由 **N** 元素和 **Q** 查询组成的数组 **arr[]** ，任务是打印子数组**【L，R】**中的[阿姆斯特朗数](https://www.geeksforgeeks.org/program-for-armstrong-numbers/)的个数。

**示例:**

> **输入:** arr[] = {18，153，8，9，14，5}
> 查询 1:查询(L=0，R=5)
> 查询 2:查询(L=3，R = 5)
> T5】输出:4
> 2
> T9】说明:
> 18 = > 1*1 + 8*8！= 18
> 153 =>1 * 1 * 1+5 * 5 * 5+3 * 3 * 3 = 153
> 8 =>8 = 8
> 9 =>9 = 9
> 14 =>1 * 1+4 * 4！= 14
> 查询 1:子阵列[0…5]有 **4** 个阿姆斯特朗编号，即。{153，8，9，5}
> 查询 2:子阵列[3…5]具有 **2** 阿姆斯特朗编号，即。{9, 5}

**方法:**
想法是使用 [MO 的算法](https://www.geeksforgeeks.org/mos-algorithm-query-square-root-decomposition-set-1-introduction/)对所有查询进行预处理，以便一个查询的结果可以用于下一个查询。

1.  对所有查询进行排序，将从 **0 到√n–1**的 **L** 值的查询放在一起，然后是从 **√n 到 2×√n–1**的查询，依此类推。一个块内的所有查询按照 **R** 值的递增顺序排序。
2.  逐个处理所有查询，增加阿姆斯特朗数的数量，并将结果存储在结构中。
    *   让' **count_Armstrong** '存储上一个查询中的 Armstrong 数的计数。
    *   移除先前查询的额外元素，并为当前查询添加新元素。例如，如果以前的查询是[0，8]，而当前的查询是[3，9]，那么删除元素 arr[0]，arr[1]和 arr[2]并添加 arr[9]。
3.  为了显示结果，请按照提供的顺序对查询进行排序。

**添加元素**

*   如果当前元素是阿姆斯特朗数，则递增**计数 _ 阿姆斯特朗**。

**移除元素**

*   如果当前元素是阿姆斯特朗数，则递减**计数 _ 阿姆斯特朗**。

下面是上述方法的实现:

## C++

```
// C++ implementation to count the
// number of Armstrong numbers
// in subarray using MO’s algorithm

#include <bits/stdc++.h>
using namespace std;

// Variable to represent block size.
// This is made global so compare()
// of sort can use it.
int block;

// Structure to represent
// a query range
struct Query {
    int L, R, index;

    // Count of Armstrong
    // numbers
    int armstrong;
};

// To store the count of
// Armstrong numbers
int count_Armstrong;

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

// Function used to sort all
// queries in order of their
// index value so that results
// of queries can be printed
// in same order as of input
bool compare1(Query x, Query y)
{
    return x.index < y.index;
}

// Function that return true
// if num is armstrong
// else return false
bool isArmstrong(int x)
{
    int n = to_string(x).size();
    int sum1 = 0;
    int temp = x;
    while (temp > 0) {
        int digit = temp % 10;
        sum1 += pow(digit, n);
        temp /= 10;
    }
    if (sum1 == x)
        return true;
    return false;
}

// Function to Add elements
// of current range
void add(int currL, int a[])
{
    // If a[currL] is a Armstrong number
    // then increment count_Armstrong
    if (isArmstrong(a[currL]))
        count_Armstrong++;
}

// Function to remove elements
// of previous range
void remove(int currR, int a[])
{
    // If a[currL] is a Armstrong number
    // then decrement count_Armstrong
    if (isArmstrong(a[currR]))
        count_Armstrong--;
}

// Function to generate the result of queries
void queryResults(int a[], int n, Query q[],
                  int m)
{

    // Initialize count_Armstrong to 0
    count_Armstrong = 0;

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

        q[i].armstrong = count_Armstrong;
    }
}

// Function to display the results of
// queries in their initial order
void printResults(Query q[], int m)
{
    sort(q, q + m, compare1);
    for (int i = 0; i < m; i++) {
        cout << q[i].armstrong << endl;
    }
}

// Driver Code
int main()
{

    int arr[] = { 18, 153, 8, 9, 14, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    Query q[] = { { 0, 5, 0, 0 },
                  { 3, 5, 1, 0 } };

    int m = sizeof(q) / sizeof(q[0]);

    queryResults(arr, n, q, m);

    printResults(q, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the
// number of Armstrong numbers
// in subarray using MO’s algorithm
import java.io.*;
import java.util.*;

// Class to represent
// a query range
class Query
{
    int L, R, index;

    // Count of Armstrong
    // numbers
    int armstrong;

    Query(int L, int R, int index,
          int armstrong)
    {
        this.L = L;
        this.R = R;
        this.index = index;
        this.armstrong = armstrong;
    }
}

class GFG{

// Variable to represent block size.
static int block;

// To store the count of
// Armstrong numbers
static int count_Armstrong;

// Function that return true
// if num is armstrong
// else return false
static boolean isArmstrong(int x)
{
    int n = String.valueOf(x).length();
    int sum1 = 0;
    int temp = x;

    while (temp > 0)
    {
        int digit = temp % 10;
        sum1 += Math.pow(digit, n);
        temp /= 10;
    }

    if (sum1 == x)
        return true;

    return false;
}

// Function to Add elements
// of current range
static void add(int currL, int a[])
{

    // If a[currL] is a Armstrong number
    // then increment count_Armstrong
    if (isArmstrong(a[currL]))
        count_Armstrong++;
}

// Function to remove elements
// of previous range
static void remove(int currR, int a[])
{

    // If a[currL] is a Armstrong number
    // then decrement count_Armstrong
    if (isArmstrong(a[currR]))
        count_Armstrong--;
}

// Function to generate the result of queries
static void queryResults(int a[], int n, Query q[],
                         int m)
{

    // Initialize count_Armstrong to 0
    count_Armstrong = 0;

    // Find block size
    block = (int)(Math.sqrt(n));

    // sort all queries so that
    // all queries of the same block are arranged
    // together and within a block, queries are
    // sorted in increasing order of R values.
    Arrays.sort(q, (Query x, Query y) ->
    {

        // Different blocks, sort by block.
        if (x.L / block != y.L / block)
            return x.L / block - y.L / block;

        // Same block, sort by R value
        return x.R - y.R;
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

        q[i].armstrong = count_Armstrong;
    }
}

// Function to display the results of
// queries in their initial order
static void printResults(Query q[], int m)
{
    Arrays.sort(q, (Query x, Query y) ->

                // sort all queries
                // in order of their
                // index value so that results
                // of queries can be printed
                // in same order as of input);
                x.index - y.index);

    for(int i = 0; i < m; i++)
    {
        System.out.println(q[i].armstrong);
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 18, 153, 8, 9, 14, 5 };
    int n = arr.length;

    Query q[] = new Query[2];
    q[0] = new Query(0, 5, 0, 0);
    q[1] = new Query(3, 5, 1, 0);

    int m = q.length;

    queryResults(arr, n, q, m);

    printResults(q, m);
}
}

// This code is contributed by jithin
```

**Output:** 

```
4
2

```

**时间复杂度:** O(Q * √N)
**相关文章:** [数组中阿姆斯特朗数的范围查询更新](https://www.geeksforgeeks.org/range-queries-for-number-of-armstrong-numbers-in-an-array-with-updates/)