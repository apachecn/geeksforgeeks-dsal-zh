# 从具有某些公共节点的两个排序链表中构造一个最大和链表

给定两个排序的链表，构造一个链表，该链表包含从头到尾的最大求和路径。 结果列表可能包含两个输入列表中的节点。 构造结果列表时，我们可能仅在交点处切换到另一个输入列表（这意味着列表中具有相同值的两个节点）。 允许您使用 O（1）多余的空间。

```
Input:
List1 =  1->3->30->90->120->240->511
List2 =  0->3->12->32->90->125->240->249

Output: Following is maximum sum linked list out of two input lists
list =  1->3->12->32->90->125->240->511
we switch at 3 and 240 to get above maximum sum linked list

```

**我们强烈建议最小化浏览器，然后自己尝试。**

以下解决方案中的想法是在公共节点之后调整下一个指针。
1.从两个链接列表的开头开始，找到第一个公共节点。 为此使用排序链表的合并技术。
2.在执行此操作时，也要跟踪元素的总和，并基于较大的总和设置结果列表的开头，直到第一个公共节点。
3.此后，直到两个列表的当前指针都不为 NULL，我们需要根据较大的和调整下一个上一个指针。

这样，就可以在原地完成并保持恒定的额外空间。
以下解决方案的时间复杂度为 O（n）。

## C++

```cpp

// C++ program to construct the maximum sum linked 
// list out of two given sorted lists 
#include<bits/stdc++.h> 
using namespace std; 

//A linked list node 
struct Node 
{ 
    int data; //data belong to that node 
    Node *next; //next pointer 
}; 

// Push the data to the head of the linked list 
void push(Node **head, int data) 
{ 
    //Allocation memory to the new node 
    Node *newnode = new Node; 

    //Assigning data to the new node 
    newnode->data = data; 

    //Adjusting next pointer of the new node 
    newnode->next = *head; 

    //New node becomes the head of the list 
    *head = newnode; 
} 

// Method that adjusts the pointers and prints the final list 
void finalMaxSumList(Node *a, Node *b) 
{ 
    Node *result = NULL; 

    // Assigning pre and cur to the head of the 
    // linked list. 
    Node *pre1 = a, *curr1 = a; 
    Node *pre2 = b, *curr2 = b; 

    // Till either of the current pointers is not 
    // NULL execute the loop 
    while (curr1 != NULL || curr2 != NULL) 
    { 
        // Keeping 2 local variables at the start of every 
        // loop run to keep track of the sum between pre 
        // and cur pointer elements. 
        int sum1 = 0, sum2 = 0; 

        // Calculating sum by traversing the nodes of linked 
        // list as the merging of two linked list.  The loop 
        // stops at a common node 
        while (curr1!=NULL && curr2!=NULL && curr1->data!=curr2->data) 
        { 
            if (curr1->data < curr2->data) 
            { 
                sum1 += curr1->data; 
                curr1 = curr1->next; 
            } 
            else // (curr2->data < curr1->data) 
            { 
                sum2 += curr2->data; 
                curr2 = curr2->next; 
            } 
        } 

        // If either of current pointers becomes NULL 
        // carry on the sum calculation for other one. 
        if (curr1 == NULL) 
        { 
            while (curr2 != NULL) 
            { 
                sum2 += curr2->data; 
                curr2 = curr2->next; 
            } 
        } 
        if (curr2 == NULL) 
        { 
            while (curr1 != NULL) 
            { 
                sum1 += curr1->data; 
                curr1 = curr1->next; 
            } 
        } 

        // First time adjustment of resultant head based on 
        // the maximum sum. 
        if (pre1 == a && pre2 == b) 
            result = (sum1 > sum2)? pre1 : pre2; 

        // If pre1 and pre2 don't contain the head pointers of 
        // lists adjust the next pointers of previous pointers. 
        else
        { 
            if (sum1 > sum2) 
                pre2->next = pre1->next; 
            else
                pre1->next = pre2->next; 
        } 

        // Adjusting previous pointers 
        pre1 = curr1, pre2 = curr2; 

        // If curr1 is not NULL move to the next. 
        if (curr1) 
            curr1 = curr1->next; 
        // If curr2 is not NULL move to the next. 
        if (curr2) 
            curr2 = curr2->next; 
    } 

    // Print the resultant list. 
    while (result != NULL) 
    { 
        cout << result->data << " "; 
        result = result->next; 
    } 
} 

//Main driver program 
int main() 
{ 
    //Linked List 1 : 1->3->30->90->110->120->NULL 
    //Linked List 2 : 0->3->12->32->90->100->120->130->NULL 
    Node *head1 = NULL, *head2 = NULL; 
    push(&head1, 120); 
    push(&head1, 110); 
    push(&head1, 90); 
    push(&head1, 30); 
    push(&head1, 3); 
    push(&head1, 1); 

    push(&head2, 130); 
    push(&head2, 120); 
    push(&head2, 100); 
    push(&head2, 90); 
    push(&head2, 32); 
    push(&head2, 12); 
    push(&head2, 3); 
    push(&head2, 0); 

    finalMaxSumList(head1, head2); 
    return 0; 
} 

```

