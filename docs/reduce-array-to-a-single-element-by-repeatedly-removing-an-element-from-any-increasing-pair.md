# 通过从任何递增对中重复移除一个元素，将数组缩减为单个元素

> 原文:[https://www . geeksforgeeks . org/通过从任意递增对中重复移除元素来将数组减少为单个元素/](https://www.geeksforgeeks.org/reduce-array-to-a-single-element-by-repeatedly-removing-an-element-from-any-increasing-pair/)

给定一个由范围**【1，N】**中的排列组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过执行以下操作来检查给定数组是否可以简化为单个非零元素:

> 选择索引 **i** 和 **j** ，使得 **i < j** 和**arr【I】<arr【j】**并将两个元素之一转换为 **0** 。

如果有可能将数组简化为单个元素，则在每次操作中打印**“是”**后跟随所选索引以及**替换元素**的索引。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = {2，4，6，1，3，5}
> **输出:**
> 是
> 0 1 1
> 0 2
> 3 4 3
> 0 4
> 0 5 5
> **说明:**
> 在第一个操作中，选择索引 0 和 1 处的元素 2 和 4。将索引 1 处的元素 4 转换为 0，arr[] = {2，0，6，1，3，5}
> 在第二个操作中，选择索引 0 和 2 处的元素 2 和 6。将索引 2 处的元素 6 转换为 0，arr[] = {2，0，0，1，3，5}
> 在第三个操作中，选择索引 3 和 4 处的元素 1 和 3。将索引 3 处的元素 1 转换为 0，arr[] = {2，0，0，0，3，5}
> 在第四个操作中，选择索引 0 和 4 处的元素 2 和 3。将索引 4 处的元素 3 转换为 0，arr[] = {2，0，0，0，0，5}
> 在第五个操作中，选择索引 0 和 5 处的元素 2 和 5。将索引 5 处的元素 5 转换为 0，arr[] = {2，0，0，0，0，0}
> 因此，数组在 5 次运算中被简化为单个正元素。
> 
> **输入:** arr[] = {2，3，1}
> **输出:**否
> **说明:**
> 没有给定数组可以转换成单个元素的操作集。

**方法:**思路是先将所有元素从索引**【1，N–2】**转换为 **0** ，然后在最后一次移动中消除**第 0**或**(N–1)**元素中的一个，得到**单例**数组。以下是解决问题的步骤:

1.  选择一组有效的索引，可以对其执行给定的操作。
2.  现在要选择要转换成 **0** 的元素，请检查以下条件:
    *   如果数组的第**0**索引是这些索引的一部分，那么将另一个索引处的元素转换为 **0** 。
    *   如果**第 0 个**指数不是所选指数的一部分，则将两个元素中较小的一个替换为 **0** 。
3.  继续此过程，直到阵列中保留一个**单个**正元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the order of
// indices of converted numbers
void order_of_removal(int a[], int n)
{
    // Stores the values of indices
    // with numbers > first index
    queue<int> greater_indices;

    int first = a[0];

    // Stores the index of the closest
    // consecutive number to index 0
    int previous_index = 0;

    // Push the indices into the queue
    for (int i = 1; i < n; i++) {
        if (a[i] > first)
            greater_indices.push(i);
    }

    // Traverse the queue
    while (greater_indices.size() > 0) {

        // Stores the index of the
        // closest number > arr[0]
        int index = greater_indices.front();

        greater_indices.pop();

        int to_remove = index;

        // Remove elements present in
        // indices [1, to_remove - 1]
        while (--to_remove > previous_index) {

            cout << to_remove << " "
                 << index << " "
                 << to_remove << endl;
        }

        cout << 0 << " " << index << " "
             << index << endl;

        // Update the previous_index
        // to index
        previous_index = index;
    }
}

// Function to check if array arr[] can
// be reduced to single element or not
void canReduced(int arr[], int N)
{
    // If array element can't be
    // reduced to single element
    if (arr[0] > arr[N - 1]) {
        cout << "No" << endl;
    }

    // Otherwise find the order
    else {
        cout << "Yes" << endl;
        order_of_removal(arr, N);
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 3, 4 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    canReduced(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print the order of
// indices of converted numbers
public static void order_of_removal(int[] a, int n)
{

    // Stores the values of indices
    // with numbers > first index
    Queue<Integer> greater_indices = new LinkedList<>();

    int first = a[0];

    // Stores the index of the closest
    // consecutive number to index 0
    int previous_index = 0;

    // Push the indices into the queue
    for(int i = 1; i < n; i++)
    {
        if (a[i] > first)
            greater_indices.add(i);
    }

    // Traverse the queue
    while (greater_indices.size() > 0)
    {

        // Stores the index of the
        // closest number > arr[0]
        int index = greater_indices.peek();

        greater_indices.remove();

        int to_remove = index;

        // Remove elements present in
        // indices [1, to_remove - 1]
        while (--to_remove > previous_index)
        {
            System.out.println(to_remove + " " +
                                   index + " " +
                                   to_remove);
        }

        System.out.println(0 + " " + index +
                               " " + index);

        // Update the previous_index
        // to index
        previous_index = index;
    }
}

// Function to check if array arr[] can
// be reduced to single element or not
public static void canReduced(int[] arr, int N)
{

    // If array element can't be
    // reduced to single element
    if (arr[0] > arr[N - 1])
    {
        System.out.println("No");
    }

    // Otherwise find the order
    else
    {
        System.out.println("Yes");
        order_of_removal(arr, N);
    }
} 

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 1, 2, 3, 4 };

    int N = arr.length;

    // Function call
    canReduced(arr, N);
}
}

// This code is contributed divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the order of
# indices of converted numbers
def order_of_removal(a, n) :

    # Stores the values of indices
    # with numbers > first index
    greater_indices = []

    first = a[0]

    # Stores the index of the closest
    # consecutive number to index 0
    previous_index = 0

    # Push the indices into the queue
    for i in range(1, n) :
        if (a[i] > first) :
            greater_indices.append(i)

    # Traverse the queue
    while (len(greater_indices) > 0) :

        # Stores the index of the
        # closest number > arr[0]
        index = greater_indices[0];

        greater_indices.pop(0)

        to_remove = index

        # Remove elements present in
        # indices [1, to_remove - 1]
        to_remove =- 1
        while (to_remove > previous_index) :

            print(to_remove, index, to_remove)

        print(0, index, index)

        # Update the previous_index
        # to index
        previous_index = index

# Function to check if array arr[] can
# be reduced to single element or not
def canReduced(arr, N) :

    # If array element can't be
    # reduced to single element
    if (arr[0] > arr[N - 1]) :
        print("No")

    # Otherwise find the order
    else :
        print("Yes")
        order_of_removal(arr, N)

# Given array arr[]
arr = [ 1, 2, 3, 4 ]

N = len(arr)

# Function Call
canReduced(arr, N)

# This code is contributed by divyesh072019
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to print the order of
// indices of converted numbers
public static void order_of_removal(int[] a,
                                    int n)
{
  // Stores the values of indices
  // with numbers > first index
  Queue<int> greater_indices = new Queue<int>();

  int first = a[0];

  // Stores the index of the closest
  // consecutive number to index 0
  int previous_index = 0;

  // Push the indices into the queue
  for(int i = 1; i < n; i++)
  {
    if (a[i] > first)
      greater_indices.Enqueue(i);
  }

  // Traverse the queue
  while (greater_indices.Count > 0)
  {
    // Stores the index of the
    // closest number > arr[0]
    int index = greater_indices.Peek();

    greater_indices.Dequeue();

    int to_remove = index;

    // Remove elements present in
    // indices [1, to_remove - 1]
    while (--to_remove > previous_index)
    {
      Console.WriteLine(to_remove + " " +
                        index + " " + to_remove);
    }

    Console.WriteLine(0 + " " + index +
                      " " + index);

    // Update the previous_index
    // to index
    previous_index = index;
  }
}

// Function to check if array []arr can
// be reduced to single element or not
public static void canReduced(int[] arr,
                              int N)
{
  // If array element can't be
  // reduced to single element
  if (arr[0] > arr[N - 1])
  {
    Console.WriteLine("No");
  }

  // Otherwise find the order
  else
  {
    Console.WriteLine("Yes");
    order_of_removal(arr, N);
  }
} 

// Driver Code
public static void Main(String[] args)
{
  // Given array []arr
  int []arr = {1, 2, 3, 4};

  int N = arr.Length;

  // Function call
  canReduced(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
      // JavaScript program for
      // the above approach
      // Function to print the order of
      // indices of converted numbers
      function order_of_removal(a, n) {
        // Stores the values of indices
        // with numbers > first index
        var greater_indices = [];

        var first = a[0];

        // Stores the index of the closest
        // consecutive number to index 0
        var previous_index = 0;

        // Push the indices into the queue
        for (var i = 1; i < n; i++) {
          if (a[i] > first) greater_indices.push(i);
        }

        // Traverse the queue
        while (greater_indices.length > 0) {
          // Stores the index of the
          // closest number > arr[0]
          var index = greater_indices[0];

          greater_indices.shift();

          var to_remove = index;

          // Remove elements present in
          // indices [1, to_remove - 1]
          to_remove -= 1;
          while (to_remove > previous_index) {
            document.write(to_remove + " " + index + " " + to_remove + "<br>");
          }

          document.write(0 + " " + index + " " + index + "<br>");

          // Update the previous_index
          // to index
          previous_index = index;
        }
      }

      // Function to check if array []arr can
      // be reduced to single element or not
      function canReduced(arr, N) {
        // If array element can't be
        // reduced to single element
        if (arr[0] > arr[N - 1]) {
          document.write("No" + "<br>");
        }

        // Otherwise find the order
        else {
          document.write("Yes" + "<br>");
          order_of_removal(arr, N);
        }
      }

      // Driver Code
      // Given array []arr
      var arr = [1, 2, 3, 4];

      var N = arr.length;

      // Function call
      canReduced(arr, N);

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
Yes
0 1 1
0 2 2
0 3 3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)