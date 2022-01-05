# 从数组构建堆

> 原文:[https://www.geeksforgeeks.org/building-heap-from-array/](https://www.geeksforgeeks.org/building-heap-from-array/)

给定一个由 N 个元素组成的数组。任务是从给定的数组构建二进制堆。堆可以是最大堆或最小堆。
**例** :

```
Input: arr[] = {4, 10, 3, 5, 1}
Output: Corresponding Max-Heap:
       10
     /   \
    5     3
   /  \
  4    1

Input: arr[] = {1, 3, 5, 4, 6, 13, 10, 9, 8, 15, 17}
Output: Corresponding Max-Heap:
                 17
              /      \
            15         13
          /    \      /  \
         9      6    5   10
        / \    /  \
       4   8  3    1
```

假设给定的输入元素是:4，10，3，5，1。
这个元素数组[4，10，3，5，1]对应的完整二叉树为:

```
       4
     /   \
    10    3
   /  \
  5    1

Note:
Root is at index 0 in array.
Left child of i-th node is at (2*i + 1)th index.
Right child of i-th node is at (2*i + 2)th index.
Parent of i-th node is at (i-1)/2 index.
```

**简单方法**:假设，我们需要从上面给定的数组元素构建一个 Max-Heap。可以清楚地看到，上面形成的完整二叉树并不遵循 Heap 属性。因此，我们的想法是按照自上而下的方法，以相反的级别顺序将数组形成的完整二叉树堆起来。
即先 heapify，层次顺序遍历树的最后一个节点，然后 heapify 第二个最后一个节点，以此类推。
**时间复杂度:**堆单个节点需要 O(log N)个时间复杂度，其中 N 是节点总数。因此，构建整个堆需要 N 次堆操作，总时间复杂度为 **O(N*logN)** 。
实际上，根据实现情况，构建一个堆需要 O(n)个时间，这可以在这里看到。
**优化方法**:上述方法可以通过观察叶节点不需要*堆化*的事实来优化，因为它们已经遵循堆属性。此外，完整二叉树的数组表示包含树的级别顺序遍历。
所以思路是找到最后一个非叶节点的位置，按逆序执行每个非叶节点的 **heapify** 操作。

```
Last non-leaf node = parent of last-node.
or, Last non-leaf node = parent of node at (n-1)th index.
or, Last non-leaf node = Node at index ((n-1) - 1)/2.
                       = (n/2) - 1.
```

**插图** :

```
Array = {1, 3, 5, 4, 6, 13, 10, 9, 8, 15, 17}

Corresponding Complete Binary Tree is:
                 1
              /     \
            3         5
         /    \     /  \
        4      6   13  10
       / \    / \
      9   8  15 17

***The task to build a Max-Heap from above array***.

Total Nodes = 11.
Last Non-leaf node index = (11/2) - 1 = 4.
Therefore, last non-leaf node = 6.

To build the heap, heapify only the nodes:
[1, 3, 5, 4, 6] in reverse order.

Heapify 6: Swap 6 and 17.
                 1
              /     \
            3         5
         /    \      /  \
        4      17   13  10
       / \    /  \
      9   8  15   6

Heapify 4: Swap 4 and 9.
                 1
              /     \
            3         5
         /    \      /  \
        9      17   13  10
       / \    /  \
      4   8  15   6

Heapify 5: Swap 13 and 5.
                 1
              /     \
            3         13
         /    \      /  \
        9      17   5   10
       / \    /  \
      4   8  15   6

Heapify 3: First Swap 3 and 17, again swap 3 and 15.
                 1
              /     \
            17         13
          /    \      /  \
         9      15   5   10
        / \    /  \
       4   8  3   6

Heapify 1: First Swap 1 and 17, again swap 1 and 15, 
           finally swap 1 and 6.
                 17
              /      \
            15         13
          /    \      /  \
         9      6    5   10
        / \    /  \
       4   8  3    1
```

**实施** :

## C++

```
// C++ program for building Heap from Array

#include <iostream>

using namespace std;

// To heapify a subtree rooted with node i which is
// an index in arr[]. N is size of heap
void heapify(int arr[], int n, int i)
{
    int largest = i; // Initialize largest as root
    int l = 2 * i + 1; // left = 2*i + 1
    int r = 2 * i + 2; // right = 2*i + 2

    // If left child is larger than root
    if (l < n && arr[l] > arr[largest])
        largest = l;

    // If right child is larger than largest so far
    if (r < n && arr[r] > arr[largest])
        largest = r;

    // If largest is not root
    if (largest != i) {
        swap(arr[i], arr[largest]);

        // Recursively heapify the affected sub-tree
        heapify(arr, n, largest);
    }
}

// Function to build a Max-Heap from the given array
void buildHeap(int arr[], int n)
{
    // Index of last non-leaf node
    int startIdx = (n / 2) - 1;

    // Perform reverse level order traversal
    // from last non-leaf node and heapify
    // each node
    for (int i = startIdx; i >= 0; i--) {
        heapify(arr, n, i);
    }
}

// A utility function to print the array
// representation of Heap
void printHeap(int arr[], int n)
{
    cout << "Array representation of Heap is:\n";

    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << "\n";
}

// Driver Code
int main()
{
    // Binary Tree Representation
    // of input array
    //                 1
    //           /     \
    //            3         5
    //      /    \     /  \
    //        4      6   13  10
    //    / \    / \
    //      9   8  15 17
    int arr[] = { 1, 3, 5, 4, 6, 13, 10, 9, 8, 15, 17 };

    int n = sizeof(arr) / sizeof(arr[0]);

    buildHeap(arr, n);

    printHeap(arr, n);
    // Final Heap:
    //                 17
    //           /      \
    //             15         13
    //       /    \      /  \
    //         9      6    5   10
    //     / \    /  \
    //       4   8  3    1

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for building Heap from Array

public class BuildHeap {

    // To heapify a subtree rooted with node i which is
    // an index in arr[].Nn is size of heap
    static void heapify(int arr[], int n, int i)
    {
        int largest = i; // Initialize largest as root
        int l = 2 * i + 1; // left = 2*i + 1
        int r = 2 * i + 2; // right = 2*i + 2

        // If left child is larger than root
        if (l < n && arr[l] > arr[largest])
            largest = l;

        // If right child is larger than largest so far
        if (r < n && arr[r] > arr[largest])
            largest = r;

        // If largest is not root
        if (largest != i) {
            int swap = arr[i];
            arr[i] = arr[largest];
            arr[largest] = swap;

            // Recursively heapify the affected sub-tree
            heapify(arr, n, largest);
        }
    }

    // Function to build a Max-Heap from the Array
    static void buildHeap(int arr[], int n)
    {
        // Index of last non-leaf node
        int startIdx = (n / 2) - 1;

        // Perform reverse level order traversal
        // from last non-leaf node and heapify
        // each node
        for (int i = startIdx; i >= 0; i--) {
            heapify(arr, n, i);
        }
    }

    // A utility function to print the array
    // representation of Heap
    static void printHeap(int arr[], int n)
    {
        System.out.println(
            "Array representation of Heap is:");

        for (int i = 0; i < n; ++i)
            System.out.print(arr[i] + " ");

        System.out.println();
    }

    // Driver Code
    public static void main(String args[])
    {
        // Binary Tree Representation
        // of input array
        // 1
        //           /     \
        // 3         5
        //      /    \     /  \
        // 4      6   13  10
        //    / \    / \
        // 9   8  15 17
        int arr[] = { 1, 3, 5, 4, 6, 13, 10, 9, 8, 15, 17 };

        int n = arr.length;

        buildHeap(arr, n);

        printHeap(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program for building Heap from Array

# To heapify a subtree rooted with node i
# which is an index in arr[]. N is size of heap

def heapify(arr, n, i):

    largest = i  # Initialize largest as root
    l = 2 * i + 1  # left = 2*i + 1
    r = 2 * i + 2  # right = 2*i + 2

    # If left child is larger than root
    if l < n and arr[l] > arr[largest]:
        largest = l

    # If right child is larger than largest so far
    if r < n and arr[r] > arr[largest]:
        largest = r

    # If largest is not root
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]

        # Recursively heapify the affected sub-tree
        heapify(arr, n, largest)

# Function to build a Max-Heap from the given array

def buildHeap(arr, n):

    # Index of last non-leaf node
    startIdx = n // 2 - 1

    # Perform reverse level order traversal
    # from last non-leaf node and heapify
    # each node
    for i in range(startIdx, -1, -1):
        heapify(arr, n, i)

# A utility function to print the array
# representation of Heap

def printHeap(arr, n):
    print("Array representation of Heap is:")

    for i in range(n):
        print(arr[i], end=" ")
    print()

# Driver Code
if __name__ == '__main__':

    # Binary Tree Representation
    # of input array
    # 1
    #         /     \
    # 3         5
    #     / \     / \
    # 4     6 13 10
    # / \ / \
    # 9 8 15 17
    arr = [1, 3, 5, 4, 6, 13,
           10, 9, 8, 15, 17]

    n = len(arr)

    buildHeap(arr, n)

    printHeap(arr, n)

    # Final Heap:
    # 17
    #         /     \
    # 15         13
    #     / \     / \
    # 9     6 5 10
    #     / \ / \
    # 4 8 3 1

# This code is contributed by Princi Singh
```

## C#

```
// C# program for building Heap from Array
using System;

public class BuildHeap {

    // To heapify a subtree rooted with node i which is
    // an index in arr[].Nn is size of heap
    static void heapify(int[] arr, int n, int i)
    {
        int largest = i; // Initialize largest as root
        int l = 2 * i + 1; // left = 2*i + 1
        int r = 2 * i + 2; // right = 2*i + 2

        // If left child is larger than root
        if (l < n && arr[l] > arr[largest])
            largest = l;

        // If right child is larger than largest so far
        if (r < n && arr[r] > arr[largest])
            largest = r;

        // If largest is not root
        if (largest != i) {
            int swap = arr[i];
            arr[i] = arr[largest];
            arr[largest] = swap;

            // Recursively heapify the affected sub-tree
            heapify(arr, n, largest);
        }
    }

    // Function to build a Max-Heap from the Array
    static void buildHeap(int[] arr, int n)
    {
        // Index of last non-leaf node
        int startIdx = (n / 2) - 1;

        // Perform reverse level order traversal
        // from last non-leaf node and heapify
        // each node
        for (int i = startIdx; i >= 0; i--) {
            heapify(arr, n, i);
        }
    }

    // A utility function to print the array
    // representation of Heap
    static void printHeap(int[] arr, int n)
    {
        Console.WriteLine(
            "Array representation of Heap is:");

        for (int i = 0; i < n; ++i)
            Console.Write(arr[i] + " ");

        Console.WriteLine();
    }

    // Driver Code
    public static void Main()
    {
        // Binary Tree Representation
        // of input array
        // 1
        //     / \
        // 3         5
        // / \     / \
        // 4     6 13 10
        // / \ / \
        // 9 8 15 17
        int[] arr = { 1, 3, 5, 4, 6, 13, 10, 9, 8, 15, 17 };

        int n = arr.Length;

        buildHeap(arr, n);

        printHeap(arr, n);
    }
}

// This code is contributed by Ryuga
```

**Output:** 

```
Array representation of Heap is:
17 15 13 9 6 5 10 4 8 3 1
```