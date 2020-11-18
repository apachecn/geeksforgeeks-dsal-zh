# 编写函数以获取链表

中的第N个节点

编写一个GetNth（）函数，该函数接受一个链表和一个整数索引，并返回存储在该索引位置的节点中的数据值。

**示例：**

```
Input:  1->10->30->14,  index = 2
Output: 30  
The node at index 2 is 30

```

**算法：**

```
1\. Initialize count = 0
2\. Loop through the link list
     a. if count is equal to the passed index then return current
         node
     b. Increment count
     c. change current to point to next of the current.

```

**实施：**

## C ++

```

// C++ program to find n'th
// node in linked list
#include <assert.h>
#include <bits/stdc++.h>
using namespace std;

// Link list node
class Node {
public:
    int data;
    Node* next;
};

/* Given a reference (pointer to
pointer) to the head of a list
and an int, push a new node on
the front of the list. */
void push(Node** head_ref, int new_data)
{

    // allocate node
    Node* new_node = new Node();

    // put in the data
    new_node->data = new_data;

    // link the old list
    // off the new node
    new_node->next = (*head_ref);

    // move the head to point
    // to the new node
    (*head_ref) = new_node;
}

// Takes head pointer of
// the linked list and index
// as arguments and return
// data at index
int GetNth(Node* head, int index)
{

    Node* current = head;

    // the index of the
    // node we're currently
    // looking at
    int count = 0;
    while (current != NULL) {
        if (count == index)
            return (current->data);
        count++;
        current = current->next;
    }

    /* if we get to this line,
    the caller was asking
    for a non-existent element
    so we assert fail */
    assert(0);
}

// Driver Code
int main()
{

    // Start with the
    // empty list
    Node* head = NULL;

    // Use push() to construct
    // below list
    // 1->12->1->4->1
    push(&head, 1);
    push(&head, 4);
    push(&head, 1);
    push(&head, 12);
    push(&head, 1);

    // Check the count
    // function
    cout << "Element at index 3 is " << GetNth(head, 3);
    return 0;
}

// This code is contributed by rathbhupendra

```

## C

```

// C program to find n'th
// node in linked list
#include <assert.h>
#include <stdio.h>
#include <stdlib.h>

// Link list node
struct Node {
    int data;
    struct Node* next;
};

/* Given a reference (pointer to
   pointer) to the head of a list
   and an int, push a new node on
   the front of the list. */
void push(struct Node** head_ref, int new_data)
{

    // allocate node
    struct Node* new_node
        = (struct Node*)malloc(sizeof(struct Node));

    // put in the data
    new_node->data = new_data;

    // link the old list
    // off the new node
    new_node->next = (*head_ref);

    // move the head to point
    // to the new node
    (*head_ref) = new_node;
}

// Takes head pointer of
// the linked list and index
// as arguments and return
// data at index
int GetNth(struct Node* head, int index)
{

    struct Node* current = head;

    // the index of the
    // node we're currently
    // looking at
    int count = 0;
    while (current != NULL) {
        if (count == index)
            return (current->data);
        count++;
        current = current->next;
    }

    /* if we get to this line,
       the caller was asking
       for a non-existent element
       so we assert fail */
    assert(0);
}

// Driver Code
int main()
{

    // Start with the
    // empty list
    struct Node* head = NULL;

    // Use push() to construct
    // below list
    // 1->12->1->4->1
    push(&head, 1);
    push(&head, 4);
    push(&head, 1);
    push(&head, 12);
    push(&head, 1);

    // Check the count
    // function
    printf("Element at index 3 is %d", GetNth(head, 3));
    getchar();
}

```

## 爪哇

```

// Java program to find n'th node in linked list

class Node {
    int data;
    Node next;
    Node(int d)
    {
        data = d;
        next = null;
    }
}

class LinkedList {
    Node head; // the head of list

    /* Takes index as argument and return data at index*/
    public int GetNth(int index)
    {
        Node current = head;
        int count = 0; /* index of Node we are
                          currently looking at */
        while (current != null)
        {
            if (count == index)
                return current.data;
            count++;
            current = current.next;
        }

        /* if we get to this line, the caller was asking
        for a non-existent element so we assert fail */
        assert (false);
        return 0;
    }

    /* Given a reference to the head of a list and an int,
       inserts a new Node on the front of the list. */
    public void push(int new_data)
    {

        /* 1\. alloc the Node and put data*/
        Node new_Node = new Node(new_data);

        /* 2\. Make next of new Node as head */
        new_Node.next = head;

        /* 3\. Move the head to point to new Node */
        head = new_Node;
    }

    /* Driver code*/
    public static void main(String[] args)
    {
        /* Start with empty list */
        LinkedList llist = new LinkedList();

        /* Use push() to construct below list
           1->12->1->4->1  */
        llist.push(1);
        llist.push(4);
        llist.push(1);
        llist.push(12);
        llist.push(1);

        /* Check the count function */
        System.out.println("Element at index 3 is "
                           + llist.GetNth(3));
    }
}

```

