# 计数数组中的反转|设置 3(使用位)

> 原文:[https://www . geesforgeks . org/count-inversion-array-set-3-using-bit/](https://www.geeksforgeeks.org/count-inversions-array-set-3-using-bit/)

数组的反转计数表示数组离排序有多远(或多近)。如果数组已经排序，则反转计数为 0。如果数组按相反的顺序排序，则反转计数为最大值。
如果 a[i] > a[j]和 i < j，两个元素 a[i]和 a[j]形成反转，为了简单起见，我们可以假设所有元素都是唯一的。
**例:**

```
Input: arr[] = {8, 4, 2, 1}
Output: 6
Explanation: Given array has six inversions:
(8,4), (4,2), (8,2), (8,1), (4,1), (2,1).     

Input: arr[] = {3, 1, 2}
Output: 2
Explanation: Given array has two inversions:
(3,1), (3,2).
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/magic-triplets4003/1)

我们已经在下面讨论了解决反转计数的方法:

1.  [初始和修改合并排序](https://www.geeksforgeeks.org/counting-inversions/)
2.  [使用 AVL 树](https://www.geeksforgeeks.org/count-inversions-in-an-array-set-2-using-self-balancing-bst/)

在进一步阅读这篇文章之前，我们建议你参考[二进制索引树(BIT)](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/) 。
**<u>使用尺寸为θ(MaxElement)的位的解决方案:</u>**

*   **方法:**遍历数组，对于每个索引，找到数组右侧较小元素的数量。这可以使用 BIT 来完成。合计数组中所有索引的计数，并打印总和。
*   **BIT 背景:**
    1.  BIT 基本上支持大小为 n 的数组 arr[]的两种操作:
        1.  O(Log n)时间内直到 arr[i]的元素总和。
        2.  在 O(Log n)时间内更新数组元素。
    2.  BIT 使用数组实现，以树的形式工作。请注意，有两种方法可以将 BIT 视为一棵树。
        1.  其中索引 x 的父代是“x –( x &-x)”的求和操作。
        2.  索引 x 的父项为“x + (x & -x)”的更新操作。
*   **算法:**
    1.  创建一个位，找出给定数字的位中较小元素的计数，以及一个变量*结果= 0* 。
    2.  从头到尾遍历数组。
    3.  对于每个索引，检查比当前元素少多少个数字出现在位中，并将其添加到结果中
    4.  为了获得较小元素的计数，使用位的 [getSum()。](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)
    5.  在他的基本思想中，BIT 表示为大小等于最大元素加 1 的数组。以便元素可以用作索引。
    6.  之后，我们通过执行更新操作将当前元素的计数从 0 更新为 1，从而将当前元素添加到 BIT[]中，并因此更新 BIT 中当前元素的祖先(详见 BIT 中的 [update())。](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/) 
*   **实施**T2】

## C++

```
// C++ program to count inversions using Binary Indexed Tree
#include<bits/stdc++.h>
using namespace std;

// Returns sum of arr[0..index]. This function assumes
// that the array is preprocessed and partial sums of
// array elements are stored in BITree[].
int getSum(int BITree[], int index)
{
    int sum = 0; // Initialize result

    // Traverse ancestors of BITree[index]
    while (index > 0)
    {
        // Add current element of BITree to sum
        sum += BITree[index];

        // Move index to parent node in getSum View
        index -= index & (-index);
    }
    return sum;
}

// Updates a node in Binary Index Tree (BITree) at given index
// in BITree.  The given value 'val' is added to BITree[i] and
// all of its ancestors in tree.
void updateBIT(int BITree[], int n, int index, int val)
{
    // Traverse all ancestors and add 'val'
    while (index <= n)
    {
       // Add 'val' to current node of BI Tree
       BITree[index] += val;

       // Update index to that of parent in update View
       index += index & (-index);
    }
}

// Returns inversion count arr[0..n-1]
int getInvCount(int arr[], int n)
{
    int invcount = 0; // Initialize result

    // Find maximum element in arr[]
    int maxElement = 0;
    for (int i=0; i<n; i++)
        if (maxElement < arr[i])
            maxElement = arr[i];

    // Create a BIT with size equal to maxElement+1 (Extra
    // one is used so that elements can be directly be
    // used as index)
    int BIT[maxElement+1];
    for (int i=1; i<=maxElement; i++)
        BIT[i] = 0;

    // Traverse all elements from right.
    for (int i=n-1; i>=0; i--)
    {
        // Get count of elements smaller than arr[i]
        invcount += getSum(BIT, arr[i]-1);

        // Add current element to BIT
        updateBIT(BIT, maxElement, arr[i], 1);
    }

    return invcount;
}

// Driver program
int main()
{
    int arr[] = {8, 4, 2, 1};
    int n = sizeof(arr)/sizeof(int);
    cout << "Number of inversions are : " << getInvCount(arr,n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count inversions
// using Binary Indexed Tree

class GFG
{

// Returns sum of arr[0..index].
// This function assumes that the
// array is preprocessed and partial
// sums of array elements are stored
// in BITree[].
static int getSum(int[] BITree, int index)
{
    int sum = 0; // Initialize result

    // Traverse ancestors of BITree[index]
    while (index > 0)
    {
        // Add current element of BITree to sum
        sum += BITree[index];

        // Move index to parent node in getSum View
        index -= index & (-index);
    }
    return sum;
}

// Updates a node in Binary Index
// Tree (BITree) at given index
// in BITree. The given value 'val'
// is added to BITree[i] and all
// of its ancestors in tree.
static void updateBIT(int[] BITree, int n,
                        int index, int val)
{
    // Traverse all ancestors and add 'val'
    while (index <= n)
    {
        // Add 'val' to current node of BI Tree
        BITree[index] += val;

        // Update index to that of parent in update View
        index += index & (-index);
    }
}

// Returns inversion count arr[0..n-1]
static int getInvCount(int[] arr, int n)
{
    int invcount = 0; // Initialize result

    // Find maximum element in arr[]
    int maxElement = 0;
    for (int i = 0; i < n; i++)
        if (maxElement < arr[i])
            maxElement = arr[i];

    // Create a BIT with size equal to
    // maxElement+1 (Extra one is used so
    // that elements can be directly be
    // used as index)
    int[] BIT = new int[maxElement + 1];
    for (int i = 1; i <= maxElement; i++)
        BIT[i] = 0;

    // Traverse all elements from right.
    for (int i = n - 1; i >= 0; i--)
    {
        // Get count of elements smaller than arr[i]
        invcount += getSum(BIT, arr[i] - 1);

        // Add current element to BIT
        updateBIT(BIT, maxElement, arr[i], 1);
    }

    return invcount;
}

// Driver code
public static void main (String[] args)
{
    int []arr = {8, 4, 2, 1};
    int n = arr.length;
    System.out.println("Number of inversions are : " +
                                getInvCount(arr,n));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to count inversions using
# Binary Indexed Tree

# Returns sum of arr[0..index]. This function
# assumes that the array is preprocessed and
# partial sums of array elements are stored
# in BITree[].
def getSum( BITree, index):
    sum = 0 # Initialize result

    # Traverse ancestors of BITree[index]
    while (index > 0):

        # Add current element of BITree to sum
        sum += BITree[index]

        # Move index to parent node in getSum View
        index -= index & (-index)

    return sum

# Updates a node in Binary Index Tree (BITree)
# at given index in BITree. The given value
# 'val' is added to BITree[i] and all of its
# ancestors in tree.
def updateBIT(BITree, n, index, val):

    # Traverse all ancestors and add 'val'
    while (index <= n):

        # Add 'val' to current node of BI Tree
        BITree[index] += val

        # Update index to that of parent
        # in update View
        index += index & (-index)

# Returns count of inversions of size three
def getInvCount(arr, n):

    invcount = 0 # Initialize result

    # Find maximum element in arrays
    maxElement = max(arr)

    # Create a BIT with size equal to
    # maxElement+1 (Extra one is used
    # so that elements can be directly
    # be used as index)
    BIT = [0] * (maxElement + 1)
    for i in range(1, maxElement + 1):
        BIT[i] = 0
    for i in range(n - 1, -1, -1):

        invcount += getSum(BIT, arr[i] - 1)
        updateBIT(BIT, maxElement, arr[i], 1)
    return invcount

# Driver code
if __name__ =="__main__":
    arr = [8, 4, 2, 1]
    n = 4
    print("Inversion Count : ",
           getInvCount(arr, n))

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to count inversions
// using Binary Indexed Tree
using System;

class GFG
{

// Returns sum of arr[0..index].
// This function assumes that the
// array is preprocessed and partial
// sums of array elements are stored
// in BITree[].
static int getSum(int []BITree, int index)
{
    int sum = 0; // Initialize result

    // Traverse ancestors of BITree[index]
    while (index > 0)
    {
        // Add current element of BITree to sum
        sum += BITree[index];

        // Move index to parent node in getSum View
        index -= index & (-index);
    }
    return sum;
}

// Updates a node in Binary Index
// Tree (BITree) at given index
// in BITree. The given value 'val'
// is added to BITree[i] and all
// of its ancestors in tree.
static void updateBIT(int []BITree, int n,
                        int index, int val)
{
    // Traverse all ancestors and add 'val'
    while (index <= n)
    {
        // Add 'val' to current node of BI Tree
        BITree[index] += val;

        // Update index to that of parent in update View
        index += index & (-index);
    }
}

// Returns inversion count arr[0..n-1]
static int getInvCount(int []arr, int n)
{
    int invcount = 0; // Initialize result

    // Find maximum element in arr[]
    int maxElement = 0;
    for (int i = 0; i < n; i++)
        if (maxElement < arr[i])
            maxElement = arr[i];

    // Create a BIT with size equal to
    // maxElement+1 (Extra one is used so
    // that elements can be directly be
    // used as index)
    int[] BIT = new int[maxElement + 1];
    for (int i = 1; i <= maxElement; i++)
        BIT[i] = 0;

    // Traverse all elements from right.
    for (int i = n - 1; i >= 0; i--)
    {
        // Get count of elements smaller than arr[i]
        invcount += getSum(BIT, arr[i] - 1);

        // Add current element to BIT
        updateBIT(BIT, maxElement, arr[i], 1);
    }

    return invcount;
}

// Driver code
static void Main()
{
    int []arr = {8, 4, 2, 1};
    int n = arr.Length;
    Console.WriteLine("Number of inversions are : " +
                                getInvCount(arr,n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count inversions
// using Binary Indexed Tree

// Returns sum of arr[0..index].
// This function assumes that the
// array is preprocessed and partial
// sums of array elements are stored
// in BITree[].
function getSum($BITree, $index)
{
    $sum = 0; // Initialize result

    // Traverse ancestors of BITree[index]
    while ($index > 0)
    {
        // Add current element of BITree to sum
        $sum += $BITree[$index];

        // Move index to parent node in getSum View
        $index -= $index & (-$index);
    }
    return $sum;
}

// Updates a node in Binary Index
// Tree (BITree) at given index
// in BITree. The given value 'val'
// is added to BITree[i] and
// all of its ancestors in tree.
function updateBIT(&$BITree, $n, $index,$val)
{
    // Traverse all ancestors and add 'val'
    while ($index <= $n)
    {
        // Add 'val' to current node of BI Tree
        $BITree[$index] += $val;

        // Update index to that of
        // parent in update View
        $index += $index & (-$index);
    }
}

// Returns inversion count arr[0..n-1]
function getInvCount($arr, $n)
{
    $invcount = 0; // Initialize result

    // Find maximum element in arr[]
    $maxElement = 0;
    for ($i=0; $i<$n; $i++)
        if ($maxElement < $arr[$i])
            $maxElement = $arr[$i];

    // Create a BIT with size equal
    // to maxElement+1 (Extra one is
    // used so that elements can be
    // directly be used as index)
    $BIT=array_fill(0,$maxElement+1,0);

    // Traverse all elements from right.
    for ($i=$n-1; $i>=0; $i--)
    {
        // Get count of elements smaller than arr[i]
        $invcount += getSum($BIT, $arr[$i]-1);

        // Add current element to BIT
        updateBIT($BIT, $maxElement, $arr[$i], 1);
    }

    return $invcount;
}

    // Driver program
    $arr = array(8, 4, 2, 1);
    $n = count($arr);
    print("Number of inversions are : ".getInvCount($arr,$n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript program to count inversions
// using Binary Indexed Tree  
// Returns sum of arr[0..index].
// This function assumes that the
// array is preprocessed and partial
// sums of array elements are stored
// in BITree.
function getSum(BITree , index)
{
    var sum = 0; // Initialize result

    // Traverse ancestors of BITree[index]
    while (index > 0)
    {
        // Add current element of BITree to sum
        sum += BITree[index];

        // Move index to parent node in getSum View
        index -= index & (-index);
    }
    return sum;
}

// Updates a node in Binary Index
// Tree (BITree) at given index
// in BITree. The given value 'val'
// is added to BITree[i] and all
// of its ancestors in tree.
function updateBIT(BITree , n, index , val)
{
    // Traverse all ancestors and add 'val'
    while (index <= n)
    {
        // Add 'val' to current node of BI Tree
        BITree[index] += val;

        // Update index to that of parent in update View
        index += index & (-index);
    }
}

// Returns inversion count arr[0..n-1]
function getInvCount(arr , n)
{
    var invcount = 0; // Initialize result

    // Find maximum element in arr
    var maxElement = 0;
    for (i = 0; i < n; i++)
        if (maxElement < arr[i])
            maxElement = arr[i];

    // Create a BIT with size equal to
    // maxElement+1 (Extra one is used so
    // that elements can be directly be
    // used as index)
    var BIT = Array.from({length: maxElement + 1}, (_, i) => 0);
    for (i = 1; i <= maxElement; i++)
        BIT[i] = 0;

    // Traverse all elements from right.
    for (i = n - 1; i >= 0; i--)
    {
        // Get count of elements smaller than arr[i]
        invcount += getSum(BIT, arr[i] - 1);

        // Add current element to BIT
        updateBIT(BIT, maxElement, arr[i], 1);
    }

    return invcount;
}

// Driver code
    var arr = [8, 4, 2, 1];
    var n = arr.length;
    document.write("Number of inversions are : " +
                                getInvCount(arr,n));

// This code is contributed by Amit Katiyar
</script>
```

*   **输出:**

```
Number of inversions are : 6
```

*   **复杂度分析:**
    *   **时间复杂度:-** 更新函数和 getSum 函数为 O(log(maximumement))运行。必须为数组中的每个元素运行 getSum 函数。所以总的时间复杂度是:O(nlog(最大值))。
    *   **辅助空间:** O(maxElement)，BIT 所需的空间是一个最大元素大小的数组。

**<u>使用θ(n)大小的位的更好解决方案:</u>**

*   **方法:**遍历数组，对于每个索引，找到数组右侧较小元素的数量。这可以使用 BIT 来完成。合计数组中所有索引的计数，并打印总和。方法保持不变，但前一种方法的问题是，它不适用于负数，因为指数不能是负数。其思想是将给定的数组转换为值从 1 到 n 的数组，并且较小和较大元素的相对顺序保持不变。
    **例** :-

```

arr[] = {7, -90, 100, 1}

It gets  converted to,
arr[] = {3, 1, 4 ,2 }
as -90 < 1 < 7 < 100.

Explanation: Make a BIT array of a number of
elements instead of a maximum element. Changing
element will not have any change in the answer
as the greater elements remain greater and at the
same position. 
```

*   **算法:**
    1.  创建一个位，找出给定数字的位中较小元素的计数，以及一个变量*结果= 0* 。
    2.  前面的解决方案不适用于包含负元素的数组。因此，将数组转换为包含元素相对编号的数组，即复制原始数组，然后对数组的副本进行排序，并用排序数组中相同元素的索引替换原始数组中的元素。
        例如，如果数组是{-3，2，0}，那么数组被转换为{1，3，2}
    3.  从头到尾遍历数组。
    4.  对于每个索引，检查比当前元素少多少个数字出现在位中，并将其添加到结果中
*   **执行:**

## C++

```
// C++ program to count inversions using Binary Indexed Tree
#include<bits/stdc++.h>
using namespace std;

// Returns sum of arr[0..index]. This function assumes
// that the array is preprocessed and partial sums of
// array elements are stored in BITree[].
int getSum(int BITree[], int index)
{
    int sum = 0; // Initialize result

    // Traverse ancestors of BITree[index]
    while (index > 0)
    {
        // Add current element of BITree to sum
        sum += BITree[index];

        // Move index to parent node in getSum View
        index -= index & (-index);
    }
    return sum;
}

// Updates a node in Binary Index Tree (BITree) at given index
// in BITree.  The given value 'val' is added to BITree[i] and
// all of its ancestors in tree.
void updateBIT(int BITree[], int n, int index, int val)
{
    // Traverse all ancestors and add 'val'
    while (index <= n)
    {
       // Add 'val' to current node of BI Tree
       BITree[index] += val;

       // Update index to that of parent in update View
       index += index & (-index);
    }
}

// Converts an array to an array with values from 1 to n
// and relative order of smaller and greater elements remains
// same.  For example, {7, -90, 100, 1} is converted to
// {3, 1, 4 ,2 }
void convert(int arr[], int n)
{
    // Create a copy of arrp[] in temp and sort the temp array
    // in increasing order
    int temp[n];
    for (int i=0; i<n; i++)
        temp[i] = arr[i];
    sort(temp, temp+n);

    // Traverse all array elements
    for (int i=0; i<n; i++)
    {
        // lower_bound() Returns pointer to the first element
        // greater than or equal to arr[i]
        arr[i] = lower_bound(temp, temp+n, arr[i]) - temp + 1;
    }
}

// Returns inversion count arr[0..n-1]
int getInvCount(int arr[], int n)
{
    int invcount = 0; // Initialize result

     // Convert arr[] to an array with values from 1 to n and
     // relative order of smaller and greater elements remains
     // same.  For example, {7, -90, 100, 1} is converted to
    //  {3, 1, 4 ,2 }
    convert(arr, n);

    // Create a BIT with size equal to maxElement+1 (Extra
    // one is used so that elements can be directly be
    // used as index)
    int BIT[n+1];
    for (int i=1; i<=n; i++)
        BIT[i] = 0;

    // Traverse all elements from right.
    for (int i=n-1; i>=0; i--)
    {
        // Get count of elements smaller than arr[i]
        invcount += getSum(BIT, arr[i]-1);

        // Add current element to BIT
        updateBIT(BIT, n, arr[i], 1);
    }

    return invcount;
}

// Driver program
int main()
{
    int arr[] = {8, 4, 2, 1};
    int n = sizeof(arr)/sizeof(int);
    cout << "Number of inversions are : " << getInvCount(arr,n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count inversions
// using Binary Indexed Tree
import java.util.*;
class GFG{

// Returns sum of arr[0..index].
// This function assumes that the
// array is preprocessed and partial
// sums of array elements are stored
// in BITree[].
static int getSum(int BITree[],
                  int index)
{
  // Initialize result
  int sum = 0;

  // Traverse ancestors of
  // BITree[index]
  while (index > 0)
  {
    // Add current element of
    // BITree to sum
    sum += BITree[index];

    // Move index to parent node
    // in getSum View
    index -= index & (-index);
  }
  return sum;
}

// Updates a node in Binary Index Tree
// (BITree) at given index in BITree. 
// The given value 'val' is added to
// BITree[i] and all of its ancestors
// in tree.
static void updateBIT(int BITree[], int n,
                      int index, int val)
{
  // Traverse all ancestors
  // and add 'val'
  while (index <= n)
  {
    // Add 'val' to current
    // node of BI Tree
    BITree[index] += val;

    // Update index to that of
    // parent in update View
    index += index & (-index);
  }
}

// Converts an array to an array
// with values from 1 to n and
// relative order of smaller and
// greater elements remains same. 
// For example, {7, -90, 100, 1}
// is converted to {3, 1, 4 ,2 }
static void convert(int arr[],
                    int n)
{
  // Create a copy of arrp[] in temp
  // and sort the temp array in
  // increasing order
  int []temp = new int[n];

  for (int i = 0; i < n; i++)
    temp[i] = arr[i];
  Arrays.sort(temp);

  // Traverse all array elements
  for (int i = 0; i < n; i++)
  {
    // lower_bound() Returns pointer
    // to the first element greater
    // than or equal to arr[i]
    arr[i] =lower_bound(temp,0,
                        n, arr[i]) + 1;
  }
}

static int lower_bound(int[] a, int low,
                       int high, int element)
{
  while(low < high)
  {
    int middle = low +
                (high - low) / 2;
    if(element > a[middle])
      low = middle + 1;
    else
      high = middle;
  }
  return low;
}

// Returns inversion count
// arr[0..n-1]
static int getInvCount(int arr[],
                       int n)
{
  // Initialize result
  int invcount = 0;

  // Convert arr[] to an array
  // with values from 1 to n and
  // relative order of smaller
  // and greater elements remains
  // same.  For example, {7, -90,
  // 100, 1} is converted to
  //  {3, 1, 4 ,2 }
  convert(arr, n);

  // Create a BIT with size equal
  // to maxElement+1 (Extra one is
  // used so that elements can be
  // directly be used as index)
  int []BIT = new int[n + 1];

  for (int i = 1; i <= n; i++)
    BIT[i] = 0;

  // Traverse all elements
  // from right.
  for (int i = n - 1; i >= 0; i--)
  {
    // Get count of elements
    // smaller than arr[i]
    invcount += getSum(BIT,
                       arr[i] - 1);

    // Add current element to BIT
    updateBIT(BIT, n, arr[i], 1);
  }

  return invcount;
}

// Driver code
public static void main(String[] args)
{
  int arr[] = {8, 4, 2, 1};
  int n = arr.length;
  System.out.print("Number of inversions are : " + 
                    getInvCount(arr, n));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to count inversions using Binary Indexed Tree
from bisect import bisect_left as lower_bound

# Returns sum of arr[0..index]. This function assumes
# that the array is preprocessed and partial sums of
# array elements are stored in BITree.
def getSum(BITree, index):

    sum = 0 # Initialize result

    # Traverse ancestors of BITree[index]
    while (index > 0):

        # Add current element of BITree to sum
        sum += BITree[index]

        # Move index to parent node in getSum View
        index -= index & (-index)

    return sum

# Updates a node in Binary Index Tree (BITree) at given index
# in BITree. The given value 'val' is added to BITree[i] and
# all of its ancestors in tree.
def updateBIT(BITree, n, index, val):

    # Traverse all ancestors and add 'val'
    while (index <= n):

        # Add 'val' to current node of BI Tree
        BITree[index] += val

    # Update index to that of parent in update View
    index += index & (-index)

# Converts an array to an array with values from 1 to n
# and relative order of smaller and greater elements remains
# same. For example, 7, -90, 100, 1 is converted to
# 3, 1, 4 ,2
def convert(arr, n):

    # Create a copy of arrp in temp and sort the temp array
    # in increasing order
    temp = [0]*(n)
    for i in range(n):
        temp[i] = arr[i]
    temp = sorted(temp)

    # Traverse all array elements
    for i in range(n):

        # lower_bound() Returns pointer to the first element
        # greater than or equal to arr[i]
        arr[i] = lower_bound(temp, arr[i]) + 1

# Returns inversion count arr[0..n-1]
def getInvCount(arr, n):

    invcount = 0 # Initialize result

    # Convert arr to an array with values from 1 to n and
    # relative order of smaller and greater elements remains
    # same. For example, 7, -90, 100, 1 is converted to
    # 3, 1, 4 ,2
    convert(arr, n)

    # Create a BIT with size equal to maxElement+1 (Extra
    # one is used so that elements can be directly be
    # used as index)
    BIT = [0] * (n + 1)

    # Traverse all elements from right.
    for i in range(n - 1, -1, -1):

        # Get count of elements smaller than arr[i]
        invcount += getSum(BIT, arr[i] - 1)

        # Add current element to BIT
        updateBIT(BIT, n, arr[i], 1)

    return invcount

# Driver program
if __name__ == '__main__':

    arr = [8, 4, 2, 1]
    n = len(arr)
    print("Number of inversions are : ",getInvCount(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to count inversions
// using Binary Indexed Tree
using System;
class GFG{

// Returns sum of arr[0..index].
// This function assumes that the
// array is preprocessed and partial
// sums of array elements are stored
// in BITree[].
static int getSum(int []BITree,
                  int index)
{
  // Initialize result
  int sum = 0;

  // Traverse ancestors of
  // BITree[index]
  while (index > 0)
  {
    // Add current element of
    // BITree to sum
    sum += BITree[index];

    // Move index to parent node
    // in getSum View
    index -= index & (-index);
  }
  return sum;
}

// Updates a node in Binary Index Tree
// (BITree) at given index in BITree. 
// The given value 'val' is added to
// BITree[i] and all of its ancestors
// in tree.
static void updateBIT(int []BITree, int n,
                      int index, int val)
{
  // Traverse all ancestors
  // and add 'val'
  while (index <= n)
  {
    // Add 'val' to current
    // node of BI Tree
    BITree[index] += val;

    // Update index to that of
    // parent in update View
    index += index & (-index);
  }
}

// Converts an array to an array
// with values from 1 to n and
// relative order of smaller and
// greater elements remains same. 
// For example, {7, -90, 100, 1}
// is converted to {3, 1, 4 ,2 }
static void convert(int []arr,
                    int n)
{
  // Create a copy of arrp[] in temp
  // and sort the temp array in
  // increasing order
  int []temp = new int[n];

  for (int i = 0; i < n; i++)
    temp[i] = arr[i];
  Array.Sort(temp);

  // Traverse all array elements
  for (int i = 0; i < n; i++)
  {
    // lower_bound() Returns pointer
    // to the first element greater
    // than or equal to arr[i]
    arr[i] =lower_bound(temp,0,
                        n, arr[i]) + 1;
  }
}

static int lower_bound(int[] a, int low,
                       int high, int element)
{
  while(low < high)
  {
    int middle = low +
                (high - low) / 2;
    if(element > a[middle])
      low = middle + 1;
    else
      high = middle;
  }
  return low;
}

// Returns inversion count
// arr[0..n-1]
static int getInvCount(int []arr,
                       int n)
{
  // Initialize result
  int invcount = 0;

  // Convert []arr to an array
  // with values from 1 to n and
  // relative order of smaller
  // and greater elements remains
  // same.  For example, {7, -90,
  // 100, 1} is converted to
  //  {3, 1, 4 ,2 }
  convert(arr, n);

  // Create a BIT with size equal
  // to maxElement+1 (Extra one is
  // used so that elements can be
  // directly be used as index)
  int []BIT = new int[n + 1];

  for (int i = 1; i <= n; i++)
    BIT[i] = 0;

  // Traverse all elements
  // from right.
  for (int i = n - 1; i >= 0; i--)
  {
    // Get count of elements
    // smaller than arr[i]
    invcount += getSum(BIT,
                       arr[i] - 1);

    // Add current element
    // to BIT
    updateBIT(BIT, n,
              arr[i], 1);
  }

  return invcount;
}

// Driver code
public static void Main(String[] args)
{
  int []arr = {8, 4, 2, 1};
  int n = arr.Length;
  Console.Write("Number of inversions are : " + 
                 getInvCount(arr, n));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program to count inversions
// using Binary Indexed Tree

// Returns sum of arr[0..index].
// This function assumes that the
// array is preprocessed and partial
// sums of array elements are stored
// in BITree[].   
function getSum(BITree,index)
{

        // Initialize result
  let sum = 0;

  // Traverse ancestors of
  // BITree[index]
  while (index > 0)
  {

    // Add current element of
    // BITree to sum
    sum += BITree[index];

    // Move index to parent node
    // in getSum View
    index -= index & (-index);
  }
  return sum;
}

// Updates a node in Binary Index Tree
// (BITree) at given index in BITree.
// The given value 'val' is added to
// BITree[i] and all of its ancestors
// in tree.
function updateBIT(BITree,n,index,val)
{

    // Traverse all ancestors
  // and add 'val'
  while (index <= n)
  {

    // Add 'val' to current
    // node of BI Tree
    BITree[index] += val;

    // Update index to that of
    // parent in update View
    index += index & (-index);
  }
}

// Converts an array to an array
// with values from 1 to n and
// relative order of smaller and
// greater elements remains same.
// For example, {7, -90, 100, 1}
// is converted to {3, 1, 4 ,2 }
function convert(arr, n)
{

    // Create a copy of arrp[] in temp
  // and sort the temp array in
  // increasing order
  let temp = new Array(n);

  for (let i = 0; i < n; i++)
    temp[i] = arr[i];
  temp.sort(function(a, b){return a - b;});

  // Traverse all array elements
  for (let i = 0; i < n; i++)
  {
    // lower_bound() Returns pointer
    // to the first element greater
    // than or equal to arr[i]
    arr[i] =lower_bound(temp,0,
                        n, arr[i]) + 1;
  }
}

function lower_bound(a,low,high,element)
{
    while(low < high)
  {
    let middle = low +
                Math.floor((high - low) / 2);
    if(element > a[middle])
      low = middle + 1;
    else
      high = middle;
  }
  return low;
}

// Returns inversion count
// arr[0..n-1]
function getInvCount(arr,n)
{
    // Initialize result
  let invcount = 0;

  // Convert arr[] to an array
  // with values from 1 to n and
  // relative order of smaller
  // and greater elements remains
  // same.  For example, {7, -90,
  // 100, 1} is converted to
  //  {3, 1, 4 ,2 }
  convert(arr, n);

  // Create a BIT with size equal
  // to maxElement+1 (Extra one is
  // used so that elements can be
  // directly be used as index)
  let BIT = new Array(n + 1);

  for (let i = 1; i <= n; i++)
    BIT[i] = 0;

  // Traverse all elements
  // from right.
  for (let i = n - 1; i >= 0; i--)
  {
    // Get count of elements
    // smaller than arr[i]
    invcount += getSum(BIT,
                       arr[i] - 1);

    // Add current element to BIT
    updateBIT(BIT, n, arr[i], 1);
  }

  return invcount;
}

// Driver code
let arr=[8, 4, 2, 1];
let n = arr.length;
document.write("Number of inversions are : " +
                    getInvCount(arr, n));

    // This code is contributed by unknown2108
</script>
```

*   **输出:**

```
Number of inversions are : 6
```

*   **复杂度分析:**
    *   **时间复杂度:**更新函数和 getSum 函数针对 O(log(n))运行。必须为数组中的每个元素运行 getSum 函数。所以总的时间复杂度是 O(nlog(n))。
    *   **辅助空间:** O(n)。
        位所需的空间是一个大小为 n 的数组

本文由 Abhiraj Smit 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。