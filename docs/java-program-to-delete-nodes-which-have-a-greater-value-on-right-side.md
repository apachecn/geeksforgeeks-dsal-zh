# 删除右侧值较大的节点的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-to-delete-nodes-哪些节点右侧的值更大/](https://www.geeksforgeeks.org/java-program-to-delete-nodes-which-have-a-greater-value-on-right-side/)

给定一个单链表，移除右边值较大的所有节点。

**示例:**

```
Input: 12->15->10->11->5->6->2->3->NULL
Output: 15->11->6->3->NULL
Explanation: 12, 10, 5 and 2 have been deleted because there is a 
             greater value on the right side. When we examine 12, 
             we see that after 12 there is one node with a value 
             greater than 12 (i.e. 15), so we delete 12. When we 
             examine 15, we find no node after 15 that has a value 
             greater than 15, so we keep this node. When we go like 
             this, we get 15->6->3

Input: 10->20->30->40->50->60->NULL
Output: 60->NULL
Explanation: 10, 20, 30, 40, and 50 have been deleted because 
             they all have a greater value on the right side.

Input: 60->50->40->30->20->10->NULL
Output: No Change.

```

**方法 1(简单):**
使用两个循环。在外循环中，逐个挑选链表的节点。在内部循环中，检查是否存在其值大于拾取节点的节点。如果存在值更大的节点，则删除拾取的节点。
**时间复杂度:** O(n^2)

**方法 2(反向使用):**
感谢帕拉斯提供以下算法。
1。颠倒列表。
2。遍历反向列表。把麦克斯留到现在。如果下一个节点小于 max，则删除下一个节点，否则 max =下一个节点。
3。再次反转列表以保留原始顺序。
**时间复杂度:** O(n)
感谢 R.Srinivasan 提供下面的代码。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to delete nodes which have 
// a greater value on right side
class LinkedList 
{
    // head of list
    Node head; 

    // Linked list Node
    class Node 
    {
        int data;
        Node next;
        Node(int d)
        {
            data = d;
            next = null;
        }
    }

    /* Deletes nodes which have a node 
       with greater value node on left side */
    void delLesserNodes()
    {
        // 1.Reverse the linked list 
        reverseList();

        /* 2\. In the reversed list, delete nodes 
              which have a node with greater value 
              node on left side. Note that head node 
              is never deleted because it is the 
              leftmost node.*/
        _delLesserNodes();

        /* 3\. Reverse the linked list again to retain
              the original order */
        reverseList();
    }

    /* Deletes nodes which have greater value 
       node(s) on left side */
    void _delLesserNodes()
    {
        Node current = head;

        // Initialise max 
        Node maxnode = head;
        Node temp;

        while (current != null && 
               current.next != null) 
        {
            /* If current is smaller than max, 
               then delete current */
            if (current.next.data < maxnode.data) 
            {
                temp = current.next;
                current.next = temp.next;
                temp = null;
            }

            /* If current is greater than max, 
               then update max and move current */
            else 
            {
                current = current.next;
                maxnode = current;
            }
        }
    }

    // Utility functions 
    /* Inserts a new Node at front of 
       the list. */
    void push(int new_data)
    {
        /* 1 & 2: Allocate the Node &
                  Put in the data*/
        Node new_node = new Node(new_data);

        // 3\. Make next of new Node as head 
        new_node.next = head;

        // 4\. Move the head to point to 
        // new Node 
        head = new_node;
    }

    // Function to reverse the linked list 
    void reverseList()
    {
        Node current = head;
        Node prev = null;
        Node next;
        while (current != null) 
        {
            next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }
        head = prev;
    }

    // Function to print linked list 
    void printList()
    {
        Node temp = head;
        while (temp != null) 
        {
            System.out.print(temp.data + 
                             " ");
            temp = temp.next;
        }
        System.out.println();
    }

    // Driver code
    public static void main(String args[])
    {
        LinkedList llist = new LinkedList();

        /* Constructed Linked List is 
           12->15->10->11->5->6->2->3 */
        llist.push(3);
        llist.push(2);
        llist.push(6);
        llist.push(5);
        llist.push(11);
        llist.push(10);
        llist.push(15);
        llist.push(12);

        System.out.println("Given Linked List");
        llist.printList();

        llist.delLesserNodes();

        System.out.println("Modified Linked List");
        llist.printList();
    }
} 
// This code is contributed by Rajat Mishra 
```

**输出:**

```
Given Linked List 
12 15 10 11 5 6 2 3
Modified Linked List 
15 11 6 3
```

**方法 3:**
另一个比较简单的方法是从开始遍历列表，当当前 node <下一个 Node 时删除该节点。要删除当前节点，请遵循这种方法。让我们假设您必须删除当前节点 X:

1.  将下一个节点的数据复制到 X 中，即 X.data = X.next.data
2.  复制下一个节点的下一个地址，即 X.next = X.next.next

仅当当前节点>下一个节点时，才在列表中向前移动。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;

// This class represents a single node 
// in a linked list
class Node 
{    
    int data;
    Node next;

    public Node(int data)
    {
        this.data = data;
        this.next = null;
    }
}

//This is a utility class for 
// linked list
class LLUtil
{    
    // This function creates a linked list 
    // from a given array and returns head
    public Node createLL(int[] arr)
    {        
        Node head = new Node(arr[0]);
        Node temp = head;

        Node newNode = null;
        for(int i = 1; i < arr.length; i++)
        {
            newNode = new Node(arr[i]);
            temp.next = newNode;
            temp = temp.next;
        }
        return head;
    }

      // This function prints given 
      // linked list
      public void printLL(Node head)
      {        
        while(head != null)
        {
            System.out.print(head.data +
                             " ");
            head = head.next;
        }
        System.out.println();
    }  
}

// Driver code
class GFG 
{
    public static void main (String[] args) 
    {        
        int[] arr = {12, 15, 10, 11, 
                     5, 6, 2, 3};
        LLUtil llu = new LLUtil();
        Node head = llu.createLL(arr);
        System.out.println("Given Linked List");
        llu.printLL(head);
        head = deleteNodesOnRightSide(head);
        System.out.println("Modified Linked List");
        llu.printLL(head);

    }

    //Main function
    public static Node deleteNodesOnRightSide(Node head)
    {
         if(head == null || head.next == null) 
             return head;

         Node nextNode = deleteNodesOnRightSide(head.next);

         if(nextNode.data > head.data) 
             return nextNode;
         head.next = nextNode;

         return head;
    }
}
```

**输出:**

```
Given Linked List
12 15 10 11 5 6 2 3 
Modified Linked List
15 11 6 3
```

来源:[https://www . geeksforgeeks . org/forum/topic/Amazon-interview-question-for-software-engineer developer-about-linked-list-6](https://www.geeksforgeeks.org/forum/topic/amazon-interview-question-for-software-engineerdeveloper-about-linked-lists-6)

详情请参考[整篇文章删除右侧](https://www.geeksforgeeks.org/delete-nodes-which-have-a-greater-value-on-right-side/)数值较大的节点！