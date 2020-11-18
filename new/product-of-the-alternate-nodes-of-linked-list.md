# 链表

的备用节点的产品

给定一个链表，任务是打印给定链表的备用节点的乘积。

**范例**：

```
Input : 1 -> 8 -> 3 -> 10 -> 17 -> 22 -> 29 -> 42
Output : 1479
Alternate nodes : 1 -> 3 -> 17 -> 29

Input : 10 -> 17 -> 33 -> 38 -> 73
Output : 24090 
Alternate nodes : 10 -> 33 -> 73

```

**迭代方法：**

1.  遍历整个链表。

2.  设置 prod = 1 并且 count = 0。

3.  当计数为偶数时，将节点的数据乘以 prod。

4.  访问下一个节点。

以下是此方法的实现：

## C++

```cpp

// C++ code to print the product of Alternate Nodes 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to get the product of alternate 
nodes of the linked list */
int productAlternateNode(struct Node* head) 
{ 
    int count = 0; 
    int prod = 1; 

    while (head != NULL) { 

        // when count is even product the data of node 
        if (count % 2 == 0) 
            prod *= head->data; 

        // count the nodes 
        count++; 

        // move on the next node. 
        head = head->next; 
    } 
    return prod; 
} 

// Function to push node at head 
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new  Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Driver code 
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Use push() function to construct  
    the below list 8 -> 23 -> 11 -> 29 -> 12 */
    push(&head, 12); 
    push(&head, 29); 
    push(&head, 11); 
    push(&head, 23); 
    push(&head, 8); 

    cout << productAlternateNode(head); 

    return 0; 
} 

// This code is contributed by shivani singh 

```

## C

```c

// C code to print the product of Alternate Nodes 
#include <stdio.h> 
#include <stdlib.h> 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to get the product of alternate 
   nodes of the linked list */
int productAlternateNode(struct Node* head) 
{ 
    int count = 0; 
    int prod = 1; 

    while (head != NULL) { 

        // when count is even product the data of node 
        if (count % 2 == 0) 
            prod *= head->data; 

        // count the nodes 
        count++; 

        // move on the next node. 
        head = head->next; 
    } 
    return prod; 
} 

// Function to push node at head 
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Driver code 
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Use push() function to construct  
       the below list 8 -> 23 -> 11 -> 29 -> 12 */
    push(&head, 12); 
    push(&head, 29); 
    push(&head, 11); 
    push(&head, 23); 
    push(&head, 8); 

    printf(" %d ", productAlternateNode(head)); 

    return 0; 
} 

```

## Java

```java

// Java code to print the product of Alternate Nodes  
class GFG 
{ 

/* Link list node */
static class Node  
{  
    int data;  
    Node next;  
};  

/* Function to get the alternate  
nodes of the linked list */
static int productAlternateNode( Node head)  
{  
    int count = 0;  
    int product = 1;  

    while (head != null) 
    {  

        // when count is even product the nodes  
        if (count % 2 == 0)  
            product *= head.data;  

        // count the nodes  
        count++;  

        // move on the next node.  
        head = head.next;  
    }  
    return product;  
}  

// Function to push node at head  
static Node push( Node head_ref, int new_data)  
{  
    Node new_node =new Node(); 
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node;  
    return head_ref; 
}  

// Driver code  
public static void main(String args[]) 
{  
    /* Start with the empty list */
    Node head = null;  

    /* Use push() function to con  
    the below list 8 . 23 . 11 . 29 . 12 */
    head = push(head, 12);  
    head = push(head, 29);  
    head = push(head, 11);  
    head = push(head, 23);  
    head = push(head, 8);  

    System.out.printf(" %d ", productAlternateNode(head));  
}  
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 code to print the  
# product of Alternate Nodes 
import math 

# Link list node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to get the product of alternate 
# nodes of the linked list  
def productAlternateNode(head): 
    count = 0
    prod = 1

    while (head != None): 

        # when count is even, product 
        # the data of node 
        if (count % 2 == 0): 
            prod *= head.data 

        # count the nodes 
        count = count + 1

        # move on the next node. 
        head = head.next

    return prod 

# Function to head=push node at head 
def push(head_ref, new_data): 
    new_node = Node(new_data) 

    #new_node.data = new_data 
    new_node.next = head_ref 
    head_ref = new_node 
    return head_ref 

# Driver code 
if __name__=='__main__': 

    # Start with the empty list  
    head = None

    # Use head=push() function to construct  
    #the below list 8 . 23 . 11 . 29 . 12  
    head = push(head, 12) 
    head = push(head, 29) 
    head = push(head, 11) 
    head = push(head, 23) 
    head = push(head, 8) 

    print(productAlternateNode(head)) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# code to print the product of Alternate Nodes  
using System; 

class GFG  
{  

/* Link list node */
public class Node  
{  
    public int data;  
    public Node next;  
};  

/* Function to get the alternate  
nodes of the linked list */
static int productAlternateNode( Node head)  
{  
    int count = 0;  
    int product = 1;  

    while (head != null)  
    {  

        // when count is even product the nodes  
        if (count % 2 == 0)  
            product *= head.data;  

        // count the nodes  
        count++;  

        // move on the next node.  
        head = head.next;  
    }  
    return product;  
}  

// Function to push node at head  
static Node push( Node head_ref, int new_data)  
{  
    Node new_node =new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node;  
    return head_ref;  
}  

// Driver code  
public static void Main(String []args)  
{  
    /* Start with the empty list */
    Node head = null;  

    /* Use push() function to con  
    the below list 8 . 23 . 11 . 29 . 12 */
    head = push(head, 12);  
    head = push(head, 29);  
    head = push(head, 11);  
    head = push(head, 23);  
    head = push(head, 8);  

    Console.Write(" {0} ", productAlternateNode(head));  
}  
}  

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
1056

```