## Java

```java

// Java program to construct a Maximum Sum Linked List out of 
// two Sorted Linked Lists having some Common nodes 
class LinkedList 
{ 
    Node head;  // head of list 

    /* Linked list Node*/
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

    // Method to adjust pointers and print final list 
    void finalMaxSumList(Node a, Node b) 
    { 
        Node result = null; 

        /* assigning pre and cur to head 
           of the linked list */
        Node pre1 = a, curr1 = a; 
        Node pre2 = b, curr2 = b; 

        /* Till either of current pointers is not null 
           execute the loop */
        while (curr1 != null || curr2 != null) 
        { 
            // Keeping 2 local variables at the start of every 
            // loop run to keep track of the sum between pre 
            // and cur reference elements. 
            int sum1 = 0, sum2 = 0; 

            // Calculating sum by traversing the nodes of linked 
            // list as the merging of two linked list.  The loop 
            // stops at a common node 
            while (curr1 != null && curr2 != null && 
                   curr1.data != curr2.data) 
            { 

                if (curr1.data<curr2.data) 
                { 
                    sum1 += curr1.data; 
                    curr1 = curr1.next; 
                } 
                else
                { 
                    sum2 += curr2.data; 
                    curr2 = curr2.next; 
                } 
            } 

            // If either of current pointers becomes null 
            // carry on the sum calculation for other one. 
            if (curr1 == null) 
            { 
                while (curr2 != null) 
                { 
                    sum2 += curr2.data; 
                    curr2 = curr2.next; 
                } 
            } 
            if (curr2 == null) 
            { 
                while(curr1 != null) 
                { 
                    sum1 += curr1.data; 
                    curr1 = curr1.next; 
                } 
            } 

            // First time adjustment of resultant head based on 
            // the maximum sum. 
            if (pre1 == a && pre2 == b) 
                result = (sum1 > sum2) ? pre1 : pre2; 

            // If pre1 and pre2 don't contain the head references of 
            // lists adjust the next pointers of previous pointers. 
            else
            { 
                if (sum1 > sum2) 
                    pre2.next = pre1.next; 
                else
                    pre1.next = pre2.next; 
            } 

            // Adjusting previous pointers 
            pre1 = curr1; 
            pre2 = curr2; 

            // If curr1 is not NULL move to the next. 
            if (curr1 != null) 
                curr1 = curr1.next; 

            // If curr2 is not NULL move to the next. 
            if (curr2 != null) 
                curr2 = curr2.next; 
        } 

        while (result != null) 
        { 
            System.out.print(result.data + " "); 
            result = result.next; 
        } 
        System.out.println(); 
    } 

    /*  Inserts a node at start of linked list */
    void push(int new_data) 
    { 
        /* 1 & 2: Allocate the Node & 
                  Put in the data*/
        Node new_node = new Node(new_data); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    /* Driver program to test above functions */
    public static void main(String args[]) 
    { 
        LinkedList llist1 = new LinkedList(); 
        LinkedList llist2 = new LinkedList(); 

        //Linked List 1 : 1->3->30->90->110->120->NULL 
        //Linked List 2 : 0->3->12->32->90->100->120->130->NULL 

        llist1.push(120); 
        llist1.push(110); 
        llist1.push(90); 
        llist1.push(30); 
        llist1.push(3); 
        llist1.push(1); 

        llist2.push(130); 
        llist2.push(120); 
        llist2.push(100); 
        llist2.push(90); 
        llist2.push(32); 
        llist2.push(12); 
        llist2.push(3); 
        llist2.push(0); 

        llist1.finalMaxSumList(llist1.head, llist2.head); 
    } 
} /* This code is contributed by Rajat Mishra */

```

