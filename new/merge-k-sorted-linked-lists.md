# 合并 K 个排序的链表 | 系列 1

> 原文：[https://www.geeksforgeeks.org/merge-k-sorted-linked-lists/](https://www.geeksforgeeks.org/merge-k-sorted-linked-lists/)

给定 K 个大小均为 N 的排序链表，将它们合并并打印排序后的输出。

**示例**：

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

 **方法 1（简单）**

**方法**：

一个简单的解决方案是将结果初始化为第一列表。 现在从第二个列表开始遍历所有列表。 以排序的方式将当前遍历列表的每个节点插入到结果中。

```

// C++ program to merge k sorted 
// arrays of size n each 
#include <bits/stdc++.h> 
using namespace std; 

// A Linked List node 
struct Node { 
    int data; 
    Node* next; 
}; 

/* Function to print nodes in  
   a given linked list */
void printList(Node* node) 
{ 
    while (node != NULL) { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

// The main function that 
// takes an array of lists 
// arr[0..last] and generates 
// the sorted output 
Node* mergeKLists(Node* arr[], int last) 
{ 

    // Traverse form second list to last 
    for (int i = 1; i <= last; i++) { 
        while (true) { 
            // head of both the lists, 
            // 0 and ith list. 
            Node *head_0 = arr[0], *head_i = arr[i]; 

            // Break if list ended 
            if (head_i == NULL) 
                break; 

            // Smaller than first element 
            if (head_0->data >= head_i->data) { 
                arr[i] = head_i->next; 
                head_i->next = head_0; 
                arr[0] = head_i; 
            } 
            else
                // Traverse the first list 
                while (head_0->next != NULL) { 
                    // Smaller than next element 
                    if (head_0->next->data 
                        >= head_i->data) { 
                        arr[i] = head_i->next; 
                        head_i->next = head_0->next; 
                        head_0->next = head_i; 
                        break; 
                    } 
                    // go to next node 
                    head_0 = head_0->next; 

                    // if last node 
                    if (head_0->next == NULL) { 
                        arr[i] = head_i->next; 
                        head_i->next = NULL; 
                        head_0->next = head_i; 
                        head_0->next->next = NULL; 
                        break; 
                    } 
                } 
        } 
    } 

    return arr[0]; 
} 

// Utility function to create a new node. 
Node* newNode(int data) 
{ 
    struct Node* temp = new Node; 
    temp->data = data; 
    temp->next = NULL; 
    return temp; 
} 

// Driver program to test 
// above functions 
int main() 
{ 
    // Number of linked lists 
    int k = 3; 

    // Number of elements in each list 
    int n = 4; 

    // an array of pointers storing the 
    // head nodes of the linked lists 
    Node* arr[k]; 

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

    // Merge all lists 
    Node* head = mergeKLists(arr, k - 1); 

    printList(head); 

    return 0; 
} 

```

**Output:**

```
0 1 2 3 4 5 6 7 8 9 10 11

```

**复杂度分析**：

*   **时间复杂度**：`O(N ^ 2)`，其中 N 是节点总数，即 N = kn。

*   **辅助空间**：`O(1)`。

    由于不需要额外的空间。

 **方法 2** ****：[**最小堆**](https://www.geeksforgeeks.org/min-heap-in-java/) 。

更好的解决方案是使用基于 Min Heap 的解决方案，在此处讨论了基于数组的解决方案。 该解决方案的时间复杂度为 **O（nk Log k）**

 **方法 3** ****：[**分而治之**](https://www.geeksforgeeks.org/divide-and-conquer-algorithm-introduction/) 。

在这篇文章中，讨论了**分而治之**方法。 这种方法不需要额外的堆空间，可以在 O（nk Log k）中使用

众所周知，可以在`O(n)`时间和`O(1)`空间（对于数组需要`O(n)`空间）中完成两个链表的[合并。](https://www.geeksforgeeks.org/merge-two-sorted-linked-lists/)

1.  这个想法是将 K 个列表配对并使用`O(1)`空间在线性时间内合并每对。

2.  在第一个循环之后，剩下的 K / 2 个列表的大小均为 2 * N。 在第二个循环之后，剩下的 K / 4 个列表的大小均为 4 * N，依此类推。

3.  重复该过程，直到只剩下一个列表。

以下是上述想法的实现。

## C++

```cpp

// C++ program to merge k sorted 
// arrays of size n each 
#include <bits/stdc++.h> 
using namespace std; 

// A Linked List node 
struct Node { 
    int data; 
    Node* next; 
}; 

/* Function to print nodes in  
   a given linked list */
void printList(Node* node) 
{ 
    while (node != NULL) { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

/* Takes two lists sorted in increasing order, and merge 
   their nodes together to make one big sorted list. Below 
   function takes O(Log n) extra space for recursive calls, 
   but it can be easily modified to work with same time and 
   O(1) extra space  */
Node* SortedMerge(Node* a, Node* b) 
{ 
    Node* result = NULL; 

    /* Base cases */
    if (a == NULL) 
        return (b); 
    else if (b == NULL) 
        return (a); 

    /* Pick either a or b, and recur */
    if (a->data <= b->data) { 
        result = a; 
        result->next = SortedMerge(a->next, b); 
    } 
    else { 
        result = b; 
        result->next = SortedMerge(a, b->next); 
    } 

    return result; 
} 

// The main function that takes an array of lists 
// arr[0..last] and generates the sorted output 
Node* mergeKLists(Node* arr[], int last) 
{ 
    // repeat until only one list is left 
    while (last != 0) { 
        int i = 0, j = last; 

        // (i, j) forms a pair 
        while (i < j) { 
            // merge List i with List j and store 
            // merged list in List i 
            arr[i] = SortedMerge(arr[i], arr[j]); 

            // consider next pair 
            i++, j--; 

            // If all pairs are merged, update last 
            if (i >= j) 
                last = j; 
        } 
    } 

    return arr[0]; 
} 

// Utility function to create a new node. 
Node* newNode(int data) 
{ 
    struct Node* temp = new Node; 
    temp->data = data; 
    temp->next = NULL; 
    return temp; 
} 

// Driver program to test above functions 
int main() 
{ 
    int k = 3; // Number of linked lists 
    int n = 4; // Number of elements in each list 

    // an array of pointers storing the head nodes 
    // of the linked lists 
    Node* arr[k]; 

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

    // Merge all lists 
    Node* head = mergeKLists(arr, k - 1); 

    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to merge k sorted arrays of size n each 
public class MergeKSortedLists { 

    /* Takes two lists sorted in increasing order, and merge  
    their nodes together to make one big sorted list. Below  
    function takes O(Log n) extra space for recursive calls,  
    but it can be easily modified to work with same time and  
    O(1) extra space  */
    public static Node SortedMerge(Node a, Node b) 
    { 
        Node result = null; 
        /* Base cases */
        if (a == null) 
            return b; 
        else if (b == null) 
            return a; 

        /* Pick either a or b, and recur */
        if (a.data <= b.data) { 
            result = a; 
            result.next = SortedMerge(a.next, b); 
        } 
        else { 
            result = b; 
            result.next = SortedMerge(a, b.next); 
        } 

        return result; 
    } 

    // The main function that takes an array of lists 
    // arr[0..last] and generates the sorted output 
    public static Node mergeKLists(Node arr[], int last) 
    { 
        // repeat until only one list is left 
        while (last != 0) { 
            int i = 0, j = last; 

            // (i, j) forms a pair 
            while (i < j) { 
                // merge List i with List j and store 
                // merged list in List i 
                arr[i] = SortedMerge(arr[i], arr[j]); 

                // consider next pair 
                i++; 
                j--; 

                // If all pairs are merged, update last 
                if (i >= j) 
                    last = j; 
            } 
        } 

        return arr[0]; 
    } 

    /* Function to print nodes in a given linked list */
    public static void printList(Node node) 
    { 
        while (node != null) { 
            System.out.print(node.data + " "); 
            node = node.next; 
        } 
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
        Node head = mergeKLists(arr, k - 1); 
        printList(head); 
    } 
} 

class Node { 
    int data; 
    Node next; 
    Node(int data) 
    { 
        this.data = data; 
    } 
} 
// This code is contributed by Gaurav Tiwari 

```

## C#

```cs

// C# program to merge k sorted arrays of size n each 
using System; 

public class MergeKSortedLists { 

    /* Takes two lists sorted in  
    increasing order, and merge  
    their nodes together to make 
    one big sorted list. Below  
    function takes O(Log n) extra  
    space for recursive calls,  
    but it can be easily modified  
    to work with same time and  
    O(1) extra space */
    public static Node SortedMerge(Node a, Node b) 
    { 
        Node result = null; 

        /* Base cases */
        if (a == null) 
            return b; 
        else if (b == null) 
            return a; 

        /* Pick either a or b, and recur */
        if (a.data <= b.data) { 
            result = a; 
            result.next = SortedMerge(a.next, b); 
        } 
        else { 
            result = b; 
            result.next = SortedMerge(a, b.next); 
        } 

        return result; 
    } 

    // The main function that takes 
    // an array of lists arr[0..last] 
    // and generates the sorted output 
    public static Node mergeKLists(Node[] arr, int last) 
    { 
        // repeat until only one list is left 
        while (last != 0) { 
            int i = 0, j = last; 

            // (i, j) forms a pair 
            while (i < j) { 
                // merge List i with List j and store 
                // merged list in List i 
                arr[i] = SortedMerge(arr[i], arr[j]); 

                // consider next pair 
                i++; 
                j--; 

                // If all pairs are merged, update last 
                if (i >= j) 
                    last = j; 
            } 
        } 

        return arr[0]; 
    } 

    /* Function to print nodes in a given linked list */
    public static void printList(Node node) 
    { 
        while (node != null) { 
            Console.Write(node.data + " "); 
            node = node.next; 
        } 
    } 

    public static void Main() 
    { 
        int k = 3; // Number of linked lists 
        int n = 4; // Number of elements in each list 

        // An array of pointers storing the head nodes 
        // of the linked lists 
        Node[] arr = new Node[k]; 

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
        Node head = mergeKLists(arr, k - 1); 
        printList(head); 
    } 
} 

public class Node { 
    public int data; 
    public Node next; 
    public Node(int data) 
    { 
        this.data = data; 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
0 1 2 3 4 5 6 7 8 9 10 11

```

**复杂度分析**：

*   **时间复杂度**：O（nk logk）。

    由于功能 mergeKLists（）中的外部 while 循环运行 k 次，每次处理 nk 个元素时，运行 log。

*   **辅助空间**：`O(1)`。

    由于不需要额外的空间。

[合并 k 个排序的链表| 第 2 组（使用最小堆）](https://www.geeksforgeeks.org/merge-k-sorted-linked-lists-set-2-using-min-heap/)

本文由 **Aditya Goel** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，那么您也可以写一篇文章，然后将您的文章邮寄到 contribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