**递归方法**：

1.  初始化静态变量（例如 flag）。

2.  如果标志为奇数，则将节点乘以乘积。

3.  将 head 和 flag 增加 1，然后递归到下一个节点。

以下是此方法的实现：

## C++

```cpp

// CPP code to print alternate nodes 
// of a linked list using recursion 
#include <bits/stdc++.h> 
using namespace std; 

// A linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Inserting node at the beginning 
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Function to find product of alternate 
// nodes of linked list. 
// The boolean flag isOdd is used to find 
// if the current node is even or odd. 
void productAlternateNodes(struct Node* node, 
                           int& prod, bool isOdd = true) 
{ 
    if (node == NULL) 
        return; 

    if (isOdd == true) 
        prod = prod * (node->data); 

    productAlternateNodes(node->next, prod, !isOdd); 
} 

// Driver code 
int main() 
{ 
    // Start with the empty list 
    struct Node* head = NULL; 

    // construct below list 
    // 8 -> 23 -> 11 -> 29 -> 12 

    push(&head, 12); 
    push(&head, 29); 
    push(&head, 11); 
    push(&head, 23); 
    push(&head, 8); 

    int prod = 1; 

    productAlternateNodes(head, prod); 

    cout << prod; 

    return 0; 
} 

```

## Java

```java

// Java code to print alternate nodes 
// of a linked list using recursion 
class GFG 
{ 

// A linked list node 
static class Node  
{ 
    int data; 
    Node next; 
}; 

// Inserting node at the beginning 
static Node push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = (head_ref); 
    (head_ref) = new_node; 
    return head_ref; 
} 
static int prod; 

// Function to find product of alternate 
// nodes of linked list. 
// The boolean flag isOdd is used to find 
// if the current node is even or odd. 
static void productAlternateNodes(Node node, 
                                  boolean isOdd) 
{ 
    if (node == null) 
        return; 

    if (isOdd == true) 
        prod = prod * (node.data); 

    productAlternateNodes(node.next, !isOdd); 
} 

// Driver code 
public static void main(String args[]) 
{ 

    // Start with the empty list 
    Node head = null; 

    // con below list 
    // 8 . 23 . 11 . 29 . 12 
    head = push(head, 12); 
    head = push(head, 29); 
    head = push(head, 11); 
    head = push(head, 23); 
    head = push(head, 8); 

    prod = 1; 

    productAlternateNodes(head, true); 

    System.out.println( prod); 
} 
} 

// This code is contributed by Arnab Kundu 

```

## 蟒蛇

```

# Python code to print alternate nodes 
# of a linked list using recursion 

# Link list node  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.next = next

# function to insert a node at the 
# beginning of the linked list 
def push(head_ref, new_data): 

    # allocate node  
    new_node = Node(0) 

    # put in the data  
    new_node.data = new_data 

    # link the old list to the new node  
    new_node.next = (head_ref) 

    # move the head to point to the new node  
    (head_ref) = new_node 

    return head_ref 

prod = 1

# Function to find product of alternate 
# nodes of linked list. 
# The boolean flag isOdd is used to find 
# if the current node is even or odd. 
def productAlternateNodes(node, isOdd): 

    global prod 

    if (node == None): 
        return

    if (isOdd == True): 
        prod = prod * (node.data) 

    productAlternateNodes(node.next, not isOdd) 

# Driver code 

# Start with the empty list 
head = None

# construct below list 
# 8 -> 23 -> 11 -> 29 -> 12 

head = push(head, 12) 
head = push(head, 29) 
head = push(head, 11) 
head = push(head, 23) 
head = push(head, 8) 

prod = 1

productAlternateNodes(head, True) 

print (prod) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# code to print alternate nodes 
// of a linked list using recursion 
using System; 

class GFG 
{ 

// A linked list node 
public class Node  
{ 
    public int data; 
    public Node next; 
}; 

// Inserting node at the beginning 
static Node push(Node head_ref, 
                  int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = (head_ref); 
    (head_ref) = new_node; 
    return head_ref; 
} 
static int prod; 

// Function to find product of alternate 
// nodes of linked list. 
// The boolean flag isOdd is used to find 
// if the current node is even or odd. 
static void productAlternateNodes(Node node, 
                                  bool isOdd) 
{ 
    if (node == null) 
        return; 

    if (isOdd == true) 
        prod = prod * (node.data); 

    productAlternateNodes(node.next, !isOdd); 
} 

// Driver code 
public static void Main(String []args) 
{ 

    // Start with the empty list 
    Node head = null; 

    // con below list 
    // 8 . 23 . 11 . 29 . 12 
    head = push(head, 12); 
    head = push(head, 29); 
    head = push(head, 11); 
    head = push(head, 23); 
    head = push(head, 8); 

    prod = 1; 

    productAlternateNodes(head, true); 

    Console.WriteLine( prod); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
1056

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。