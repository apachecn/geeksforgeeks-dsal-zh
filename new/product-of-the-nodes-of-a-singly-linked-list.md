# 单链接列表

的节点的乘积

给定一个单链表。 任务是找到给定链表所有节点的乘积。

**范例**：

```
Input : List = 7->6->8->4->1
Output : Product = 1344
Product of nodes: 7 * 6 * 8 * 4 * 1 = 1344

Input : List = 1->7->3->9->11->5
Output : Product = 10395

```

**算法**：

1.  使用链接列表的开头初始化指针 ptr，并使用 1 初始化产品变量。
2.  使用循环开始遍历链表，直到遍历所有节点。
3.  将当前节点的值乘以乘积，即**乘积* = ptr->数据**。
4.  递增指向链表的下一个节点的指针，即 **ptr = ptr-> next** 。
5.  重复上述两个步骤，直到到达链表的末尾。
6.  最后，退回产品。

下面是上述算法的实现：

## C++

```cpp

// C++ implementation to find the product of 
// nodes of the Linked List 

#include <iostream> 
using namespace std; 

// A Linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to insert a node at the 
// beginning of the linked list 
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = new Node; 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list to the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

// Function to find the product of 
// nodes of the given linked list 
int productOfNodes(struct Node* head) 
{ 
    // Pointer to traverse the list 
    struct Node* ptr = head; 

    int product = 1; // Variable to store product 

    // Traverse the list and 
    // calculate the product 
    while (ptr != NULL) { 

        product *= ptr->data; 
        ptr = ptr->next; 
    } 

    // Return the product 
    return product; 
} 

// Driver Code 
int main() 
{ 
    struct Node* head = NULL; 

    // create linked list 7->6->8->4->1 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 8); 
    push(&head, 4); 
    push(&head, 1); 

    cout << "Product = " << productOfNodes(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation to find the product of  
// nodes of the Linked List  
class GFG  
{ 

// A Linked list node  
static class Node 
{  
    int data;  
    Node next;  
};  

// Function to insert a node at the  
// beginning of the linked list  
static Node push( Node head_ref, int new_data)  
{  
    // allocate node / 
    Node new_node = new Node();  

    // put in the data / 
    new_node.data = new_data;  

    // link the old list to the new node / 
    new_node.next = (head_ref);  

    // move the head to point to the new node / 
    (head_ref) = new_node; 
    return head_ref; 
}  

// Function to find the product of  
// nodes of the given linked list  
static int productOfNodes( Node head)  
{  
    // Pointer to traverse the list  
    Node ptr = head;  

    int product = 1; // Variable to store product  

    // Traverse the list and  
    // calculate the product  
    while (ptr != null) 
    {  

        product *= ptr.data;  
        ptr = ptr.next;  
    }  

    // Return the product  
    return product;  
}  

// Driver Code  
public static void main(String args[]) 
{  
    Node head = null;  

    // create linked list 7.6.8.4.1  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 8);  
    head = push(head, 4);  
    head = push(head, 1);  

    System.out.println("Product = " + productOfNodes(head));  
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation to find the product of  
# nodes of the Linked List  
import math 

# A linked List node 
class Node: 
    def __init__(self,data): 
        self.data = data 
        self.next = None

# Function to insert a node at the  
# beginning of the linked list  
def push(head,data): 
    if not head: 

        # Return new node 
        return Node(data) 

    # allocate node  
    new_node = Node(data) 

    # link the old list to the new node  
    new_node.next = head 

    # move the head to point to the new node 
    head = new_node 
    return head 

# Function to find the product of  
# nodes of the given linked list  
def productOfNodes(head): 

    # Pointer to traverse the list  
    ptr = head 
    product = 1 # Variable to store product  

    # Traverse the list and  
    # calculate the product 
    while(ptr): 
        product *= ptr.data 
        ptr = ptr.next

    # Return the product      
    return product 

# Driver Code  
if __name__=='__main__': 
    head = None

    # create linked list 7->6->8->4->1 
    head = push(head,7) 
    head = push(head,6) 
    head = push(head,8) 
    head = push(head,4) 
    head = push(head,1) 
    print("Product = {}".format(productOfNodes(head))) 

# This Code is Contribute By Vikash Kumar 37 

```

## C#

```cs

// C# implementation to find the product of  
// nodes of the Linked List  
using System; 

class GFG  
{  

// A Linked list node  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Function to insert a node at the  
// beginning of the linked list  
static Node push(Node head_ref, int new_data)  
{  
    // allocate node /  
    Node new_node = new Node();  

    // put in the data /  
    new_node.data = new_data;  

    // link the old list to the new node /  
    new_node.next = (head_ref);  

    // move the head to point to the new node /  
    (head_ref) = new_node;  
    return head_ref;  
}  

// Function to find the product of  
// nodes of the given linked list  
static int productOfNodes( Node head)  
{  
    // Pointer to traverse the list  
    Node ptr = head;  

    int product = 1; // Variable to store product  

    // Traverse the list and  
    // calculate the product  
    while (ptr != null)  
    {  
        product *= ptr.data;  
        ptr = ptr.next;  
    }  

    // Return the product  
    return product;  
}  

// Driver Code  
public static void Main(String []args)  
{  
    Node head = null;  

    // create linked list 7.6.8.4.1  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 8);  
    head = push(head, 4);  
    head = push(head, 1);  

    Console.WriteLine("Product = " +  
                       productOfNodes(head));  
}  
}  

// This code is contributed by Rajput-Ji 

```

**Output:**

```
Product = 1344

```

**时间复杂度**：O（N），其中 N 是链​​表中节点的数量。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。