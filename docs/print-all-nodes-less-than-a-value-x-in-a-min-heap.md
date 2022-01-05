# 打印最小堆中小于 x 值的所有节点。

> 原文:[https://www . geesforgeks . org/print-all-nodes-小于值-x-in-a-min-heap/](https://www.geeksforgeeks.org/print-all-nodes-less-than-a-value-x-in-a-min-heap/)

给定一个[二进制最小堆](https://www.geeksforgeeks.org/binary-heap/)和值 x，打印所有值小于给定值 x 的二进制堆节点。

```
Examples : Consider the below min heap as
        common input two both below examples.
                   2
                /     \
               3        15
            /    \     / \
           5       4  45  80
          / \     / \
         6   150 77 120

Input  : x = 15        
Output : 2 3 5 6 4

Input  : x = 80
Output : 2 3 5 6 4 77 15 45

```

想法是对给定的二进制堆进行[前序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。在进行前序遍历时，如果一个节点的值大于给定值 x，我们返回到前面的递归调用。因为最小堆中的所有子节点都大于父节点。否则，我们打印当前节点并为其子节点重现。

## c++

```
// A C++ program to print all values
// smaller than a given value in Binary
// Heap
#include <bits/stdc++.h>
using namespace std;

// A class for Min Heap
class MinHeap {
    // pointer to array of elements in heap
    int* harr;

    // maximum possible size of min heap
    int capacity;
    int heap_size; // Current no. of elements.
public:
    // Constructor
    MinHeap(int capacity);

    // to heapify a subtree with root at
    // given index
    void MinHeapify(int);

    int parent(int i) { return (i - 1) / 2; }
    int left(int i) { return (2 * i + 1); }
    int right(int i) { return (2 * i + 2); }

    // Inserts a new key 'k'
    void insertKey(int k);

    // Function to print all nodes smaller than k
    void printSmallerThan(int k, int pos);
};

// Function to print all elements smaller than k
void MinHeap::printSmallerThan(int x, int pos = 0)
{
    /* Make sure item exists */
    if (pos >= heap_size)
        return;

    if (harr[pos] >= x) {
        /* Skip this node and its descendants,
          as they are all >= x . */
        return;
    }

    cout << harr[pos] << " ";

    printSmallerThan(x, left(pos));
    printSmallerThan(x, right(pos));
}

// Constructor: Builds a heap from a given
// array a[] of given size
MinHeap::MinHeap(int cap)
{
    heap_size = 0;
    capacity = cap;
    harr = new int[cap];
}

// Inserts a new key 'k'
void MinHeap::insertKey(int k)
{
    if (heap_size == capacity) {
        cout << "\nOverflow: Could not insertKey\n";
        return;
    }

    // First insert the new key at the end
    heap_size++;
    int i = heap_size - 1;
    harr[i] = k;

    // Fix the min heap property if it is violated
    while (i != 0 && harr[parent(i)] > harr[i]) {
        swap(harr[i], harr[parent(i)]);
        i = parent(i);
    }
}

// A recursive method to heapify a subtree with
// root at given index. This method assumes that
// the subtrees are already heapified
void MinHeap::MinHeapify(int i)
{
    int l = left(i);
    int r = right(i);
    int smallest = i;
    if (l < heap_size && harr[l] < harr[i])
        smallest = l;
    if (r < heap_size && harr[r] < harr[smallest])
        smallest = r;
    if (smallest != i) {
        swap(harr[i], harr[smallest]);
        MinHeapify(smallest);
    }
}

// Driver program to test above functions
int main()
{
    MinHeap h(50);
    h.insertKey(3);
    h.insertKey(2);
    h.insertKey(15);
    h.insertKey(5);
    h.insertKey(4);
    h.insertKey(45);
    h.insertKey(80);
    h.insertKey(6);
    h.insertKey(150);
    h.insertKey(77);
    h.insertKey(120);

    // Print all nodes smaller than 100.
    int x = 100;
    h.printSmallerThan(x);

    return 0;
}
```

## Java

```
// A Java program to print all values
// smaller than a given value in Binary
// Heap

// A class for Min Heap
class MinHeap {
    // array of elements in heap
    int[] harr;

    // maximum possible size of min heap
    int capacity;
    int heap_size; // Current no. of elements.

    int parent(int i) { return (i - 1) / 2; }
    int left(int i) { return (2 * i + 1); }
    int right(int i) { return (2 * i + 2); }

    // Function to print all elements smaller than k
    void printSmallerThan(int x, int pos)
    {
        /* Make sure item exists */
        if (pos >= heap_size)
            return;

        if (harr[pos] >= x) {
            /* Skip this node and its descendants,
            as they are all >= x . */
            return;
        }

        System.out.print(harr[pos] + " ");

        printSmallerThan(x, left(pos));
        printSmallerThan(x, right(pos));
    }

    // Constructor: Builds a heap of given size
    public MinHeap(int cap)
    {
        heap_size = 0;
        capacity = cap;
        harr = new int[cap];
    }

    // Inserts a new key 'k'
    void insertKey(int k)
    {
        if (heap_size == capacity) {
            System.out.println("Overflow: Could not insertKey");
            return;
        }

        // First insert the new key at the end
        heap_size++;
        int i = heap_size - 1;
        harr[i] = k;

        // Fix the min heap property if it is violated
        while (i != 0 && harr[parent(i)] > harr[i]) {
            swap(i, parent(i));
            i = parent(i);
        }
    }

    // A utility function to swap two elements
    void swap(int x, int y)
    {
        int temp = harr[x];
        harr[x] = harr[y];
        harr[y] = temp;
    }

    // Driver code
    public static void main(String[] args)
    {
        MinHeap h = new MinHeap(15);
        h.insertKey(3);
        h.insertKey(2);
        h.insertKey(15);
        h.insertKey(5);
        h.insertKey(4);
        h.insertKey(45);
        h.insertKey(80);
        h.insertKey(6);
        h.insertKey(150);
        h.insertKey(77);
        h.insertKey(120);

        // Print all nodes smaller than 100.
        int x = 100;
        h.printSmallerThan(x, 0);
    }
};

// This code is contributed by shubham96301
```

## c#

```
// A C# program to print all values
// smaller than a given value in 
// Binary Heap
using System;

// A class for Min Heap
public class MinHeap
{
    // array of elements in heap
    int[] harr;

    // maximum possible size of min heap
    int capacity;

    // Current no. of elements
    int heap_size; 

    int parent(int i) { return (i - 1) / 2; }
    int left(int i) { return (2 * i + 1); }
    int right(int i) { return (2 * i + 2); }

    // Function to print 
    // all elements smaller than k
    void printSmallerThan(int x, int pos)
    {
        /* Make sure item exists */
        if (pos >= heap_size)
            return;

        if (harr[pos] >= x) 
        {
            /* Skip this node and its descendants,
            as they are all >= x . */
            return;
        }

        Console.Write(harr[pos] + " ");

        printSmallerThan(x, left(pos));
        printSmallerThan(x, right(pos));
    }

    // Constructor: Builds a heap of given size
    public MinHeap(int cap)
    {
        heap_size = 0;
        capacity = cap;
        harr = new int[cap];
    }

    // Inserts a new key 'k'
    void insertKey(int k)
    {
        if (heap_size == capacity) 
        {
            Console.WriteLine("Overflow: Could not insertKey");
            return;
        }

        // First insert the new key at the end
        heap_size++;
        int i = heap_size - 1;
        harr[i] = k;

        // Fix the min heap property 
        // if it is violated
        while (i != 0 && 
               harr[parent(i)] > harr[i])
        {
            swap(i, parent(i));
            i = parent(i);
        }
    }

    // A utility function to swap two elements
    void swap(int x, int y)
    {
        int temp = harr[x];
        harr[x] = harr[y];
        harr[y] = temp;
    }

    // Driver code
    public static void Main(String[] args)
    {
        MinHeap h = new MinHeap(15);
        h.insertKey(3);
        h.insertKey(2);
        h.insertKey(15);
        h.insertKey(5);
        h.insertKey(4);
        h.insertKey(45);
        h.insertKey(80);
        h.insertKey(6);
        h.insertKey(150);
        h.insertKey(77);
        h.insertKey(120);

        // Print all nodes smaller than 100.
        int x = 100;
        h.printSmallerThan(x, 0);
    }
}

// This code is contributed by PrinciRaj1992
```

**输出:**

```
2 3 5 6 4 77 15 45 80

```

本文由 **Raghav Sharma** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。