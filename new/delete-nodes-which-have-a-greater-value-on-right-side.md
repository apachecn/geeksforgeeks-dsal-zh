# 删除右侧

上具有较大值的节点

给定一个单链列表，请删除右侧所有具有较大值的所有节点。
示例：
**a）**列表12- > 15- > 10- > 11- > 5- > 6- > 2- > 3- > NULL应该更改为15- > 11- > 6- > 3- > NULL。 请注意，已删除12、10、5和2，因为右侧的值更大。
当我们检查12时，我们发现在12之后有一个值大于12（即15）的节点，因此我们删除了12。
当我们检查15时，我们发现在15之后没有节点具有更大的值。 大于15，因此我们保留此节点。
像这样，我们得到15- > 6- > 3
**b）**列表10- > 20- > 30- > 40- > 50- > 60- > NULL应该更改为60- > NULL。 请注意，已删除10、20、30、40和50，因为它们在右侧都具有较大的值。
**c）**列表60- > 50- > 40- > 30- > 20- > 10- > NULL不应更改。

**方法1（简单）**
使用两个循环。 在外部循环中，一个接一个地选择链表的节点。 在内部循环中，检查是否存在一个节点的值大于选取的节点。 如果存在一个值更大的节点，则删除选择的节点。
时间复杂度：O（n ^ 2）
**方法2（反向使用）**
感谢Paras提供了以下算法。
1.反转列表。
2.遍历反向列表。 保持最大到现在为止。 如果下一个节点小于最大节点，则删除下一个节点，否则最大=下一个节点。
3.再次反转列表以保留原始顺序。
时间复杂度：O（n）
感谢R.Srinivasan提供的以下代码。

## C++

```cpp

// C++ program to delete nodes 
// which have a greater value on
// right side
#include <bits/stdc++.h>
using namespace std;

/* structure of a linked list node */
struct Node
{
    int data;
    struct Node* next;
};

/* prototype for utility functions */
void reverseList(struct Node** headref);
void _delLesserNodes(struct Node* head);

/* Deletes nodes which have a node with 
greater value node on left side */
void delLesserNodes(struct Node** head_ref)
{
    /* 1) Reverse the linked list */
    reverseList(head_ref);

    /* 2) In the reversed list, delete nodes 
    which have a node with greater value node 
    on left side. Note that head node is never 
    deleted because it is the leftmost node.*/
    _delLesserNodes(*head_ref);

    /* 3) Reverse the linked list again to 
    retain the original order */
    reverseList(head_ref);
}

/* Deletes nodes which have
greater value node(s) on left side */
void _delLesserNodes(struct Node* head)
{
    struct Node* current = head;

    /* Initialize max */
    struct Node* maxnode = head;
    struct Node* temp;

    while (current != NULL && 
           current->next != NULL) 
    {
        /* If current is smaller than max,
        then delete current */
        if (current->next->data < maxnode->data) 
        {
            temp = current->next;
            current->next = temp->next;
            free(temp);
        }

        /* If current is greater than max, 
            then update max and move current */
        else
        {
            current = current->next;
            maxnode = current;
        }
    }
}

/* Utility function to insert a node 
at the beginning */
void push(struct Node** head_ref, int new_data)
{
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = new_data;
    new_node->next = *head_ref;
    *head_ref = new_node;
}

/* Utility function to reverse a linked list */
void reverseList(struct Node** headref)
{
    struct Node* current = *headref;
    struct Node* prev = NULL;
    struct Node* next;
    while (current != NULL) 
    {
        next = current->next;
        current->next = prev;
        prev = current;
        current = next;
    }
    *headref = prev;
}

/* Utility function to print a linked list */
void printList(struct Node* head)
{
    while (head != NULL) 
    {
        cout << " " << head->data ;
        head = head->next;
    }
    cout << "\n" ;
}

/* Driver program to test above functions */
int main()
{
    struct Node* head = NULL;

    /* Create following linked list
    12->15->10->11->5->6->2->3 */
    push(&head, 3);
    push(&head, 2);
    push(&head, 6);
    push(&head, 5);
    push(&head, 11);
    push(&head, 10);
    push(&head, 15);
    push(&head, 12);

    cout << "Given Linked List \n" ;
    printList(head);

    delLesserNodes(&head);

    cout << "Modified Linked List \n" ;
    printList(head);

    return 0;
}

// This code is contributed by shivanisinghss2110

```

## C

