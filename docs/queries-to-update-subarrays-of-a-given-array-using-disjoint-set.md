# 使用不相交集合更新给定阵列的子阵列的查询

> 原文:[https://www . geesforgeks . org/query-to-update-给定数组的子数组-使用不相交集/](https://www.geeksforgeeks.org/queries-to-update-subarrays-of-a-given-array-using-disjoint-set/)

给定一个由 **N** 整数组成的数组 **arr[]** ，该数组最初只由 **0** 组成，并以 **{L，R，C}** 的形式查询 **Q[][]** ，每个查询的任务是用值 **C** 更新子数组**【L，R】**。打印执行所有查询后生成的最终数组。

**示例:**

> **输入:** N = 5，Q = {{1，4，1}，{3，5，2}，{2，4，3}}
> **输出:** 1 3 3 3 2
> **解释:**
> 最初，数组是{0，0，0，0，0}
> 查询 1 将数组修改为{1，1，1，0}
> 查询 2 将数组修改为{1，1，2，2 }【2】
> 
> **输入:** N = 3，Q = {{1，2，1}，{2，3，2}}
> **输出:** 1 2 2
> **解释:**
> 最初，数组为{0，0，0}
> 查询 1 将数组修改为{1，1，0}
> 查询 2 将数组修改为{1，2，2}

**方法:**思路是用[不相交集并集](https://cp-algorithms.com/data_structures/disjoint_set_union.html)来解决问题。按照以下步骤解决问题:

*   最初，所有数组元素将被视为独立的集合和自身的父元素，并将存储值为 0 的下一个数组元素。
*   首先，存储查询并按照从后到前的相反顺序处理查询，因为分配给每个集合的值都是最终值。
*   在处理完第一个查询后，具有已更改值的元素将指向下一个元素。这样在执行查询时，我们只需要给子数组**【l，r】**中未更新的集合赋值。所有其他单元格已经包含它们的最终值。
*   找到最左边的未更新的集合，并更新它，然后用指针向右移动到下一个未更新的集合。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Maximum possible size of array
#define MAX_NODES 100005

// Stores the parent of each element
int parent[MAX_NODES];

// Stores the final array values
int final_val[MAX_NODES];

// Structure to store queries
struct query {
    int l, r, c;
};

// Function to initialize the
// parent of each vertex
void make_set(int v)
{
    // Initially parent
    // of each node points
    // to itself
    parent[v] = v;
}

// Function to find the representative
// of the set which contain element v
int find_set(int v)
{
    if (v == parent[v])
        return v;

    // Path compression
    return parent[v] = find_set(parent[v]);
}

// Function to assign a
// parent to each element
void Initialize(int n)
{

    for (int i = 0; i <= n; i++)

        make_set(i + 1);
}

// Function to process the queries
void Process(query Q[], int q)
{

    for (int i = q - 1; i >= 0; i--) {

        int l = Q[i].l, r = Q[i].r, c = Q[i].c;

        for (int v = find_set(l); v <= r;
             v = find_set(v)) {

            final_val[v] = c;
            parent[v] = v + 1;
        }
    }
}

// Function to print the final array
void PrintAns(int n)
{

    for (int i = 1; i <= n; i++) {

        cout << final_val[i] << " ";
    }

    cout << endl;
}

// Driver Code
int main()
{
    int n = 5;

    // Set all the elements as the
    // parent of itself using make_set
    Initialize(n);

    int q = 3;
    query Q[q];

    // Store the queries
    Q[0].l = 1, Q[0].r = 4, Q[0].c = 1;
    Q[1].l = 3, Q[1].r = 5, Q[1].c = 2;
    Q[2].l = 2, Q[2].r = 4, Q[2].c = 3;

    // Process the queries
    Process(Q, q);

    // Print the required array
    PrintAns(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Maximum possible size of array
static final int MAX_NODES = 100005;

// Stores the parent of each element
static int []parent = new int[MAX_NODES];

// Stores the final array values
static int []final_val = new int[MAX_NODES];

// Structure to store queries
static class query
{
    int l, r, c;
};

// Function to initialize the
// parent of each vertex
static void make_set(int v)
{

    // Initially parent
    // of each node points
    // to itself
    parent[v] = v;
}

// Function to find the representative
// of the set which contain element v
static int find_set(int v)
{
    if (v == parent[v])
        return v;

    // Path compression
    return parent[v] = find_set(parent[v]);
}

// Function to assign a
// parent to each element
static void Initialize(int n)
{
    for(int i = 0; i <= n; i++)
        make_set(i + 1);
}

// Function to process the queries
static void Process(query Q[], int q)
{
    for(int i = q - 1; i >= 0; i--)
    {
        int l = Q[i].l, r = Q[i].r, c = Q[i].c;

        for(int v = find_set(l); v <= r;
                v = find_set(v))
        {
            final_val[v] = c;
            parent[v] = v + 1;
        }
    }
}

// Function to print the final array
static void PrintAns(int n)
{
    for(int i = 1; i <= n; i++)
    {
        System.out.print(final_val[i] + " ");
    }
    System.out.println();
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;

    // Set all the elements as the
    // parent of itself using make_set
    Initialize(n);

    int q = 3;

    query []Q = new query[q];
    for(int i = 0; i < Q.length; i++)
        Q[i] = new query();

    // Store the queries
    Q[0].l = 1; Q[0].r = 4; Q[0].c = 1;
    Q[1].l = 3; Q[1].r = 5; Q[1].c = 2;
    Q[2].l = 2; Q[2].r = 4; Q[2].c = 3;

    // Process the queries
    Process(Q, q);

    // Print the required array
    PrintAns(n);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
MAX_NODES = 100005

# Stores the parent of each element
parent = [0] * MAX_NODES

# Stores the final array values
final_val = [0] * MAX_NODES

# Structure to store queries

# Function to initialize the
# parent of each vertex
def make_set(v):

    # Initially parent
    # of each node points
    # to itself
    parent[v] = v

# Function to find the representative
# of the set which contain element v
def find_set(v):

    if (v == parent[v]):
        return v

    # Path compression
    parent[v] = find_set(parent[v])
    return parent[v]

# Function to assign a
# parent to each element
def Initialize(n):

    for i in range(n + 1):
        make_set(i + 1)

# Function to process the queries
def Process(Q, q):

    for i in range(q - 1, -1, -1):
        l = Q[i][0]
        r = Q[i][1]
        c = Q[i][2]

        v = find_set(l)

        while v <= r:
            final_val[v] = c
            parent[v] = v + 1
            v = find_set(v)

# Function to print the final array
def PrintAns(n):

    for i in range(1, n + 1):
        print(final_val[i], end = " ")

# Driver Code
if __name__ == '__main__':

    n = 5

    # Set all the elements as the
    # parent of itself using make_set
    Initialize(n)

    q = 3
    Q = [[0 for i in range(3)] 
            for i in range(q)]

    # Store the queries
    Q[0][0] = 1
    Q[0][1] = 4
    Q[0][2] = 1
    Q[1][0] = 3
    Q[1][1] = 5
    Q[1][2] = 2
    Q[2][0] = 2
    Q[2][1] = 4
    Q[2][2] = 3

    # Process the queries
    Process(Q, q)

    # Print the required array
    PrintAns(n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Maximum possible size of array
static readonly int MAX_NODES = 100005;

// Stores the parent of each element
static int []parent = new int[MAX_NODES];

// Stores the readonly array values
static int []final_val = new int[MAX_NODES];

// Structure to store queries
class query
{
    public int l, r, c;
};

// Function to initialize the
// parent of each vertex
static void make_set(int v)
{

    // Initially parent
    // of each node points
    // to itself
    parent[v] = v;
}

// Function to find the representative
// of the set which contain element v
static int find_set(int v)
{
    if (v == parent[v])
        return v;

    // Path compression
    return parent[v] = find_set(parent[v]);
}

// Function to assign a
// parent to each element
static void Initialize(int n)
{
    for(int i = 0; i <= n; i++)
        make_set(i + 1);
}

// Function to process the queries
static void Process(query []Q, int q)
{
    for(int i = q - 1; i >= 0; i--)
    {
        int l = Q[i].l, r = Q[i].r, c = Q[i].c;

        for(int v = find_set(l); v <= r;
                v = find_set(v))
        {
            final_val[v] = c;
            parent[v] = v + 1;
        }
    }
}

// Function to print the readonly array
static void PrintAns(int n)
{
    for(int i = 1; i <= n; i++)
    {
        Console.Write(final_val[i] + " ");
    }
    Console.WriteLine();
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;

    // Set all the elements as the
    // parent of itself using make_set
    Initialize(n);

    int q = 3;

    query []Q = new query[q];
    for(int i = 0; i < Q.Length; i++)
        Q[i] = new query();

    // Store the queries
    Q[0].l = 1; Q[0].r = 4; Q[0].c = 1;
    Q[1].l = 3; Q[1].r = 5; Q[1].c = 2;
    Q[2].l = 2; Q[2].r = 4; Q[2].c = 3;

    // Process the queries
    Process(Q, q);

    // Print the required array
    PrintAns(n);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Maximum possible size of array
let MAX_NODES = 100005;

// Stores the parent of each element
let parent = new Array(MAX_NODES);

// Stores the final array values
let final_val = new Array(MAX_NODES);

// Structure to store queries
class query
{
    constructor()
    {
        let l, r, c;
    }
}

// Function to initialize the
// parent of each vertex
function make_set(v)
{
    // Initially parent
    // of each node points
    // to itself
    parent[v] = v;
}

// Function to find the representative
// of the set which contain element v
function find_set(v)
{
    if (v == parent[v])
        return v;

    // Path compression
    return parent[v] = find_set(parent[v]);
}

// Function to assign a
// parent to each element
function Initialize(n)
{
    for(let i = 0; i <= n; i++)
        make_set(i + 1);
}

// Function to process the queries
function Process(Q,q)
{
    for(let i = q - 1; i >= 0; i--)
    {
        let l = Q[i].l, r = Q[i].r, c = Q[i].c;

        for(let v = find_set(l); v <= r;
                v = find_set(v))
        {
            final_val[v] = c;
            parent[v] = v + 1;
        }
    }
}

// Function to print the final array
function PrintAns(n)
{
    for(let i = 1; i <= n; i++)
    {
        document.write(final_val[i] + " ");
    }
    document.write("<br>");
}

// Driver Code
let n = 5;

// Set all the elements as the
// parent of itself using make_set
Initialize(n);

let q = 3;

let Q = new Array(q);
for(let i = 0; i < Q.length; i++)
    Q[i] = new query();

// Store the queries
Q[0].l = 1; Q[0].r = 4; Q[0].c = 1;
Q[1].l = 3; Q[1].r = 5; Q[1].c = 2;
Q[2].l = 2; Q[2].r = 4; Q[2].c = 3;

// Process the queries
Process(Q, q);

// Print the required array
PrintAns(n);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
1 3 3 3 2
```

***时间复杂度:** O(log N)*
***辅助空间:** O(MAX_NODES)*