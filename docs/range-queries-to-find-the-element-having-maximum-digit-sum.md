# 范围查询查找具有最大数字和的元素

> 原文:[https://www . geesforgeks . org/range-query-to-find-the-element-having-maximum-digital-sum/](https://www.geeksforgeeks.org/range-queries-to-find-the-element-having-maximum-digit-sum/)

给定一个由 **N** 整数和 **Q** 查询组成的数组 **Arr** ，每个查询的范围从 **L** 到 **R** 。找出 L 到 R 范围内具有最大数字和的元素，如果不止一个元素具有最大数字和，那么从这些元素中找出最大元素。
**示例:**

```
Input: Arr[] = { 16, 12, 43, 55} 
       Q = 2
       L = 0, R = 3
       L = 0, R = 2

Output: 55
        43

Explanation:
 The range (0, 3) in the 1st query has
 [16, 12, 43, 55]. Here, the digit sums are:
 for 16, 1 + 6 = 7
 for 12, 1 + 2 = 3
 for 43, 4 + 3 = 7
 for 55, 5 + 5 = 10
 Hence, the max digit sum is 10 and 
 max digit sum value is 55.

 The range (0, 2) in the 1st query has
 [16, 12, 43]. Here, the digit sums are:
 for 16, 1 + 6 = 7
 for 12, 1 + 2 = 3
 for 43, 4 + 3 = 7
 Hence, the max digit sum is 7 and 
 max digit sum value is max( 16, 43) = 43\. 
```

**天真方法:**
一个简单的解决方案是运行一个从 L 到 R 的循环，计算每个元素的数字和，并为每个查询找到从 L 到 R 的最大数字和元素。

**时间复杂度**:O(Q * N)
T3】辅助空间 : O(1)

**有效方法:**

*   一个有效的方法是建立一个[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)，其中每个节点存储两个值(**值**和**max _ digital _ sum**，并对其进行范围查询，以找到最大数字和和对应的元素。但是为了构建段树，我们必须考虑在树的节点上存储什么。
*   为了找出最大数字和值，我们需要两件事，一件是值，另一件是数字和。合并将返回两件事，数字和将在段树中存储 max(max _ digital _ sum . left，max _ digit _ sum.right)，值将包含相应的元素值。
*   如果我们深入研究，任何两个范围组合的最大位数总和将是左侧的最大位数总和或右侧的最大位数总和，无论哪个是最大值都将被考虑在内。
*   **段树的表示:**
    1.  叶节点是给定数组的元素。
    2.  每个内部节点代表叶节点的一些合并。对于不同的问题，合并可能会有所不同。对于这个问题，合并是节点下叶子的最大数字和的最大值。
    3.  树的数组表示用于表示段树。对于索引 I 处的每个节点，左子节点位于索引 ***2*i+1*** ，右子节点位于 ***2*i+2*** ，父节点位于 ***(i-1)/2*** 。

*   **从给定数组构建段树:**
    1.  我们从片段 arr[0]开始。。。n-1]。并且每次我们将当前段分成两半(如果它还没有变成长度为 1 的段)，然后在两半上调用相同的过程，并且对于每个这样的段，我们将 max_digit_sum 和值存储在相应的节点中。
    2.  然后，我们对段树进行范围查询，找出给定范围的 max_digit_sum，并输出相应的值。

下面是上述方法的实现。

## C++

```
// C++ program to find
// maximum digit sum value
#include <bits/stdc++.h>
using namespace std;

// Struct two store two values in one node
struct Node {
    int value;
    int max_digit_sum;
};

Node tree[4 * 10000];

// Function to find the digit sum
// for a number
int digitSum(int x)
{
    int sum = 0;
    while (x) {
        sum += (x % 10);
        x /= 10;
    }
}

// Function to build the segment tree
void build(int a[], int index, int beg, int end)
{
    if (beg == end) {

        // If there is one element in array,
        tree[index].value = a[beg];
        tree[index].max_digit_sum = digitSum(a[beg]);
    }
    else {

        int mid = (beg + end) / 2;

        // If there are more than one elements,
        // then recur for left and right subtrees
        build(a, 2 * index + 1, beg, mid);
        build(a, 2 * index + 2, mid + 1, end);

        if (tree[2 * index + 1].max_digit_sum >
            tree[2 * index + 2].max_digit_sum)
        {
            tree[index].max_digit_sum =
                tree[2 * index + 1].max_digit_sum;
            tree[index].value =
                tree[2 * index + 1].value;
        }
        else if (tree[2 * index + 2].max_digit_sum >
                 tree[2 * index + 1].max_digit_sum)
        {
            tree[index].max_digit_sum =
                tree[2 * index + 2].max_digit_sum;
            tree[index].value =
                tree[2 * index + 2].value;
        }
        else
        {
            tree[index].max_digit_sum =
                tree[2 * index + 2].max_digit_sum;
            tree[index].value =
                max(tree[2 * index + 2].value,
                    tree[2 * index + 1].value);
        }
    }
}

// Function to do the range query in the segment
// tree for the maximum digit sum
Node query(int index, int beg, int end,
           int l, int r)
{
    Node result;
    result.value = result.max_digit_sum = -1;

    // If segment of this node is outside the given
    // range, then return the minimum valueue.
    if (beg > r || end < l)
        return result;

    // If segment of this node is a part of given
    // range, then return the node of the segment
    if (beg >= l && end <= r)
        return tree[index];

    int mid = (beg + end) / 2;

    // If left segment of this node falls out of
    // range, then recur in the right side of
    // the tree
    if (l > mid)
        return query(2 * index + 2, mid + 1,
                     end, l, r);

    // If right segment of this node falls out of
    // range, then recur in the left side of
    // the tree
    if (r <= mid)
        return query(2 * index + 1, beg,
                     mid, l, r);

    // If a part of this segment overlaps with
    // the given range
    Node left = query(2 * index + 1, beg,
                      mid, l, r);
    Node right = query(2 * index + 2, mid + 1,
                       end, l, r);

    if (left.max_digit_sum > right.max_digit_sum)
    {
        result.max_digit_sum = left.max_digit_sum;
        result.value = left.value;
    }
    else if (right.max_digit_sum > left.max_digit_sum)
    {
        result.max_digit_sum = right.max_digit_sum;
        result.value = right.value;
    }
    else
    {
        result.max_digit_sum = left.max_digit_sum;
        result.value = max(right.value, left.value);
    }

    // Returns the value
    return result;
}

// Driver code
int main()
{

    int a[] = {16, 12, 43, 55};

    // Calculates the length of array
    int N = sizeof(a) / sizeof(a[0]);

    // Calls the build function to build
    // the segment tree
    build(a, 0, 0, N - 1);

    // Find the max digit-sum valueue between
    // 0th and 3rd index of array
    cout << query(0, 0, N - 1, 0, 3).value
         << endl;

    // Find the max digit-sum value between
    // 0th and 2nd index of array
    cout << query(0, 0, N - 1, 0, 2).value
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// maximum digit sum value
import java.util.*;

class GFG{

// Struct two store two values
// in one node
static class Node
{
    int value;
    int max_digit_sum;
};

static Node []tree = new Node[4 * 10000];

// Function to find the digit sum
// for a number
static int digitSum(int x)
{
    int sum = 0;

    while (x > 0)
    {
        sum += (x % 10);
        x /= 10;
    }
    return sum;
}

// Function to build the segment tree
static void build(int a[], int index,
                  int beg, int end)
{
    if (beg == end)
    {

        // If there is one element in array,
        tree[index].value = a[beg];
        tree[index].max_digit_sum = digitSum(a[beg]);
    }
    else
    {
        int mid = (beg + end) / 2;

        // If there are more than one elements,
        // then recur for left and right subtrees
        build(a, 2 * index + 1, beg, mid);
        build(a, 2 * index + 2, mid + 1, end);

        if (tree[2 * index + 1].max_digit_sum >
            tree[2 * index + 2].max_digit_sum)
        {
            tree[index].max_digit_sum =
                tree[2 * index + 1].max_digit_sum;
            tree[index].value =
                tree[2 * index + 1].value;
        }
        else if (tree[2 * index + 2].max_digit_sum >
                 tree[2 * index + 1].max_digit_sum)
        {
            tree[index].max_digit_sum =
                tree[2 * index + 2].max_digit_sum;
            tree[index].value =
                tree[2 * index + 2].value;
        }
        else
        {
            tree[index].max_digit_sum =
                tree[2 * index + 2].max_digit_sum;
            tree[index].value =
                Math.max(tree[2 * index + 2].value,
                         tree[2 * index + 1].value);
        }
    }
}

// Function to do the range query in the segment
// tree for the maximum digit sum
static Node query(int index, int beg, int end,
                  int l, int r)
{
    Node result = new Node();
    result.value = result.max_digit_sum = -1;

    // If segment of this node is outside the given
    // range, then return the minimum valueue.
    if (beg > r || end < l)
        return result;

    // If segment of this node is a part of given
    // range, then return the node of the segment
    if (beg >= l && end <= r)
        return tree[index];

    int mid = (beg + end) / 2;

    // If left segment of this node falls out of
    // range, then recur in the right side of
    // the tree
    if (l > mid)
        return query(2 * index + 2, mid + 1,
                     end, l, r);

    // If right segment of this node falls out of
    // range, then recur in the left side of
    // the tree
    if (r <= mid)
        return query(2 * index + 1, beg,
                     mid, l, r);

    // If a part of this segment overlaps with
    // the given range
    Node left = query(2 * index + 1, beg,
                      mid, l, r);
    Node right = query(2 * index + 2, mid + 1,
                       end, l, r);

    if (left.max_digit_sum > right.max_digit_sum)
    {
        result.max_digit_sum = left.max_digit_sum;
        result.value = left.value;
    }
    else if (right.max_digit_sum > left.max_digit_sum)
    {
        result.max_digit_sum = right.max_digit_sum;
        result.value = right.value;
    }
    else
    {
        result.max_digit_sum = left.max_digit_sum;
        result.value = Math.max(right.value,
                                 left.value);
    }

    // Returns the value
    return result;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 16, 12, 43, 55 };

    // Calculates the length of array
    int N = a.length;

    for(int i = 0; i < tree.length; i++)
        tree[i] = new Node();

    // Calls the build function to build
    // the segment tree
    build(a, 0, 0, N - 1);

    // Find the max digit-sum valueue between
    // 0th and 3rd index of array
    System.out.print(
        query(0, 0, N - 1, 0, 3).value + "\n");

    // Find the max digit-sum value between
    // 0th and 2nd index of array
    System.out.print(
        query(0, 0, N - 1, 0, 2).value + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to find
# maximum digit sum value

# Struct two store two values in one node
class Node:

    def __init__(self):

        self.value = 0
        self.max_digit_sum = 0

tree = [Node() for i in range(4 * 10000)]

# Function to find the digit sum
# for a number
def digitSum(x):

    sum = 0;
    while(x != 0):
        sum += (x % 10)
        x //= 10

    return sum

# Function to build the segment tree
def build(a, index, beg, end):

    if (beg == end):

        # If there is one element in array,
        tree[index].value = a[beg]
        tree[index].max_digit_sum = digitSum(a[beg])

    else:
        mid = (beg + end) // 2

        # If there are more than one elements,
        # then recur for left and right subtrees
        build(a, 2 * index + 1, beg, mid)
        build(a, 2 * index + 2, mid + 1, end)

        if (tree[2 * index + 1].max_digit_sum >
            tree[2 * index + 2].max_digit_sum):

            tree[index].max_digit_sum = tree[2 * index + 1].max_digit_sum
            tree[index].value = tree[2 * index + 1].value

        elif (tree[2 * index + 2].max_digit_sum >
              tree[2 * index + 1].max_digit_sum):

            tree[index].max_digit_sum = tree[2 * index + 2].max_digit_sum
            tree[index].value = tree[2 * index + 2].value

        else:
            tree[index].max_digit_sum = tree[2 * index + 2].max_digit_sum
            tree[index].value = max(tree[2 * index + 2].value,
                                    tree[2 * index + 1].value)

# Function to do the range query in the segment
# tree for the maximum digit sum
def query(index, beg, end, l, r):

    result = Node()
    result.value = result.max_digit_sum = -1

    # If segment of this node is outside the given
    # range, then return the minimum valueue.
    if (beg > r or end < l):
        return result

    # If segment of this node is a part of given
    # range, then return the node of the segment
    if (beg >= l and end <= r):
        return tree[index]

    mid = (beg + end) // 2

    # If left segment of this node falls out of
    # range, then recur in the right side of
    # the tree
    if (l > mid):
        return query(2 * index + 2, mid + 1, end, l, r)

    # If right segment of this node falls out of
    # range, then recur in the left side of
    # the tree
    if (r <= mid):
        return query(2 * index + 1, beg, mid, l, r)

    # If a part of this segment overlaps with
    # the given range
    left = query(2 * index + 1, beg, mid, l, r)
    right = query(2 * index + 2, mid + 1, end, l, r)

    if (left.max_digit_sum > right.max_digit_sum):
        result.max_digit_sum = left.max_digit_sum
        result.value = left.value

    elif (right.max_digit_sum > left.max_digit_sum):
        result.max_digit_sum = right.max_digit_sum
        result.value = right.value

    else:
        result.max_digit_sum = left.max_digit_sum
        result.value = max(right.value, left.value)

    # Returns the value
    return result

# Driver code
if __name__=="__main__":

    a = [ 16, 12, 43, 55 ]

    # Calculates the length of array
    N = len(a)

    # Calls the build function to build
    # the segment tree
    build(a, 0, 0, N - 1)

    # Find the max digit-sum valueue between
    # 0th and 3rd index of array
    print(query(0, 0, N - 1, 0, 3).value)

    # Find the max digit-sum value between
    # 0th and 2nd index of array
    print(query(0, 0, N - 1, 0, 2).value)

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find
// maximum digit sum value
using System;
class GFG{

// Struct two store
// two values in one node
class Node
{
  public int value;
  public int max_digit_sum;
};

static Node []tree = new Node[4 * 10000];

// Function to find the digit sum
// for a number
static int digitSum(int x)
{
  int sum = 0;

  while (x > 0)
  {
    sum += (x % 10);
    x /= 10;
  }
  return sum;
}

// Function to build the segment tree
static void build(int []a, int index,
                  int beg, int end)
{
  if (beg == end)
  {
    // If there is one element in array,
    tree[index].value = a[beg];
    tree[index].max_digit_sum =
                digitSum(a[beg]);
  }
  else
  {
    int mid = (beg + end) / 2;

    // If there are more than one elements,
    // then recur for left and right subtrees
    build(a, 2 * index + 1, beg, mid);
    build(a, 2 * index + 2, mid + 1, end);

    if (tree[2 * index + 1].max_digit_sum >
        tree[2 * index + 2].max_digit_sum)
    {
      tree[index].max_digit_sum =
           tree[2 * index + 1].max_digit_sum;
      tree[index].value =
           tree[2 * index + 1].value;
    }
    else if (tree[2 * index + 2].max_digit_sum >
             tree[2 * index + 1].max_digit_sum)
    {
      tree[index].max_digit_sum =
           tree[2 * index + 2].max_digit_sum;
      tree[index].value =
           tree[2 * index + 2].value;
    }
    else
    {
      tree[index].max_digit_sum =
           tree[2 * index + 2].max_digit_sum;
      tree[index].value =
           Math.Max(tree[2 * index + 2].value,
                tree[2 * index + 1].value);
    }
  }
}

// Function to do the range query
// in the segment tree for the
// maximum digit sum
static Node query(int index, int beg,
                  int end, int l, int r)
{
  Node result = new Node();
  result.value = result.max_digit_sum = -1;

  // If segment of this node is
  // outside the given range,
  // then return the minimum valueue.
  if (beg > r || end < l)
    return result;

  // If segment of this node
  // is a part of given range,
  // then return the node of the segment
  if (beg >= l && end <= r)
    return tree[index];

  int mid = (beg + end) / 2;

  // If left segment of this
  // node falls out of range,
  // then recur in the right
  // side of the tree
  if (l > mid)
    return query(2 * index + 2, mid + 1,
                 end, l, r);

  // If right segment of this
  // node falls out of range,
  // then recur in the left side of
  // the tree
  if (r <= mid)
    return query(2 * index + 1, beg,
                 mid, l, r);

  // If a part of this segment
  // overlaps with the given range
  Node left = query(2 * index + 1, beg,
                    mid, l, r);
  Node right = query(2 * index + 2, mid + 1,
                     end, l, r);

  if (left.max_digit_sum > right.max_digit_sum)
  {
    result.max_digit_sum = left.max_digit_sum;
    result.value = left.value;
  }
  else if (right.max_digit_sum > left.max_digit_sum)
  {
    result.max_digit_sum = right.max_digit_sum;
    result.value = right.value;
  }
  else
  {
    result.max_digit_sum = left.max_digit_sum;
    result.value = Math.Max(right.value,
                            left.value);
  }

  // Returns the value
  return result;
}

// Driver code
public static void Main(String[] args)
{
  int []a = {16, 12, 43, 55};

  // Calculates the length
  // of array
  int N = a.Length;

  for(int i = 0; i < tree.Length; i++)
    tree[i] = new Node();

  // Calls the build function
  // to build the segment tree
  build(a, 0, 0, N - 1);

  // Find the max digit-sum value between
  // 0th and 3rd index of array
  Console.Write(query(0, 0,
                      N - 1,
                      0, 3).value + "\n");

  // Find the max digit-sum value between
  // 0th and 2nd index of array
  Console.Write(query(0, 0,
                      N - 1,
                      0, 2).value + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to find maximum digit sum value

    // Struct two store two values in one node
    class Node
    {
        constructor() {
           this.value = 0;
           this.max_digit_sum = 0;
        }
    }

    let tree = new Array(4 * 10000);

    // Function to find the digit sum for a number
    function digitSum(x)
    {
      let sum = 0;

      while (x > 0)
      {
        sum += (x % 10);
        x = parseInt(x / 10, 10);
      }
      return sum;
    }

    // Function to build the segment tree
    function build(a, index, beg, end)
    {
      if (beg == end)
      {
        // If there is one element in array,
        tree[index].value = a[beg];
        tree[index].max_digit_sum = digitSum(a[beg]);
      }
      else
      {
        let mid = parseInt((beg + end) / 2, 10);

        // If there are more than one elements,
        // then recur for left and right subtrees
        build(a, 2 * index + 1, beg, mid);
        build(a, 2 * index + 2, mid + 1, end);

        if (tree[2 * index + 1].max_digit_sum >
            tree[2 * index + 2].max_digit_sum)
        {
          tree[index].max_digit_sum =
               tree[2 * index + 1].max_digit_sum;
          tree[index].value =
               tree[2 * index + 1].value;
        }
        else if (tree[2 * index + 2].max_digit_sum >
                 tree[2 * index + 1].max_digit_sum)
        {
          tree[index].max_digit_sum =
               tree[2 * index + 2].max_digit_sum;
          tree[index].value =
               tree[2 * index + 2].value;
        }
        else
        {
          tree[index].max_digit_sum =
               tree[2 * index + 2].max_digit_sum;
          tree[index].value =
               Math.max(tree[2 * index + 2].value,
                    tree[2 * index + 1].value);
        }
      }
    }

    // Function to do the range query
    // in the segment tree for the
    // maximum digit sum
    function query(index, beg, end, l, r)
    {
      let result = new Node();
      result.value = result.max_digit_sum = -1;

      // If segment of this node is
      // outside the given range,
      // then return the minimum valueue.
      if (beg > r || end < l)
        return result;

      // If segment of this node
      // is a part of given range,
      // then return the node of the segment
      if (beg >= l && end <= r)
        return tree[index];

      let mid = parseInt((beg + end) / 2, 10);

      // If left segment of this
      // node falls out of range,
      // then recur in the right
      // side of the tree
      if (l > mid)
        return query(2 * index + 2, mid + 1, end, l, r);

      // If right segment of this
      // node falls out of range,
      // then recur in the left side of
      // the tree
      if (r <= mid)
        return query(2 * index + 1, beg, mid, l, r);

      // If a part of this segment
      // overlaps with the given range
      let left = query(2 * index + 1, beg,
                        mid, l, r);
      let right = query(2 * index + 2, mid + 1,
                         end, l, r);

      if (left.max_digit_sum > right.max_digit_sum)
      {
        result.max_digit_sum = left.max_digit_sum;
        result.value = left.value;
      }
      else if (right.max_digit_sum > left.max_digit_sum)
      {
        result.max_digit_sum = right.max_digit_sum;
        result.value = right.value;
      }
      else
      {
        result.max_digit_sum = left.max_digit_sum;
        result.value = Math.max(right.value, left.value);
      }

      // Returns the value
      return result;
    }

    let a = [16, 12, 43, 55];

    // Calculates the length
    // of array
    let N = a.length;

    for(let i = 0; i < tree.length; i++)
      tree[i] = new Node();

    // Calls the build function
    // to build the segment tree
    build(a, 0, 0, N - 1);

    // Find the max digit-sum value between
    // 0th and 3rd index of array
    document.write(query(0, 0,
                        N - 1,
                        0, 3).value + "</br>");

    // Find the max digit-sum value between
    // 0th and 2nd index of array
    document.write(query(0, 0,
                        N - 1,
                        0, 2).value + "</br>");

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
55
43
```

**复杂度分析:**
树构建的时间复杂度为 O(N)。总共有 2n-1 个节点，每个节点的值在树构造中只计算一次。
每个查询的时间复杂度为 0(对数 N)。
问题的时间复杂度为 **O(Q * log N)**