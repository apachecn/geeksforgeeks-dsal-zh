# 删除两个最大的元素，如果它们不相等，则用它们的绝对差值来替换最后剩余的元素

> 原文:[https://www . geeksforgeeks . org/最后一个元素-通过删除两个最大的元素并通过它们不相等时的绝对差来替换剩余的元素/](https://www.geeksforgeeks.org/last-element-remaining-by-deleting-two-largest-elements-and-replacing-by-their-absolute-difference-if-they-are-unequal/)

给定一个由 **N** 元素组成的[阵](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是执行以下操作:

*   从数组中选择两个最大的元素并移除这些元素。如果元素不相等，则将元素的绝对差插入数组。
*   执行上述操作，直到数组中有 1 个或没有元素。如果数组只剩下一个元素，那么打印那个元素，否则打印“-1”。

**示例:**

> **输入:** arr[] = { 3，5，2，7 }
> **输出:** 1
> **说明:**
> 最大的两个元素是 7 和 5。扔掉它们。因为两者不相等，所以在数组中插入 7–5 = 2。因此，arr[] = { 3，2，2 }
> 最大的两个元素是 3 和 2。扔掉它们。因为两者不相等，所以在数组中插入 3–2 = 1。因此，arr[] = { 1，2 }
> 两个最大的元素是 2 和 1。扔掉它们。因为两者不相等，所以在数组中插入 2–1 = 1。因此，arr[] = { 1 }
> 剩下的唯一元素是 1。打印剩下的唯一元素的值。
> 
> **输入:** arr[] = { 3，3 }
> **输出:** -1
> **说明:**
> 最大的两个元素是 3 和 3。扔掉它们。现在数组没有元素了。所以，打印-1。

**方法:**为了解决上述问题，我们将使用[优先级队列数据结构](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)。以下是步骤:

1.  将所有数组元素插入优先级队列。
2.  因为优先级队列是基于[最大堆](https://www.geeksforgeeks.org/max-heap-in-java/)的实现。因此，从其中移除元素会产生最大元素。
3.  直到优先级队列的大小不小于 2，从中删除两个元素(比如 **X & Y** ，并执行以下操作:
    *   如果 **X 和 Y** 不相同，则将 **X 和 Y** 的绝对值插入优先级队列。
    *   否则返回步骤 3。
4.  如果堆只有一个元素，那么打印该元素。
5.  否则打印“-1”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the remaining element
int final_element(int arr[], int n)
{

    // Priority queue can be used
    // to construct max-heap
    priority_queue<int> heap;

    // Insert all element of arr[]
    // into priority queue
    for (int i = 0; i < n; i++)
        heap.push(arr[i]);

    // Perform operation until heap
    // size becomes 0 or 1
    while (heap.size() > 1) {

        // Remove largest element
        int X = heap.top();
        heap.pop();

        // Remove 2nd largest element
        int Y = heap.top();
        heap.pop();

        // If extracted element
        // are not equal
        if (X != Y) {

            // Find X - Y and push
            // it to heap
            int diff = abs(X - Y);
            heap.push(diff);
        }
    }

    // If heap size is 1, then
    // print the remaining element
    if (heap.size() == 1) {

        cout << heap.top();
    }

    // Else print "-1"
    else {
        cout << "-1";
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 3, 5, 2, 7 };

    // Size of array arr[]
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    final_element(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.Collections;
import java.util.*;

class GFG{

// Function to print the remaining element    
static public int final_element(Integer[] arr, int n)
{
    if(arr == null)
    {
        return 0;
    }

    // Priority queue can be used
    // to construct max-heap
    PriorityQueue<Integer> heap = new
    PriorityQueue<Integer>(Collections.reverseOrder());

    // Insert all element of arr[]
    // into priority queue
    for(int i = 0; i < n; i++)
    {
       heap.offer(arr[i]);
    }

    // Perform operation until heap
    // size becomes 0 or 1
    while (heap.size() > 1)
    {

        // Remove largest element
        int X = heap.poll();

        // Remove 2nd largest element
        int Y = heap.poll();

        // If extracted element
        // are not equal
        if (X != Y)
        {
            // Find X - Y and push
            // it to heap
            int diff = Math.abs(X - Y);
            heap.offer(diff);
        }
    }

    // If heap size is 1, then
    // print the remaining element
    // Else print "-1"
    return heap.size() == 1 ? heap.poll() : -1;
}

// Driver code
public static void main (String[] args)
{
    // Given array arr[]
    Integer arr[] = new Integer[] { 3, 5, 2, 7};

    // Size of array arr[]
    int n = arr.length;

    // Function Call
    System.out.println(final_element(arr, n)); 
}
}

// This code is contributed by deepika_sharma
```

## 蟒蛇 3

```
# Python3 program for the above approach
from queue import PriorityQueue

# Function to print the remaining element
def final_element(arr, n):

    # Priority queue can be used
    # to construct max-heap
    heap = PriorityQueue()

    # Insert all element of
    # arr[] into priority queue.
    # Default priority queue in Python
    # is min-heap so use -1*arr[i]
    for i in range(n):
        heap.put(-1 * arr[i])

    # Perform operation until heap
    # size becomes 0 or 1
    while (heap.qsize() > 1):

        # Remove largest element
        X = -1 * heap.get()

        # Remove 2nd largest element
        Y = -1 * heap.get()

        # If extracted elements
        # are not equal
        if (X != Y):

            # Find X - Y and push
            # it to heap
            diff = abs(X - Y)
            heap.put(-1 * diff)

    # If heap size is 1, then
    # print the remaining element
    if (heap.qsize() == 1):
        print(-1 * heap.get())

    # Else print "-1"
    else:
        print("-1")

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 3, 5, 2, 7 ]

    # Size of array arr[]
    n = len(arr)

    # Function call
    final_element(arr, n)

# This code is contributed by himanshu77
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the remaining element
static void final_element(int[] arr, int n)
{

    // Priority queue can be used
    // to construct max-heap
    List<int> heap = new List<int>();

    // Insert all element of arr[]
    // into priority queue
    for(int i = 0; i < n; i++)
        heap.Add(arr[i]);

    // Perform operation until heap
    // size becomes 0 or 1
    while (heap.Count > 1)
    {

        // Remove largest element
        heap.Sort();
        heap.Reverse();
        int X = heap[0];
        heap.RemoveAt(0);

        // Remove 2nd largest element
        int Y = heap[0];
        heap.RemoveAt(0);

        // If extracted element
        // are not equal
        if (X != Y)
        {

            // Find X - Y and push
            // it to heap
            int diff = Math.Abs(X - Y);
            heap.Add(diff);
        }
    }

    // If heap size is 1, then
    // print the remaining element
    if (heap.Count == 1)
    {
        heap.Sort();
        heap.Reverse();
        Console.Write(heap[0]);
    }

    // Else print "-1"
    else
    {
        Console.Write(-1);
    }
}

// Driver code
static void Main()
{

    // Given array arr[]
    int[] arr = { 3, 5, 2, 7 };

    // Size of array arr[]
    int n = arr.Length;

    // Function Call
    final_element(arr, n);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print the remaining element
function final_element(arr, n)
{

    // Priority queue can be used
    // to construct max-heap
    var heap = [];

    // Insert all element of arr[]
    // into priority queue
    for (var i = 0; i < n; i++)
        heap.push(arr[i]);

    heap.sort((a,b)=>a-b);
    // Perform operation until heap
    // size becomes 0 or 1
    while (heap.length > 1) {

        // Remove largest element
        var X = heap[heap.length-1];
        heap.pop();

        // Remove 2nd largest element
        var Y =  heap[heap.length-1];
        heap.pop();

        // If extracted element
        // are not equal
        if (X != Y) {

            // Find X - Y and push
            // it to heap
            var diff = Math.abs(X - Y);
            heap.push(diff);
        }
        heap.sort((a,b)=>a-b);
    }

    // If heap size is 1, then
    // print the remaining element
    if (heap.length == 1) {
        document.write(heap[heap.length-1]);
    }

    // Else print "-1"
    else {
        document.write("-1");
    }
}

// Driver Code
// Given array arr[]
var arr = [3, 5, 2, 7 ];

// Size of array arr[]
var n = arr.length;

// Function Call
final_element(arr, n);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
1
```

**时间复杂度:***O(N * log(N))*
T5】辅助空间复杂度: *O(N)*