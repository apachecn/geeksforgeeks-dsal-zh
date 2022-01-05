# 对存储在不同机器上的号码进行分类

> 原文:[https://www . geesforgeks . org/sort-numbers-存储在不同机器上/](https://www.geeksforgeeks.org/sort-numbers-stored-on-different-machines/)

给定 N 台机器。每台机器都包含一些有序的数字。但是每台机器拥有的数量并不是固定的。以排序的非递减形式输出所有机器的数字。
**例:**

```
       Machine M1 contains 3 numbers: {30, 40, 50}
       Machine M2 contains 2 numbers: {35, 45} 
       Machine M3 contains 5 numbers: {10, 60, 70, 80, 100}

       Output: {10, 30, 35, 40, 45, 50, 60, 70, 80, 100}

```

每台机器上的数字流表示被视为链表。最小堆可用于按排序顺序打印所有数字。

以下是详细的过程

**1。**将链表的头部指针存储在一个大小为 N 的 minHeap 中，其中 N 是机器的数量。

**2。**从最小项目提取最小项目。更新 minHeap，方法是用链表中的下一个数字替换 minHeap 的头，或者用 minHeap 中的最后一个数字替换 minHeap 的头，然后将堆的大小减少 1。

**3。**重复上述步骤 2，直到堆不为空。

下面是上述方法的 C++实现。

```
// A program to take numbers from different machines and print them in sorted order
#include <stdio.h>

// A Linked List node
struct ListNode
{
    int data;
    struct ListNode* next;
};

// A Min Heap Node
struct MinHeapNode
{
    ListNode* head;
};

// A Min Heao (Collection of Min Heap nodes)
struct MinHeap
{
    int count;
    int capacity;
    MinHeapNode* array;
};

// A function to create a Min Heap of given capacity
MinHeap* createMinHeap( int capacity )
{
    MinHeap* minHeap = new MinHeap;
    minHeap->capacity = capacity;
    minHeap->count = 0;
    minHeap->array = new MinHeapNode [minHeap->capacity];
    return minHeap;
}

/* A utility function to insert a new node at the beginning
   of linked list */
void push (ListNode** head_ref, int new_data)
{
    /* allocate node */
    ListNode* new_node = new ListNode;

    /* put in the data  */
    new_node->data  = new_data;

    /* link the old list off the new node */
    new_node->next = (*head_ref);

    /* move the head to point to the new node */
    (*head_ref)    = new_node;
}

// A utility function to swap two min heap nodes. This function
// is needed in minHeapify
void swap( MinHeapNode* a, MinHeapNode* b )
{
    MinHeapNode temp = *a;
    *a = *b;
    *b = temp;
}

// The standard minHeapify function.
void minHeapify( MinHeap* minHeap, int idx )
{
    int left, right, smallest;
    left = 2 * idx + 1;
    right = 2 * idx + 2;
    smallest = idx;

    if ( left < minHeap->count &&
         minHeap->array[left].head->data <
         minHeap->array[smallest].head->data
       )
        smallest = left;

    if ( right < minHeap->count &&
         minHeap->array[right].head->data <
         minHeap->array[smallest].head->data
       )
        smallest = right;

    if( smallest != idx )
    {
        swap( &minHeap->array[smallest], &minHeap->array[idx] );
        minHeapify( minHeap, smallest );
    }
}

// A utility function to check whether a Min Heap is empty or not
int isEmpty( MinHeap* minHeap )
{
    return (minHeap->count == 0);
}

// A standard function to build a heap
void buildMinHeap( MinHeap* minHeap )
{
    int i, n;
    n = minHeap->count  - 1;
    for( i = (n - 1) / 2; i >= 0; --i )
        minHeapify( minHeap, i );
}

// This function inserts array elements to heap and then calls
// buildHeap for heap property among nodes
void populateMinHeap( MinHeap* minHeap, ListNode* *array, int n )
{
    for( int i = 0; i < n; ++i )
        minHeap->array[ minHeap->count++ ].head = array[i];

    buildMinHeap( minHeap );
}

// Return minimum element from all linked lists
ListNode* extractMin( MinHeap* minHeap )
{
    if( isEmpty( minHeap ) )
         return NULL;

    // The root of heap will have minimum value
    MinHeapNode temp = minHeap->array[0];

    // Replace root either with next node of the same list.
    if( temp.head->next )
        minHeap->array[0].head = temp.head->next;
    else // If list empty, then reduce heap size
    {
        minHeap->array[0] = minHeap->array[ minHeap->count - 1 ];
        --minHeap->count;
    }

    minHeapify( minHeap, 0 );
    return temp.head;
}

// The main function that takes an array of lists from N machines
// and generates the sorted output
void externalSort( ListNode *array[], int N )
{
    // Create a min heap of size equal to number of machines
    MinHeap* minHeap = createMinHeap( N );

    // populate first item from all machines
    populateMinHeap( minHeap, array, N );

    while ( !isEmpty( minHeap ) )
    {
        ListNode* temp = extractMin( minHeap );
        printf( "%d ",temp->data );
    }
}

// Driver program to test above functions
int main()
{
    int N = 3; // Number of machines

    // an array of pointers storing the head nodes of the linked lists
    ListNode *array[N];

    // Create a Linked List 30->40->50 for first machine
    array[0] = NULL;
    push (&array[0], 50);
    push (&array[0], 40);
    push (&array[0], 30);

    // Create a Linked List 35->45 for second machine
    array[1] = NULL;
    push (&array[1], 45);
    push (&array[1], 35);

    // Create Linked List 10->60->70->80 for third machine
    array[2] = NULL;
    push (&array[2], 100);
    push (&array[2], 80);
    push (&array[2], 70);
    push (&array[2], 60);
    push (&array[2], 10);

    // Sort all elements
    externalSort( array, N );

    return 0;
}
```

输出:

```
10 30 35 40 45 50 60 70 80 100
```

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。