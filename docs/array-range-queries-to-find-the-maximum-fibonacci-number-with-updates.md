# 数组范围查询，通过更新找到最大斐波那契数

> 原文:[https://www . geesforgeks . org/array-range-query-to-find-max-Fibonacci-number-with-updates/](https://www.geeksforgeeks.org/array-range-queries-to-find-the-maximum-fibonacci-number-with-updates/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是执行以下两个查询:

*   **最大值(开始，结束)**:从开始到结束打印子数组中元素的最大斐波那契数
*   **更新(I，x)** :将 x 添加到数组索引 **i** 引用的数组元素中，即:arr[i] = x

**注意:**以下示例由基于 0 的索引组成。

**示例:**

> **输入:** arr = [1，3，5，7，9，11]
> 查询 1:最大值(Start = 1，End = 3)
> 查询 2:更新(3，8)即 arr[3] = 8
> **输出:**
> 给定范围内最大斐波那契数= 5
> 给定范围内更新的最大斐波那契数= 8
> **解释:**
> 在最大值查询中，子数组【1{3，5，7}
> 因此，5 是给定范围内的最大斐波那契数。
> 在更新查询中，索引 3 处的值被更新
> 为 8，数组 arr 现在为[1，3，5，8，9，11]
> 在更新最大查询中，子数组[1…3]
> 具有全部 3 个斐波那契数 3，5 和 8，即。[3，5，8]
> 因此，8 是给定范围内的最大斐波那契数。

**简单方法:**

一个简单的解决方案是运行一个从 l 到 r 的循环，并计算给定范围内所有元素的最大斐波那契数。要更新一个值，只需执行 arr[i] = x。第一个操作需要 **O(N)** 时间，第二个操作需要 **O(1)** 时间。

**高效方法:**
这里，我们需要在 **O(Log N** )时间执行操作，所以我们可以使用 [**段树**](https://www.geeksforgeeks.org/tag/segment-tree/) 在 **O(Log N)** 时间执行这两个操作。
**段树的表示:**
1。叶节点是输入数组的元素。
2。每个内部节点代表其所有子节点的最大斐波那契数，如果范围内不存在斐波那契数，则为-1。
树的数组表示用于表示段树。对于索引 I 处的每个节点，**左子节点**位于索引 **2*i+1** ，**右子节点**位于索引 **2*i+2** ，**父节点**位于索引 **(i-1)/2** 。
**从给定数组构建段树:**
我们从段 arr[0]开始。。。n-1]，并且每次我们将当前段分成两半(如果它还没有变成长度为 1 的段)，然后在两半上调用相同的过程，并且对于每个这样的段，我们将最大斐波那契数值或-1 存储在段树节点中。构建的段树的所有层都将被完全填充，除了最后一层。此外，该树将是一个完整的二叉树，因为我们总是在每一层将片段分成两半。由于构造的树总是一棵有 n 片叶子的完全二叉树，因此会有 n-1 个内部节点。所以**总节点**将为**2 * n–1**。段树高度为**原木 <sub>2</sub> N** 。由于树是用数组表示的，并且父索引和子索引之间的关系必须保持，因此为段树分配的内存大小将为**2 *(2<sup>ceil(log2n)</sup>)–1**。
为了检查斐波那契数，我们可以使用动态编程构建一个哈希表，包含所有小于或等于最大值的斐波那契数 **arr** 可以取比方说 MAX，它将用于在 O(1)时间内测试一个数。
然后我们对段树进行范围查询，找出给定范围的 max_set_bits，并输出相应的值。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP code for range maximum query and updates
#include <bits/stdc++.h>
using namespace std;

set<int> fibonacci;

// A utility function to get the
// middle index of given range.
int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

// Function to create hash table
// to check Fibonacci numbers
void createHash(int maxElement)
{
    int prev = 0, curr = 1;
    fibonacci.insert(prev);
    fibonacci.insert(curr);

    while (curr <= maxElement) {
        int temp = curr + prev;
        fibonacci.insert(temp);
        prev = curr;
        curr = temp;
    }
}

/*  A recursive function to get the sum of
    values in given range of the array.
    The following are parameters for this
    function.

    st       -> Pointer to segment tree
    node     -> Index of current node in
                the segment tree .
    ss & se  -> Starting and ending indexes
                of the segment represented
                by current node, i.e., st[node]
    l & r    -> Starting and ending indexes
                of range query */
int MaxUtil(int* st, int ss, int se, int l,
            int r, int node)
{
    // If segment of this node is completely
    // part of given range, then return
    // the max of segment
    if (l <= ss && r >= se)
        return st[node];

    // If segment of this node does not
    // belong to given range
    if (se < l || ss > r)
        return -1;

    // If segment of this node is partially
    // the part of given range
    int mid = getMid(ss, se);

    return max(MaxUtil(st, ss, mid, l, r,
                       2 * node + 1),
               MaxUtil(st, mid + 1, se, l,
                       r, 2 * node + 2));
}

/* A recursive function to update the nodes which
   have the given index in their range. The following
   are parameters st, ss and se are same as defined
   above index -> index of the element to be updated.*/
void updateValue(int arr[], int* st, int ss, int se,
                 int index, int value, int node)
{
    if (index < ss || index > se) {
        cout << "Invalid Input" << endl;
        return;
    }

    if (ss == se) {
        // update value in array and in segment tree
        arr[index] = value;

        if (fibonacci.find(value) != fibonacci.end())
            st[node] = value;
        else
            st[node] = -1;
    }
    else {
        int mid = getMid(ss, se);

        if (index >= ss && index <= mid)
            updateValue(arr, st, ss, mid, index,
                        value, 2 * node + 1);
        else
            updateValue(arr, st, mid + 1, se,
                        index, value, 2 * node + 2);

        st[node] = max(st[2 * node + 1],
                       st[2 * node + 2]);
    }
    return;
}

// Return max of elements in range from
// index l (query start) to r (query end).
int getMax(int* st, int n, int l, int r)
{
    // Check for erroneous input values
    if (l < 0 || r > n - 1 || l > r) {
        printf("Invalid Input");
        return -1;
    }

    return MaxUtil(st, 0, n - 1, l, r, 0);
}

// A recursive function that constructs Segment
// Tree for array[ss..se]. si is index of
// current node in segment tree st
int constructSTUtil(int arr[], int ss, int se,
                    int* st, int si)
{
    // If there is one element in array, store
    // it in current node of segment tree and return
    if (ss == se) {
        if (fibonacci.find(arr[ss])
            != fibonacci.end())
            st[si] = arr[ss];
        else
            st[si] = -1;
        return st[si];
    }

    // If there are more than one elements, then
    // recur for left and right subtrees and
    // store the max of values in this node
    int mid = getMid(ss, se);

    st[si]
        = max(constructSTUtil(
                  arr, ss, mid, st,
                  si * 2 + 1),
              constructSTUtil(
                  arr, mid + 1, se,
                  st, si * 2 + 2));

    return st[si];
}

/* Function to construct segment tree
   from given array.
   This function allocates memory
   for segment tree.*/
int* constructST(int arr[], int n)
{
    // Height of segment tree
    int x = (int)(ceil(log2(n)));

    // Maximum size of segment tree
    int max_size = 2 * (int)pow(2, x) - 1;

    // Allocate memory
    int* st = new int[max_size];

    // Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, st, 0);

    // Return the constructed segment tree
    return st;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 5, 7, 9, 11 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // find the largest node value
    // in the array
    int maxEle = *max_element(arr, arr + n);

    // creating a set containing
    // all fibonacci numbers
    // upto the maximum data value
    // in the array
    createHash(maxEle);

    // Build segment tree from given array
    int* st = constructST(arr, n);

    // Print max of values in array
    // from index 1 to 3
    cout << "Maximum fibonacci number"
         << " in given range = "
         << getMax(st, n, 1, 3) << endl;

    // Update: set arr[1] = 8 and update
    // corresponding segment tree nodes.
    updateValue(arr, st, 0, n - 1, 3, 8, 0);

    // Find max after the value is updated
    cout << "Updated Maximum Fibonacci"
         << " number in given range = "
         << getMax(st, n, 1, 3) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for range maximum query and updates
import java.util.Arrays;
import java.util.HashSet;
import java.util.Set;

class GFG {

  static Set<Integer> fibonacci = new HashSet<>();

  // A utility function to get the
  // middle index of given range.
  static int getMid(int s, int e) {
    return s + (e - s) / 2;
  }

  // Function to create hash table
  // to check Fibonacci numbers
  static void createHash(int maxElement) {
    int prev = 0, curr = 1;
    fibonacci.add(prev);
    fibonacci.add(curr);

    while (curr <= maxElement) {
      int temp = curr + prev;
      fibonacci.add(temp);
      prev = curr;
      curr = temp;
    }
  }

  /*
     * A recursive function to get the sum of
     * values in given range of the array.
     * The following are parameters for this function.
     *
     * st       -> Pointer to segment tree
     * node     -> Index of current node
     *             in the segment tree .
     * ss & se  -> Starting and ending indexes
     *             of the segment represented
     *             by current node, i.e., st[node]
     * l & r    -> Starting and ending indexes
     *             of range query
     */
  static int MaxUtil(int[] st, int ss, int se,
                     int l, int r, int node)
  {

    // If segment of this node is completely
    // part of given range, then return
    // the max of segment
    if (l <= ss && r >= se)
      return st[node];

    // If segment of this node does not
    // belong to given range
    if (se < l || ss > r)
      return -1;

    // If segment of this node is partially
    // the part of given range
    int mid = getMid(ss, se);

    return Math.max(MaxUtil(st, ss, mid, l, r, 2 * node + 1),
                    MaxUtil(st, mid + 1, se, l, r, 2 * node + 2));
  }

  /*
     * A recursive function to update the nodes which
     * have the given index in their range. The following
     * are parameters st, ss and se are same as defined
     * above index -> index of the element to be updated.
     */
  static void updateValue(int arr[], int[] st, int ss, int se,
                          int index, int value, int node) {
    if (index < ss || index > se) {
      System.out.println("Invalid Input");
      return;
    }

    if (ss == se) {
      // update value in array and in segment tree
      arr[index] = value;

      if (fibonacci.contains(value))
        st[node] = value;
      else
        st[node] = -1;
    } else {
      int mid = getMid(ss, se);

      if (index >= ss && index <= mid)
        updateValue(arr, st, ss, mid, index,
                    value, 2 * node + 1);
      else
        updateValue(arr, st, mid + 1, se,
                    index, value, 2 * node + 2);

      st[node] = Math.max(st[2 * node + 1], st[2 * node + 2]);
    }
    return;
  }

  // Return max of elements in range from
  // index l (query start) to r (query end).
  static int getMax(int[] st, int n, int l, int r)
  {

    // Check for erroneous input values
    if (l < 0 || r > n - 1 || l > r)
    {
      System.out.printf("Invalid Input\n");
      return -1;
    }

    return MaxUtil(st, 0, n - 1, l, r, 0);
  }

  // A recursive function that constructs Segment
  // Tree for array[ss..se]. si is index of
  // current node in segment tree st
  static int constructSTUtil(int arr[], int ss, int se,
                             int[] st, int si)
  {

    // If there is one element in array, store
    // it in current node of segment tree and return
    if (ss == se) {
      if (fibonacci.contains(arr[ss]))
        st[si] = arr[ss];
      else
        st[si] = -1;
      return st[si];
    }

    // If there are more than one elements, then
    // recur for left and right subtrees and
    // store the max of values in this node
    int mid = getMid(ss, se);

    st[si] = Math.max(constructSTUtil(arr, ss, mid, st, si * 2 + 1),
                      constructSTUtil(arr, mid + 1, se, st, si * 2 + 2));

    return st[si];
  }

  /*
     * Function to construct segment tree
     * from given array. This function allocates
     * memory for segment tree.
     */
  static int[] constructST(int arr[], int n)
  {

    // Height of segment tree
    int x = (int) (Math.ceil(Math.log(n) / Math.log(2)));

    // Maximum size of segment tree
    int max_size = 2 * (int) Math.pow(2, x) - 1;

    // Allocate memory
    int[] st = new int[max_size];

    // Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, st, 0);

    // Return the constructed segment tree
    return st;
  }

  // Driver code
  public static void main(String[] args)
  {

    int arr[] = { 1, 3, 5, 7, 9, 11 };
    int n = arr.length;

    // find the largest node value
    // in the array
    int maxEle = Arrays.stream(arr).max().getAsInt();

    // creating a set containing
    // all fibonacci numbers
    // upto the maximum data value
    // in the array
    createHash(maxEle);

    // Build segment tree from given array
    int[] st = constructST(arr, n);

    // Print max of values in array
    // from index 1 to 3
    System.out.println("Maximum fibonacci number in given range = " +
                       getMax(st, n, 1, 3));

    // Update: set arr[1] = 8 and update
    // corresponding segment tree nodes.
    updateValue(arr, st, 0, n - 1, 3, 8, 0);

    // Find max after the value is updated
    System.out.println("Updated Maximum fibonacci number in given range = " +
                       getMax(st, n, 1, 3));
  }
}

// This code is contributed by sanjeev2552
```

**Output:** Maximum fibonacci number in given range = 5 Updated Maximum fibonacci number in given range = 8