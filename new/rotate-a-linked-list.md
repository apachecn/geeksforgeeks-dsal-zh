# 旋转链接列表

给定一个单链表，将链表逆时针旋转k个节点。 其中k是给定的正整数。 例如，如果给定的链表是10-> 20-> 30-> 40-> 50-> 60且k为4，则该链表应修改为50-> 60-> 10-> 20-> 30- > 40。 假设k小于链表中节点的数量。

**<u>方法-1：</u>**
要旋转链接列表，我们需要将第k个节点的下一个更改为NULL，将最后一个节点的下一个更改为上一个头节点，最后， 将头更改为第（k + 1）个节点。 因此，我们需要掌握三个节点：第k个节点，第（k + 1）个节点和最后一个节点。
从头开始遍历列表，并在第k个节点处停止。 存储指向第k个节点的指针。 接下来我们可以使用kthNode- >获得第（k + 1）个节点。 继续遍历最后一点，并存储指向最后一个节点的指针。 最后，如上所述更改指针。

下图显示了rotate函数在代码中的工作方式：

![](img/d20bcab15c5c1bfdac020daf13ed0cb5.png)

## C ++

```

// C++ program to rotate 
// a linked list counter clock wise 

#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node { 
public: 
    int data; 
    Node* next; 
}; 

// This function rotates a linked list 
// counter-clockwise and updates the 
// head. The function assumes that k is 
// smaller than size of linked list. 
// It doesn't modify the list if 
// k is greater than or equal to size 
void rotate(Node** head_ref, int k) 
{ 
    if (k == 0) 
        return; 

    // Let us understand the below 
    // code for example k = 4 and 
    // list = 10->20->30->40->50->60\. 
    Node* current = *head_ref; 

    // current will either point to 
    // kth or NULL after this loop. 
    // current will point to node 
    // 40 in the above example 
    int count = 1; 
    while (count < k && current != NULL) { 
        current = current->next; 
        count++; 
    } 

    // If current is NULL, k is greater than 
    // or equal to count of nodes in linked list. 
    // Don't change the list in this case 
    if (current == NULL) 
        return; 

    // current points to kth node. 
    // Store it in a variable. kthNode 
    // points to node 40 in the above example 
    Node* kthNode = current; 

    // current will point to 
    // last node after this loop 
    // current will point to 
    // node 60 in the above example 
    while (current->next != NULL) 
        current = current->next; 

    // Change next of last node to previous head 
    // Next of 60 is now changed to node 10 
    current->next = *head_ref; 

    // Change head to (k+1)th node 
    // head is now changed to node 50 
    *head_ref = kthNode->next; 

    // change next of kth node to NULL 
    // next of 40 is now NULL 
    kthNode->next = NULL; 
} 

/* UTILITY FUNCTIONS */
/* Function to push a node */
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

/* Function to print linked list */
void printList(Node* node) 
{ 
    while (node != NULL) { 
        cout << node->data << " "; 
        node = node->next; 
    } 
} 

/* Driver code*/
int main(void) 
{ 
    /* Start with the empty list */
    Node* head = NULL; 

    // create a list 10->20->30->40->50->60 
    for (int i = 60; i > 0; i -= 10) 
        push(&head, i); 

    cout << "Given linked list \n"; 
    printList(head); 
    rotate(&head, 4); 

    cout << "\nRotated Linked list \n"; 
    printList(head); 

    return (0); 
} 

// This code is contributed by rathbhupendra 

```

## C

```

// C program to rotate a linked list counter clock wise 

#include <stdio.h> 
#include <stdlib.h> 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// This function rotates a linked list counter-clockwise and 
// updates the head. The function assumes that k is smaller 
// than size of linked list. It doesn't modify the list if 
// k is greater than or equal to size 
void rotate(struct Node** head_ref, int k) 
{ 
    if (k == 0) 
        return; 

    // Let us understand the below code for example k = 4 and 
    // list = 10->20->30->40->50->60\. 
    struct Node* current = *head_ref; 

    // current will either point to kth or NULL after this loop. 
    // current will point to node 40 in the above example 
    int count = 1; 
    while (count < k && current != NULL) { 
        current = current->next; 
        count++; 
    } 

    // If current is NULL, k is greater than or equal to count 
    // of nodes in linked list. Don't change the list in this case 
    if (current == NULL) 
        return; 

    // current points to kth node. Store it in a variable. 
    // kthNode points to node 40 in the above example 
    struct Node* kthNode = current; 

    // current will point to last node after this loop 
    // current will point to node 60 in the above example 
    while (current->next != NULL) 
        current = current->next; 

    // Change next of last node to previous head 
    // Next of 60 is now changed to node 10 
    current->next = *head_ref; 

    // Change head to (k+1)th node 
    // head is now changed to node 50 
    *head_ref = kthNode->next; 

    // change next of kth node to NULL 
    // next of 40 is now NULL 
    kthNode->next = NULL; 
} 

/* UTILITY FUNCTIONS */
/* Function to push a node */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data  */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* Function to print linked list */
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

/* Driver program to test above function*/
int main(void) 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    // create a list 10->20->30->40->50->60 
    for (int i = 60; i > 0; i -= 10) 
        push(&head, i); 

    printf("Given linked list \n"); 
    printList(head); 
    rotate(&head, 4); 

    printf("\nRotated Linked list \n"); 
    printList(head); 

    return (0); 
} 

```

