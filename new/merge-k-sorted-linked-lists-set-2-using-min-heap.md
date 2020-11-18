# 合并 k 个排序的链表| 第 2 组（使用最小堆）

> 原文：[https://www.geeksforgeeks.org/merge-k-sorted-linked-lists-set-2-using-min-heap/](https://www.geeksforgeeks.org/merge-k-sorted-linked-lists-set-2-using-min-heap/)

给定 **k** 链接列表，每个链接列表的大小为 **n** ，并且每个列表以非降序排序，将它们合并为一个排序的（非降序）链接列表，并打印排序的链接 列出作为输出。

**范例**：

```
Input: k = 3, n =  4
list1 = 1->3->5->7->NULL
list2 = 2->4->6->8->NULL
list3 = 0->9->10->11->NULL

Output: 0->1->2->3->4->5->6->7->8->9->10->11
Merged lists in a sorted order 
where every element is greater 
than the previous element.

Input: k = 3, n =  3
list1 = 1->3->7->NULL
list2 = 2->4->8->NULL
list3 = 9->10->11->NULL

Output: 1->2->3->4->7->8->9->10->11
Merged lists in a sorted order 
where every element is greater 
than the previous element.

```

**来源**：[合并 K 个排序的链表| 方法 2](https://www.geeksforgeeks.org/merge-k-sorted-linked-lists/)

此问题的有效解决方案已在此的**方法 3** 中讨论。

**方法**：此解决方案基于 **MIN HEAP** 方法，用于解决“合并 k 个排序的数组”问题，此处在[中进行了讨论](https://www.geeksforgeeks.org/merge-k-sorted-arrays/)。

*MinHeap：* Min-Heap 是一个完整的二叉树，其中每个内部节点中的值小于或等于该节点的子级中的值。 将堆的元素映射到数组很简单：如果节点存储在索引 k 处，则其左子节点存储在索引 2k + 1 处，其右子节点存储在索引 2k + 2 处。

1.  创建一个最小堆，然后插入所有“ k”链接列表的第一个元素。

2.  只要 min-heap 不为空，请执行以下步骤：

    1.  删除 min-heap 的顶部元素（这是 min-heap 中所有元素的当前最小值），并将其添加到结果列表中。

    2.  如果在上一步中弹出的元素旁边有一个元素（在同一链接列表中），则将其插入 min-heap 中。

3.  返回合并列表的头节点地址。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to merge k
// sorted linked lists
// | Using MIN HEAP method
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    struct Node* next;
};

// Utility function to create a new node
struct Node* newNode(int data)
{
    // allocate node
    struct Node* new_node = new Node();

    // put in the data
    new_node->data = data;
    new_node->next = NULL;

    return new_node;
}

// 'compare' function used to build up the
// priority queue
struct compare {
    bool operator()(
        struct Node* a, struct Node* b)
    {
        return a->data > b->data;
    }
};

// function to merge k sorted linked lists
struct Node* mergeKSortedLists(
    struct Node* arr[], int k)
{
    // priority_queue 'pq' implemented
    // as min heap with the
    // help of 'compare' function
    priority_queue<Node*, vector<Node*>, compare> pq;

    // push the head nodes of all
    // the k lists in 'pq'
    for (int i = 0; i < k; i++)
        if (arr[i] != NULL)
            pq.push(arr[i]);

      // Handles the case when k = 0 
      // or lists have no elements in them    
      if (pq.empty())
        return NULL;

      struct Node *dummy = newNode(0);
      struct Node *last = dummy;

    // loop till 'pq' is not empty
    while (!pq.empty()) {

        // get the top element of 'pq'
        struct Node* curr = pq.top();
        pq.pop();

          // add the top element of 'pq'
          // to the resultant merged list
        last->next = curr;
          last = last->next;  

          // check if there is a node
        // next to the 'top' node
        // in the list of which 'top'
        // node is a member
        if (curr->next != NULL)
            // push the next node of top node in 'pq'
            pq.push(curr->next);
    }

    // address of head node of the required merged list
    return dummy->next;
}

// function to print the singly linked list
void printList(struct Node* head)
{
    while (head != NULL) {
        cout << head->data << " ";
        head = head->next;
    }
}

// Driver program to test above
int main()
{
    int k = 3; // Number of linked lists
    int n = 4; // Number of elements in each list

    // an array of pointers storing the head nodes
    // of the linked lists
    Node* arr[k];

    // creating k = 3 sorted lists
    arr[0] = newNode(1);
    arr[0]->next = newNode(3);
    arr[0]->next->next = newNode(5);
    arr[0]->next->next->next = newNode(7);

    arr[1] = newNode(2);
    arr[1]->next = newNode(4);
    arr[1]->next->next = newNode(6);
    arr[1]->next->next->next = newNode(8);

    arr[2] = newNode(0);
    arr[2]->next = newNode(9);
    arr[2]->next->next = newNode(10);
    arr[2]->next->next->next = newNode(11);

    // merge the k sorted lists
    struct Node* head = mergeKSortedLists(arr, k);

    // print the merged list
    printList(head);

    return 0;
}

```

## Java

```java

// Java implementation to merge
// k sorted linked lists
// Using MIN HEAP method
import java.util.PriorityQueue;
import java.util.Comparator;
public class MergeKLists {

    // function to merge k
    // sorted linked lists
    public static Node mergeKSortedLists(
        Node arr[], int k)
    {
        Node head = null, last = null;

        // priority_queue 'pq' implemeted
        // as min heap with the
        // help of 'compare' function
        PriorityQueue<Node> pq
            = new PriorityQueue<>(
                new Comparator<Node>() {
                    public int compare(Node a, Node b)
                    {
                        return a.data - b.data;
                    }
                });

        // push the head nodes of all
        // the k lists in 'pq'
        for (int i = 0; i < k; i++)
            if (arr[i] != null)
                pq.add(arr[i]);

        // loop till 'pq' is not empty
        while (!pq.isEmpty()) {
            // get the top element of 'pq'
            Node top = pq.peek();
            pq.remove();

            // check if there is a node
            // next to the 'top' node
            // in the list of which 'top'
            // node is a member
            if (top.next != null)
                // push the next node in 'pq'
                pq.add(top.next);

            // if final merged list is empty
            if (head == null) {
                head = top;
                // points to the last node so far of
                // the final merged list
                last = top;
            }
            else {
                // insert 'top' at the end
                // of the merged list so far
                last.next = top;

                // update the 'last' pointer
                last = top;
            }
        }
        // head node of the required merged list
        return head;
    }

    // function to print the singly linked list
    public static void printList(Node head)
    {
        while (head != null) {
            System.out.print(head.data + " ");
            head = head.next;
        }
    }

    // Utility function to create a new node
    public Node push(int data)
    {
        Node newNode = new Node(data);
        newNode.next = null;
        return newNode;
    }

    public static void main(String args[])
    {
        int k = 3; // Number of linked lists
        int n = 4; // Number of elements in each list

        // an array of pointers storing the head nodes
        // of the linked lists
        Node arr[] = new Node[k];

        arr[0] = new Node(1);
        arr[0].next = new Node(3);
        arr[0].next.next = new Node(5);
        arr[0].next.next.next = new Node(7);

        arr[1] = new Node(2);
        arr[1].next = new Node(4);
        arr[1].next.next = new Node(6);
        arr[1].next.next.next = new Node(8);

        arr[2] = new Node(0);
        arr[2].next = new Node(9);
        arr[2].next.next = new Node(10);
        arr[2].next.next.next = new Node(11);

        // Merge all lists
        Node head = mergeKSortedLists(arr, k);
        printList(head);
    }
}

class Node {
    int data;
    Node next;
    Node(int data)
    {
        this.data = data;
        next = null;
    }
}
// This code is contributed by Gaurav Tiwari

```

**Output**

```
0 1 2 3 4 5 6 7 8 9 10 11 
```

**复杂度分析**：

*   **时间复杂度**：O（N * k * log k），其中，“ N”是所有链接列表中元素的总数，而“ k”是列表总数。

    在最小堆中插入和删除需要 log k 时间。 因此，总体时间复杂度为 O（N * log k）。

*   **辅助空间**：O（k）。

    优先级队列在任何时间点最多具有“ k”个元素，因此我们的算法所需的额外空间为 O（k）。

本文由 **Ayush Jauhari** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的内容，或者想分享有关上述主题的更多信息，请发表评论。