## 蟒蛇

```

# A complete working Python program to find n'th node
# in a linked list

# Node class

class Node:
    # Function to initialise the node object
    def __init__(self, data):
        self.data = data  # Assign data
        self.next = None  # Initialize next as null

# Linked List class contains a Node object
class LinkedList:

    # Function to initialize head
    def __init__(self):
        self.head = None

    # This function is in LinkedList class. It inserts
    # a new node at the beginning of Linked List.

    def push(self, new_data):

        # 1 & 2: Allocate the Node &
        #     Put in the data
        new_node = Node(new_data)

        # 3\. Make next of new Node as head
        new_node.next = self.head

        # 4\. Move the head to point to new Node
        self.head = new_node

    # Returns data at given index in linked list
    def getNth(self, index):
        current = self.head  # Initialise temp
        count = 0  # Index of current node

        # Loop while end of linked list is not reached
        while (current):
            if (count == index):
                return current.data
            count += 1
            current = current.next

        # if we get to this line, the caller was asking
        # for a non-existent element so we assert fail
        assert(false)
        return 0

# Driver Code
if __name__ == '__main__':

    llist = LinkedList()

    # Use push() to construct below list
    # 1->12->1->4->1
    llist.push(1)
    llist.push(4)
    llist.push(1)
    llist.push(12)
    llist.push(1)

    n = 3
    print("Element at index 3 is :", llist.getNth(n))

```

## C＃

```

// C# program to find n'th node in linked list
using System;
using System.Diagnostics;

public class Node {
    public int data;
    public Node next;
    public Node(int d)
    {
        data = d;
        next = null;
    }
}

class LinkedList {
    Node head; // the head of list

    /* Takes index as argument and return data at index*/
    public int GetNth(int index)
    {
        Node current = head;
        int count = 0; /* index of Node we are
                        currently looking at */
        while (current != null) {
            if (count == index)
                return current.data;
            count++;
            current = current.next;
        }

        /* if we get to this line, the caller was asking
        for a non-existent element so we assert fail */
        Debug.Assert(false);
        return 0;
    }

    /* Given a reference to the head of a list and an int,
    inserts a new Node on the front of the list. */
    public void push(int new_data)
    {

        /* 1\. alloc the Node and put data*/
        Node new_Node = new Node(new_data);

        /* 2\. Make next of new Node as head */
        new_Node.next = head;

        /* 3\. Move the head to point to new Node */
        head = new_Node;
    }

    /* Driver code*/
    public static void Main(String[] args)
    {
        /* Start with empty list */
        LinkedList llist = new LinkedList();

        /* Use push() to construct below list
        1->12->1->4->1 */
        llist.push(1);
        llist.push(4);
        llist.push(1);
        llist.push(12);
        llist.push(1);

        /* Check the count function */
        Console.WriteLine("Element at index 3 is "
                          + llist.GetNth(3));
    }
}

// This code is contributed by Arnab Kundu

```

**Output**

```
Element at index 3 is 4
```

**时间复杂度：** O（n）

