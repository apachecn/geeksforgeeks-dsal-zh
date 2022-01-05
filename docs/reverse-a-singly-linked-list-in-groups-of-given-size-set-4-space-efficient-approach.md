# 在给定大小的组中反转单链表|集合 4(空间有效方法)

> 原文:[https://www . geesforgeks . org/reverse-a-single-link-list-in-group-of-size-set-4-space-efficient-approach/](https://www.geeksforgeeks.org/reverse-a-singly-linked-list-in-groups-of-given-size-set-4-space-efficient-approach/)

给定一个链表，编写一个函数来反转每 k 个节点(其中 k 是该函数的输入)。示例:

> **投入:**>【2】>【3】>【4】>【5】>【6】>【7】>【8】>**输出:【t】**
> 
> **投入:**>【2】>【3】>【4】>【5】>【6】>【7】>【8】>**输出:【t】**

上述问题的多种解决方法已经在下面的帖子中讨论过了:

*   [在给定大小的组中反转链表|设置 1](https://www.geeksforgeeks.org/reverse-a-list-in-groups-of-given-size/) - >使用带有 O(n/k)个额外空间的递归
*   [在给定大小的组中反转链表|设置 2](https://www.geeksforgeeks.org/reverse-linked-list-groups-given-size-set-2/) - >使用带有 O(k)个额外空间的堆栈
*   [在给定大小的组中反转单链表|设置 3](https://www.geeksforgeeks.org/reverse-a-singly-linked-list-in-groups-of-given-size-set-3/) - >使用带有 O(k)个额外空间的 deque

**进场:**本文重点介绍一种使用 ***O(1)*** 辅助空间的进场方式。以下是要遵循的步骤:

*   跟踪链表中每组 **k** 元素的指针中的第一个节点。
*   使用[这个](https://www.geeksforgeeks.org/reverse-a-linked-list/)算法，从当前组的第一个节点开始颠倒下 k 个元素的顺序。
*   反转后，当前组的第一个节点将成为最后一个节点。将其与链表的 **k+1 <sup>第</sup>** 节点连接。
*   第**k+1**节点将成为下一组 **k** 元素的第一个节点。类似地，对每组 **k** 元素重复该过程，直到遍历了整个链表。

下面是上述方法的实现:

## C++

```
// C++ program to reverse a linked
// list in groups of given size
#include <bits/stdc++.h>
using namespace std;

    // Linked list Node
   class Node {
    public:
        int data;
        Node* next;
        Node(int d)
        {
            data = d;
            next = NULL;
        }
    };

    void reverse(Node** node, int k)
    {
        if (k == 1)
            return;

        // Keeps track of the final list
        Node* result = NULL;

        // Append a new node at initial step
        Node* head = new Node(0);
        head->next = *(node);
        Node* next = (*node)->next;

        int count = 0;
        while (next) {
            count++;

            // Update the pointer and
            // iterate linked list by
            // using node & next pointer
            Node* tmp = next->next;
            next->next = *(node);
            *(node) = next;
            next = tmp;

            if (count == k - 1) {
                count = 0;

                if (result == NULL)
                    result = *(node);

                // Last step to join the
                // reversed k-group with
                // the linked list
                tmp = head->next;
                tmp->next = next;
                head->next = *(node);
                head = tmp;

                // Move on to the next k-group
                *(node) = next;
                if (*(node)!= NULL)
                    next = (*node)->next;
            }
        }

        // Process last elements
        Node* tmp = head->next;
        if (tmp)
            tmp->next = NULL;
        head->next = *(node);

      *(node) = result;
        return;
    }

    // Utility functions

    // Function to inserts a new
    // Node at front of the list

    void push(Node** head,int new_data)
    {
        Node* new_node = new Node(new_data);
        new_node->next = *(head);
        *(head) = new_node;
    }

    // Function to print linked list
    void printList(Node** head)
    {
        Node* temp = *(head);
        while (temp) {
            cout << temp->data << " ";
            temp = temp->next;
        }
        cout << endl;
    }

/* Driver program to test above functions */

int main()
{
    Node* head = NULL;

    /* Constructed Linked List is
     * 1->2->3->4->5->6->7->8->null */
    push(&head,8);
    push(&head,7);
    push(&head,6);
    push(&head,5);
    push(&head,4);
    push(&head,3);
    push(&head,2);
    push(&head,1);

    reverse(&head, 3);
    printList(&head);

    return 0;
}

// This code is contributed by maddler.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reverse a linked
// list in groups of given size

class LinkedList {

    // head of list
    Node head;

    // Linked list Node
    class Node {
        int data;
        Node next;
        Node(int d)
        {
            data = d;
            next = null;
        }
    }

    Node reverse(Node node, int k)
    {
        if (k == 1)
            return node;

        // Keeps track of the final list
        Node result = null;

        // Append a new node at initial step
        Node head = new Node(0);
        head.next = node;
        Node next = node.next;

        int count = 0;
        while (next != null) {
            count++;

            // Update the pointer and
            // iterate linked list by
            // using node & next pointer
            Node tmp = next.next;
            next.next = node;
            node = next;
            next = tmp;

            if (count == k - 1) {
                count = 0;

                if (result == null)
                    result = node;

                // Last step to join the
                // reversed k-group with
                // the linked list
                tmp = head.next;
                tmp.next = next;
                head.next = node;
                head = tmp;

                // Move on to the next k-group
                node = next;
                if (node != null)
                    next = node.next;
            }
        }

        // Process last elements
        Node tmp = head.next;
        if (tmp != null)
            tmp.next = null;
        head.next = node;

        return result;
    }

    // Utility functions

    // Function to inserts a new
    // Node at front of the list
    public void push(int new_data)
    {
        Node new_node = new Node(new_data);
        new_node.next = head;
        head = new_node;
    }

    // Function to print linked list
    void printList()
    {
        Node temp = head;
        while (temp != null) {
            System.out.print(temp.data + " ");
            temp = temp.next;
        }
        System.out.println();
    }

    /* Driver program to test above functions */
    public static void main(String args[])
    {
        LinkedList llist = new LinkedList();

        /* Constructed Linked List is
         * 1->2->3->4->5->6->7->8->null */
        llist.push(8);
        llist.push(7);
        llist.push(6);
        llist.push(5);
        llist.push(4);
        llist.push(3);
        llist.push(2);
        llist.push(1);

        llist.head = llist.reverse(llist.head, 3);
        llist.printList();
    }
}
```

## C#

```
using System;

// C# program to reverse a linked
// list in groups of given size
public class List {

    // head of list
    public Node head;

    // Linked list Node
    public class Node {
    public     int data;
    public     Node next;

    public     Node(int d) {
            data = d;
            next = null;
        }
    }

    Node reverse(Node node, int k) {
        if (k == 1)
            return node;

        // Keeps track of the readonly list
        Node result = null;

        // Append a new node at initial step
        Node head = new Node(0);
        head.next = node;
        Node next = node.next;

        int count = 0;
        while (next != null) {
            count++;

            // Update the pointer and
            // iterate linked list by
            // using node & next pointer
            Node tmp1 = next.next;
            next.next = node;
            node = next;
            next = tmp1;

            if (count == k - 1) {
                count = 0;

                if (result == null)
                    result = node;

                // Last step to join the
                // reversed k-group with
                // the linked list
                tmp1 = head.next;
                tmp1.next = next;
                head.next = node;
                head = tmp1;

                // Move on to the next k-group
                node = next;
                if (node != null)
                    next = node.next;
            }
        }

        // Process last elements
        Node tmp = head.next;
        if (tmp != null)
            tmp.next = null;
        head.next = node;

        return result;
    }

    // Utility functions

    // Function to inserts a new
    // Node at front of the list
    public void Push(int new_data) {
        Node new_node = new Node(new_data);
        new_node.next = head;
        head = new_node;
    }

    // Function to print linked list
    void printList() {
        Node temp = head;
        while (temp != null) {
            Console.Write(temp.data + " ");
            temp = temp.next;
        }
        Console.WriteLine();
    }

    /* Driver program to test above functions */
    public static void Main(String []args)
    {
        List llist = new List();

        /*
         * Constructed Linked List is 1->2->3->4->5->6->7->8->null
         */
        llist.Push(8);
        llist.Push(7);
        llist.Push(6);
        llist.Push(5);
        llist.Push(4);
        llist.Push(3);
        llist.Push(2);
        llist.Push(1);

        llist.head = llist.reverse(llist.head, 3);
        llist.printList();
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// javascript program to reverse a linked
// list in groups of given size

    // head of list
    var head;

    // Linked list Node
     class Node {
        constructor(val) {
            this.data = val;
            this.next = null;
        }
    }

    function reverse(node , k) {
        if (k == 1)
            return node;

        // Keeps track of the final list
        var result = null;

        // Append a new node at initial step
        var head = new Node(0);
        head.next = node;
        var next = node.next;

        var count = 0;
        while (next != null) {
            count++;

            // Update the pointer and
            // iterate linked list by
            // using node & next pointer
            var tmp = next.next;
            next.next = node;
            node = next;
            next = tmp;

            if (count == k - 1) {
                count = 0;

                if (result == null)
                    result = node;

                // Last step to join the
                // reversed k-group with
                // the linked list
                tmp = head.next;
                tmp.next = next;
                head.next = node;
                head = tmp;

                // Move on to the next k-group
                node = next;
                if (node != null)
                    next = node.next;
            }
        }

        // Process last elements
    var tmp = head.next;
        if (tmp != null)
            tmp.next = null;
        head.next = node;

        return result;
    }

    // Utility functions

    // Function to inserts a new
    // Node at front of the list
     function push(new_data) {
var new_node = new Node(new_data);
        new_node.next = head;
        head = new_node;
    }

    // Function to prvar linked list
    function printList() {
var temp = head;
        while (temp != null) {
            document.write(temp.data + " ");
            temp = temp.next;
        }
        document.write();
    }

    /* Driver program to test above functions */

        /*
         * Constructed Linked List is 1->2->3->4->5->6->7->8->null
         */
        push(8);
        push(7);
        push(6);
        push(5);
        push(4);
        push(3);
        push(2);
        push(1);

        head = reverse(head, 3);
        printList();

// This code is contributed by gauravrajput1
</script>
```

**Output**

```
3 2 1 6 5 4 8 7 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)