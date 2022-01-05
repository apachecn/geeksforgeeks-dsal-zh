# 从 n 个数组中选择一个元素的组合

> 原文:[https://www . geeksforgeeks . org/combinations-from-n-arrays-picking-one-element-from-from-arrays/](https://www.geeksforgeeks.org/combinations-from-n-arrays-picking-one-element-from-each-array/)

给定数组列表，找到所有组合，其中每个组合包含每个给定数组中的一个元素。

**示例:**

```
Input : [ [1, 2], [3, 4] ]
Output : 1 3  
         1 4 
         2 3 
         2 4       

Input : [ [1], [2, 3, 4], [5] ]
Output : 1 2 5  
         1 3 5
         1 4 5           
```

我们保持数组的大小等于数组的总数。这个名为 index 的数组帮助我们跟踪 n 个数组中每个数组的当前元素的索引。最初，它用全 0 初始化，表示每个数组中的当前索引是第一个元素的索引。我们一直打印组合，直到找不到新的组合。从最右边的数组开始，我们检查该数组中是否有更多的元素。如果是，我们在索引中增加该数组的条目，即移动到该数组中的下一个元素。我们还将该数组右侧所有数组中的当前索引设为 0。我们继续向左移动以检查所有数组，直到找到一个这样的数组。如果没有发现更多的数组，我们就此打住。

## C++

```
// C++ program to find combinations from n
// arrays such that one element from each
// array is present
#include <bits/stdc++.h>

using namespace std;

// function to print combinations that contain
// one element from each of the given arrays
void print(vector<vector<int> >& arr)
{
    // number of arrays
    int n = arr.size();

    // to keep track of next element in each of
    // the n arrays
    int* indices = new int[n];

    // initialize with first element's index
    for (int i = 0; i < n; i++)
        indices[i] = 0;

    while (1) {

        // print current combination
        for (int i = 0; i < n; i++)
            cout << arr[i][indices[i]] << " ";
        cout << endl;

        // find the rightmost array that has more
        // elements left after the current element
        // in that array
        int next = n - 1;
        while (next >= 0 &&
              (indices[next] + 1 >= arr[next].size()))
            next--;

        // no such array is found so no more
        // combinations left
        if (next < 0)
            return;

        // if found move to next element in that
        // array
        indices[next]++;

        // for all arrays to the right of this
        // array current index again points to
        // first element
        for (int i = next + 1; i < n; i++)
            indices[i] = 0;
    }
}

// driver function to test above function
int main()
{
    // initializing a vector with 3 empty vectors
    vector<vector<int> > arr(3, vector<int>(0, 0));

    // now entering data
    // [[1, 2, 3], [4], [5, 6]]
    arr[0].push_back(1);
    arr[0].push_back(2);
    arr[0].push_back(3);
    arr[1].push_back(4);
    arr[2].push_back(5);
    arr[2].push_back(6);

    print(arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find combinations from n
// arrays such that one element from each
// array is present
import java.util.*;

class GFG{

// Function to print combinations that contain
// one element from each of the given arrays
static void print(Vector<Integer> []arr)
{

    // Number of arrays
    int n = arr.length;

    // To keep track of next element in
    // each of the n arrays
    int []indices = new int[n];

    // Initialize with first element's index
    for(int i = 0; i < n; i++)
        indices[i] = 0;

    while (true)
    {

        // Print current combination
        for(int i = 0; i < n; i++)
            System.out.print(
                arr[i].get(indices[i]) + " ");

        System.out.println();

        // Find the rightmost array that has more
        // elements left after the current element
        // in that array
        int next = n - 1;
        while (next >= 0 &&
              (indices[next] + 1 >=
                   arr[next].size()))
            next--;

        // No such array is found so no more
        // combinations left
        if (next < 0)
            return;

        // If found move to next element in that
        // array
        indices[next]++;

        // For all arrays to the right of this
        // array current index again points to
        // first element
        for(int i = next + 1; i < n; i++)
            indices[i] = 0;
    }
}

// Driver code
public static void main(String[] args)
{

    // Initializing a vector with 3 empty vectors
    @SuppressWarnings("unchecked")
    Vector<Integer> []arr = new Vector[3];
    for(int i = 0; i < arr.length; i++)
        arr[i] = new Vector<Integer>();

    // Now entering data
    // [[1, 2, 3], [4], [5, 6]]
    arr[0].add(1);
    arr[0].add(2);
    arr[0].add(3);
    arr[1].add(4);
    arr[2].add(5);
    arr[2].add(6);

    print(arr);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to find combinations from n
# arrays such that one element from each
# array is present

# function to prcombinations that contain
# one element from each of the given arrays
def print1(arr):

    # number of arrays
    n = len(arr)

    # to keep track of next element
    # in each of the n arrays
    indices = [0 for i in range(n)]

    while (1):

        # prcurrent combination
        for i in range(n):
            print(arr[i][indices[i]], end = " ")
        print()

        # find the rightmost array that has more
        # elements left after the current element
        # in that array
        next = n - 1
        while (next >= 0 and
              (indices[next] + 1 >= len(arr[next]))):
            next-=1

        # no such array is found so no more
        # combinations left
        if (next < 0):
            return

        # if found move to next element in that
        # array
        indices[next] += 1

        # for all arrays to the right of this
        # array current index again points to
        # first element
        for i in range(next + 1, n):
            indices[i] = 0

# Driver Code

# initializing a vector with 3 empty vectors
arr = [[] for i in range(3)]

# now entering data
# [[1, 2, 3], [4], [5, 6]]
arr[0].append(1)
arr[0].append(2)
arr[0].append(3)
arr[1].append(4)
arr[2].append(5)
arr[2].append(6)

print1(arr)

# This code is contributed by mohit kumar
```

## C#

```
// C# program to find
// combinations from n
// arrays such that one
// element from each
// array is present
using System;
using System.Collections.Generic;
class GFG{

// Function to print combinations
// that contain one element from
// each of the given arrays
static void print(List<int> []arr)
{
  // Number of arrays
  int n = arr.Length;

  // To keep track of next
  // element in each of
  // the n arrays
  int []indices = new int[n];

  // Initialize with first
  // element's index
  for(int i = 0; i < n; i++)
    indices[i] = 0;

  while (true)
  {
    // Print current combination
    for(int i = 0; i < n; i++)
      Console.Write(arr[i][indices[i]] + " ");

    Console.WriteLine();

    // Find the rightmost array
    // that has more elements
    // left after the current
    // element in that array
    int next = n - 1;
    while (next >= 0 &&
          (indices[next] + 1 >=
           arr[next].Count))
      next--;

    // No such array is found
    // so no more combinations left
    if (next < 0)
      return;

    // If found move to next
    // element in that array
    indices[next]++;

    // For all arrays to the right
    // of this array current index
    // again points to first element
    for(int i = next + 1; i < n; i++)
      indices[i] = 0;
  }
}

// Driver code
public static void Main(String[] args)
{
  // Initializing a vector
  // with 3 empty vectors
  List<int> []arr = new List<int>[3];
  for(int i = 0; i < arr.Length; i++)
    arr[i] = new List<int>();

  // Now entering data
  // [[1, 2, 3], [4], [5, 6]]
  arr[0].Add(1);
  arr[0].Add(2);
  arr[0].Add(3);
  arr[1].Add(4);
  arr[2].Add(5);
  arr[2].Add(6);

  print(arr);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to find combinations from n
// arrays such that one element from each
// array is present

// Function to print combinations that contain
// one element from each of the given arrays
function print(arr)
{

    // Number of arrays
    let n = arr.length;

    // To keep track of next element in
    // each of the n arrays
    let indices = new Array(n);

    // Initialize with first element's index
    for(let i = 0; i < n; i++)
        indices[i] = 0;

    while (true)
    {

        // Print current combination
        for(let i = 0; i < n; i++)
            document.write(
            arr[i][indices[i]] + " ");

        document.write("<br>");

        // Find the rightmost array that has more
        // elements left after the current element
        // in that array
        let next = n - 1;
        while (next >= 0 && (indices[next] + 1 >=
                                 arr[next].length))
            next--;

        // No such array is found so no more
        // combinations left
        if (next < 0)
            return;

        // If found move to next element in that
        // array
        indices[next]++;

        // For all arrays to the right of this
        // array current index again points to
        // first element
        for(let i = next + 1; i < n; i++)
            indices[i] = 0;
    }
}

// Driver code

// Initializing a vector with 3 empty vectors
let arr = new Array(3);
for(let i = 0; i < arr.length; i++)
    arr[i] = [];

// Now entering data
// [[1, 2, 3], [4], [5, 6]]
arr[0].push(1);
arr[0].push(2);
arr[0].push(3);
arr[1].push(4);
arr[2].push(5);
arr[2].push(6);

print(arr);

// This code is contributed by unknown2108

</script>
```

**输出:**

```
1 4 5
1 4 6
2 4 5
2 4 6
3 4 5
3 4 6
```

本文由 [**阿迪提·夏尔马 2**](https://auth.geeksforgeeks.org/profile.php?user=aditi sharma 2&list=practice) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。