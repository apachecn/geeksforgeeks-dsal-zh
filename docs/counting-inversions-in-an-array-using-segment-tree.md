# 使用段树对数组中的反转进行计数

> 原文:[https://www . geesforgeks . org/counting-inversion-in-a-array-use-segment-tree/](https://www.geeksforgeeks.org/counting-inversions-in-an-array-using-segment-tree/)

给定一个整数数组 *arr* ，任务是计算数组中的逆序数。
如果 A[i] > A[j]和 i < j，那么这一对(A[i]，A[j])是逆序的一部分。
**示例:**

> **输入:** arr[] = {8，4，2，1}
> **输出:** 6
> **输入:** arr[] = {3，1，2}
> **输出:** 2

**进场:**

*   构建一个段树，其中每个节点将代表该节点范围内出现的总数。
*   假设任何节点的范围是[i，j]，那么该节点将包含大于或等于 I 且小于或等于 j 的数的计数。
*   叶节点只能是 1 或 0，因为节点的范围是 1。
*   遍历数组，让索引 I 处的数字为[i]。我们将在[a[i]+1，max]范围内找到段树中有多少个数字，其中 max 是数组的最大元素，并将其添加到答案变量中。
*   然后，我们将在段树中插入该数字，并继续到数组的最后一个索引。这样，对于每个元素，我们将出现在该元素之前且大于该元素的数字相加，即它们形成一个反转对。

以下是上述方法的实现:

## C++

```
// C++ program to count the inversions
// present in the array using segment tree
#include "algorithm"
#include "cstring"
#include "iostream"
using namespace std;

// Function to update segment tree
// i.e. to insert the element
void update(int* Tree, int index, int s, int e, int num)
{
    // Leaf node condition
    if (s == num and e == num) {
        Tree[index] = 1;
        return;
    }

    // No overlap condition
    if (num < s or num > e) {
        return;
    }

    // Else call on both the children nodes
    int mid = (s + e) >> 1;
    update(Tree, 2 * index, s, mid, num);
    update(Tree, 2 * index + 1, mid + 1, e, num);

    Tree[index] = Tree[2 * index] + Tree[2 * index + 1];
}

// Function to count the total numbers
// present in the range [a[i]+1, mx]
int query(int* Tree, int index, int s,
          int e, int qs, int qe)
{
    // Complete overlap
    if (qs <= s and e <= qe) {
        return Tree[index];
    }

    // No Overlap
    if (s > qe or e < qs) {
        return 0;
    }

    int mid = (s + e) >> 1;

    return query(Tree, 2 * index, s,
                 mid, qs, qe)
           + query(Tree, 2 * index + 1,
                   mid + 1, e, qs, qe);
}

// Driver code
int main(int argc, char const* argv[])
{
    int arr[] = { 8, 4, 2, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Maximum element present in the array.
    int mx = *max_element(arr, arr + n);

    // Segment Tree
    int Tree[6 * mx];

    // Initialize every node
    // of segment tree to 0
    memset(Tree, 0, sizeof(Tree));

    int answer = 0;

    for (int i = 0; i < n; ++i) {

        // add the count of inversion pair
        // formed with the element a[i] and the
        // elements appearing before the index i.
        answer += query(Tree, 1, 1, mx, arr[i] + 1, mx);

        // Insert the a[i] in the segment tree
        update(Tree, 1, 1, mx, arr[i]);
    }

    cout << answer;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the inversions
// present in the array using segment tree
import java.io.*;
import java.util.Arrays;
class GFG
{

  // Function to update segment tree
  // i.e. to insert the element
  static void update(int[] Tree, int index,
                     int s, int e, int num)
  {

    // Leaf node condition
    if (s == num && e == num)
    {
      Tree[index] = 1;
      return;
    }

    // No overlap condition
    if (num < s || num > e)
    {
      return;
    }

    // Else call on both the children nodes
    int mid = (s + e) >> 1;
    update(Tree, 2 * index, s, mid, num);
    update(Tree, 2 * index + 1, mid + 1, e, num);

    Tree[index] = Tree[2 * index] + Tree[2 * index + 1];
  }

  // Function to count the total numbers
  // present in the range [a[i]+1, mx]
  static int query(int[] Tree, int index, int s,
                   int e, int qs, int qe)
  {
    // Complete overlap
    if (qs <= s && e <= qe)
    {
      return Tree[index];
    }

    // No Overlap
    if (s > qe || e < qs)
    {
      return 0;
    }
    int mid = (s + e) >> 1;
    return query(Tree, 2 * index, s, mid, qs, qe) +
      query(Tree, 2 * index + 1, mid + 1, e, qs, qe);
  }

  // Driver code
  public static void main (String[] args)
  {
    int arr[] = { 8, 4, 2, 1 };
    int n = arr.length;

    // Maximum element present in the array.
    int mx = Arrays.stream(arr).max().getAsInt();

    // Segment Tree
    int[] Tree = new int[6 * mx];
    int answer = 0;
    for (int i = 0; i < n; ++i)
    {

      // add the count of inversion pair
      // formed with the element a[i] and the
      // elements appearing before the index i.
      answer += query(Tree, 1, 1, mx, arr[i] + 1, mx);

      // Insert the a[i] in the segment tree
      update(Tree, 1, 1, mx, arr[i]);
    }   
    System.out.println(answer);
  }
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 program to count the inversions
# present in the array using segment tree

# Function to update segment tree
# i.e. to insert the element
def update(Tree, index, s, e, num):

    # Leaf node condition
    if (s == num and e == num):
        Tree[index] = 1
        return

    # No overlap condition
    if (num < s or num > e):
        return

    # Else call on both the children nodes
    mid = (s + e) >> 1
    update(Tree, 2 * index, s, mid, num)
    update(Tree, 2 * index + 1, mid + 1, e, num)

    Tree[index] = Tree[2 * index] + Tree[2 * index + 1]

# Function to count the total numbers
# present in the range [a[i]+1, mx]
def query(Tree,index, s,e, qs, qe):

    # Complete overlap
    if (qs <= s and e <= qe):
        return Tree[index]

    # No Overlap
    if (s > qe or e < qs):
        return 0

    mid = (s + e) >> 1

    return query(Tree, 2 * index, s,mid, qs, qe) +\
           query(Tree, 2 * index + 1, mid + 1, e, qs, qe)

# Driver code
if __name__ == '__main__':
    arr = [8, 4, 2, 1]
    n = len(arr)

    # Maximum element present in the array.
    mx = max(arr)

    # Segment Tree
    Tree = [0] * (6 * mx)

    # Initialize every node
    # of segment tree to 0
    answer = 0

    for i in range(n):

        # add the count of inversion pair
        # formed with the element a[i] and the
        # elements appearing before the index i.
        answer += query(Tree, 1, 1, mx, arr[i] + 1, mx)

        # Insert the a[i] in the segment tree
        update(Tree, 1, 1, mx, arr[i])

    print(answer)

# This code is contributed by Mohit Kumar
```

## C#

```
using System;
using System.Linq;

class GFG
{

  // Function to update segment tree
  // i.e. to insert the element
  static void update(int[] Tree, int index,
                     int s, int e, int num)
  {

    // Leaf node condition
    if (s == num && e == num)
    {
      Tree[index] = 1;
      return;
    }

    // No overlap condition
    if (num < s || num > e)
    {
      return;
    }

    // Else call on both the children nodes
    int mid = (s + e) >> 1;
    update(Tree, 2 * index, s, mid, num);
    update(Tree, 2 * index + 1, mid + 1, e, num); 
    Tree[index] = Tree[2 * index] + Tree[2 * index + 1];
  }

  // Function to count the total numbers
  // present in the range [a[i]+1, mx]
  static int query(int[] Tree, int index,
                   int s, int e, int qs, int qe)
  {

    // Complete overlap
    if (qs <= s && e <= qe)
    {
      return Tree[index];
    }

    // No Overlap
    if (s > qe || e < qs)
    {
      return 0;
    }
    int mid = (s + e) >> 1;
    return query(Tree, 2 * index, s, mid, qs, qe) +
      query(Tree, 2 * index + 1, mid + 1, e, qs, qe);
  }

  // Driver code
  static public void Main ()
  {
    int[] arr = { 8, 4, 2, 1 };
    int n = arr.Length;

    // Maximum element present in the array.
    int mx =  arr.Max();

    // Segment Tree
    int[] Tree = new int[6 * mx];
    int answer = 0;
    for (int i = 0; i < n; ++i)
    {

      // add the count of inversion pair
      // formed with the element a[i] and the
      // elements appearing before the index i.
      answer += query(Tree, 1, 1, mx, arr[i] + 1, mx);

      // Insert the a[i] in the segment tree
      update(Tree, 1, 1, mx, arr[i]);
    }  
    Console.WriteLine(answer);
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// JavaScript program to count the inversions
// present in the array using segment tree

 // Function to update segment tree
  // i.e. to insert the element
function update(Tree,index,s,e,num)
{
    // Leaf node condition
    if (s == num && e == num)
    {
      Tree[index] = 1;
      return;
    }

    // No overlap condition
    if (num < s || num > e)
    {
      return;
    }

    // Else call on both the children nodes
    let mid = (s + e) >> 1;
    update(Tree, 2 * index, s, mid, num);
    update(Tree, 2 * index + 1, mid + 1, e, num);

    Tree[index] = Tree[2 * index] + Tree[2 * index + 1];
  }

  // Function to count the total numbers
  // present in the range [a[i]+1, mx]
  function query(Tree, index, s,
                    e,  qs,  qe)
  {
    // Complete overlap
    if (qs <= s && e <= qe)
    {
      return Tree[index];
    }

    // No Overlap
    if (s > qe || e < qs)
    {
      return 0;
    }
    let mid = (s + e) >> 1;
    return query(Tree, 2 * index, s, mid, qs, qe) +
      query(Tree, 2 * index + 1, mid + 1, e, qs, qe);
}

// Driver code

let arr=[ 8, 4, 2, 1 ];
let n = arr.length;

// Maximum element present in the array.
    let mx = Math.max(...arr);

    // Segment Tree
    let Tree = new Array(6 * mx);
    for(let i=0;i<Tree.length;i++)
    {
        Tree[i]=0;
    }
    let answer = 0;
    for (let i = 0; i < n; ++i)
    {

      // add the count of inversion pair
      // formed with the element a[i] and the
      // elements appearing before the index i.
      answer += query(Tree, 1, 1, mx, arr[i] + 1, mx);

      // Insert the a[i] in the segment tree
      update(Tree, 1, 1, mx, arr[i]);
    }  
    document.write(answer);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
6
```