## 爪哇

```

// Java program to rotate a linked list 

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

    // This function rotates a linked list counter-clockwise 
    // and updates the head. The function assumes that k is 
    // smaller than size of linked list. It doesn't modify 
    // the list if k is greater than or equal to size 
    void rotate(int k) 
    { 
        if (k == 0) 
            return; 

        // Let us understand the below code for example k = 4 
        // and list = 10->20->30->40->50->60\. 
        Node current = head; 

        // current will either point to kth or NULL after this 
        // loop. current will point to node 40 in the above example 
        int count = 1; 
        while (count < k && current != null) { 
            current = current.next; 
            count++; 
        } 

        // If current is NULL, k is greater than or equal to count 
        // of nodes in linked list. Don't change the list in this case 
        if (current == null) 
            return; 

        // current points to kth node. Store it in a variable. 
        // kthNode points to node 40 in the above example 
        Node kthNode = current; 

        // current will point to last node after this loop 
        // current will point to node 60 in the above example 
        while (current.next != null) 
            current = current.next; 

        // Change next of last node to previous head 
        // Next of 60 is now changed to node 10 

        current.next = head; 

        // Change head to (k+1)th node 
        // head is now changed to node 50 
        head = kthNode.next; 

        // change next of kth node to null 
        kthNode.next = null; 
    } 

    /*  Given a reference (pointer to pointer) to the head 
        of a list and an int, push a new node on the front 
        of the list. */
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

    void printList() 
    { 
        Node temp = head; 
        while (temp != null) { 
            System.out.print(temp.data + " "); 
            temp = temp.next; 
        } 
        System.out.println(); 
    } 

    /* Driver program to test above functions */
    public static void main(String args[]) 
    { 
        LinkedList llist = new LinkedList(); 

        // create a list 10->20->30->40->50->60 
        for (int i = 60; i >= 10; i -= 10) 
            llist.push(i); 

        System.out.println("Given list"); 
        llist.printList(); 

        llist.rotate(4); 

        System.out.println("Rotated Linked List"); 
        llist.printList(); 
    } 
} /* This code is contributed by Rajat Mishra */

```

## 蟒蛇

```

# Python program to rotate a linked list 

# Node class  
class Node: 

    # Constructor to initialize the node object 
    def __init__(self, data): 
        self.data = data 
        self.next = None

class LinkedList: 

    # Function to initialize head 
    def __init__(self): 
        self.head = None

    # Function to insert a new node at the beginning 
    def push(self, new_data): 
        # allocate node and put the data 
        new_node = Node(new_data) 

        # Make next of new node as head 
        new_node.next = self.head 

        # move the head to point to the new Node 
        self.head = new_node 

    # Utility function to print it the linked LinkedList 
    def printList(self): 
        temp = self.head 
        while(temp): 
            print temp.data, 
            temp = temp.next

    # This function rotates a linked list counter-clockwise and  
    # updates the head. The function assumes that k is smaller 
    # than size of linked list. It doesn't modify the list if 
    # k is greater than of equal to size 
    def rotate(self, k): 
        if k == 0:  
            return 

        # Let us understand the below code for example k = 4 
        # and list = 10->20->30->40->50->60 
        current = self.head 

        # current will either point to kth or NULL after 
        # this loop 
        # current will point to node 40 in the above example 
        count = 1 
        while(count <k and current is not None): 
            current = current.next
            count += 1

        # If current is None, k is greater than or equal  
        # to count of nodes in linked list. Don't change 
        # the list in this case 
        if current is None: 
            return

        # current points to kth node. Store it in a variable 
        # kth node points to node 40 in the above example 
        kthNode = current  

        # current will point to lsat node after this loop 
        # current will point to node 60 in above example 
        while(current.next is not None): 
            current = current.next

        # Change next of last node to previous head 
        # Next of 60 is now changed to node 10 
        current.next = self.head 

        # Change head to (k + 1)th node 
        # head is not changed to node 50 
        self.head = kthNode.next

        # change next of kth node to NULL  
        # next of 40 is not NULL  
        kthNode.next = None

# Driver program to test above function 
llist = LinkedList() 

# Create a list 10->20->30->40->50->60 
for i in range(60, 0, -10): 
    llist.push(i) 

print "Given linked list"
llist.printList() 
llist.rotate(4) 

print "\nRotated Linked list"
llist.printList() 

# This code is contributed by Nikhil Kumar Singh(nickzuck_007) 

```

