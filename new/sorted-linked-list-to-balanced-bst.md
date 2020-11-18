# 链接列表到平衡 BST

给定一个单链列表，其中的数据成员按升序排序。 构造一个[平衡二进制搜索树](https://www.geeksforgeeks.org/how-to-determine-if-a-binary-tree-is-balanced/)，该树的数据成员与给定的链接列表相同。

 **范例：**

```
Input:  Linked List 1->2->3
Output: A Balanced BST 
     2   
   /  \  
  1    3 

Input: Linked List 1->2->3->4->5->6->7
Output: A Balanced BST
        4
      /   \
     2     6
   /  \   / \
  1   3  5   7  

Input: Linked List 1->2->3->4
Output: A Balanced BST
      3   
    /  \  
   2    4 
 / 
1

Input:  Linked List 1->2->3->4->5->6
Output: A Balanced BST
      4   
    /   \  
   2     6 
 /  \   / 
1   3  5   

```

**方法 1（简单）**

下面是一个简单的算法，在该算法中，我们首先找到列表的中间节点，并将其设为要构建的树的根。

```
1) Get the Middle of the linked list and make it root.
2) Recursively do same for the left half and right half.
       a) Get the middle of the left half and make it left child of the root
          created in step 1.
       b) Get the middle of right half and make it the right child of the
          root created in step 1.

```

时间复杂度：O（nLogn）其中 n 是链表中的节点数。

**方法 2（棘手）**

方法 1 从根到叶构造树。 在这种方法中，我们从叶到根进行构建。 想法是按照与在“链表”中出现的顺序相同的顺序在 BST 中插入节点，以便可以以 O（n）时间复杂度构造树。 我们首先计算给定链接列表中的节点数。 让计数为 n。 在计数节点之后，我们取左 n / 2 个节点并递归构造左子树。 构造左子树后，我们为 root 分配内存，并将左子树与 root 链接。 最后，我们递归构造正确的子树并将其与根链接。

在构造 BST 时，我们还不断将列表头指针移到 next 位置，以便在每个递归调用中都有适当的指针。

下面是方法 2 的实现。突出显示了创建 Balanced BST 的主要代码。

## C++

```cpp

// C++ implementation of above approach 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class LNode  
{  
    public: 
    int data;  
    LNode* next;  
};  

/* A Binary Tree node */
class TNode  
{  
    public: 
    int data;  
    TNode* left;  
    TNode* right;  
};  

TNode* newNode(int data);  
int countLNodes(LNode *head);  
TNode* sortedListToBSTRecur(LNode **head_ref, int n);  

/* This function counts the number of  
nodes in Linked List and then calls  
sortedListToBSTRecur() to construct BST */
TNode* sortedListToBST(LNode *head)  
{  
    /*Count the number of nodes in Linked List */
    int n = countLNodes(head);  

    /* Construct BST */
    return sortedListToBSTRecur(&head, n);  
}  

/* The main function that constructs  
balanced BST and returns root of it.  
head_ref --> Pointer to pointer to  
head node of linked list n --> No. 
of nodes in Linked List */
TNode* sortedListToBSTRecur(LNode **head_ref, int n)  
{  
    /* Base Case */
    if (n <= 0)  
        return NULL;  

    /* Recursively construct the left subtree */
    TNode *left = sortedListToBSTRecur(head_ref, n/2);  

    /* Allocate memory for root, and  
    link the above constructed left  
    subtree with root */
    TNode *root = newNode((*head_ref)->data);  
    root->left = left;  

    /* Change head pointer of Linked List 
    for parent recursive calls */
    *head_ref = (*head_ref)->next;  

    /* Recursively construct the right  
        subtree and link it with root  
        The number of nodes in right subtree 
        is total nodes - nodes in  
        left subtree - 1 (for root) which is n-n/2-1*/
    root->right = sortedListToBSTRecur(head_ref, n - n / 2 - 1);  

    return root;  
}  

/* UTILITY FUNCTIONS */

/* A utility function that returns  
count of nodes in a given Linked List */
int countLNodes(LNode *head)  
{  
    int count = 0;  
    LNode *temp = head;  
    while(temp)  
    {  
        temp = temp->next;  
        count++;  
    }  
    return count;  
}  

/* Function to insert a node  
at the beginging of the linked list */
void push(LNode** head_ref, int new_data)  
{  
    /* allocate node */
    LNode* new_node = new LNode(); 

    /* put in the data */
    new_node->data = new_data;  

    /* link the old list off the new node */
    new_node->next = (*head_ref);  

    /* move the head to point to the new node */
    (*head_ref) = new_node;  
}  

/* Function to print nodes in a given linked list */
void printList(LNode *node)  
{  
    while(node!=NULL)  
    {  
        cout << node->data << " ";  
        node = node->next;  
    }  
}  

/* Helper function that allocates a new node with the  
given data and NULL left and right pointers. */
TNode* newNode(int data)  
{  
    TNode* node = new TNode(); 
    node->data = data;  
    node->left = NULL;  
    node->right = NULL;  

    return node;  
}  

/* A utility function to  
print preorder traversal of BST */
void preOrder(TNode* node)  
{  
    if (node == NULL)  
        return;  
    cout<<node->data<<" ";  
    preOrder(node->left);  
    preOrder(node->right);  
}  

/* Driver code*/
int main()  
{  
    /* Start with the empty list */
    LNode* head = NULL;  

    /* Let us create a sorted linked list to test the functions  
    Created linked list will be 1->2->3->4->5->6->7 */
    push(&head, 7);  
    push(&head, 6);  
    push(&head, 5);  
    push(&head, 4);  
    push(&head, 3);  
    push(&head, 2);  
    push(&head, 1);  

    cout<<"Given Linked List ";  
    printList(head);  

    /* Convert List to BST */
    TNode *root = sortedListToBST(head);  
    cout<<"\nPreOrder Traversal of constructed BST ";  
    preOrder(root);  

    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

#include<stdio.h> 
#include<stdlib.h> 

/* Link list node */
struct LNode 
{ 
    int data; 
    struct LNode* next; 
}; 

/* A Binary Tree node */
struct TNode 
{ 
    int data; 
    struct TNode* left; 
    struct TNode* right; 
}; 

struct TNode* newNode(int data); 
int countLNodes(struct LNode *head); 
struct TNode* sortedListToBSTRecur(struct LNode **head_ref, int n); 

/* This function counts the number of nodes in Linked List and then calls 
   sortedListToBSTRecur() to construct BST */
struct TNode* sortedListToBST(struct LNode *head) 
{ 
    /*Count the number of nodes in Linked List */
    int n = countLNodes(head); 

    /* Construct BST */
    return sortedListToBSTRecur(&head, n); 
} 

/* The main function that constructs balanced BST and returns root of it. 
       head_ref -->  Pointer to pointer to head node of linked list 
       n  --> No. of nodes in Linked List */
struct TNode* sortedListToBSTRecur(struct LNode **head_ref, int n) 
{ 
    /* Base Case */
    if (n <= 0) 
        return NULL; 

    /* Recursively construct the left subtree */
    struct TNode *left = sortedListToBSTRecur(head_ref, n/2); 

    /* Allocate memory for root, and link the above constructed left  
       subtree with root */
    struct TNode *root = newNode((*head_ref)->data); 
    root->left = left; 

    /* Change head pointer of Linked List for parent recursive calls */
    *head_ref = (*head_ref)->next; 

    /* Recursively construct the right subtree and link it with root  
      The number of nodes in right subtree  is total nodes - nodes in  
      left subtree - 1 (for root) which is n-n/2-1*/
    root->right = sortedListToBSTRecur(head_ref, n-n/2-1); 

    return root; 
} 

/* UTILITY FUNCTIONS */

/* A utility function that returns count of nodes in a given Linked List */
int countLNodes(struct LNode *head) 
{ 
    int count = 0; 
    struct LNode *temp = head; 
    while(temp) 
    { 
        temp = temp->next; 
        count++; 
    } 
    return count; 
} 

/* Function to insert a node at the beginging of the linked list */
void push(struct LNode** head_ref, int new_data) 
{ 
    /* allocate node */
    struct LNode* new_node = 
        (struct LNode*) malloc(sizeof(struct LNode)); 
    /* put in the data  */
    new_node->data  = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref)    = new_node; 
} 

/* Function to print nodes in a given linked list */
void printList(struct LNode *node) 
{ 
    while(node!=NULL) 
    { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

/* Helper function that allocates a new node with the 
   given data and NULL left and right pointers. */
struct TNode* newNode(int data) 
{ 
    struct TNode* node = (struct TNode*) 
                         malloc(sizeof(struct TNode)); 
    node->data = data; 
    node->left = NULL; 
    node->right = NULL; 

    return node; 
} 

/* A utility function to print preorder traversal of BST */
void preOrder(struct TNode* node) 
{ 
    if (node == NULL) 
        return; 
    printf("%d ", node->data); 
    preOrder(node->left); 
    preOrder(node->right); 
} 

/* Driver program to test above functions*/
int main() 
{ 
    /* Start with the empty list */
    struct LNode* head = NULL; 

    /* Let us create a sorted linked list to test the functions 
     Created linked list will be 1->2->3->4->5->6->7 */
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 

    printf("\n Given Linked List "); 
    printList(head); 

    /* Convert List to BST */
    struct TNode *root = sortedListToBST(head); 
    printf("\n PreOrder Traversal of constructed BST "); 
    preOrder(root); 

    return 0; 
} 

```

## Java

```java

class LinkedList { 

    /* head node of link list */
    static LNode head; 

    /* Link list Node */
    class LNode  
    { 
        int data; 
        LNode next, prev; 

        LNode(int d)  
        { 
            data = d; 
            next = prev = null; 
        } 
    } 

    /* A Binary Tree Node */
    class TNode  
    { 
        int data; 
        TNode left, right; 

        TNode(int d)  
        { 
            data = d; 
            left = right = null; 
        } 
    } 

    /* This function counts the number of nodes in Linked List 
       and then calls sortedListToBSTRecur() to construct BST */
    TNode sortedListToBST()  
    { 
        /*Count the number of nodes in Linked List */
        int n = countNodes(head); 

        /* Construct BST */
        return sortedListToBSTRecur(n); 
    } 

    /* The main function that constructs balanced BST and 
       returns root of it. 
       n  --> No. of nodes in the Doubly Linked List */
    TNode sortedListToBSTRecur(int n)  
    { 
        /* Base Case */
        if (n <= 0)  
            return null; 

        /* Recursively construct the left subtree */
        TNode left = sortedListToBSTRecur(n / 2); 

        /* head_ref now refers to middle node,  
           make middle node as root of BST*/
        TNode root = new TNode(head.data); 

        // Set pointer to left subtree 
        root.left = left; 

        /* Change head pointer of Linked List for parent  
           recursive calls */
        head = head.next; 

        /* Recursively construct the right subtree and link it  
           with root. The number of nodes in right subtree  is  
           total nodes - nodes in left subtree - 1 (for root) */
        root.right = sortedListToBSTRecur(n - n / 2 - 1); 

        return root; 
    } 

    /* UTILITY FUNCTIONS */
    /* A utility function that returns count of nodes in a  
       given Linked List */
    int countNodes(LNode head)  
    { 
        int count = 0; 
        LNode temp = head; 
        while (temp != null) 
        { 
            temp = temp.next; 
            count++; 
        } 
        return count; 
    } 

    /* Function to insert a node at the beginging of  
       the Doubly Linked List */
    void push(int new_data)  
    { 
        /* allocate node */
        LNode new_node = new LNode(new_data); 

        /* since we are adding at the beginning, 
           prev is always NULL */
        new_node.prev = null; 

        /* link the old list off the new node */
        new_node.next = head; 

        /* change prev of head node to new node */
        if (head != null) 
            head.prev = new_node; 

        /* move the head to point to the new node */
        head = new_node; 
    } 

    /* Function to print nodes in a given linked list */
    void printList(LNode node)  
    { 
        while (node != null)  
        { 
            System.out.print(node.data + " "); 
            node = node.next; 
        } 
    } 

    /* A utility function to print preorder traversal of BST */
    void preOrder(TNode node)  
    { 
        if (node == null) 
            return; 
        System.out.print(node.data + " "); 
        preOrder(node.left); 
        preOrder(node.right); 
    } 

    /* Driver program to test above functions */
    public static void main(String[] args) { 
        LinkedList llist = new LinkedList(); 

        /* Let us create a sorted linked list to test the functions 
           Created linked list will be 7->6->5->4->3->2->1 */
        llist.push(7); 
        llist.push(6); 
        llist.push(5); 
        llist.push(4); 
        llist.push(3); 
        llist.push(2); 
        llist.push(1); 

        System.out.println("Given Linked List "); 
        llist.printList(head); 

        /* Convert List to BST */
        TNode root = llist.sortedListToBST(); 
        System.out.println(""); 
        System.out.println("Pre-Order Traversal of constructed BST "); 
        llist.preOrder(root); 
    } 
} 

// This code has been contributed by Mayank Jaiswal(mayank_24) 

```

## Python3

```py

# Python3 implementation of above approach 

# Link list node  
class LNode : 
    def __init__(self): 
        self.data = None
        self.next = None

# A Binary Tree node  
class TNode : 
    def __init__(self): 
        self.data = None
        self.left = None
        self.right = None

head = None

# This function counts the number of  
# nodes in Linked List and then calls  
# sortedListToBSTRecur() to construct BST  
def sortedListToBST():  
    global head 

    # Count the number of nodes in Linked List  
    n = countLNodes(head)  

    # Construct BST  
    return sortedListToBSTRecur(n)  

# The main function that constructs  
# balanced BST and returns root of it.  
# head -. Pointer to pointer to  
# head node of linked list n -. No. 
# of nodes in Linked List  
def sortedListToBSTRecur( n) : 
    global head 

    # Base Case  
    if (n <= 0) : 
        return None

    # Recursively construct the left subtree  
    left = sortedListToBSTRecur( int(n/2))  

    # Allocate memory for root, and  
    # link the above constructed left  
    # subtree with root  
    root = newNode((head).data)  
    root.left = left  

    # Change head pointer of Linked List 
    # for parent recursive calls  
    head = (head).next

    # Recursively construct the right  
    # subtree and link it with root  
    # The number of nodes in right subtree 
    # is total nodes - nodes in  
    # left subtree - 1 (for root) which is n-n/2-1 
    root.right = sortedListToBSTRecur( n - int(n/2) - 1)  

    return root  

# UTILITY FUNCTIONS  

# A utility function that returns  
# count of nodes in a given Linked List  
def countLNodes(head) : 

    count = 0
    temp = head  
    while(temp != None):  

        temp = temp.next
        count = count + 1

    return count  

# Function to insert a node  
#at the beginging of the linked list  
def push(head, new_data) : 

    # allocate node  
    new_node = LNode() 

    # put in the data  
    new_node.data = new_data  

    # link the old list off the new node  
    new_node.next = (head)  

    # move the head to point to the new node  
    (head) = new_node  
    return head 

# Function to print nodes in a given linked list  
def printList(node):  

    while(node != None):  

        print( node.data ,end= " ")  
        node = node.next

# Helper function that allocates a new node with the  
# given data and None left and right pointers.  
def newNode(data) : 

    node = TNode() 
    node.data = data  
    node.left = None
    node.right = None

    return node  

# A utility function to  
# print preorder traversal of BST  
def preOrder( node) : 

    if (node == None) : 
        return
    print(node.data, end = " " ) 
    preOrder(node.left)  
    preOrder(node.right)  

# Driver code 

# Start with the empty list  
head = None

# Let us create a sorted linked list to test the functions  
# Created linked list will be 1.2.3.4.5.6.7  
head = push(head, 7)  
head = push(head, 6)  
head = push(head, 5)  
head = push(head, 4)  
head = push(head, 3)  
head = push(head, 2)  
head = push(head, 1)  

print("Given Linked List " ) 
printList(head)  

# Convert List to BST  
root = sortedListToBST()  
print("\nPreOrder Traversal of constructed BST ")  
preOrder(root)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation of above approach 
using System; 

public class LinkedList  
{ 

    /* head node of link list */
    static LNode head; 

    /* Link list Node */
    class LNode  
    { 
        public int data; 
        public LNode next, prev; 

        public LNode(int d)  
        { 
            data = d; 
            next = prev = null; 
        } 
    } 

    /* A Binary Tree Node */
    class TNode  
    { 
        public int data; 
        public TNode left, right; 

        public TNode(int d)  
        { 
            data = d; 
            left = right = null; 
        } 
    } 

    /* This function counts the number 
    of nodes in Linked List and then calls 
      sortedListToBSTRecur() to construct BST */
    TNode sortedListToBST()  
    { 
        /*Count the number of nodes in Linked List */
        int n = countNodes(head); 

        /* Construct BST */
        return sortedListToBSTRecur(n); 
    } 

    /* The main function that constructs 
     balanced BST and returns root of it. 
    n --> No. of nodes in the Doubly Linked List */
    TNode sortedListToBSTRecur(int n)  
    { 
        /* Base Case */
        if (n <= 0)  
            return null; 

        /* Recursively construct the left subtree */
        TNode left = sortedListToBSTRecur(n / 2); 

        /* head_ref now refers to middle node,  
        make middle node as root of BST*/
        TNode root = new TNode(head.data); 

        // Set pointer to left subtree 
        root.left = left; 

        /* Change head pointer of Linked List 
         for parent recursive calls */
        head = head.next; 

        /* Recursively construct the  
         right subtree and link it  
        with root. The number of  
        nodes in right subtree is  
        total nodes - nodes in left 
        subtree - 1 (for root) */
        root.right = sortedListToBSTRecur(n - n / 2 - 1); 

        return root; 
    } 

    /* UTILITY FUNCTIONS */
    /* A utility function that returns count   
    of nodes in a given Linked List */
    int countNodes(LNode head)  
    { 
        int count = 0; 
        LNode temp = head; 
        while (temp != null) 
        { 
            temp = temp.next; 
            count++; 
        } 
        return count; 
    } 

    /* Function to insert a node at the beginning of  
    the Doubly Linked List */
    void push(int new_data)  
    { 
        /* allocate node */
        LNode new_node = new LNode(new_data); 

        /* since we are adding at the beginning, 
        prev is always NULL */
        new_node.prev = null; 

        /* link the old list off the new node */
        new_node.next = head; 

        /* change prev of head node to new node */
        if (head != null) 
            head.prev = new_node; 

        /* move the head to point to the new node */
        head = new_node; 
    } 

    /* Function to print nodes in a given linked list */
    void printList(LNode node)  
    { 
        while (node != null)  
        { 
            Console.Write(node.data + " "); 
            node = node.next; 
        } 
    } 

    /* A utility function to print  
    preorder traversal of BST */
    void preOrder(TNode node)  
    { 
        if (node == null) 
            return; 
        Console.Write(node.data + " "); 
        preOrder(node.left); 
        preOrder(node.right); 
    } 

    /* Driver code */
    public static void Main(String[] args)  
    { 
        LinkedList llist = new LinkedList(); 

        /* Let us create a sorted  
        linked list to test the functions 
        Created linked list will be  
        7->6->5->4->3->2->1 */
        llist.push(7); 
        llist.push(6); 
        llist.push(5); 
        llist.push(4); 
        llist.push(3); 
        llist.push(2); 
        llist.push(1); 

        Console.WriteLine("Given Linked List "); 
        llist.printList(head); 

        /* Convert List to BST */
        TNode root = llist.sortedListToBST(); 
        Console.WriteLine(""); 
        Console.WriteLine("Pre-Order Traversal of constructed BST "); 
        llist.preOrder(root); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
Given Linked List 1 2 3 4 5 6 7 
 PreOrder Traversal of constructed BST 4 2 1 3 6 5 7

```

**时间复杂度：** O（n）

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

