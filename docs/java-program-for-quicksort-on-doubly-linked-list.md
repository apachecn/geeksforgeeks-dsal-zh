# 双链表快速排序的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-for-quick sort-on-double-link-list/](https://www.geeksforgeeks.org/java-program-for-quicksort-on-doubly-linked-list/)

以下是数组的[快速排序](http://en.wikipedia.org/wiki/Quicksort)的典型递归实现。该实现使用最后一个元素作为透视。

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* A typical recursive implementation of
   Quicksort for array*/

/* This function takes last element as pivot, 
   places the pivot element at its correct 
   position in sorted array, and places all 
   smaller (smaller than pivot) to left of
   pivot and all greater elements to right 
   of pivot */
static int partition (int []arr, int l, int h)
{
    int x = arr[h];
    int i = (l - 1);

    for(int j = l; j <= h - 1; j++)
    {
        if (arr[j] <= x)
        {
            i++;
            int tmp = arr[i];
            arr[i] = arr[j];
            arr[j] = tmp;
        }
    }    
    int tmp = arr[i + 1];
    arr[i + 1] = arr[h];
    arr[h] = tmp;
    return(i + 1);
}

/* A[] --> Array to be sorted,
    l  --> Starting index, 
    h  --> Ending index */
static void quickSort(int []A, int l, 
                      int h)
{
    if (l < h)
    {

        // Partitioning index 
        int p = partition(A, l, h); 
        quickSort(A, l, p - 1);  
        quickSort(A, p + 1, h);
    }
}

// This code is contributed by pratham76.
```

**链表可以用同样的算法吗？**
下面是双链表的 C++实现。思路很简单，我们先找出指向最后一个节点的指针。一旦我们有了指向最后一个节点的指针，我们就可以使用指向链表的第一个和最后一个节点的指针来递归地对链表进行排序，类似于上面的递归函数，在那里我们传递第一个和最后一个数组元素的索引。链表的分区函数也类似于数组的分区。它不是返回透视元素的索引，而是返回指向透视元素的指针。在下面的实现中，quickSort()只是一个包装函数，主要的递归函数是 _quickSort()，对于数组的实现类似于 quickSort()。

![](img/907e6783a6130c711cfa83c52cb7210e.png)

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to sort a linked list using Quicksort
class QuickSort_using_Doubly_LinkedList{
    Node head;

/* a node of the doubly linked list */  
    static class Node{
        private int data;
        private Node next;
        private Node prev;

        Node(int d){
            data = d;
            next = null;
            prev = null;
        }
    }

// A utility function to find last node of linked list    
    Node lastNode(Node node){
        while(node.next!=null)
            node = node.next;
        return node;
    }

/* Considers last element as pivot, places the pivot element at its
   correct position in sorted array, and places all smaller (smaller than
   pivot) to left of pivot and all greater elements to right of pivot */
    Node partition(Node l,Node h)
    {
       // set pivot as h element
        int x = h.data;

        // similar to i = l-1 for array implementation
        Node i = l.prev;

        // Similar to "for (int j = l; j <= h- 1; j++)"
        for(Node j=l; j!=h; j=j.next)
        {
            if(j.data <= x)
            {
                // Similar to i++ for array
                i = (i==null) ? l : i.next;
                int temp = i.data;
                i.data = j.data;
                j.data = temp;
            }
        }
        i = (i==null) ? l : i.next;  // Similar to i++
        int temp = i.data;
        i.data = h.data;
        h.data = temp;
        return i;
    }

    /* A recursive implementation of quicksort for linked list */
    void _quickSort(Node l,Node h)
    {
        if(h!=null && l!=h && l!=h.next){
            Node temp = partition(l,h);
            _quickSort(l,temp.prev);
            _quickSort(temp.next,h);
        }
    }

    // The main function to sort a linked list. It mainly calls _quickSort()
    public void quickSort(Node node)
    {
        // Find last node
        Node head = lastNode(node);

        // Call the recursive QuickSort
        _quickSort(node,head);
    }

     // A utility function to print contents of arr
     public void printList(Node head)
     {
        while(head!=null){
            System.out.print(head.data+" ");
            head = head.next;
        }
    }

    /* Function to insert a node at the beginning of the Doubly Linked List */
    void push(int new_Data)
    {
        Node new_Node = new Node(new_Data);     /* allocate node */

        // if head is null, head = new_Node
        if(head==null){
            head = new_Node;
            return;
        }

        /* link the old list off the new node */
        new_Node.next = head;

        /* change prev of head node to new node */
        head.prev = new_Node;

        /* since we are adding at the beginning, prev is always NULL */
        new_Node.prev = null;

        /* move the head to point to the new node */
        head = new_Node;
    }

    /* Driver program to test above function */
    public static void main(String[] args){
            QuickSort_using_Doubly_LinkedList list = new QuickSort_using_Doubly_LinkedList();

            list.push(5);
            list.push(20);
            list.push(4);
            list.push(3);
            list.push(30);

            System.out.println("Linked List before sorting ");
            list.printList(list.head);
            System.out.println("
Linked List after sorting");
            list.quickSort(list.head);
            list.printList(list.head);

    }
}

// This code has been contributed by Amit Khandelwal
```

**输出:**

```
Linked List before sorting
30  3  4  20  5
Linked List after sorting
3  4  5  20  30
```

**时间复杂度:**上述实现的时间复杂度与快速排序()对于数组的时间复杂度相同。最坏的情况下需要 O(n^2 时间，一般情况下和最好的情况下都需要 0。最坏的情况发生在链表已经排序的时候。
我们能为链表实现随机快速排序吗？
只有当我们可以选择一个固定点作为轴心时(就像上面实现中的最后一个元素)，链表才能实现快速排序。随机快速排序不能通过选择随机透视来有效地实现链表。

详情请参考[双链表快速排序](https://www.geeksforgeeks.org/quicksort-for-linked-list/)整篇文章！