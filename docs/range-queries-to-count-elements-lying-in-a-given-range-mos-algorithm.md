# 对给定范围内的元素进行计数的范围查询:维护对象的算法

> 原文:[https://www . geesforgeks . org/range-query-to-count-elements-躺在给定范围内-mos-algorithm/](https://www.geeksforgeeks.org/range-queries-to-count-elements-lying-in-a-given-range-mos-algorithm/)

给定一个由 **N** 元素和两个整数 **A** 到 **B** 组成的数组**arr【】**，任务是回答 Q 个查询，每个查询都有两个整数 **L** 和**R**。对于每个查询，找到子数组**arr【L…R】**中位于 **A** 到 **B** (含)范围内的元素数量。

**示例:**

> **输入:** arr[] = {7，3，9，13，5，4}，A = 4，B = 7
> 查询= {1，5}
> **输出:** 2
> **解释:**
> 在子阵列{3，9，13，5，4}
> 中只有 5 和 4 位于 4 到 7
> 之间，因此，此类元素的计数为 2。
> 
> **输入:** arr[] = {0，1，2，3，4，5，6，7}，A = 1，B = 5
> 查询= {3，5}
> **输出:** 3
> **解释:**
> 所有元素 3，4 和 5 都位于子阵列{3，4，5}中的
> 范围 1 到 5 内。
> 因此，此类元素的计数为 3。

**先决条件:** [MO 的算法](https://www.geeksforgeeks.org/mos-algorithm-query-square-root-decomposition-set-1-introduction/)[SQRT 分解](https://www.geeksforgeeks.org/sqrt-square-root-decomposition-technique-set-1-introduction/)

**方法:**想法是使用 [MO 的算法](https://www.geeksforgeeks.org/mos-algorithm-query-square-root-decomposition-set-1-introduction/)对所有查询进行预处理，以便一个查询的结果可以用于下一个查询。下面是步骤的图示:

*   将查询分组到多个块中，其中每个块包含起始范围为(0 到√N–1)、(√N 到 2x√N–1)等的值。按照 **R** 的递增顺序对块内的查询进行排序。
*   逐个处理所有查询，每个查询都使用上一个查询中计算的结果。
*   当 arr[i]出现在范围[L，R]内时，保持对 arr[I]频率进行计数的频率阵列。

> **例如:** arr[] = [3，4，6，2，7，1]，L = 0，R = 4 和 A = 1，B = 6
> 初始频率数组初始化为 0 即 freq[]=[0…0]
> **步骤 1:** 添加 arr[0]并将其频率递增为 freq[arr[0]]++即 freq[3]+
> 和 freq[]=[0，0，0，1，0，0，0，0，0 0]
> **步骤 3:** 添加 arr[2]并增加 freq[arr[2]]++即 freq[6]+
> 和 freq[]=[0，0，0，1，1，0，1，0]
> **步骤 4:** 添加 arr[3]并增加 freq[arr[3]]++即 freq[2]+
> 和 freq[]=[0，0，1，1，1 1]
> **第 6 步:**现在我们需要找到 A 和 b 之间的元素数量。
> **第 7 步:**答案等于![\sum_{i=A}^B freq[i]     ](img/274f38e5a497cfb575be0e3f43e36cf4.png "Rendered by QuickLaTeX.com")
> 要计算**第 7 步中的和，**我们无法进行迭代，因为这样会导致每个查询的时间复杂度为 O(N)，所以我们将使用 **sqrt 分解技术**来找到每个查询的**时间复杂度为 O(√N)的和**

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// values in the range A to B
// in a subarray of L to R

#include <bits/stdc++.h>

using namespace std;

#define MAX 100001
#define SQRSIZE 400

// Variable to represent block size.
// This is made global so compare()
// of sort can use it.
int query_blk_sz;

// Structure to represent a
// query range
struct Query {
    int L;
    int R;
};

// Frequency array
// to keep count of elements
int frequency[MAX];

// Array which contains the frequency
// of a particular block
int blocks[SQRSIZE];

// Block size
int blk_sz;

// Function used to sort all queries
// so that all queries of the same
// block are arranged together and
// within a block, queries are sorted
// in increasing order of R values.
bool compare(Query x, Query y)
{
    if (x.L / query_blk_sz != y.L / query_blk_sz)
        return x.L / query_blk_sz < y.L / query_blk_sz;

    return x.R < y.R;
}

// Function used to get the block
// number of current a[i] i.e ind
int getblocknumber(int ind)
{
    return (ind) / blk_sz;
}

// Function to get the answer
// of range [0, k] which uses the
// sqrt decomposition technique
int getans(int A, int B)
{
    int ans = 0;
    int left_blk, right_blk;
    left_blk = getblocknumber(A);
    right_blk = getblocknumber(B);

    // If left block is equal to
    // right block then we can traverse
    // that block
    if (left_blk == right_blk) {
        for (int i = A; i <= B; i++)
            ans += frequency[i];
    }
    else {
        // Traversing first block in
        // range
        for (int i = A; i < (left_blk + 1) * blk_sz; i++)
            ans += frequency[i];

        // Traversing completely overlapped
        // blocks in range
        for (int i = left_blk + 1;
            i < right_blk; i++)
            ans += blocks[i];

        // Traversing last block in range
        for (int i = right_blk * blk_sz;
            i <= B; i++)
            ans += frequency[i];
    }
    return ans;
}

void add(int ind, int a[])
{
    // Increment the frequency of a[ind]
    // in the frequency array
    frequency[a[ind]]++;

    // Get the block number of a[ind]
    // to update the result in blocks
    int block_num = getblocknumber(a[ind]);

    blocks[block_num]++;
}
void remove(int ind, int a[])
{
    // Decrement the frequency of
    // a[ind] in the frequency array
    frequency[a[ind]]--;

    // Get the block number of a[ind]
    // to update the result in blocks
    int block_num = getblocknumber(a[ind]);

    blocks[block_num]--;
}
void queryResults(int a[], int n,
                Query q[], int m, int A, int B)
{

    // Initialize the block size
    // for queries
    query_blk_sz = sqrt(m);

    // Sort all queries so that queries
    // of same blocks are arranged
    // together.
    sort(q, q + m, compare);

    // Initialize current L,
    // current R and current result
    int currL = 0, currR = 0;

    for (int i = 0; i < m; i++) {

        // L and R values of the
        // current range

        int L = q[i].L, R = q[i].R;

        // Add Elements of current
        // range
        while (currR <= R) {
            add(currR, a);
            currR++;
        }
        while (currL > L) {
            add(currL - 1, a);
            currL--;
        }

        // Remove element of previous
        // range
        while (currR > R + 1)

        {
            remove(currR - 1, a);
            currR--;
        }
        while (currL < L) {
            remove(currL, a);
            currL++;
        }
        printf("%d\n", getans(A, B));
    }
}

// Driver code
int main()
{

    int arr[] = { 2, 0, 3, 1, 4, 2, 5, 11 };
    int N = sizeof(arr) / sizeof(arr[0]);

    int A = 1, B = 5;
    blk_sz = sqrt(N);
    Query Q[] = { { 0, 2 }, { 0, 3 }, { 5, 7 } };

    int M = sizeof(Q) / sizeof(Q[0]);

    // Answer the queries
    queryResults(arr, N, Q, M, A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// values in the range A to B
// in a subarray of L to R
import java.util.*;
import java.lang.Math;

public class GFG {

  public static int MAX=100001;
  public static int SQRSIZE=400;

  // Variable to represent block size.
  // This is made global so compare()
  // of sort can use it.
  public static int query_blk_sz;

  // Frequency array
  // to keep count of elements
  public static int[] frequency = new int[MAX];

  // Array which contains the frequency
  // of a particular block
  public static int[] blocks = new int[SQRSIZE];

  // Block size
  public static int blk_sz;

  // Function used to sort all queries
  // so that all queries of the same
  // block are arranged together and
  // within a block, queries are sorted
  // in increasing order of R values.

  static Comparator<int[]> arrayComparator = new Comparator<int[]>() {
    @Override
    public int compare(int[] x, int[] y) {
      if (x[0] / query_blk_sz != y[0] / query_blk_sz)
        return Integer.compare(x[0] / query_blk_sz, y[0] / query_blk_sz);

      return Integer.compare(x[1],y[1]);
    }
  };

  // Function used to get the block
  // number of current a[i] i.e ind
  public static int getblocknumber(int ind)
  {
    return (ind) / blk_sz;
  }

  // Function to get the answer
  // of range [0, k] which uses the
  // sqrt decomposition technique
  public static int getans(int A, int B)
  {
    int ans = 0;
    int left_blk, right_blk;
    left_blk = getblocknumber(A);
    right_blk = getblocknumber(B);

    // If left block is equal to
    // right block then we can traverse
    // that block
    if (left_blk == right_blk) {
      for (int i = A; i <= B; i++)
        ans += frequency[i];
    }
    else {
      // Traversing first block in
      // range
      for (int i = A; i < (left_blk + 1) * blk_sz; i++)
        ans += frequency[i];

      // Traversing completely overlapped
      // blocks in range
      for (int i = left_blk + 1;
           i < right_blk; i++)
        ans += blocks[i];

      // Traversing last block in range
      for (int i = right_blk * blk_sz;
           i <= B; i++)
        ans += frequency[i];
    }
    return ans;
  }

  public static void add(int ind, int a[])
  {

    // Increment the frequency of a[ind]
    // in the frequency array
    frequency[a[ind]]++;

    // Get the block number of a[ind]
    // to update the result in blocks
    int block_num = getblocknumber(a[ind]);

    blocks[block_num]++;
  }
  public static void remove(int ind, int a[])
  {

    // Decrement the frequency of
    // a[ind] in the frequency array
    frequency[a[ind]]--;

    // Get the block number of a[ind]
    // to update the result in blocks
    int block_num = getblocknumber(a[ind]);

    blocks[block_num]--;
  }
  public static void queryResults(int a[], int n,
                                  int[][] q, int m, int A, int B)
  {

    // Initialize the block size
    // for queries
    query_blk_sz = (int)Math.sqrt(m);

    // Sort all queries so that queries
    // of same blocks are arranged
    // together.
    Arrays.sort(q,arrayComparator);

    // Initialize current L,
    // current R and current result
    int currL = 0, currR = 0;

    for (int i = 0; i < m; i++) {

      // L and R values of the
      // current range

      int L = q[i][0], R = q[i][1];

      // Add Elements of current
      // range
      while (currR <= R) {
        add(currR, a);
        currR++;
      }
      while (currL > L) {
        add(currL - 1, a);
        currL--;
      }

      // Remove element of previous
      // range
      while (currR > R + 1)

      {
        remove(currR - 1, a);
        currR--;
      }
      while (currL < L) {
        remove(currL, a);
        currL++;
      }
      System.out.println(getans(A, B));
    }
  }

  // Driver code
  public static void main(String[] args) {
    int arr[] = { 2, 0, 3, 1, 4, 2, 5, 11 };
    int N = arr.length;

    int A = 1, B = 5;
    blk_sz = (int) Math.sqrt(N);
    int[][] Q = { { 0, 2 }, { 0, 3 }, { 5, 7 } };

    int M = Q.length;

    // Answer the queries
    queryResults(arr, N, Q, M, A, B);
  }
}

// This code is contributed
// by Shubham Singh
```

**Output:**

```
2
3
2
```