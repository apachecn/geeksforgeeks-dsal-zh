# 用于在给定约束下删除链表中给定节点的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-用于在给定约束下删除链表中给定节点的程序/](https://www.geeksforgeeks.org/java-program-for-deleting-a-given-node-in-linked-list-under-given-constraints/)

给定一个单链表，编写一个函数来删除给定的节点。您的函数必须遵循以下约束:

1.  它必须接受指向起始节点的指针作为第一个参数，接受要删除的节点作为第二个参数，即指向头节点的指针不是全局的。
2.  它不应该返回指向头节点的指针。
3.  它不应该接受指向头节点的指针。

您可以假设链表永远不会变成空的。
让函数名为 deleteNode()。在一个简单的实现中，当要删除的节点是第一个节点时，函数需要修改头指针。正如[上一篇文章](https://www.geeksforgeeks.org/how-to-write-functions-that-modify-the-head-pointer-of-a-linked-list/)中所讨论的，当一个函数修改头部指针时，该函数必须使用其中一个[给定的方法](https://www.geeksforgeeks.org/how-to-write-functions-that-modify-the-head-pointer-of-a-linked-list/)，这里我们不能使用这些方法中的任何一个。
**解决方案:**
我们明确处理待删除节点是第一个节点的情况，我们把下一个节点的数据复制到头上，删除下一个节点。被删除的节点不是头节点的情况可以通过找到前一个节点并改变前一个节点的下一个节点来正常处理。以下是实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to delete a given node 
// in linked list under given constraints
class LinkedList 
{
    static Node head;

    static class Node 
    {
        int data;
        Node next;

        Node(int d) 
        {
            data = d;
            next = null;
        }
    }

    void deleteNode(Node node, Node n) 
    {        
        // When node to be deleted is 
        // head node
        if (node == n) 
        {
            if (node.next == null) 
            {
                System.out.println("There is only one node. The list " + 
                                   "can't be made empty ");
                return;
            }

            // Copy the data of next node to head 
            node.data = node.next.data;

            // Store address of next node
            n = node.next;

            // Remove the link of next node
            node.next = node.next.next;

            // Free memory
            System.gc();

            return;
        }

        // When not first node, follow the normal 
        // deletion process find the previous node
        Node prev = node;
        while (prev.next != null && 
               prev.next != n) 
        {
            prev = prev.next;
        }

        // Check if node really exists in 
        // Linked List
        if (prev.next == null) {
            System.out.println("Given node is not present in Linked List");
            return;
        }

        // Remove node from Linked List
        prev.next = prev.next.next;

        // Free memory
        System.gc();

        return;
    }

    /* Utility function to print a linked list */
    void printList(Node head) {
        while (head != null) {
            System.out.print(head.data + " ");
            head = head.next;
        }
        System.out.println("");
    }

    public static void main(String[] args) {
        LinkedList list = new LinkedList();
        list.head = new Node(12);
        list.head.next = new Node(15);
        list.head.next.next = new Node(10);
        list.head.next.next.next = new Node(11);
        list.head.next.next.next.next = new Node(5);
        list.head.next.next.next.next.next = new Node(6);
        list.head.next.next.next.next.next.next = new Node(2);
        list.head.next.next.next.next.next.next.next = new Node(3);

        System.out.println("Given Linked List :");
        list.printList(head);
        System.out.println("");

        // Let us delete the node with value 10
        System.out.println("Deleting node :" + head.next.next.data);
        list.deleteNode(head, head.next.next);

        System.out.println("Modified Linked list :");
        list.printList(head);
        System.out.println("");

        // Lets delete the first node
        System.out.println("Deleting first Node");
        list.deleteNode(head, head);
        System.out.println("Modified Linked List");
        list.printList(head);

    }
}

// this code has been contributed by Mayank Jaiswal
```

**输出:**

```
Given Linked List: 12 15 10 11 5 6 2 3

Deleting node 10:
Modified Linked List: 12 15 11 5 6 2 3

Deleting first node
Modified Linked List: 15 11 5 6 2 3
```

详情请参考[在给定约束下删除链表中给定节点](https://www.geeksforgeeks.org/delete-a-given-node-in-linked-list-under-given-constraints/)的完整文章！