```c

// C program to delete nodes which have a greater value on
// right side
#include <stdio.h>
#include <stdlib.h>

/* structure of a linked list node */
struct Node {
    int data;
    struct Node* next;
};

/* prototype for utility functions */
void reverseList(struct Node** headref);
void _delLesserNodes(struct Node* head);

/* Deletes nodes which have a node with greater value node
  on left side */
void delLesserNodes(struct Node** head_ref)
{
    /* 1) Reverse the linked list */
    reverseList(head_ref);

    /* 2) In the reversed list, delete nodes which have a node
       with greater value node on left side. Note that head
       node is never deleted because it is the leftmost node.*/
    _delLesserNodes(*head_ref);

    /* 3) Reverse the linked list again to retain the
       original order */
    reverseList(head_ref);
}

/* Deletes nodes which have greater value node(s) on left side */
void _delLesserNodes(struct Node* head)
{
    struct Node* current = head;

    /* Initialize max */
    struct Node* maxnode = head;
    struct Node* temp;

    while (current != NULL && current->next != NULL) {
        /* If current is smaller than max, then delete current */
        if (current->next->data < maxnode->data) {
            temp = current->next;
            current->next = temp->next;
            free(temp);
        }

        /* If current is greater than max, then update max and
            move current */
        else {
            current = current->next;
            maxnode = current;
        }
    }
}

/* Utility function to insert a node at the beginning */
void push(struct Node** head_ref, int new_data)
{
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = new_data;
    new_node->next = *head_ref;
    *head_ref = new_node;
}

/* Utility function to reverse a linked list */
void reverseList(struct Node** headref)
{
    struct Node* current = *headref;
    struct Node* prev = NULL;
    struct Node* next;
    while (current != NULL) {
        next = current->next;
        current->next = prev;
        prev = current;
        current = next;
    }
    *headref = prev;
}

/* Utility function to print a linked list */
void printList(struct Node* head)
{
    while (head != NULL) {
        printf("%d ", head->data);
        head = head->next;
    }
    printf("\n");
}

/* Driver program to test above functions */
int main()
{
    struct Node* head = NULL;

    /* Create following linked list
      12->15->10->11->5->6->2->3 */
    push(&head, 3);
    push(&head, 2);
    push(&head, 6);
    push(&head, 5);
    push(&head, 11);
    push(&head, 10);
    push(&head, 15);
    push(&head, 12);

    printf("Given Linked List \n");
    printList(head);

    delLesserNodes(&head);

    printf("Modified Linked List \n");
    printList(head);

    return 0;
}

```

## Java

```java

// Java program to delete nodes which have a greater value on
// right side
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

    /* Deletes nodes which have a node with greater
       value node on left side */
    void delLesserNodes()
    {
        /* 1.Reverse the linked list */
        reverseList();

        /* 2) In the reversed list, delete nodes which
           have a node with greater value node on left
           side. Note that head node is never deleted
           because it is the leftmost node.*/
        _delLesserNodes();

        /* 3) Reverse the linked list again to retain
           the original order */
        reverseList();
    }

    /* Deletes nodes which have greater value node(s)
       on left side */
    void _delLesserNodes()
    {
        Node current = head;

        /* Initialise max */
        Node maxnode = head;
        Node temp;

        while (current != null && current.next != null) {
            /* If current is smaller than max, then delete
               current */
            if (current.next.data < maxnode.data) {
                temp = current.next;
                current.next = temp.next;
                temp = null;
            }

            /* If current is greater than max, then update
               max and move current */
            else {
                current = current.next;
                maxnode = current;
            }
        }
    }

    /* Utility functions */

    /* Inserts a new Node at front of the list. */
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

    /* Function to reverse the linked list */
    void reverseList()
    {
        Node current = head;
        Node prev = null;
        Node next;
        while (current != null) {
            next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }
        head = prev;
    }

    /* Function to print linked list */
    void printList()
    {
        Node temp = head;
        while (temp != null) {
            System.out.print(temp.data + " ");
            temp = temp.next;
        }
        System.out.println();
    }

    /* Drier program to test above functions */
    public static void main(String args[])
    {
        LinkedList llist = new LinkedList();

        /* Constructed Linked List is 12->15->10->11->
           5->6->2->3 */
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
} /* This code is contributed by Rajat Mishra */

```

**Output**

```
Given Linked List 
 12 15 10 11 5 6 2 3
Modified Linked List 
 15 11 6 3

```

**方法3：**

另一种更简单的方法是从开始遍历列表，并在当前节点

让我们假设您必须删除当前节点X

1.将下一个节点的数据复制到X，即X.data = X.next.data

2.复制下一个节点的下一个地址，即X.next = X.next.next;

仅当当前节点>下一个节点时，才在列表中向前移动。

## Java

```java

// Java program for above approach
import java.io.*;

// This class represents a single node 
// in a linked list
class Node {

    int data;
    Node next;

    public Node(int data){
        this.data = data;
        this.next = null;
    }
}

//This is a utility class for linked list
class LLUtil{

      // This function creates a linked list from a 
    // given array and returns head
    public Node createLL(int[] arr){

        Node head = new Node(arr[0]);
        Node temp = head;

        Node newNode = null;
        for(int i = 1; i < arr.length; i++){
            newNode = new Node(arr[i]);
            temp.next = newNode;
            temp = temp.next;
        }
        return head;
    }

      //This function prints given linked list
      public void printLL(Node head){

        while(head != null){
            System.out.print(head.data + " ");
            head = head.next;
        }
        System.out.println();
    }

}

class GFG {
    public static void main (String[] args) {

          int[] arr = {12,15,10,11,5,6,2,3};
        LLUtil llu = new LLUtil();
          Node head = llu.createLL(arr);
        System.out.println("Given Linked List");
        llu.printLL(head);
        deleteNodesOnRightSide(head);
          System.out.println("Modified Linked List");
          llu.printLL(head);

    }

  //Main function
     public static void deleteNodesOnRightSide(Node head){

        Node temp = head;
        while(temp != null && temp.next != null){

            //Copying next node data into current node
              //i.e. we are indirectly deleting current node
            if(temp.data < temp.next.data){
                temp.data = temp.next.data;
                temp.next = temp.next.next;
            }
            else{
                  //move to the next node
                temp = temp.next;
            }
        }
    }
}

```

资源：

[https://www.geeksforgeeks.org/forum/topic/amazon-interview-question-for-software-engineerdeveloper-about-linked-lists-6](https://www.geeksforgeeks.org/forum/topic/amazon-interview-question-for-software-engineerdeveloper-about-linked-lists-6)

如果您发现上述代码/算法有误，请写评论，或者找到其他解决相同问题的方法。

