# 删除双向链表中节点的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-删除双链表中节点的程序/](https://www.geeksforgeeks.org/java-program-for-deleting-a-node-in-a-doubly-linked-list/)

**先决条件:** [双向链接列表集 1|介绍和插入](https://www.geeksforgeeks.org/doubly-linked-list/)

编写一个函数来删除双向链表中的给定节点。
**原双链表**

![](img/b9016fd69bcaae1bff3fbeb66cc6e586.png)

**方法:**双链表中节点的删除可以分为三大类:

*   **删除头节点后。**

![](img/405dde32f84337015261164de1d959e4.png)

*   **删除中间节点后。**

![](img/9f00d861ab5bd6a0e30b64c64cdec641.png)

*   **删除最后一个节点后。**

![](img/adf06162647ff64bd621686bd799358e.png)

**如果要删除的节点的指针和头指针已知，那么上述三种情况都可以分两步处理。**

1.  如果要删除的节点是头节点，则将下一个节点作为头。
2.  如果删除了一个节点，请连接已删除节点的下一个和上一个节点。

![](img/60f66c57bb20c5cb13276b1b64f219a1.png)

**算法**

*   让要删除的节点为 *del* 。
*   如果要删除的节点是头节点，则将头指针更改为下一个当前头。

```
if *headnode* == *del* then
      *headnode* =  *del*.nextNode
```

*   如果存在上一个 *del* ，则将上一个的*下一个*设置为 *del* 。

```
if *del*.nextNode != *none* 
      *del*.nextNode.previousNode = *del*.previousNode 
```

*   如果在 *del* 旁边，则设置 *del* 旁边的 *prev* 。

```
if *del*.previousNode != *none* 
      *del*.previousNode.nextNode = *del*.next
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to delete a node from
// Doubly Linked List

// Class for Doubly Linked List
public class DLL 
{
    // Head of list
    Node head; 

    // Doubly Linked list Node
    class Node 
    {
        int data;
        Node prev;
        Node next;

        // Constructor to create a new 
        // node. next and prev is by 
        // default initialized as null
        Node(int d) { data = d; }
    }

    // Adding a node at the front of 
    // the list
    public void push(int new_data)
    {
        // 1\. Allocate node
        // 2\. Put in the data
        Node new_Node = new Node(new_data);

        // 3\. Make next of new node as head
        //    and previous as NULL
        new_Node.next = head;
        new_Node.prev = null;

        // 4\. Change prev of head node to 
        //    new node
        if (head != null)
            head.prev = new_Node;

        // 5\. Move the head to point to the 
        //    new node
        head = new_Node;
    }

    // This function prints contents of 
    // linked list starting from the given node
    public void printlist(Node node)
    {
        Node last = null;

        while (node != null) 
        {
            System.out.print(node.data + " ");
            last = node;
            node = node.next;
        }

        System.out.println();
    }

    // Function to delete a node in a Doubly 
    // Linked List. head_ref --> pointer to 
    // head node pointer. del --> data of node 
    // to be deleted.
    void deleteNode(Node del)
    {
        // Base case
        if (head == null || del == null) 
        {
            return;
        }

        // If node to be deleted is head node
        if (head == del) 
        {
            head = del.next;
        }

        // Change next only if node to be 
        // deleted is NOT the last node
        if (del.next != null) 
        {
            del.next.prev = del.prev;
        }

        // Change prev only if node to be 
        // deleted is NOT the first node
        if (del.prev != null) 
        {
            del.prev.next = del.next;
        }

        // Finally, free the memory occupied 
        // by del
        return;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Start with the empty list
        DLL dll = new DLL();

        // Insert 2\. So linked list becomes 
        // 2->NULL
        dll.push(2);

        // Insert 4\. So linked list becomes 
        // 4->2->NULL
        dll.push(4);

        // Insert 8\. So linked list becomes 
        // 8->4->2->NULL
        dll.push(8);

        // Insert 10\. So linked list becomes 
        // 10->8->4->2->NULL
        dll.push(10);

        System.out.print("Created DLL is: ");
        dll.printlist(dll.head);

        // Deleting first node
        dll.deleteNode(dll.head);

        // List after deleting first node
        // 8->4->2
        System.out.print(
        "List after deleting first node: ");
        dll.printlist(dll.head);

        // Deleting middle node from 8->4->2
        dll.deleteNode(dll.head.next);

        System.out.print(
        "List after Deleting middle node: ");
        dll.printlist(dll.head);
    }
}
```

**输出:**

```
Original Linked list 10 8 4 2 
Modified Linked list 8
```

**复杂度分析:**

*   **时间复杂度:** O(1)。
    因为不需要遍历链表，所以时间复杂度是恒定的。
*   **空间复杂度:** O(1)。
    由于不需要额外的空间，所以空间复杂度不变。

详情请参考[删除双向链表](https://www.geeksforgeeks.org/delete-a-node-in-a-doubly-linked-list/)中的一个节点的完整文章！