## 蟒蛇

```

# Python program to construct a Maximum Sum Linked List out of 
# two Sorted Linked Lists having some Common nodes 
class LinkedList(object): 
    def __init__(self): 
     # head of list 
         self.head = None

    # Linked list Node 
    class Node(object): 
        def __init__(self, d): 
            self.data = d 
            self.next = None

    # Method to adjust pointers and print final list 
    def finalMaxSumList(self, a, b): 
        result = None
        # assigning pre and cur to head 
        # of the linked list 
        pre1 = a 
        curr1 = a 
        pre2 = b 
        curr2 = b 
        # Till either of current pointers is not null 
        # execute the loop 
        while curr1 != None or curr2 != None: 
            # Keeping 2 local variables at the start of every 
            # loop run to keep track of the sum between pre 
            # and cur reference elements. 
            sum1 = 0
            sum2 = 0
            # Calculating sum by traversing the nodes of linked 
            # list as the merging of two linked list.  The loop 
            # stops at a common node 
            while curr1 != None and curr2 != None and curr1.data != curr2.data: 
                if curr1.data < curr2.data: 
                    sum1 += curr1.data 
                    curr1 = curr1.next
                else: 
                    sum2 += curr2.data 
                    curr2 = curr2.next
            # If either of current pointers becomes null 
            # carry on the sum calculation for other one. 
            if curr1 == None: 
                while curr2 != None: 
                    sum2 += curr2.data 
                    curr2 = curr2.next
            if curr2 == None: 
                while curr1 != None: 
                    sum1 += curr1.data 
                    curr1 = curr1.next
            # First time adjustment of resultant head based on 
            # the maximum sum. 
            if pre1 == a and pre2 == b: 
                result = pre1 if (sum1 > sum2) else pre2 
            else: 
                # If pre1 and pre2 don't contain the head references of 
                # lists adjust the next pointers of previous pointers. 
                if sum1 > sum2: 
                    pre2.next = pre1.next
                else: 
                    pre1.next = pre2.next
            # Adjusting previous pointers 
            pre1 = curr1 
            pre2 = curr2 
            # If curr1 is not NULL move to the next. 
            if curr1 != None: 
                curr1 = curr1.next
            # If curr2 is not NULL move to the next. 
            if curr2 != None: 
                curr2 = curr2.next

        while result != None: 
            print str(result.data), 
            result = result.next
        print '' 

    # Utility functions 
    # Inserts a new Node at front of the list. 
    def push(self, new_data): 
        # 1 & 2: Allocate the Node & 
        # Put in the data 
        new_node = self.Node(new_data) 
        # 3\. Make next of new Node as head 
        new_node.next = self.head 
        # 4\. Move the head to point to new Node 
        self.head = new_node 

# Driver program 
llist1 = LinkedList() 
llist2 = LinkedList() 

# Linked List 1 : 1->3->30->90->110->120->NULL 
# Linked List 2 : 0->3->12->32->90->100->120->130->NULL 

llist1.push(120) 
llist1.push(110) 
llist1.push(90) 
llist1.push(30) 
llist1.push(3) 
llist1.push(1) 

llist2.push(130) 
llist2.push(120) 
llist2.push(100) 
llist2.push(90) 
llist2.push(32) 
llist2.push(12) 
llist2.push(3) 
llist2.push(0) 

llist1.finalMaxSumList(llist1.head, llist2.head) 

# This code is contributed by BHAVYA JAIN 

```

## C#

