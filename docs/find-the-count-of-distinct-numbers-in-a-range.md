# 找出一个范围内不同数字的计数

> 原文:[https://www . geeksforgeeks . org/find-范围内不同数字的计数/](https://www.geeksforgeeks.org/find-the-count-of-distinct-numbers-in-a-range/)

给定一个大小为 N 的数组，其中只包含从 0 到 63 的数字，然后你会被问及关于它的问题。
查询如下:

*   1 X Y，即将索引 X 处的元素更改为 Y
*   2 L R，即打印介于左和右之间的不同元素的计数

**例:**

```
Input:
N = 7
ar = {1, 2, 1, 3, 1, 2, 1}
Q = 5
{ {2, 1, 4},
  {1, 4, 2},
  {1, 5, 2},
  {2, 4, 6},
  {2, 1, 7} }
Output:
3
1
2

Input:
N = 15
ar = {4, 6, 3, 2, 2, 3, 6, 5, 5, 5, 4, 2, 1, 5, 1}
Q = 5
{ {1, 6, 5},
  {1, 4, 2},
  {2, 6, 14},
  {2, 6, 8},
  {2, 1, 6} };

Output:
5
2
5
```

**先决条件:** [段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)和[位操作](https://www.geeksforgeeks.org/bits-manipulation-important-tactics/)
**方法:**

*   问题中形成的位掩码将表示第 I 个数字的存在与否，我们将通过检查我们的位掩码的第 I 个位来发现，如果第 I 个位是 on，这意味着第 I 个元素存在，否则不存在。
*   构建一个经典的段树，它的每个节点将包含一个位掩码，用于解码由特定节点定义的特定段中不同元素的数量。
*   以自下而上的方式构建段树，因此可以通过对该节点的左右子节点的位掩码执行按位“或”运算来轻松计算段树的当前节点的位掩码。叶节点将被单独处理。更新也将以同样的方式进行。

以下是上述方法的实现:

## C++

```
// C++ Program to find the distinct
// elements in a range
#include <bits/stdc++.h>
using namespace std;

// Function to perform queries in a range
long long query(int start, int end, int left, int right,
                int node, long long seg[])
{
    // No overlap
    if (end < left || start > right) {
        return 0;
    }

    // Totally Overlap
    else if (start >= left && end <= right) {
        return seg[node];
    }

    // Partial Overlap
    else {
        int mid = (start + end) / 2;

        // Finding the Answer
        // for the left Child
        long long leftChild = query(start, mid, left,
                                    right, 2 * node, seg);

        // Finding the Answer
        // for the right Child
        long long rightChild = query(mid + 1, end, left,
                                     right, 2 * node + 1, seg);

        // Combining the BitMasks
        return (leftChild | rightChild);
    }
}

// Function to perform update operation
// in the Segment seg
void update(int left, int right, int index, int Value,
            int node, int ar[], long long seg[])
{
    if (left == right) {
        ar[index] = Value;

        // Forming the BitMask
        seg[node] = (1LL << Value);
        return;
    }

    int mid = (left + right) / 2;
    if (index > mid) {

        // Updating the left Child
        update(mid + 1, right, index, Value, 2 * node + 1, ar, seg);
    }
    else {

        // Updating the right Child
        update(left, mid, index, Value, 2 * node, ar, seg);
    }

    // Updating the BitMask
    seg[node] = (seg[2 * node] | seg[2 * node + 1]);
}

// Building the Segment Tree
void build(int left, int right, int node, int ar[],
           long long seg[])
{
    if (left == right) {

        // Building the Initial BitMask
        seg[node] = (1LL << ar[left]);

        return;
    }

    int mid = (left + right) / 2;

    // Building the left seg tree
    build(left, mid, 2 * node, ar, seg);

    // Building the right seg tree
    build(mid + 1, right, 2 * node + 1, ar, seg);

    // Forming the BitMask
    seg[node] = (seg[2 * node] | seg[2 * node + 1]);
}

// Utility Function to answer the queries
void getDistinctCount(vector<vector<int> >& queries,
                      int ar[], long long seg[], int n)
{

    for (int i = 0; i < queries.size(); i++) {

        int op = queries[i][0];

        if (op == 2) {

            int l = queries[i][1], r = queries[i][2];

            long long tempMask = query(0, n - 1, l - 1,
                                       r - 1, 1, seg);

            int countOfBits = 0;

            // Counting the set bits which denote the
            // distinct elements
            for (int i = 63; i >= 0; i--) {

                if (tempMask & (1LL << i)) {

                    countOfBits++;
                }
            }

            cout << countOfBits << '\n';
        }
        else {

            int index = queries[i][1];
            int val = queries[i][2];

            // Updating the value
            update(0, n - 1, index - 1, val, 1, ar, seg);
        }
    }
}

// Driver Code
int main()
{
    int n = 7;
    int ar[] = { 1, 2, 1, 3, 1, 2, 1 };

    long long seg[4 * n] = { 0 };
    build(0, n - 1, 1, ar, seg);

    int q = 5;
    vector<vector<int> > queries = {
        { 2, 1, 4 },
        { 1, 4, 2 },
        { 1, 5, 2 },
        { 2, 4, 6 },
        { 2, 1, 7 }
    };

    getDistinctCount(queries, ar, seg, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the distinct
// elements in a range
import java.util.*;

class GFG{

// Function to perform queries in a range
static long query(int start, int end, int left, int right,
                int node, long seg[])
{
    // No overlap
    if (end < left || start > right) {
        return 0;
    }

    // Totally Overlap
    else if (start >= left && end <= right) {
        return seg[node];
    }

    // Partial Overlap
    else {
        int mid = (start + end) / 2;

        // Finding the Answer
        // for the left Child
        long leftChild = query(start, mid, left,
                                    right, 2 * node, seg);

        // Finding the Answer
        // for the right Child
        long rightChild = query(mid + 1, end, left,
                                     right, 2 * node + 1, seg);

        // Combining the BitMasks
        return (leftChild | rightChild);
    }
}

// Function to perform update operation
// in the Segment seg
static void update(int left, int right, int index, int Value,
            int node, int ar[], long seg[])
{
    if (left == right) {
        ar[index] = Value;

        // Forming the BitMask
        seg[node] = (1L << Value);
        return;
    }

    int mid = (left + right) / 2;
    if (index > mid) {

        // Updating the left Child
        update(mid + 1, right, index, Value, 2 * node + 1, ar, seg);
    }
    else {

        // Updating the right Child
        update(left, mid, index, Value, 2 * node, ar, seg);
    }

    // Updating the BitMask
    seg[node] = (seg[2 * node] | seg[2 * node + 1]);
}

// Building the Segment Tree
static void build(int left, int right, int node, int ar[],
           long seg[])
{
    if (left == right) {

        // Building the Initial BitMask
        seg[node] = (1L << ar[left]);

        return;
    }

    int mid = (left + right) / 2;

    // Building the left seg tree
    build(left, mid, 2 * node, ar, seg);

    // Building the right seg tree
    build(mid + 1, right, 2 * node + 1, ar, seg);

    // Forming the BitMask
    seg[node] = (seg[2 * node] | seg[2 * node + 1]);
}

// Utility Function to answer the queries
static void getDistinctCount(int  [][]queries,
                      int ar[], long seg[], int n)
{

    for (int i = 0; i < queries.length; i++) {

        int op = queries[i][0];

        if (op == 2) {

            int l = queries[i][1], r = queries[i][2];

            long tempMask = query(0, n - 1, l - 1,
                                       r - 1, 1, seg);

            int countOfBits = 0;

            // Counting the set bits which denote the
            // distinct elements
            for (int s = 63; s >= 0; s--) {

                if ((tempMask & (1L << s))>0) {

                    countOfBits++;
                }
            }

            System.out.println(countOfBits);
        }
        else {

            int index = queries[i][1];
            int val = queries[i][2];

            // Updating the value
            update(0, n - 1, index - 1, val, 1, ar, seg);
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int n = 7;
    int ar[] = { 1, 2, 1, 3, 1, 2, 1 };

    long seg[] = new long[4 * n];
    build(0, n - 1, 1, ar, seg);

    int [][]queries = {
        { 2, 1, 4 },
        { 1, 4, 2 },
        { 1, 5, 2 },
        { 2, 4, 6 },
        { 2, 1, 7 }
    };

    getDistinctCount(queries, ar, seg, n);

}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 Program to find the distinct
# elements in a range

# Function to perform queries in a range
def query(start, end, left,
          right, node, seg):

    # No overlap
    if (end < left or start > right):
        return 0

    # Totally Overlap
    elif (start >= left and
            end <= right):
        return seg[node]

    # Partial Overlap
    else:
        mid = (start + end) // 2

        # Finding the Answer
        # for the left Child
        leftChild = query(start, mid, left,
                          right, 2 * node, seg)

        # Finding the Answer
        # for the right Child
        rightChild = query(mid + 1, end, left,
                           right, 2 * node + 1, seg)

        # Combining the BitMasks
        return (leftChild | rightChild)

# Function to perform update operation
# in the Segment seg
def update(left, right, index,
           Value, node, ar, seg):
    if (left == right):
        ar[index] = Value

        # Forming the BitMask
        seg[node] = (1 << Value)
        return

    mid = (left + right) // 2
    if (index > mid):

        # Updating the left Child
        update(mid + 1, right, index,
               Value, 2 * node + 1, ar, seg)
    else:

        # Updating the right Child
        update(left, mid, index,
               Value, 2 * node, ar, seg)

    # Updating the BitMask
    seg[node] = (seg[2 * node] |
                 seg[2 * node + 1])

# Building the Segment Tree
def build(left, right, node, ar, eg):

    if (left == right):

        # Building the Initial BitMask
        seg[node] = (1 << ar[left])

        return

    mid = (left + right) // 2

    # Building the left seg tree
    build(left, mid, 2 * node, ar, seg)

    # Building the right seg tree
    build(mid + 1, right,
                2 * node + 1, ar, seg)

    # Forming the BitMask
    seg[node] = (seg[2 * node] |
                 seg[2 * node + 1])

# Utility Function to answer the queries
def getDistinctCount(queries, ar, seg, n):

    for i in range(len(queries)):

        op = queries[i][0]

        if (op == 2):

            l = queries[i][1]
            r = queries[i][2]

            tempMask = query(0, n - 1, l - 1,
                             r - 1, 1, seg)

            countOfBits = 0

            # Counting the set bits which denote
            # the distinct elements
            for i in range(63, -1, -1):

                if (tempMask & (1 << i)):

                    countOfBits += 1

            print(countOfBits)
        else:

            index = queries[i][1]
            val = queries[i][2]

            # Updating the value
            update(0, n - 1, index - 1,
                       val, 1, ar, seg)

# Driver Code
if __name__ == '__main__':
    n = 7
    ar = [1, 2, 1, 3, 1, 2, 1]

    seg = [0] * 4 * n
    build(0, n - 1, 1, ar, seg)

    q = 5
    queries = [[ 2, 1, 4 ],
               [ 1, 4, 2 ],
               [ 1, 5, 2 ],
               [ 2, 4, 6 ],
               [ 2, 1, 7 ]]

    getDistinctCount(queries, ar, seg, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# Program to find the distinct
// elements in a range
using System;

class GFG{

// Function to perform queries in a range
static long query(int start, int end, int left, int right,
                int node, long []seg)
{
    // No overlap
    if (end < left || start > right) {
        return 0;
    }

    // Totally Overlap
    else if (start >= left && end <= right) {
        return seg[node];
    }

    // Partial Overlap
    else {
        int mid = (start + end) / 2;

        // Finding the Answer
        // for the left Child
        long leftChild = query(start, mid, left,
                                    right, 2 * node, seg);

        // Finding the Answer
        // for the right Child
        long rightChild = query(mid + 1, end, left,
                                     right, 2 * node + 1, seg);

        // Combining the BitMasks
        return (leftChild | rightChild);
    }
}

// Function to perform update operation
// in the Segment seg
static void update(int left, int right, int index, int Value,
            int node, int []ar, long []seg)
{
    if (left == right) {
        ar[index] = Value;

        // Forming the BitMask
        seg[node] = (1L << Value);
        return;
    }

    int mid = (left + right) / 2;
    if (index > mid) {

        // Updating the left Child
        update(mid + 1, right, index, Value, 2 * node + 1, ar, seg);
    }
    else {

        // Updating the right Child
        update(left, mid, index, Value, 2 * node, ar, seg);
    }

    // Updating the BitMask
    seg[node] = (seg[2 * node] | seg[2 * node + 1]);
}

// Building the Segment Tree
static void build(int left, int right, int node, int []ar,
           long []seg)
{
    if (left == right) {

        // Building the Initial BitMask
        seg[node] = (1L << ar[left]);

        return;
    }

    int mid = (left + right) / 2;

    // Building the left seg tree
    build(left, mid, 2 * node, ar, seg);

    // Building the right seg tree
    build(mid + 1, right, 2 * node + 1, ar, seg);

    // Forming the BitMask
    seg[node] = (seg[2 * node] | seg[2 * node + 1]);
}

// Utility Function to answer the queries
static void getDistinctCount(int  [,]queries,
                      int []ar, long []seg, int n)
{

    for (int i = 0; i < queries.GetLength(0); i++) {

        int op = queries[i,0];

        if (op == 2) {

            int l = queries[i,1], r = queries[i,2];

            long tempMask = query(0, n - 1, l - 1,
                                       r - 1, 1, seg);

            int countOfBits = 0;

            // Counting the set bits which denote the
            // distinct elements
            for (int s = 63; s >= 0; s--) {

                if ((tempMask & (1L << s))>0) {

                    countOfBits++;
                }
            }

            Console.WriteLine(countOfBits);
        }
        else {

            int index = queries[i,1];
            int val = queries[i,2];

            // Updating the value
            update(0, n - 1, index - 1, val, 1, ar, seg);
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    int n = 7;
    int []ar = { 1, 2, 1, 3, 1, 2, 1 };

    long []seg = new long[4 * n];
    build(0, n - 1, 1, ar, seg);

    int [,]queries = {
        { 2, 1, 4 },
        { 1, 4, 2 },
        { 1, 5, 2 },
        { 2, 4, 6 },
        { 2, 1, 7 }
    };

    getDistinctCount(queries, ar, seg, n);

}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
3
1
2
```

**时间复杂度:** O(N + Q*Log(N))