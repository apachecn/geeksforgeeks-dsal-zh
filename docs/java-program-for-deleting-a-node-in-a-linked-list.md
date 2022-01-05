# 删除链表中节点的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-删除链表中节点的程序/](https://www.geeksforgeeks.org/java-program-for-deleting-a-node-in-a-linked-list/)

我们在之前关于单链表的文章中讨论过[链表介绍](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)和[链表插入](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)。
让我们制定问题陈述，了解删除过程。*给定一个‘键’，删除链表中该键的第一次出现*。

**<u>迭代方法:</u>**
要从链表中删除一个节点，我们需要做以下步骤。
1)找到要删除节点的上一个节点。
2)更改上一个节点的下一个。
3)为要删除的节点释放内存。

![linkedlist_deletion](img/fe3a6a2699fb99ae5429afd588e89619.png)

由于链表的每个节点都是使用 C 语言中的 malloc()动态分配的，所以我们需要调用 [free()](http://www.cplusplus.com/reference/cstdlib/free/) 来释放分配给待删除节点的内存。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A complete working Java program 
// to demonstrate deletion
// in singly linked list
class LinkedList {
    Node head; // head of list

    /* Linked list Node*/
    class Node {
        int data;
        Node next;
        Node(int d)
        {
            data = d;
            next = null;
        }
    }

    /* Given a key, deletes the first 
       occurrence of key in
     * linked list */
    void deleteNode(int key)
    {
        // Store head node
        Node temp = head, prev = null;

        // If head node itself holds the key to be deleted
        if (temp != null && temp.data == key) {
            head = temp.next; // Changed head
            return;
        }

        // Search for the key to be deleted, keep track of
        // the previous node as we need to change temp.next
        while (temp != null && temp.data != key) {
            prev = temp;
            temp = temp.next;
        }

        // If key was not present in linked list
        if (temp == null)
            return;

        // Unlink the node from linked list
        prev.next = temp.next;
    }

    /* Inserts a new Node at front of the list. */
    public void push(int new_data)
    {
        Node new_node = new Node(new_data);
        new_node.next = head;
        head = new_node;
    }

    /* This function prints contents of linked list starting
       from the given node */
    public void printList()
    {
        Node tnode = head;
        while (tnode != null) {
            System.out.print(tnode.data + " ");
            tnode = tnode.next;
        }
    }

    /* Driver program to test above functions. Ideally this
    function should be in a separate user class. It is kept
    here to keep code compact */
    public static void main(String[] args)
    {
        LinkedList llist = new LinkedList();

        llist.push(7);
        llist.push(1);
        llist.push(3);
        llist.push(2);

        System.out.println("
Created Linked list is:");
        llist.printList();

        llist.deleteNode(1); // Delete node with data 1

        System.out.println(
            "
Linked List after Deletion of 1:");
        llist.printList();
    }
}
```

**Output:**

```
Created Linked List: 
 2  3  1  7 
Linked List after Deletion of 1: 
 2  3  7
```

详情请参考[链表|集合 3(删除节点)](https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/)整篇文章！