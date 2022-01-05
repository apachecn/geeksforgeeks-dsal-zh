# K-ary 堆

> 原文:[https://www.geeksforgeeks.org/k-ary-heap/](https://www.geeksforgeeks.org/k-ary-heap/)

先决条件–[二进制堆](http://geeksquiz.com/binary-heap/)

K 元堆是二进制堆(K=2)的推广，其中每个节点都有 K 个子堆，而不是 2。就像二进制堆一样，它遵循两个性质:
1)几乎完全二叉树，所有层次都有最大数量的节点，除了最后一个，以从左到右的方式填充。
2)和 Binary Heap 一样，可以分为两类:(a) Max k 元堆(根处的 key 大于所有后代，所有节点递归相同)。(b)最小 k 元堆(根处的键小于所有后代，所有节点都递归为真)

示例:

```
3-ary max heap - root node is maximum
                 of all nodes
         10
     /    |   \
   7      9     8
 / | \   /
4  6  5 7

3-ary min heap -root node is minimum 
                of all nodes
         10
      /   |  \
    12    11  13
  / | \
14 15 18 
```

具有 n 个节点的完整 K 元树的高度由 log 给出<sub>K</sub>n .
T3】K 元堆的应用:

*   与二进制堆(二进制堆的 0(log<sub>2</sub>n))相比，K 进制堆用于实现[优先级队列](http://geeksquiz.com/priority-queue-set-1-introduction/)时，允许更快的减少键操作。然而，当使用二进制堆作为优先级队列时，与 O(log <sub>2</sub> n)的复杂性相比，它导致 extractMin()操作的复杂性增加到 O(k log <sub>k</sub> n)。这使得 K 元堆在降低优先级操作比 extractMin()操作更常见的算法中更有效。例如: [Dijkstra 的](https://www.geeksforgeeks.org/greedy-algorithms-set-6-dijkstras-shortest-path-algorithm/)单源最短路径算法和 [Prim 的](https://www.geeksforgeeks.org/greedy-algorithms-set-5-prims-minimum-spanning-tree-mst-2/)最小生成树算法
*   k 元堆具有比二进制堆更好的内存缓存行为，这使得它们在实践中运行得更快，尽管它具有更大的 extractMin()和 delete()操作的最坏情况运行时间(两者都是 O(k log <sub>k</sub> n))。

**实现**
假设基于 0 的数组索引，数组代表一个 K 元堆，因此对于任何节点，我们考虑:

*   索引 I 处节点的父节点(根节点除外)位于索引(i-1)/k 处
*   索引 I 处的节点的子节点位于索引(k*i)+1、(k*i)+2 …(k*i)+k
*   大小为 n 的堆的最后一个非叶节点位于索引(n-2)/k 处

**buildHeap()** :从输入数组构建一个堆。
这个函数运行一个循环，从最后一个非叶节点开始，一直到根节点，为每个索引调用一个函数 restoreDown(也称为 maHeapify)，通过在 K 元堆中下移节点并以自下而上的方式构建它，在堆的正确位置恢复传递的索引。
*为什么从最后一个非叶节点开始循环？*
因为在此之后的所有节点都是叶节点，这些叶节点通常满足堆属性，因为它们没有任何子节点，因此已经是 K 元最大堆的根。
**restore own()(或 maxHeapify)** :用于维护堆属性。
它运行一个循环，在该循环中，它找到所有节点的子节点的最大值，将其与自己的值进行比较，并交换最大值(所有子节点的值)>(节点处的值)。它重复这个步骤，直到节点恢复到堆中的原始位置。
**extractMax() :** 提取根节点。
k 元最大堆在其根中存储最大的元素。它返回根节点，将最后一个节点复制到第一个节点，在第一个节点上向下调用 restore，从而维护堆属性。
**insert() :** 将节点插入堆中
这可以通过在最后一个位置插入节点，并在给定的索引上调用 restoreUp()将节点恢复到堆中的适当位置来实现。restoreUp()反复比较给定节点与其父节点，因为在 max 堆中，父节点总是大于或等于其子节点，只有当节点的键大于父节点时，该节点才会与其父节点交换。
综合以上，下面是 K 元堆的 C++实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to demonstrate all operations of
// k-ary Heap
#include<bits/stdc++.h>

using namespace std;

// function to heapify (or restore the max- heap
// property). This is used to build a k-ary heap
// and in extractMin()
// att[] -- Array that stores heap
// len   -- Size of array
// index -- index of element to be restored
//          (or heapified)
void restoreDown(int arr[], int len, int index,
                                        int k)
{
    // child array to store indexes of all
    // the children of given node
    int child[k+1];

    while (1)
    {
        // child[i]=-1 if the node is a leaf
        // children (no children)
        for (int i=1; i<=k; i++)
            child[i] = ((k*index + i) < len) ?
                    (k*index + i) : -1;

        // max_child stores the maximum child and
        // max_child_index holds its index
        int max_child = -1, max_child_index ;

        // loop to find the maximum of all
        // the children of a given node
        for (int i=1; i<=k; i++)
        {
            if (child[i] != -1 &&
                arr[child[i]] > max_child)
            {
                max_child_index = child[i];
                max_child = arr[child[i]];
            }
        }

        // leaf node
        if (max_child == -1)
            break;

        // swap only if the key of max_child_index
        // is greater than the key of node
        if (arr[index] < arr[max_child_index])
            swap(arr[index], arr[max_child_index]);

        index = max_child_index;
    }
}

// Restores a given node up in the heap. This is used
// in decreaseKey() and insert()
void restoreUp(int arr[], int index, int k)
{
    // parent stores the index of the parent variable
    // of the node
    int parent = (index-1)/k;

    // Loop should only run till root node in case the
    // element inserted is the maximum restore up will
    // send it to the root node
    while (parent>=0)
    {
        if (arr[index] > arr[parent])
        {
            swap(arr[index], arr[parent]);
            index = parent;
            parent = (index -1)/k;
        }

        // node has been restored at the correct position
        else
            break;
    }
}

// Function to build a heap of arr[0..n-1] and value of k.
void buildHeap(int arr[], int n, int k)
{
    // Heapify all internal nodes starting from last
    // non-leaf node all the way upto the root node
    // and calling restore down on each
    for (int i= (n-1)/k; i>=0; i--)
        restoreDown(arr, n, i, k);
}

// Function to insert a value in a heap. Parameters are
// the array, size of heap, value k and the element to
// be inserted
void insert(int arr[], int* n, int k, int elem)
{
    // Put the new element in the last position
    arr[*n] = elem;

    // Increase heap size by 1
    *n = *n+1;

    // Call restoreUp on the last index
    restoreUp(arr, *n-1, k);
}

// Function that returns the key of root node of
// the heap and then restores the heap property
// of the remaining nodes
int extractMax(int arr[], int* n, int k)
{
    // Stores the key of root node to be returned
    int max = arr[0];

    // Copy the last node's key to the root node
    arr[0] = arr[*n-1];

    // Decrease heap size by 1
    *n = *n-1;

    // Call restoreDown on the root node to restore
    // it to the correct position in the heap
    restoreDown(arr, *n, 0, k);

    return max;
}

// Driver program
int main()
{
    const int capacity = 100;
    int arr[capacity] = {4, 5, 6, 7, 8, 9, 10};
    int n = 7;
    int k = 3;

    buildHeap(arr, n, k);

    printf("Built Heap : \n");
    for (int i=0; i<n; i++)
        printf("%d ", arr[i]);

    int element = 3;
    insert(arr, &n, k, element);

    printf("\n\nHeap after insertion of %d: \n",
            element);
    for (int i=0; i<n; i++)
        printf("%d ", arr[i]);

    printf("\n\nExtracted max is %d",
                   extractMax(arr, &n, k));

    printf("\n\nHeap after extract max: \n");
    for (int i=0; i<n; i++)
        printf("%d ", arr[i]);

    return 0;
}
```

输出

```
Built Heap : 
10 9 6 7 8 4 5 

Heap after insertion of 3: 
10 9 6 7 8 4 5 3 

Extracted max is 10

Heap after extract max: 
9 8 6 7 3 4 5 
```

**时间复杂度分析**

*   对于 k 元堆，在有 n 个节点的情况下，给定堆的最大高度将是 log <sub>k</sub> n。因此 restoreUp()最多运行 log <sub>k</sub> n 次(因为在每次迭代中，如果是 restoreUp()的情况，节点会向上移动一级，如果是 restoreDown 的情况，则向下移动一级)。
*   restoreDown()为 k 个子代递归调用自身。所以这个函数的时间复杂度是 O(k log <sub>k</sub> n)。
*   Insert 和 decreaseKey()操作调用 restoreUp()一次。所以复杂度为 O(log <sub>k</sub> n)。
*   由于 extractMax()调用 restoreDown()一次，因此其复杂度为 O(k log <sub>k</sub> n)
*   构建堆的时间复杂度为 O(n)(分析类似于二进制堆)

本文由 **Anurag Rai** 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论