**方法2-递归**
此方法由 [MY_DOOM](https://auth.geeksforgeeks.org/user/MY_DOOM) 贡献。

**算法：**

```
Algorithm
getnth(node,n)
1\. Initialize count = 0
2\. if count==n
     return node->data
3\. else
    return getnth(node->next,n-1)

```

**实施：**

## C ++

```

// C program to find n'th node in linked list
// using recursion
#include <bits/stdc++.h>
using namespace std;

/* Link list node */
struct Node {
    int data;
    struct Node* next;
};

/*  Given a reference (pointer to pointer) to
    the head of a list and an int, push a
    new node on the front of the list. */
void push(struct Node** head_ref, int new_data)
{
    /* allocate node */
    struct Node* new_node
        = (struct Node*)malloc(sizeof(struct Node));

    /* put in the data */
    new_node->data = new_data;

    /* link the old list off the new node */
    new_node->next = (*head_ref);

    /* move the head to point to the new node */
    (*head_ref) = new_node;
}

/* Takes head pointer of the linked list and index
    as arguments and return data at index*/
int GetNth(struct Node* head, int n)
{
    //if length of the list is less
    // than the given index, return 0
    if(head == NULL)
      return -1;
    int count = 0;

    // if count equal to n return node->data
    if (count == n)
        return head->data;

    // recursively decrease n and increase
    // head to next pointer
    return GetNth(head->next, n - 1);
}

/* Driver code*/
int main()
{
    /* Start with the empty list */
    struct Node* head = NULL;

    /* Use push() to construct below list
     1->12->1->4->1  */
    push(&head, 1);
    push(&head, 4);
    push(&head, 1);
    push(&head, 12);
    push(&head, 1);

    /* Check the count function */
    printf("Element at index 3 is %d", GetNth(head, 3));
    getchar();
}

```

## 爪哇

```

// Java program to find n'th node in linked list
// using recursion
class GFG {

    /* Link list node */
    static class Node {
        int data;
        Node next;
        Node(int data) { this.data = data; }
    }

    /* Given a reference (pointer to pointer) to
        the head of a list and an int, push a
        new node on the front of the list. */
    static Node push(Node head, int new_data)
    {
        /* allocate node */
        Node new_node = new Node(new_data);

        /* put in the data */
        new_node.data = new_data;

        new_node.next = head;

        head = new_node;

        return head;
    }

    /* Takes head pointer of the linked list and index
        as arguments and return data at index*/
    static int GetNth(Node head, int n)
    {
        int count = 0;
        if (head == null) // edge case - if head is null
            return -1;
        // if count equal too n return node.data
        if (count == n)
            return head.data;

        // recursively decrease n and increase
        // head to next pointer
        return GetNth(head.next, n - 1);
    }

    /* Driver code*/
    public static void main(String args[])
    {
        /* Start with the empty list */
        Node head = null;

        /* Use push() to con below list
        1.12.1.4.1 */
        head = push(head, 1);
        head = push(head, 4);
        head = push(head, 1);
        head = push(head, 12);
        head = push(head, 1);

        /* Check the count function */
        System.out.printf("Element at index 3 is %d",
                          GetNth(head, 3));
    }
}
// This code is contributed by Arnab Kundu

```

## Python3

```

# Python3 program to find n'th node in
# linked list using recursion

class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    ''' Given a reference (pointer to pointer) to the
        head of a list and an int, push a new node on
        the front of the list. '''

    def push(self, new_data):  # make new node and add
                              # into LinkedList
        new_node = Node(new_data)
        new_node.next = self.head
        self.head = new_node

    def getNth(self, llist, position):

        # call recursive method
        llist.getNthNode(self.head, position, llist)

    # recursive method to find Nth Node
    def getNthNode(self, head, position, llist):
        count = 0  # initialize count
        if(head):
            if count == position:  # if count is equal to position,
                                  # it means we have found the position
                print(head.data)
            else:
                llist.getNthNode(head.next, position - 1, llist)
        else:  # if head doesn't exist we have
              # traversed the LinkedList
            print('Index Doesn\'t exist')

# Driver Code
if __name__ == "__main__":
    llist = LinkedList()
    llist.push(1)
    llist.push(4)
    llist.push(1)
    llist.push(12)
    llist.push(1)
    # llist.getNth(llist,int(input()))
    # Enter the node position here
    # first argument is instance of LinkedList

    print("Element at Index 3 is", end=" ")
    llist.getNth(llist, 3)

# This code is contributed by Yogesh Joshi

```

## C＃

```

// C# program to find n'th node in
// linked list using recursion
using System;

class GFG {

    /* Link list node */
    public class Node {
        public int data;
        public Node next;
        public Node(int data) { this.data = data; }
    }

    /* Given a reference (pointer to pointer) to
        the head of a list and an int, push a
        new node on the front of the list. */
    static Node push(Node head, int new_data)
    {
        /* allocate node */
        Node new_node = new Node(new_data);

        /* put in the data */
        new_node.data = new_data;

        new_node.next = head;

        head = new_node;

        return head;
    }

    /* Takes head pointer of the linked list and index
        as arguments and return data at index*/
    static int GetNth(Node head, int n)
    {
        // Base Condition
        if (head == null)
            return -1;

        int count = 0;

        // if count equal too n return node.data
        // Test Condition
        if (count == n)
            return head.data;

        // recursively decrease n and increase
        // head to next pointer
        return GetNth(head.next, n - 1);
    }

    /* Driver code*/
    public static void Main()
    {
        /* Start with the empty list */
        Node head = null;

        /* Use push() to con below list
        1.12.1.4.1 */
        head = push(head, 1);
        head = push(head, 4);
        head = push(head, 1);
        head = push(head, 12);
        head = push(head, 1);

        /* Check the count function */
        Console.Write("Element at index 3 is {0}",
                      GetNth(head, 3));
    }
}
/*Code improvement by Aishwarya Mittal*/
/* This code contributed by PrinciRaj1992 */

```

**Output**

```
Element at index 3 is 4
```

**时间复杂度：** O（n）
https://youtu.be/iyOh1IWXnq4

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。