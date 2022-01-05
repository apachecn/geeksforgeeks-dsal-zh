# 用于重新排列链表以使所有偶数和奇数位置的节点在一起的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-用于重新排列链表的程序-使得所有偶数和奇数位置的节点都在一起/](https://www.geeksforgeeks.org/java-program-for-rearranging-a-linked-list-such-that-all-even-and-odd-positioned-nodes-are-together/)

重新排列链表，所有奇数位置节点在一起，所有偶数位置节点在一起，
**示例:**

```
Input:   1->2->3->4
Output:  1->3->2->4

Input:   10->22->30->43->56->70
Output:  10->30->56->22->43->70
```

这个问题中重要的一点是确保下面所有的案件都得到处理

1.  空链表。
2.  只有一个节点的链表。
3.  只有两个节点的链表。
4.  具有奇数个节点的链表。
5.  节点数为偶数的链表。

下面的程序为奇数和偶数位置的当前节点维护两个指针“奇数”和“偶数”。我们还存储了偶链表的第一个节点，这样我们就可以在两个不同的列表中将所有奇数和偶数节点连接在一起后，将偶列表附加在奇数列表的末尾。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to rearrange a linked list 
// in such a way that all odd positioned  
// node are stored before all even 
// positioned nodes 
class GfG { 

// Linked List Node 
static class Node 
{ 
    int data; 
    Node next; 
}

// A utility function to create 
// a new node 
static Node newNode(int key) 
{ 
    Node temp = new Node(); 
    temp.data = key; 
    temp.next = null; 
    return temp; 
} 

// Rearranges given linked list 
// such that all even positioned 
// nodes are before odd positioned. 
// Returns new head of linked List. 
static Node rearrangeEvenOdd(Node head) 
{ 
    // Corner case 
    if (head == null) 
        return null; 

    // Initialize first nodes of even 
    // and odd lists 
    Node odd = head; 
    Node even = head.next; 

    // Remember the first node of even 
    // list so that we can connect the 
    // even list at the end of odd list. 
    Node evenFirst = even; 

    while (1 == 1) 
    { 
        // If there are no more nodes,  
        // then connect first node of even  
        // list to the last node of odd list 
        if (odd == null || even == null ||
           (even.next) == null) 
        { 
            odd.next = evenFirst; 
            break; 
        } 

        // Connecting odd nodes 
        odd.next = even.next; 
        odd = even.next; 

        // If there are NO more even 
        // nodes after current odd. 
        if (odd.next == null) 
        { 
            even.next = null; 
            odd.next = evenFirst; 
            break; 
        } 

        // Connecting even nodes 
        even.next = odd.next; 
        even = odd.next; 
    } 
    return head; 
} 

// A utility function to print 
// a linked list 
static void printlist(Node node) 
{ 
    while (node != null) 
    { 
        System.out.print(node.data + "->"); 
        node = node.next; 
    } 
    System.out.println("NULL") ; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    Node head = newNode(1); 
    head.next = newNode(2); 
    head.next.next = newNode(3); 
    head.next.next.next = newNode(4); 
    head.next.next.next.next = newNode(5); 

    System.out.println("Given Linked List"); 
    printlist(head); 

    head = rearrangeEvenOdd(head); 

    System.out.println("Modified Linked List"); 
    printlist(head); 
}
} 
// This code is contributed by Prerna saini
```

**输出:**

```
Given Linked List
1->2->3->4->5->NULL
Modified Linked List
1->3->5->2->4->NULL
```

更多细节请参考[整篇文章重新排列链表，让所有偶数和奇数位置的节点都在一起](https://www.geeksforgeeks.org/rearrange-a-linked-list-such-that-all-even-and-odd-positioned-nodes-are-together/)！