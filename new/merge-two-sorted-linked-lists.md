# 合并两个排序的链表

> 原文：[https://www.geeksforgeeks.org/merge-two-sorted-linked-lists/](https://www.geeksforgeeks.org/merge-two-sorted-linked-lists/)

编写一个`SortedMerge()`函数，该函数接受两个列表，每个列表按升序排序，然后将两个列表合并为一个列表，该列表按升序排序。 `SortedMerge()`应该返回新列表。 应通过将前两个列表的节点拼接在一起来创建新列表。

例如，如果第一个链表`a`为`5 -> 10 -> 15`，而另一个链表`b`为`2 -> 3 -> 20`，则`SortedMerge()`应该返回一个指针 到合并列表的头节点`2 -> 3 -> 5 -> 10 -> 15 -> 20`。

有很多情况需要处理：`a`或`b`可能为空，在处理过程中`a`或`b`可能先用尽，最后，问题是开始将结果列表为空，并在通过`a`和`b`时建立结果列表 。

**方法 1（使用虚拟节点）**

这里的策略使用一个临时虚拟节点作为结果列表的开始。 指针`Tail`始终指向结果列表中的最后一个节点，因此添加新节点很容易。

当结果列表为空时，虚拟节点为尾部提供一些初始指向的内容。 该虚拟节点是有效的，因为它只是临时的，并且在栈中分配。 循环继续进行，从`a`或`b`中删除一个节点，并将其添加到尾部。 完成后，结果在`dummy.next`中。

下图是上述方法的模拟：

![](img/e80386c09dc1031bf5e29bd86c8841ff.png)

下面是上述方法的实现：

## C++

```cpp

/* C++ program to merge two sorted linked lists */
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node  
{  
    public: 
    int data;  
    Node* next;  
};  

/* pull off the front node of  
the source and put it in dest */
void MoveNode(Node** destRef, Node** sourceRef);  

/* Takes two lists sorted in increasing 
order, and splices their nodes together 
to make one big sorted list which  
is returned. */
Node* SortedMerge(Node* a, Node* b)  
{  
    /* a dummy first node to hang the result on */
    Node dummy;  

    /* tail points to the last result node */
    Node* tail = &dummy;  

    /* so tail->next is the place to   
    add new nodes to the result. */
    dummy.next = NULL;  
    while (1)  
    {  
        if (a == NULL)  
        {  
            /* if either list runs out, use the  
            other list */
            tail->next = b;  
            break;  
        }  
        else if (b == NULL)  
        {  
            tail->next = a;  
            break;  
        }  
        if (a->data <= b->data)  
            MoveNode(&(tail->next), &a);  
        else
            MoveNode(&(tail->next), &b);  

        tail = tail->next;  
    }  
    return(dummy.next);  
}  

/* UTILITY FUNCTIONS */
/* MoveNode() function takes the 
node from the front of the source, 
and move it to the front of the dest.  
It is an error to call this with the  
source list empty.  

Before calling MoveNode():  
source == {1, 2, 3}  
dest == {1, 2, 3}  

Affter calling MoveNode():  
source == {2, 3}  
dest == {1, 1, 2, 3} */
void MoveNode(Node** destRef, Node** sourceRef)  
{  
    /* the front source node */
    Node* newNode = *sourceRef;  
    assert(newNode != NULL);  

    /* Advance the source pointer */
    *sourceRef = newNode->next;  

    /* Link the old dest off the new node */
    newNode->next = *destRef;  

    /* Move dest to point to the new node */
    *destRef = newNode;  
}  

/* Function to insert a node at   
the beginging of the linked list */
void push(Node** head_ref, int new_data)  
{  
    /* allocate node */
    Node* new_node = new Node(); 

    /* put in the data */
    new_node->data = new_data;  

    /* link the old list off the new node */
    new_node->next = (*head_ref);  

    /* move the head to point to the new node */
    (*head_ref) = new_node;  
}  

/* Function to print nodes in a given linked list */
void printList(Node *node)  
{  
    while (node!=NULL)  
    {  
        cout<<node->data<<" ";  
        node = node->next;  
    }  
}  

/* Driver code*/
int main()  
{  
    /* Start with the empty list */
    Node* res = NULL;  
    Node* a = NULL;  
    Node* b = NULL;  

    /* Let us create two sorted linked lists   
    to test the functions  
    Created lists, a: 5->10->15, b: 2->3->20 */
    push(&a, 15);  
    push(&a, 10);  
    push(&a, 5);  

    push(&b, 20);  
    push(&b, 3);  
    push(&b, 2);  

    /* Remove duplicates from linked list */
    res = SortedMerge(a, b);  

    cout << "Merged Linked List is: \n";  
    printList(res);  

    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

/* C program to merge two sorted linked lists */
#include<stdio.h> 
#include<stdlib.h> 
#include<assert.h> 

/* Link list node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

/* pull off the front node of the source and put it in dest */
void MoveNode(struct Node** destRef, struct Node** sourceRef); 

/* Takes two lists sorted in increasing order, and splices 
   their nodes together to make one big sorted list which 
   is returned.  */
struct Node* SortedMerge(struct Node* a, struct Node* b) 
{ 
    /* a dummy first node to hang the result on */
    struct Node dummy; 

    /* tail points to the last result node  */
    struct Node* tail = &dummy; 

    /* so tail->next is the place to add new nodes 
      to the result. */
    dummy.next = NULL; 
    while (1) 
    { 
        if (a == NULL) 
        { 
            /* if either list runs out, use the 
               other list */
            tail->next = b; 
            break; 
        } 
        else if (b == NULL) 
        { 
            tail->next = a; 
            break; 
        } 
        if (a->data <= b->data) 
            MoveNode(&(tail->next), &a); 
        else
            MoveNode(&(tail->next), &b); 

        tail = tail->next; 
    } 
    return(dummy.next); 
} 

/* UTILITY FUNCTIONS */
/* MoveNode() function takes the node from the front of the 
   source, and move it to the front of the dest. 
   It is an error to call this with the source list empty. 

   Before calling MoveNode(): 
   source == {1, 2, 3} 
   dest == {1, 2, 3} 

   Affter calling MoveNode(): 
   source == {2, 3} 
   dest == {1, 1, 2, 3} */
void MoveNode(struct Node** destRef, struct Node** sourceRef) 
{ 
    /* the front source node  */
    struct Node* newNode = *sourceRef; 
    assert(newNode != NULL); 

    /* Advance the source pointer */
    *sourceRef = newNode->next; 

    /* Link the old dest off the new node */
    newNode->next = *destRef; 

    /* Move dest to point to the new node */
    *destRef = newNode; 
} 

/* Function to insert a node at the beginging of the 
   linked list */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = 
        (struct Node*) malloc(sizeof(struct Node)); 

    /* put in the data  */
    new_node->data  = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref)    = new_node; 
} 

/* Function to print nodes in a given linked list */
void printList(struct Node *node) 
{ 
    while (node!=NULL) 
    { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

/* Drier program to test above functions*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* res = NULL; 
    struct Node* a = NULL; 
    struct Node* b = NULL; 

    /* Let us create two sorted linked lists to test 
      the functions 
       Created lists, a: 5->10->15,  b: 2->3->20 */
    push(&a, 15); 
    push(&a, 10); 
    push(&a, 5); 

    push(&b, 20); 
    push(&b, 3); 
    push(&b, 2); 

    /* Remove duplicates from linked list */
    res = SortedMerge(a, b); 

    printf("Merged Linked List is: \n"); 
    printList(res); 

    return 0; 
} 

```

## Java

```java

/* Java program to merge two 
   sorted linked lists */
import java.util.*; 

/* Link list node */
class Node  
{ 
    int data; 
    Node next; 
    Node(int d) {data = d; 
                 next = null;} 
} 

class MergeLists  
{ 
Node head;  

/* Method to insert a node at  
   the end of the linked list */
public void addToTheLast(Node node)  
{ 
    if (head == null) 
    { 
        head = node; 
    } 
    else 
    { 
        Node temp = head; 
        while (temp.next != null) 
            temp = temp.next; 
        temp.next = node; 
    } 
} 

/* Method to print linked list */
void printList() 
{ 
    Node temp = head; 
    while (temp != null) 
    { 
        System.out.print(temp.data + " "); 
        temp = temp.next; 
    }  
    System.out.println(); 
} 

// Driver Code 
public static void main(String args[]) 
{ 
    /* Let us create two sorted linked 
       lists to test the methods  
       Created lists: 
           llist1: 5->10->15, 
           llist2: 2->3->20 
    */
    MergeLists llist1 = new MergeLists(); 
    MergeLists llist2 = new MergeLists(); 

    // Node head1 = new Node(5); 
    llist1.addToTheLast(new Node(5)); 
    llist1.addToTheLast(new Node(10)); 
    llist1.addToTheLast(new Node(15)); 

    // Node head2 = new Node(2); 
    llist2.addToTheLast(new Node(2)); 
    llist2.addToTheLast(new Node(3)); 
    llist2.addToTheLast(new Node(20)); 

    llist1.head = new Gfg().sortedMerge(llist1.head,  
                                        llist2.head); 
    llist1.printList();      

} 
} 

class Gfg 
{ 
/* Takes two lists sorted in  
increasing order, and splices  
their nodes together to make  
one big sorted list which is  
returned. */
Node sortedMerge(Node headA, Node headB) 
{ 

    /* a dummy first node to  
       hang the result on */
    Node dummyNode = new Node(0); 

    /* tail points to the  
    last result node */
    Node tail = dummyNode; 
    while(true)  
    { 

        /* if either list runs out,  
        use the other list */
        if(headA == null) 
        { 
            tail.next = headB; 
            break; 
        } 
        if(headB == null) 
        { 
            tail.next = headA; 
            break; 
        } 

        /* Compare the data of the two 
        lists whichever lists' data is  
        smaller, append it into tail and 
        advance the head to the next Node 
        */
        if(headA.data <= headB.data) 
        { 
            tail.next = headA; 
            headA = headA.next; 
        }  
        else
        { 
            tail.next = headB; 
            headB = headB.next; 
        } 

        /* Advance the tail */
        tail = tail.next; 
    } 
    return dummyNode.next; 
} 
} 

// This code is contributed 
// by Shubhaw Kumar 

```

## Python3

```py

""" Python program to merge two 
sorted linked lists """

# Linked List Node 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# Create & Handle List operations 
class LinkedList: 
    def __init__(self): 
        self.head = None

    # Method to display the list 
    def printList(self): 
        temp = self.head 
        while temp: 
            print(temp.data, end=" ") 
            temp = temp.next

    # Method to add element to list 
    def addToList(self, newData): 
        newNode = Node(newData) 
        if self.head is None: 
            self.head = newNode 
            return

        last = self.head 
        while last.next: 
            last = last.next

        last.next = newNode 

# Function to merge the lists 
# Takes two lists which are sorted 
# joins them to get a single sorted list 
def mergeLists(headA, headB): 

    # A dummy node to store the result 
    dummyNode = Node(0) 

    # Tail stores the last node 
    tail = dummyNode 
    while True: 

        # If any of the list gets completely empty 
        # directly join all the elements of the other list 
        if headA is None: 
            tail.next = headB 
            break
        if headB is None: 
            tail.next = headA 
            break

        # Compare the data of the lists and whichever is smaller is 
        # appended to the last of the merged list and the head is changed 
        if headA.data <= headB.data: 
            tail.next = headA 
            headA = headA.next
        else: 
            tail.next = headB 
            headB = headB.next

        # Advance the tail 
        tail = tail.next

    # Returns the head of the merged list 
    return dummyNode.next

# Create 2 lists 
listA = LinkedList() 
listB = LinkedList() 

# Add elements to the list in sorted order 
listA.addToList(5) 
listA.addToList(10) 
listA.addToList(15) 

listB.addToList(2) 
listB.addToList(3) 
listB.addToList(20) 

# Call the merge function 
listA.head = mergeLists(listA.head, listB.head) 

# Display merged list 
print("Merged Linked List is:") 
listA.printList() 

""" This code is contributed 
by Debidutta Rath """

```

## C#

```cs

/* C# program to merge two  
sorted linked lists */
using System; 

    /* Link list node */
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

    public class MergeLists  
    {  
        Node head;  

        /* Method to insert a node at  
        the end of the linked list */
        public void addToTheLast(Node node)  
        {  
            if (head == null)  
            {  
                head = node;  
            }  
            else
            {  
                Node temp = head;  
                while (temp.next != null)  
                    temp = temp.next;  
                temp.next = node;  
            }  
        }  

        /* Method to print linked list */
        void printList()  
        {  
            Node temp = head;  
            while (temp != null)  
            {  
                   Console.Write(temp.data + " ");  
                temp = temp.next;  
            }  
            Console.WriteLine();  
        }  

        // Driver Code  
        public static void Main(String []args)  
        {  
            /* Let us create two sorted linked  
            lists to test the methods  
            Created lists:  
                   llist1: 5->10->15,  
                llist2: 2->3->20  
            */
            MergeLists llist1 = new MergeLists();  
            MergeLists llist2 = new MergeLists();  

            // Node head1 = new Node(5);  
            llist1.addToTheLast(new Node(5));  
            llist1.addToTheLast(new Node(10));  
            llist1.addToTheLast(new Node(15));  

            // Node head2 = new Node(2);  
            llist2.addToTheLast(new Node(2));  
            llist2.addToTheLast(new Node(3));  
            llist2.addToTheLast(new Node(20));  

            llist1.head = new Gfg().sortedMerge(llist1.head,  
                                            llist2.head);  
            llist1.printList();  

        }  
    }  

    public class Gfg  
    {  
    /* Takes two lists sorted in  
    increasing order, and splices  
    their nodes together to make  
    one big sorted list which is  
    returned. */
    public Node sortedMerge(Node headA, Node headB)  
    {  

        /* a dummy first node to  
        hang the result on */
        Node dummyNode = new Node(0);  

        /* tail points to the  
        last result node */
        Node tail = dummyNode;  
        while(true)  
        {  

            /* if either list runs out,  
            use the other list */
            if(headA == null)  
            {  
                tail.next = headB;  
                break;  
            }  
            if(headB == null)  
            {  
                tail.next = headA;  
                break;  
            }  

            /* Compare the data of the two  
            lists whichever lists' data is  
            smaller, append it into tail and  
            advance the head to the next Node  
            */
            if(headA.data <= headB.data)  
            {  
                tail.next = headA;  
                headA = headA.next;  
            }  
            else
            {  
                tail.next = headB;  
                headB = headB.next;  
            }  

            /* Advance the tail */
            tail = tail.next;  
        }  
        return dummyNode.next;  
    }  
}  

// This code is contributed 29AjayKumar 

```

**输出**：

```
Merged Linked List is: 
2 3 5 10 15 20 

```

**方法 2（使用本地引用）**

此解决方案在结构上与上述非常相似，但避免使用虚拟节点。 相反，它维护一个`struct node`指针`lastPtrRef`，该指针始终指向结果列表的最后一个指针。 这解决了虚拟节点所做的相同情况—在结果列表为空时处理结果列表。 如果您试图在列表尾部建立列表，则可以使用虚拟节点或结构节点的“引用”策略（有关详细信息，请参见第 1 节）。

## C++

```cpp

Node* SortedMerge(Node* a, Node* b)  
{  
Node* result = NULL;  

/* point to the last result pointer */
Node** lastPtrRef = &result;  

while(1)  
{  
    if (a == NULL)  
    {  
    *lastPtrRef = b;  
    break;  
    }  
    else if (b==NULL)  
    {  
    *lastPtrRef = a;  
    break;  
    }  
    if(a->data <= b->data)  
    {  
    MoveNode(lastPtrRef, &a);  
    }  
    else
    {  
    MoveNode(lastPtrRef, &b);  
    }  

    /* tricky: advance to point to the next ".next" field */
    lastPtrRef = &((*lastPtrRef)->next);  
}  
return(result);  
}  

//This code is contributed by rathbhupendra 

```

## C

```c

struct Node* SortedMerge(struct Node* a, struct Node* b)  
{ 
  struct Node* result = NULL; 

  /* point to the last result pointer */
  struct Node** lastPtrRef = &result;  

  while(1)  
  { 
    if (a == NULL)  
    { 
      *lastPtrRef = b; 
       break; 
    } 
    else if (b==NULL)  
    { 
       *lastPtrRef = a; 
       break; 
    } 
    if(a->data <= b->data)  
    { 
      MoveNode(lastPtrRef, &a); 
    } 
    else 
    { 
      MoveNode(lastPtrRef, &b); 
    } 

    /* tricky: advance to point to the next ".next" field */
    lastPtrRef = &((*lastPtrRef)->next);  
  } 
  return(result); 
} 

```

**方法 3（使用递归）**

合并是那些不错的递归问题之一，其中递归解决方案代码比迭代代码干净得多。 但是，您可能不希望将递归版本用于生产代码，因为它会使用与列表长度成比例的栈空间。

## C++

```cpp

Node* SortedMerge(Node* a, Node* b)  
{  
    Node* result = NULL;  

    /* Base cases */
    if (a == NULL)  
        return(b);  
    else if (b == NULL)  
        return(a);  

    /* Pick either a or b, and recur */
    if (a->data <= b->data)  
    {  
        result = a;  
        result->next = SortedMerge(a->next, b);  
    }  
    else
    {  
        result = b;  
        result->next = SortedMerge(a, b->next);  
    }  
    return(result);  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

struct Node* SortedMerge(struct Node* a, struct Node* b)  
{ 
  struct Node* result = NULL; 

  /* Base cases */
  if (a == NULL)  
     return(b); 
  else if (b==NULL)  
     return(a); 

  /* Pick either a or b, and recur */
  if (a->data <= b->data)  
  { 
     result = a; 
     result->next = SortedMerge(a->next, b); 
  } 
  else 
  { 
     result = b; 
     result->next = SortedMerge(a, b->next); 
  } 
  return(result); 
} 

```

## Java

```java

class GFG  
{ 
    public Node SortedMerge(Node A, Node B)  
    { 

        if(A == null) return B; 
        if(B == null) return A; 

        if(A.data < B.data)  
        { 
            A.next = SortedMerge(A.next, B); 
            return A; 
        } 
        else 
        { 
            B.next = SortedMerge(A, B.next); 
            return B; 
        } 

    } 
} 

// This code is contributed by Tuhin Das 

```

## Python3

```py

# Python3 program merge two sorted linked 
# in third linked list using recursive. 

# Node class 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# Constructor to initialize the node object 
class LinkedList: 

    # Function to initialize head 
    def __init__(self): 
        self.head = None

    # Method to print linked list 
    def printList(self): 
        temp = self.head 

        while temp : 
            print(temp.data, end="->") 
            temp = temp.next

    # Function to add of node at the end. 
    def append(self, new_data): 
        new_node = Node(new_data) 

        if self.head is None: 
            self.head = new_node 
            return
        last = self.head 

        while last.next: 
            last = last.next
        last.next = new_node 

# Function to merge two sorted linked list. 
def mergeLists(head1, head2): 

    # create a temp node NULL 
    temp = None

    # List1 is empty then return List2 
    if head1 is None: 
        return head2 

    # if List2 is empty then return List1 
    if head2 is None: 
        return head1 

    # If List1's data is smaller or 
    # equal to List2's data 
    if head1.data <= head2.data: 

        # assign temp to List1's data 
        temp = head1 

        # Again check List1's data is smaller or equal List2's  
        # data and call mergeLists function. 
        temp.next = mergeLists(head1.next, head2) 

    else: 
        # If List2's data is greater than or equal List1's  
        # data assign temp to head2 
        temp = head2 

        # Again check List2's data is greater or equal List's 
        # data and call mergeLists function. 
        temp.next = mergeLists(head1, head2.next) 

    # return the temp list. 
    return temp 

# Driver Function 
if __name__ == '__main__': 

    # Create linked list : 
    # 10->20->30->40->50 
    list1 = LinkedList() 
    list1.append(10) 
    list1.append(20) 
    list1.append(30) 
    list1.append(40) 
    list1.append(50) 

    # Create linked list 2 : 
    # 5->15->18->35->60 
    list2 = LinkedList() 
    list2.append(5) 
    list2.append(15) 
    list2.append(18) 
    list2.append(35) 
    list2.append(60) 

    # Create linked list 3 
    list3 = LinkedList() 

    # Merging linked list 1 and linked list 2 
    # in linked list 3 
    list3.head = mergeLists(list1.head, list2.head) 

    print(" Merged Linked List is : ", end="") 
    list3.printList()      

# This code is contributed by 'Shriaknt13'.          

```

## C#

```cs

using System; 

class GFG{ 

public Node sortedMerge(Node A, Node B)  
{ 

    // Base cases 
    if (A == null) 
        return B; 
    if (B == null)  
        return A; 

    // Pick either a or b, and recur  
    if (A.data < B.data)  
    { 
        A.next = sortedMerge(A.next, B); 
        return A; 
    } 
    else
    { 
        B.next = sortedMerge(A, B.next); 
        return B; 
    } 
} 
} 

// This code is contributed by hunter2000

```

请参考以下帖子以了解更简单的实现：

[**合并两个排序列表（原地）**](https://www.geeksforgeeks.org/merge-two-sorted-lists-place/)

来源： [http://cslibrary.stanford.edu/ 105 / LinkedListProblems.pdf](http://cslibrary.stanford.edu/105/LinkedListProblems.pdf)

如果您发现上述代码/算法不正确，或者找到解决相同问题的更好方法，请写评论。