## C＃

```

// C# program to rotate a linked list 
using System; 

public class LinkedList { 
    Node head; // head of list 

    /* Linked list Node*/
    public class Node { 
        public int data; 
        public Node next; 
        public Node(int d) 
        { 
            data = d; 
            next = null; 
        } 
    } 

    // This function rotates a linked list 
    // counter-clockwise and updates the head. 
    // The function assumes that k is smaller 
    // than size of linked list. It doesn't modify 
    // the list if k is greater than or equal to size 
    void rotate(int k) 
    { 
        if (k == 0) 
            return; 

        // Let us understand the below 
        // code for example k = 4 
        // and list = 10->20->30->40->50->60\. 
        Node current = head; 

        // current will either point to kth 
        // or NULL after this loop. current 
        // will point to node 40 in the above example 
        int count = 1; 
        while (count < k && current != null) { 
            current = current.next; 
            count++; 
        } 

        // If current is NULL, k is greater than 
        // or equal to count of nodes in linked list. 
        // Don't change the list in this case 
        if (current == null) 
            return; 

        // current points to kth node. 
        // Store it in a variable. 
        // kthNode points to node 
        // 40 in the above example 
        Node kthNode = current; 

        // current will point to 
        // last node after this loop 
        // current will point to 
        // node 60 in the above example 
        while (current.next != null) 
            current = current.next; 

        // Change next of last node to previous head 
        // Next of 60 is now changed to node 10 

        current.next = head; 

        // Change head to (k+1)th node 
        // head is now changed to node 50 
        head = kthNode.next; 

        // change next of kth node to null 
        kthNode.next = null; 
    } 

    /* Given a reference (pointer to pointer) to the head 
        of a list and an int, push a new node on the front 
        of the list. */
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

    void printList() 
    { 
        Node temp = head; 
        while (temp != null) { 
            Console.Write(temp.data + " "); 
            temp = temp.next; 
        } 
        Console.WriteLine(); 
    } 

    /* Driver code */
    public static void Main() 
    { 
        LinkedList llist = new LinkedList(); 

        // create a list 10->20->30->40->50->60 
        for (int i = 60; i >= 10; i -= 10) 
            llist.push(i); 

        Console.WriteLine("Given list"); 
        llist.printList(); 

        llist.rotate(4); 

        Console.WriteLine("Rotated Linked List"); 
        llist.printList(); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**输出：**

```
Given linked list
10  20  30  40  50  60
Rotated Linked list
50  60  10  20  30  40

```

时间复杂度：O（n），其中n是链表中的节点数。 该代码仅遍历链接列表一次。
如果发现任何不正确的内容，或者想共享有关上述主题的更多信息，请发表评论。

**<u>方法2：</u>**
要按k旋转链表，我们可以先使链表呈圆形，然后从头节点向前移动k-1步，使其为空 并使第k个节点为head。

## C ++

```

// C++ program to rotate 
// a linked list counter clock wise 

#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node { 
public: 
    int data; 
    Node* next; 
}; 

// This function rotates a linked list 
// counter-clockwise and updates the 
// head. The function assumes that k is 
// smaller than size of linked list. 
void rotate(Node** head_ref, int k) 
{ 
    if (k == 0) 
        return; 

    // Let us understand the below 
    // code for example k = 4 and 
    // list = 10->20->30->40->50->60\. 
    Node* current = *head_ref; 

    // Traverse till the end. 
    while (current->next != NULL) 
        current = current->next; 

    current->next = *head_ref; 
    current = *head_ref; 

    // traverse the linked list to k-1 position which 
    // will be last element for rotated array. 
    for (int i = 0; i < k - 1; i++) 
        current = current->next; 

    // update the head_ref and last element pointer to NULL 
    *head_ref = current->next; 
    current->next = NULL; 
} 

/* UTILITY FUNCTIONS */
/* Function to push a node */
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

/* Function to print linked list */
void printList(Node* node) 
{ 
    while (node != NULL) { 
        cout << node->data << " "; 
        node = node->next; 
    } 
} 

/* Driver code*/
int main(void) 
{ 
    /* Start with the empty list */
    Node* head = NULL; 

    // create a list 10->20->30->40->50->60 
    for (int i = 60; i > 0; i -= 10) 
        push(&head, i); 

    cout << "Given linked list \n"; 
    printList(head); 
    rotate(&head, 4); 

    cout << "\nRotated Linked list \n"; 
    printList(head); 

    return (0); 
} 

// This code is contributed by pkurada 

```

**Output:** 

```
Given linked list 
10 20 30 40 50 60 
Rotated Linked list 
50 60 10 20 30 40

```

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。