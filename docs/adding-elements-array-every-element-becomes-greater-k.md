# 添加一个数组的元素，直到每个元素都大于或等于 k

> 原文:[https://www . geeksforgeeks . org/add-elements-array-ever-element-变得更大-k/](https://www.geeksforgeeks.org/adding-elements-array-every-element-becomes-greater-k/)

给我们一个 **N** 个未排序元素的列表，我们需要找到列表元素可以添加的最小步数，使所有元素大于或等于 **K** 。我们可以把两个元素加在一起，使它们合二为一。
示例:

```
Input : arr[] = {1 10 12 9 2 3}
          K = 6
Output : 2
First we add (1 + 2), now the new list becomes 
3 10 12 9 3, then we add (3 + 3),  now the new 
list becomes 6 10 12 9, Now all the elements in 
the list are greater than 6. Hence the output is 
2 i:e 2 operations are required 
to do this.
```

从上面的解释可以看出，我们需要提取两个最小的元素，然后将它们的总和添加到列表中。我们需要继续这一步，直到所有元素都大于或等于 K。
**方法 1(蛮力):**
我们可以创建一个简单的数组，对其进行排序，然后添加两个最小元素，并继续将它们存储回数组中，直到所有元素都大于 **K** 。
**方法二(高效):**
如果我们仔细观察，可以注意到这个问题类似于[霍夫曼编码](https://www.geeksforgeeks.org/huffman-decoding/)。我们使用 [**Min Heap**](https://www.geeksforgeeks.org/binary-heap/) 作为这里的主要操作是提取 Min 和插入。这两个操作都可以在 O(Log n)时间内完成。

## C++

```
// A C++ program to count minimum steps to make all
// elements greater than or equal to k.
#include<bits/stdc++.h>
using namespace std;

// A class for Min Heap
class MinHeap
{
    int *harr;
    int capacity; // maximum size
    int heap_size; // Current count
public:
    // Constructor
    MinHeap(int *arr, int capacity);

    // to heapify a subtree with root at
    // given index
    void heapify(int );

    int parent(int i)
    {
        return (i-1)/2;
    }

    // to get index of left child of
    // node at index i
    int left(int i)
    {
        return (2*i + 1);
    }

    // to get index of right child of
    // node at index i
    int right(int i)
    {
        return (2*i + 2);
    }

    // to extract the root which is the
    // minimum element
    int extractMin();

    // Returns the minimum key (key at
    // root) from min heap
    int getMin()
    {
        return harr[0];
    }

    int getSize()
    {
        return heap_size;
    }

    // Inserts a new key 'k'
    void insertKey(int k);
};

// Constructor: Builds a heap from
// a given array a[] of given size
MinHeap::MinHeap(int arr[], int n)
{
    heap_size = n;
    capacity = n;
    harr = new int[n];

    for (int i=0; i<n; i++)
        harr[i] = arr[i];

    // building the heap from first
    // non-leaf node by calling max
    // heapify function
    for (int i=n/2-1; i>=0; i--)
        heapify(i);
}

// Inserts a new key 'k'
void MinHeap::insertKey(int k)
{
    // First insert the new key at the end
    heap_size++;
    int i = heap_size - 1;
    harr[i] = k;

    // Fix the min heap property if it is violated
    while (i != 0 && harr[parent(i)] > harr[i])
    {
        swap(harr[i], harr[parent(i)]);
        i = parent(i);
    }
}

// Method to remove minimum element
// (or root) from min heap
int MinHeap::extractMin()
{
    if (heap_size <= 0)
        return INT_MAX;
    if (heap_size == 1)
    {
        heap_size--;
        return harr[0];
    }

    // Store the minimum value, and
    // remove it from heap
    int root = harr[0];
    harr[0] = harr[heap_size-1];
    heap_size--;
    heapify(0);

    return root;
}

// A recursive method to heapify a subtree
// with root at given index. This method
// assumes that the subtrees are already
// heapified
void MinHeap::heapify(int i)
{
    int l = left(i);
    int r = right(i);
    int smallest = i;
    if (l < heap_size && harr[l] < harr[i])
        smallest = l;
    if (r < heap_size && harr[r] < harr[smallest])
        smallest = r;
    if (smallest != i)
    {
        swap(harr[i], harr[smallest]);
        heapify(smallest);
    }
}

// Returns count of steps needed to make
// all elements greater than or equal to
// k by adding elements
int countMinOps(int arr[], int n, int k)
{
    // Build a min heap of array elements
    MinHeap h(arr, n);

    long int res = 0;

    while (h.getMin() < k)
    {
        if (h.getSize() == 1)
            return -1;

        // Extract two minimum elements
        // and insert their sum
        int first = h.extractMin();
        int second = h.extractMin();
        h.insertKey(first + second);

        res++;
    }

    return res;
}

// Driver code
int main()
{
    int arr[] = {1, 10, 12, 9, 2, 3};
    int n  = sizeof(arr)/sizeof(arr[0]);
    int k = 6;
    cout << countMinOps(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to count minimum steps to make all
// elements greater than or equal to k.
public class Add_Elements {

    // A class for Min Heap
    static class MinHeap
    {
        int[] harr;
        int capacity; // maximum size
        int heap_size; // Current count

        // Constructor: Builds a heap from
        // a given array a[] of given size
        MinHeap(int arr[], int n)
        {
            heap_size = n;
            capacity = n;
            harr = new int[n];

            for (int i=0; i<n; i++)
                harr[i] = arr[i];

            // building the heap from first
            // non-leaf node by calling max
            // heapify function
            for (int i=n/2-1; i>=0; i--)
                heapify(i);
        }

        // A recursive method to heapify a subtree
        // with root at given index. This method
        // assumes that the subtrees are already
        // heapified
        void heapify(int i)
        {
            int l = left(i);
            int r = right(i);
            int smallest = i;
            if (l < heap_size && harr[l] < harr[i])
                smallest = l;
            if (r < heap_size && harr[r] < harr[smallest])
                smallest = r;
            if (smallest != i)
            {
                int temp = harr[i];
                harr[i] = harr[smallest];
                harr[smallest] = temp;
                heapify(smallest);
            }
        }

        static int parent(int i)
        {
            return (i-1)/2;
        }

        // to get index of left child of
        // node at index i
        static int left(int i)
        {
            return (2*i + 1);
        }

        // to get index of right child of
        // node at index i
        int right(int i)
        {
            return (2*i + 2);
        }

        // Method to remove minimum element
        // (or root) from min heap
        int extractMin()
        {
            if (heap_size <= 0)
                return Integer.MAX_VALUE;
            if (heap_size == 1)
            {
                heap_size--;
                return harr[0];
            }

            // Store the minimum value, and
            // remove it from heap
            int root = harr[0];
            harr[0] = harr[heap_size-1];
            heap_size--;
            heapify(0);

            return root;
        }

        // Returns the minimum key (key at
        // root) from min heap
        int getMin()
        {
            return harr[0];
        }

        int getSize()
        {
            return heap_size;
        }

        // Inserts a new key 'k'
        void insertKey(int k)
        {
            // First insert the new key at the end
            heap_size++;
            int i = heap_size - 1;
            harr[i] = k;

            // Fix the min heap property if it is violated
            while (i != 0 && harr[parent(i)] > harr[i])
            {
                 int temp = harr[i];
                 harr[i] = harr[parent(i)];
                 harr[parent(i)] = temp;
                 i = parent(i);
            }
        }
    }

    // Returns count of steps needed to make
    // all elements greater than or equal to
    // k by adding elements
    static int countMinOps(int arr[], int n, int k)
    {
        // Build a min heap of array elements
        MinHeap h = new MinHeap(arr, n);

        int res = 0;

        while (h.getMin() < k)
        {
            if (h.getSize() == 1)
                return -1;

            // Extract two minimum elements
            // and insert their sum
            int first = h.extractMin();
            int second = h.extractMin();
            h.insertKey(first + second);

            res++;
        }

        return res;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = {1, 10, 12, 9, 2, 3};
        int n  = arr.length;
        int k = 6;
        System.out.println(countMinOps(arr, n, k));
    }
}
// This code is contributed by Sumit Ghosh
```

## C#

```
// A C# program to count minimum steps to make all
// elements greater than or equal to k.
using System;

public class Add_Elements
{

    // A class for Min Heap
    public class MinHeap
    {
        public int[] harr;
        public int capacity; // maximum size
        public int heap_size; // Current count

        // Constructor: Builds a heap from
        // a given array a[] of given size
        public MinHeap(int []arr, int n)
        {
            heap_size = n;
            capacity = n;
            harr = new int[n];

            for (int i = 0; i < n; i++)
                harr[i] = arr[i];

            // building the heap from first
            // non-leaf node by calling max
            // heapify function
            for (int i = n/2-1; i >= 0; i--)
                heapify(i);
        }

        // A recursive method to heapify a subtree
        // with root at given index. This method
        // assumes that the subtrees are already
        // heapified
        public void heapify(int i)
        {
            int l = left(i);
            int r = right(i);
            int smallest = i;
            if (l < heap_size && harr[l] < harr[i])
                smallest = l;
            if (r < heap_size && harr[r] < harr[smallest])
                smallest = r;
            if (smallest != i)
            {
                int temp = harr[i];
                harr[i] = harr[smallest];
                harr[smallest] = temp;
                heapify(smallest);
            }
        }

        public static int parent(int i)
        {
            return (i-1)/2;
        }

        // to get index of left child of
        // node at index i
        static int left(int i)
        {
            return (2*i + 1);
        }

        // to get index of right child of
        // node at index i
        public int right(int i)
        {
            return (2*i + 2);
        }

        // Method to remove minimum element
        // (or root) from min heap
        public int extractMin()
        {
            if (heap_size <= 0)
                return int.MaxValue;
            if (heap_size == 1)
            {
                heap_size--;
                return harr[0];
            }

            // Store the minimum value, and
            // remove it from heap
            int root = harr[0];
            harr[0] = harr[heap_size-1];
            heap_size--;
            heapify(0);

            return root;
        }

        // Returns the minimum key (key at
        // root) from min heap
        public int getMin()
        {
            return harr[0];
        }

        public int getSize()
        {
            return heap_size;
        }

        // Inserts a new key 'k'
        public void insertKey(int k)
        {
            // First insert the new key at the end
            heap_size++;
            int i = heap_size - 1;
            harr[i] = k;

            // Fix the min heap property if it is violated
            while (i != 0 && harr[parent(i)] > harr[i])
            {
                int temp = harr[i];
                harr[i] = harr[parent(i)];
                harr[parent(i)] = temp;
                i = parent(i);
            }
        }
    }

    // Returns count of steps needed to make
    // all elements greater than or equal to
    // k by adding elements
    static int countMinOps(int []arr, int n, int k)
    {
        // Build a min heap of array elements
        MinHeap h = new MinHeap(arr, n);

        int res = 0;

        while (h.getMin() < k)
        {
            if (h.getSize() == 1)
                return -1;

            // Extract two minimum elements
            // and insert their sum
            int first = h.extractMin();
            int second = h.extractMin();
            h.insertKey(first + second);

            res++;
        }

        return res;
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = {1, 10, 12, 9, 2, 3};
        int n = arr.Length;
        int k = 6;
        Console.WriteLine(countMinOps(arr, n, k));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// A JavaScript program to count minimum steps to make all
// elements greater than or equal to k.

let harr;
let capacity; // maximum size
let heap_size; // Current count

// Constructor: Builds a heap from
        // a given array a[] of given size
function MinHeap(arr,n)
{
    heap_size = n;
            capacity = n;
            harr = new Array(n);

            for (let i=0; i<n; i++)
                harr[i] = arr[i];

            // building the heap from first
            // non-leaf node by calling max
            // heapify function
            for (let i=n/2-1; i>=0; i--)
                heapify(i);
}

// A recursive method to heapify a subtree
        // with root at given index. This method
        // assumes that the subtrees are already
        // heapified
function heapify(i)
{
    let l = left(i);
            let r = right(i);
            let smallest = i;
            if (l < heap_size && harr[l] < harr[i])
                smallest = l;
            if (r < heap_size && harr[r] < harr[smallest])
                smallest = r;
            if (smallest != i)
            {
                let temp = harr[i];
                harr[i] = harr[smallest];
                harr[smallest] = temp;
                heapify(smallest);
            }
}

function parent(i)
{
    return (i-1)/2;
}

// to get index of left child of
        // node at index i
function left(i)
{
    return (2*i + 1);
}

// to get index of right child of
        // node at index i
function right(i)
{
    return (2*i + 2);
}

// Method to remove minimum element
        // (or root) from min heap
function extractMin()
{
    if (heap_size <= 0)
                return Number.MAX_VALUE;
            if (heap_size == 1)
            {
                heap_size--;
                return harr[0];
            }

            // Store the minimum value, and
            // remove it from heap
            let root = harr[0];
            harr[0] = harr[heap_size-1];
            heap_size--;
            heapify(0);

            return root;
}

// Returns the minimum key (key at
        // root) from min heap
function getMin()
{
    return harr[0];
}

function getSize()
{
    return heap_size;
}

// Inserts a new key 'k'
function insertKey(k)
{
    // First insert the new key at the end
            heap_size++;
            let i = heap_size - 1;
            harr[i] = k;

            // Fix the min heap property if it is violated
            while (i != 0 && harr[parent(i)] > harr[i])
            {
                 let temp = harr[i];
                 harr[i] = harr[parent(i)];
                 harr[parent(i)] = temp;
                 i = parent(i);
            }
}

// Returns count of steps needed to make
    // all elements greater than or equal to
    // k by adding elements
function countMinOps(arr,n,k)
{
    // Build a min heap of array elements
        MinHeap(arr, n);

        let res = 0;

        while (getMin() < k)
        {
            if (getSize() == 1)
                return -1;

            // Extract two minimum elements
            // and insert their sum
            let first = extractMin();
            let second = extractMin();
            insertKey(first + second);

            res++;
        }

        return res;
}

// Driver code
let arr=[1, 10, 12, 9, 2, 3];
let n  = arr.length;
let  k = 6;
document.write(countMinOps(arr, n, k));

// This code is contributed by rag2127

</script>
```

**输出:**

```
2
```

本文由**萨尔特哈克·科利**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。