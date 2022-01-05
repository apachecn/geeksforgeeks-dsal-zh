# 堆中的插入和删除

> 原文:[https://www . geeksforgeeks . org/堆中插入和删除/](https://www.geeksforgeeks.org/insertion-and-deletion-in-heaps/)

**堆中删除**

> 给定一个二进制堆和一个存在于给定堆中的元素。任务是从此堆中删除一个元素。

对堆的标准删除操作是删除堆根节点上的元素。也就是说，如果它是最大堆，标准删除操作将删除最大元素，如果它是最小堆，它将删除最小元素。

**删除的过程** :
由于删除堆中任意中间位置的元素代价很高，所以我们可以简单地用最后一个元素替换要删除的元素，删除堆中的最后一个元素。

*   用最后一个元素替换要删除的根或元素。
*   从堆中删除最后一个元素。
*   因为，最后一个元素现在被放置在根节点的位置。因此，它可能不遵循堆属性。因此，**将最后一个节点放在根的位置。**

插图:

```
Suppose the Heap is a Max-Heap as:
      10
    /    \
   5      3
  / \
 2   4

*The element to be deleted is root, i.e. 10.*

Process:
The last element is 4.

Step 1: Replace the last element with root, and delete it.
      4
    /    \
   5      3
  / 
 2   

Step 2: Heapify root.
Final Heap:
      5
    /    \
   4      3
  / 
 2   
```

**实施**:

## C++

```
// C++ program for implement deletion in Heaps

#include <iostream>

using namespace std;

// To heapify a subtree rooted with node i which is
// an index of arr[] and n is the size of heap
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

// Function to delete the root from Heap
void deleteRoot(int arr[], int& n)
{
    // Get the last element
    int lastElement = arr[n - 1];

    // Replace root with last element
    arr[0] = lastElement;

    // Decrease size of heap by 1
    n = n - 1;

    // heapify the root node
    heapify(arr, n, 0);
}

/* A utility function to print array of size n */
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << "\n";
}

// Driver Code
int main()
{
    // Array representation of Max-Heap
    //     10
    //    /  \
    //   5    3
    //  / \
    // 2   4
    int arr[] = { 10, 5, 3, 2, 4 };

    int n = sizeof(arr) / sizeof(arr[0]);

    deleteRoot(arr, n);

    printArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for implement deletion in Heaps
public class deletionHeap {

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

    // Function to delete the root from Heap
    static int deleteRoot(int arr[], int n)
    {
        // Get the last element
        int lastElement = arr[n - 1];

        // Replace root with first element
        arr[0] = lastElement;

        // Decrease size of heap by 1
        n = n - 1;

        // heapify the root node
        heapify(arr, n, 0);

        // return new size of Heap
        return n;
    }

    /* A utility function to print array of size N */
    static void printArray(int arr[], int n)
    {
        for (int i = 0; i < n; ++i)
            System.out.print(arr[i] + " ");

        System.out.println();
    }

    // Driver Code
    public static void main(String args[])
    {
        // Array representation of Max-Heap
        // 10
        //    /  \
        // 5    3
        //  / \
        // 2   4
        int arr[] = { 10, 5, 3, 2, 4 };

        int n = arr.length;

        n = deleteRoot(arr, n);

        printArray(arr, n);
    }
}
```

## C#

```
// C# program for implement deletion in Heaps
using System;

public class deletionHeap
{

    // To heapify a subtree rooted with node i which is
    // an index in arr[].Nn is size of heap
    static void heapify(int []arr, int n, int i)
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
        if (largest != i)
        {
            int swap = arr[i];
            arr[i] = arr[largest];
            arr[largest] = swap;

            // Recursively heapify the affected sub-tree
            heapify(arr, n, largest);
        }
    }

    // Function to delete the root from Heap
    static int deleteRoot(int []arr, int n)
    {
        // Get the last element
        int lastElement = arr[n - 1];

        // Replace root with first element
        arr[0] = lastElement;

        // Decrease size of heap by 1
        n = n - 1;

        // heapify the root node
        heapify(arr, n, 0);

        // return new size of Heap
        return n;
    }

    /* A utility function to print array of size N */
    static void printArray(int []arr, int n)
    {
        for (int i = 0; i < n; ++i)
            Console.Write(arr[i] + " ");

        Console.WriteLine();
    }

    // Driver Code
    public static void Main()
    {
        // Array representation of Max-Heap
        // 10
        // / \
        // 5 3
        // / \
        // 2 4
        int []arr = { 10, 5, 3, 2, 4 };
        int n = arr.Length;
        n = deleteRoot(arr, n);
        printArray(arr, n);
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>
    // Javascript program for implement deletion in Heaps

    // To heapify a subtree rooted with node i which is
    // an index in arr[].Nn is size of heap
    function heapify(arr, n, i)
    {
        let largest = i; // Initialize largest as root
        let l = 2 * i + 1; // left = 2*i + 1
        let r = 2 * i + 2; // right = 2*i + 2

        // If left child is larger than root
        if (l < n && arr[l] > arr[largest])
            largest = l;

        // If right child is larger than largest so far
        if (r < n && arr[r] > arr[largest])
            largest = r;

        // If largest is not root
        if (largest != i)
        {
            let swap = arr[i];
            arr[i] = arr[largest];
            arr[largest] = swap;

            // Recursively heapify the affected sub-tree
            heapify(arr, n, largest);
        }
    }

    // Function to delete the root from Heap
    function deleteRoot(arr, n)
    {
        // Get the last element
        let lastElement = arr[n - 1];

        // Replace root with first element
        arr[0] = lastElement;

        // Decrease size of heap by 1
        n = n - 1;

        // heapify the root node
        heapify(arr, n, 0);

        // return new size of Heap
        return n;
    }

    /* A utility function to print array of size N */
    function printArray(arr, n)
    {
        for (let i = 0; i < n; ++i)
            document.write(arr[i] + " ");

        document.write("</br>");
    }

    let arr = [ 10, 5, 3, 2, 4 ];
    let n = arr.length;
    n = deleteRoot(arr, n);
    printArray(arr, n);

// This code is contributed by divyeshrabdiya07.
</script>
```

## 蟒蛇 3

```
# Python 3 program for implement deletion in Heaps

# To heapify a subtree rooted with node i which is
# an index of arr[] and n is the size of heap
def heapify(arr, n, i):

    largest = i #Initialize largest as root
    l = 2 * i + 1 # left = 2*i + 1
    r = 2 * i + 2 # right = 2*i + 2

    #If left child is larger than root
    if (l < n and arr[l] > arr[largest]):
        largest = l

    #If right child is larger than largest so far
    if (r < n and arr[r] > arr[largest]):
        largest = r

    # If largest is not root
    if (largest != i):
        arr[i],arr[largest]=arr[largest],arr[i]

        #Recursively heapify the affected sub-tree
        heapify(arr, n, largest)

#Function to delete the root from Heap
def deleteRoot(arr):
    global n

    # Get the last element
    lastElement = arr[n - 1]

    # Replace root with last element
    arr[0] = lastElement

    # Decrease size of heap by 1
    n = n - 1

    # heapify the root node
    heapify(arr, n, 0)

# A utility function to print array of size n
def printArray(arr, n):

    for i in range(n):
        print(arr[i],end=" ")
    print()

# Driver Code
if __name__ == '__main__':

    # Array representation of Max-Heap
    #      10
    #     /  \
    #    5    3
    #   / \
    #  2   4
    arr = [ 10, 5, 3, 2, 4 ]

    n = len(arr)

    deleteRoot(arr)

    printArray(arr, n)
```

**Output:** 

```
5 4 3 2
```

**堆中插入**

插入操作也类似于删除过程。

> ***给定一个二进制堆和一个要添加到该堆的新元素。任务是将新元素插入到堆中，维护堆的属性。***

**插入过程**:可以按照上面讨论的类似方法将元素插入堆中进行删除。这个想法是:

*   首先将堆大小增加 1，以便它可以存储新元素。
*   在堆的末尾插入新元素。
*   这个新插入的元素可能会扭曲其父元素的堆属性。因此，为了保持堆的属性，**按照自下而上的方法堆化这个新插入的元素。**

插图:

```
Suppose the Heap is a Max-Heap as:
      10
    /    \
   5      3
  / \
 2   4

*The new element to be inserted is 15.*

***Process***:
Step 1: Insert the new element at the end.
      10
    /    \
   5      3
  / \    /
 2   4  15

Step 2: Heapify the new element following bottom-up 
        approach.
-> 15 is more than its parent 3, swap them.
       10
    /    \
   5      15
  / \    /
 2   4  3

-> 15 is again more than its parent 10, swap them.
       15
    /    \
   5      10
  / \    /
 2   4  3

Therefore, the final heap after insertion is:
       15
    /    \
   5      10
  / \    /
 2   4  3
```

**实施**:

## C++

```
// C++ program to insert new element to Heap

#include <iostream>
using namespace std;

#define MAX 1000 // Max size of Heap

// Function to heapify ith node in a Heap
// of size n following a Bottom-up approach
void heapify(int arr[], int n, int i)
{
    // Find parent
    int parent = (i - 1) / 2;

    if (arr[parent] > 0) {
        // For Max-Heap
        // If current node is greater than its parent
        // Swap both of them and call heapify again
        // for the parent
        if (arr[i] > arr[parent]) {
            swap(arr[i], arr[parent]);

            // Recursively heapify the parent node
            heapify(arr, n, parent);
        }
    }
}

// Function to insert a new node to the Heap
void insertNode(int arr[], int& n, int Key)
{
    // Increase the size of Heap by 1
    n = n + 1;

    // Insert the element at end of Heap
    arr[n - 1] = Key;

    // Heapify the new node following a
    // Bottom-up approach
    heapify(arr, n, n - 1);
}

// A utility function to print array of size n
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";

    cout << "\n";
}

// Driver Code
int main()
{
    // Array representation of Max-Heap
    // 10
    //    /  \
    // 5    3
    //  / \
    // 2   4
    int arr[MAX] = { 10, 5, 3, 2, 4 };

    int n = 5;

    int key = 15;

    insertNode(arr, n, key);

    printArray(arr, n);
    // Final Heap will be:
    // 15
    //    /   \
    // 5     10
    //  / \   /
    // 2   4 3
    return 0;
}
```

**Output:** 

```
15 5 10 2 4 3
```