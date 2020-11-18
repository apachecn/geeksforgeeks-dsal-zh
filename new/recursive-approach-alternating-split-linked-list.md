# 交替拆分链表

的递归方法

给定一个链表，将链表分为两个备用节点。

**示例：**

```
Input : 1 2 3 4 5 6 7
Output : 1 3 5 7
         2 4 6

Input : 1 4 5 6
Output : 1 5
         4 6

```

我们已经讨论了[链表的迭代拆分。](https://www.geeksforgeeks.org/alternating-split-of-a-given-singly-linked-list/)

这个想法是从第一个节点和第二个节点开始的。 让我们将这些节点称为“ a”和“ b”。 我们重复

## C ++

```

// CPP code to split linked list 
#include <bits/stdc++.h> 
using namespace std; 

// Node structure 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to push nodes 
// into linked list 
void push(Node** head, int new_data) 
{ 
    Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head); 
    (*head) = new_node; 
} 

// We basically remove link between 'a' 
// and its next. Similarly we remove link 
// between 'b' and its next. Then we recur 
// for remaining lists. 
void moveNode(Node* a, Node* b) 
{ 
    if (b == NULL || a == NULL) 
        return; 

    if (a->next != NULL) 
        a->next = a->next->next; 

    if (b->next != NULL) 
        b->next = b->next->next; 

    moveNode(a->next, b->next); 
} 

// function to split linked list 
void alternateSplitLinkedList(Node* head, Node** aRef, 
                                        Node** bRef) 
{ 
    Node* curr = head; 
    *aRef = curr; 
    *bRef = curr->next; 
    moveNode(*aRef, *bRef); 
} 

void display(Node* head) 
{ 
    Node* curr = head; 
    while (curr != NULL) { 
        printf("%d ", curr->data); 
        curr = curr->next; 
    } 
} 

// Driver code 
int main() 
{ 
    Node* head = NULL;  
    Node *a = NULL, *b = NULL; 

    push(&head, 7); 
    push(&head, 6); 
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 

    alternateSplitLinkedList(head, &a, &b); 

    printf("a : "); 
    display(a); 
    printf("\nb : "); 
    display(b); 

    return 0; 
} 

```

## 爪哇

```

// Java code to split linked list 
class GFG 
{ 

// Node structure 
static class Node  
{ 
    int data; 
    Node next; 
}; 

// Function to push nodes 
// into linked list 
static Node push(Node head, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = (head); 
    (head) = new_node; 
    return head; 
} 

static Node a = null, b = null; 

// We basically remove link between 'a' 
// and its next. Similarly we remove link 
// between 'b' and its next. Then we recur 
// for remaining lists. 
static void moveNode(Node a, Node b) 
{ 
    if (b == null || a == null) 
        return; 

    if (a.next != null) 
        a.next = a.next.next; 

    if (b.next != null) 
        b.next = b.next.next; 

    moveNode(a.next, b.next); 
} 

// function to split linked list 
static void alternateSplitLinkedList(Node head) 
{ 
    Node curr = head; 
    a = curr; 
    b = curr.next; 
    Node aRef = a, bRef = b; 
    moveNode(aRef, bRef); 
} 

static void display(Node head) 
{ 
    Node curr = head; 
    while (curr != null)  
    { 
        System.out.printf("%d ", curr.data); 
        curr = curr.next; 
    } 
} 

// Driver code 
public static void main(String args[]) 
{ 
    Node head = null;  
    head = push(head, 7); 
    head = push(head, 6); 
    head = push(head, 5); 
    head = push(head, 4); 
    head = push(head, 3); 
    head = push(head, 2); 
    head = push(head, 1); 

    alternateSplitLinkedList(head); 

    System.out.printf("a : "); 
    display(a); 
    System.out.printf("\nb : "); 
    display(b); 
} 
} 

// This code is contributed by Arnab Kundu 

```

## 蟒蛇

```

# Python code to split linked list  

# Node structure  
class Node(object):  
    def __init__(self, d):  
        self.data = d  
        self.next = None

# Function to push nodes  
# into linked list  
def push( head, new_data) : 

    new_node = Node(0)  
    new_node.data = new_data  
    new_node.next = (head)  
    (head) = new_node  
    return head  

a = None
b = None

# We basically remove link between 'a'  
# and its next. Similarly we remove link  
# between 'b' and its next. Then we recur  
# for remaining lists.  
def moveNode( a, b) : 
    if (b == None or a == None) : 
        return
    if (a.next != None) : 
        a.next = a.next.next
    if (b.next != None) : 
        b.next = b.next.next

    moveNode(a.next, b.next)  

# function to split linked list  
def alternateSplitLinkedList(head) : 

    curr = head 
    global a 
    global b 
    a = curr  
    b = curr.next
    aRef = a 
    bRef = b  
    moveNode(aRef, bRef)  
    return head; 

def display(head) : 

    curr = head  
    while (curr != None) : 

        print( curr.data,end = " ")  
        curr = curr.next

# Driver code  
head = None
head = push(head, 7)  
head = push(head, 6)  
head = push(head, 5)  
head = push(head, 4)  
head = push(head, 3)  
head = push(head, 2)  
head = push(head, 1)  

head=alternateSplitLinkedList(head)  

print("a : ",end="")  
display(a)  
print("\nb : ",end="")  
display(b)  

# This code is contributed by Arnab Kundu  

```

## C＃

```

// C# code to split linked list 
using System; 

class GFG 
{ 

// Node structure 
public class Node  
{ 
    public int data; 
    public Node next; 
}; 

// Function to push nodes 
// into linked list 
static Node push(Node head, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = (head); 
    (head) = new_node; 
    return head; 
} 

static Node a = null, b = null; 

// We basically remove link between 'a' 
// and its next. Similarly we remove link 
// between 'b' and its next. Then we recur 
// for remaining lists. 
static void moveNode(Node a, Node b) 
{ 
    if (b == null || a == null) 
        return; 

    if (a.next != null) 
        a.next = a.next.next; 

    if (b.next != null) 
        b.next = b.next.next; 

    moveNode(a.next, b.next); 
} 

// function to split linked list 
static void alternateSplitLinkedList(Node head) 
{ 
    Node curr = head; 
    a = curr; 
    b = curr.next; 
    Node aRef = a, bRef = b; 
    moveNode(aRef, bRef); 
} 

static void display(Node head) 
{ 
    Node curr = head; 
    while (curr != null)  
    { 
        Console.Write("{0} ", curr.data); 
        curr = curr.next; 
    } 
} 

// Driver code 
public static void Main(String []args) 
{ 
    Node head = null;  
    head = push(head, 7); 
    head = push(head, 6); 
    head = push(head, 5); 
    head = push(head, 4); 
    head = push(head, 3); 
    head = push(head, 2); 
    head = push(head, 1); 

    alternateSplitLinkedList(head); 

    Console.Write("a : "); 
    display(a); 
    Console.Write("\nb : "); 
    display(b); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
a : 1 3 5 7 
b : 2 4 6 

```

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。