# 查找链接列表的长度（迭代和递归）

编写一个函数以计算给定单链列表中的节点数。

[![linkedlist_find_length](img/e38a7cce1aae90394ef3ebc5cd8323c1.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2015/03/Linkedlist_find_length.png)

例如，对于链接列表1-> 3-> 1-> 2-> 1，该函数应返回5。

**迭代解决方案**

```
1) Initialize count as 0 
2) Initialize a node pointer, current = head.
3) Do following while current is not NULL
     a) current = current -> next
     b) count++;
4) Return count 
```

以下是上述算法的实现，以找到节点数。

## C ++

```

// Iterative C++ program to find length  
// or count of nodes in a linked list  
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node  
{  
    public: 
    int data;  
    Node* next;  
};  

/* Given a reference (pointer to pointer) to the head  
of a list and an int, push a new node on the front  
of the list. */
void push(Node** head_ref, int new_data)  
{  
    /* allocate node */
    Node* new_node =new Node(); 

    /* put in the data */
    new_node->data = new_data;  

    /* link the old list off the new node */
    new_node->next = (*head_ref);  

    /* move the head to point to the new node */
    (*head_ref) = new_node;  
}  

/* Counts no. of nodes in linked list */
int getCount(Node* head)  
{  
    int count = 0; // Initialize count  
    Node* current = head; // Initialize current  
    while (current != NULL)  
    {  
        count++;  
        current = current->next;  
    }  
    return count;  
}  

/* Driver program to test count function*/
int main()  
{  
    /* Start with the empty list */
    Node* head = NULL;  

    /* Use push() to construct below list  
    1->2->1->3->1 */
    push(&head, 1);  
    push(&head, 3);  
    push(&head, 1);  
    push(&head, 2);  
    push(&head, 1);  

    /* Check the count function */
    cout<<"count of nodes is "<< getCount(head);  
    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## C

```

// Iterative C program to find length or count of nodes in a linked list 
#include<stdio.h> 
#include<stdlib.h> 

/* Link list node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

/* Given a reference (pointer to pointer) to the head 
  of a list and an int, push a new node on the front 
  of the list. */
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

/* Counts no. of nodes in linked list */
int getCount(struct Node* head) 
{ 
    int count = 0;  // Initialize count 
    struct Node* current = head;  // Initialize current 
    while (current != NULL) 
    { 
        count++; 
        current = current->next; 
    } 
    return count; 
} 

/* Driver program to test count function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Use push() to construct below list 
     1->2->1->3->1  */
    push(&head, 1); 
    push(&head, 3); 
    push(&head, 1); 
    push(&head, 2); 
    push(&head, 1); 

    /* Check the count function */
    printf("count of nodes is %d", getCount(head)); 
    return 0; 
} 

```

## 爪哇

```

// Java program to count number of nodes in a linked list 

/* Linked list Node*/
class Node 
{ 
    int data; 
    Node next; 
    Node(int d)  { data = d;  next = null; } 
} 

// Linked List class 
class LinkedList 
{ 
    Node head;  // head of list 

    /* Inserts a new Node at front of the list. */
    public void push(int new_data) 
    { 
        /* 1 & 2: Allocate the Node & 
                  Put in the data*/
        Node new_node = new Node(new_data); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    /* Returns count of nodes in linked list */
    public int getCount() 
    { 
        Node temp = head; 
        int count = 0; 
        while (temp != null) 
        { 
            count++; 
            temp = temp.next; 
        } 
        return count; 
    } 

    /* Driver program to test above functions. Ideally 
       this function should be in a separate user class. 
       It is kept here to keep code compact */
    public static void main(String[] args) 
    { 
        /* Start with the empty list */
        LinkedList llist = new LinkedList(); 
        llist.push(1); 
        llist.push(3); 
        llist.push(1); 
        llist.push(2); 
        llist.push(1); 

        System.out.println("Count of nodes is " + 
                           llist.getCount()); 
    } 
} 

```

## 蟒蛇

```

# A complete working Python program to find length of a 
# Linked List iteratively 

# Node class 
class Node: 
    # Function to initialise the node object 
    def __init__(self, data): 
        self.data = data # Assign data 
        self.next = None # Initialize next as null 

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

    # This function counts number of nodes in Linked List 
    # iteratively, given 'node' as starting node. 
    def getCount(self): 
        temp = self.head # Initialise temp 
        count = 0 # Initialise count 

        # Loop while end of linked list is not reached 
        while (temp): 
            count += 1
            temp = temp.next
        return count 

# Code execution starts here 
if __name__=='__main__': 
    llist = LinkedList() 
    llist.push(1) 
    llist.push(3) 
    llist.push(1) 
    llist.push(2) 
    llist.push(1) 
    print ("Count of nodes is :",llist.getCount()) 

```

## C＃

```

// C# program to count number 
// of nodes in a linked list 
using System; 

/* Linked list Node*/
public class Node 
{ 
    public int data; 
    public Node next; 
    public Node(int d)  
    {  
        data = d; next = null;  
    } 
} 

// Linked List class 
public class LinkedList 
{ 
    Node head; // head of list 