```cs

// C# program to construct a Maximum 
// Sum Linked List out of two Sorted  
// Linked Lists having some Common nodes  
using System; 

public class LinkedList  
{  
    Node head; // head of list  

    /* Linked list Node*/
    public class Node  
    {  
        public int data;  
        public Node next;  
        public Node(int d)  
        {  
            data = d;  
            next = null;  
        }  
    }  

    // Method to adjust pointers 
    // and print final list  
    void finalMaxSumList(Node a, Node b)  
    {  
        Node result = null;  

        /* assigning pre and cur to head  
        of the linked list */
        Node pre1 = a, curr1 = a;  
        Node pre2 = b, curr2 = b;  

        /* Till either of current pointers  
        is not null execute the loop */
        while (curr1 != null || curr2 != null)  
        {  
            // Keeping 2 local variables at the start 
            //  of every loop run to keep track of the  
            // sum between pre and cur reference elements.  
            int sum1 = 0, sum2 = 0;  

            // Calculating sum by traversing the nodes of linked  
            // list as the merging of two linked list. The loop  
            // stops at a common node  
            while (curr1 != null && curr2 != null &&  
                curr1.data != curr2.data)  
            {  

                if (curr1.data<curr2.data)  
                {  
                    sum1 += curr1.data;  
                    curr1 = curr1.next;  
                }  
                else
                {  
                    sum2 += curr2.data;  
                    curr2 = curr2.next;  
                }  
            }  

            // If either of current pointers becomes null  
            // carry on the sum calculation for other one.  
            if (curr1 == null)  
            {  
                while (curr2 != null)  
                {  
                    sum2 += curr2.data;  
                    curr2 = curr2.next;  
                }  
            }  
            if (curr2 == null)  
            {  
                while(curr1 != null)  
                {  
                    sum1 += curr1.data;  
                    curr1 = curr1.next;  
                }  
            }  

            // First time adjustment of resultant   
            // head based on the maximum sum.  
            if (pre1 == a && pre2 == b)  
                result = (sum1 > sum2) ? pre1 : pre2;  

            // If pre1 and pre2 don't contain  
            // the head references of lists adjust 
            // the next pointers of previous pointers.  
            else
            {  
                if (sum1 > sum2)  
                    pre2.next = pre1.next;  
                else
                    pre1.next = pre2.next;  
            }  

            // Adjusting previous pointers  
            pre1 = curr1;  
            pre2 = curr2;  

            // If curr1 is not NULL move to the next.  
            if (curr1 != null)  
                curr1 = curr1.next;  

            // If curr2 is not NULL move to the next.  
            if (curr2 != null)  
                curr2 = curr2.next;  
        }  

        while (result != null)  
        {  
            Console.Write(result.data + " ");  
            result = result.next;  
        }  
        Console.WriteLine();  
    }  

    /* Inserts a node at start of linked list */
    void push(int new_data)  
    {  
        /* 1 & 2: Allocate the Node &  
                Put in the data*/
        Node new_node = new Node(new_data);  

        /* 3\. Make next of new Node as head */
        new_node.next = head;  

        /* 4\. Move the head to point to new Node */
        head = new_node;  
    }  

    /* Driver code */
    public static void Main()  
    {  
        LinkedList llist1 = new LinkedList();  
        LinkedList llist2 = new LinkedList();  

        //Linked List 1 : 1->3->30->90->110->120->NULL  
        //Linked List 2 : 0->3->12->32->90->100->120->130->NULL  

        llist1.push(120);  
        llist1.push(110);  
        llist1.push(90);  
        llist1.push(30);  
        llist1.push(3);  
        llist1.push(1);  

        llist2.push(130);  
        llist2.push(120);  
        llist2.push(100);  
        llist2.push(90);  
        llist2.push(32);  
        llist2.push(12);  
        llist2.push(3);  
        llist2.push(0);  

        llist1.finalMaxSumList(llist1.head, llist2.head);  
    }  
}  

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
1 3 12 32 90 110 120 130
```

**时间复杂度：** O（n）其中 n 是较大链表的长度
**辅助空间：** O（1）
但是，此解决方案中的问题是 原始列表已更改。

练习
1.当辅助空间不是约束时，请尝试此问题。
2.当我们不修改实际列表并创建结果列表时，请尝试解决此问题。

本文由 **Kumar Gautam** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