    /* Inserts a new Node at front of the list. */
    public void push(int new_data) 
    { 
        /* 1 & 2: Allocate the Node & 
                Put in the data*/
        Node new_node = new Node(new_data); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    /* Returns count of nodes in linked list */
    public int getCount() 
    { 
        Node temp = head; 
        int count = 0; 
        while (temp != null) 
        { 
            count++; 
            temp = temp.next; 
        } 
        return count; 
    } 

    /* Driver program to test above functions. Ideally 
    this function should be in a separate user class. 
    It is kept here to keep code compact */
    public static void Main() 
    { 
        /* Start with the empty list */
        LinkedList llist = new LinkedList(); 
        llist.push(1); 
        llist.push(3); 
        llist.push(1); 
        llist.push(2); 
        llist.push(1); 

        Console.WriteLine("Count of nodes is " + 
                        llist.getCount()); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
count of nodes is 5
```

**递归解决方案**

```
int getCount(head)
1) If head is NULL, return 0.
2) Else return 1 + getCount(head->next) 
```

以下是上述算法的实现，以找到节点数。

## C / C ++

```

// Recursive C program to find length or count of nodes in a linked list 
#include<stdio.h> 
#include<stdlib.h> 

/* Link list node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

/* Given a reference (pointer to pointer) to the head 
  of a list and an int, push a new node on the front 
  of the list. */
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

/* Counts the no. of occurrences of a node 
   (search_for) in a linked list (head)*/
int getCount(struct Node* head) 
{ 
    // Base case 
    if (head == NULL) 
        return 0; 

    // count is 1 + count of remaining list 
    return 1 + getCount(head->next); 
} 

/* Driver program to test count function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Use push() to construct below list 
     1->2->1->3->1  */
    push(&head, 1); 
    push(&head, 3); 
    push(&head, 1); 
    push(&head, 2); 
    push(&head, 1); 

    /* Check the count function */
    printf("count of nodes is %d", getCount(head)); 
    return 0; 
} 

```

## 爪哇

```

// Recursive Java program to count number of nodes in  
// a linked list 

/* Linked list Node*/
class Node 
{ 
    int data; 
    Node next; 
    Node(int d)  { data = d;  next = null; } 
} 

// Linked List class 
class LinkedList 
{ 
    Node head;  // head of list 

    /* Inserts a new Node at front of the list. */
    public void push(int new_data) 
    { 
        /* 1 & 2: Allocate the Node & 
                  Put in the data*/
        Node new_node = new Node(new_data); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    /* Returns count of nodes in linked list */
    public int getCountRec(Node node) 
    { 
        // Base case 
        if (node == null) 
            return 0; 

        // Count is this node plus rest of the list 
        return 1 + getCountRec(node.next); 
    } 

    /* Wrapper over getCountRec() */
    public int getCount() 
    { 
        return getCountRec(head); 
    } 

    /* Driver program to test above functions. Ideally 
       this function should be in a separate user class. 
       It is kept here to keep code compact */
    public static void main(String[] args) 
    { 
        /* Start with the empty list */
        LinkedList llist = new LinkedList(); 
        llist.push(1); 
        llist.push(3); 
        llist.push(1); 
        llist.push(2); 
        llist.push(1); 

        System.out.println("Count of nodes is " + 
                           llist.getCount()); 
    } 
} 

```

## 蟒蛇

```

# A complete working Python program to find length of a 
# Linked List recursively 

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
        #        Put in the data 
        new_node = Node(new_data) 

        # 3\. Make next of new Node as head 
        new_node.next = self.head 

        # 4\. Move the head to point to new Node 
        self.head = new_node 

    # This function counts number of nodes in Linked List 
    # recursively, given 'node' as starting node. 
    def getCountRec(self, node): 
        if (not node): # Base case 
            return 0
        else: 
            return 1 + self.getCountRec(node.next) 

    # A wrapper over getCountRec() 
    def getCount(self): 
       return self.getCountRec(self.head) 

# Code execution starts here 
if __name__=='__main__': 
    llist = LinkedList() 
    llist.push(1) 
    llist.push(3) 
    llist.push(1) 
    llist.push(2) 
    llist.push(1) 
    print 'Count of nodes is :',llist.getCount() 

```

## C＃

```

// Recursive C# program to count number of nodes in  
// a linked list  
using System; 

/* Linked list Node*/
public class Node  
{  
    public int data;  
    public Node next;  
    public Node(int d)  
    {  
        data = d; next = null;  
    }  
}  

// Linked List class  
public class LinkedList  
{  
    Node head; // head of list  

    /* Inserts a new Node at front of the list. */
    public void push(int new_data)  
    {  
        /* 1 & 2: Allocate the Node &  
                Put in the data*/
        Node new_node = new Node(new_data);  

        /* 3\. Make next of new Node as head */
        new_node.next = head;  

        /* 4\. Move the head to point to new Node */
        head = new_node;  
    }  

    /* Returns count of nodes in linked list */
    public int getCountRec(Node node)  
    {  
        // Base case  
        if (node == null)  
            return 0;  

        // Count is this node plus rest of the list  
        return 1 + getCountRec(node.next);  
    }  

    /* Wrapper over getCountRec() */
    public int getCount()  
    {  
        return getCountRec(head);  
    }  

    /* Driver program to test above functions. Ideally  
    this function should be in a separate user class.  
    It is kept here to keep code compact */
    public static void Main(String[] args)  
    {  
        /* Start with the empty list */
        LinkedList llist = new LinkedList();  
        llist.push(1);  
        llist.push(3);  
        llist.push(1);  
        llist.push(2);  
        llist.push(1);  

        Console.WriteLine("Count of nodes is " +  
                        llist.getCount());  
    }  
}  

// This code is contributed 29AjayKumar 

```

**Output:**

```
count of nodes is 5
```

本文由 **Ravi** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。