# 可被K整除的单个链接列表的节点的总和和

给定一个单链表。 任务是找到给定链表的所有节点的和和乘积，这些节点可被给定数k整除。

**范例**：

```
Input : List = 7->60->8->40->1
        k = 10 
Output : Product = 2400, Sum = 100
Product of nodes: 60 * 40 = 2400

Input : List = 15->7->3->9->11->5
        k = 5
Output : Product = 75, Sum = 20

```

**算法：**

1.  用链接列表的开头初始化指针 **ptr** ，将**乘积**变量初始化为1，将**和**变量初始化为0。
2.  使用循环开始遍历链表，直到遍历所有节点。
3.  对于每个节点：
    *   如果当前节点可被k整除，则将当前节点的值乘以乘积。
    *   如果当前节点可被k整除，则将当前节点的值加到总和上。
4.  增加指向链接列表下一个节点的指针，即ptr = ptr-> next。
5.  重复上述步骤，直到到达链表的末尾。
6.  最后，打印乘积和总和。

下面是上述方法的实现：

## C ++

```

// C++ implementation to find the product 
// and sum of nodes which are divisible by k 

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

// Function to find the product and sum of 
// nodes which are divisible by k 
// of the given linked list 
void productAndSum(struct Node* head, int k) 
{ 
    // Pointer to traverse the list 
    struct Node* ptr = head; 

    int product = 1; // Variable to store product 
    int sum = 0; // Variable to store sum 

    // Traverse the list and 
    // calculate the product 
    // and sum 
    while (ptr != NULL) { 
        if (ptr->data % k == 0) { 
            product *= ptr->data; 
            sum += ptr->data; 
        } 

        ptr = ptr->next; 
    } 

    // Print the product and sum 
    cout << "Product = " << product << endl; 
    cout << "Sum = " << sum; 
} 

// Driver Code 
int main() 
{ 
    struct Node* head = NULL; 

    // create linked list 70->6->8->4->10 
    push(&head, 70); 
    push(&head, 6); 
    push(&head, 8); 
    push(&head, 4); 
    push(&head, 10); 

    int k = 10; 

    productAndSum(head, k); 

    return 0; 
} 

```

## 爪哇

```

// Java implementation to find the product  
// and sum of nodes which are divisible by k  
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

// Function to find the product and sum of  
// nodes which are divisible by k  
// of the given linked list  
static void productAndSum( Node head, int k)  
{  
    // Pointer to traverse the list  
    Node ptr = head;  

    int product = 1; // Variable to store product  
    int sum = 0; // Variable to store sum  

    // Traverse the list and  
    // calculate the product  
    // and sum  
    while (ptr != null) 
    {  
        if (ptr.data % k == 0) 
        {  
            product *= ptr.data;  
            sum += ptr.data;  
        }  

        ptr = ptr.next;  
    }  

    // Print the product and sum  
    System.out.println( "Product = " + product );  
    System.out.println( "Sum = " + sum);  
}  

// Driver Code  
public static void main(String args[]) 
{  
    Node head = null;  

    // create linked list 70.6.8.4.10  
    head = push(head, 70);  
    head = push(head, 6);  
    head = push(head, 8);  
    head = push(head, 4);  
    head = push(head, 10);  

    int k = 10;  

    productAndSum(head, k);  

} 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```

# Python3 implementation to find the product 
# and sum of nodes which are divisible by k 
import math 

# A Linked list node 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to insert a node at the 
# beginning of the linked list 
def push(head_ref, new_data): 

    # allocate node  
    new_node =Node(new_data) 

    # put in the data  
    new_node.data = new_data 

    # link the old list to the new node  
    new_node.next = head_ref 

    # move the head to point to the new node  
    head_ref = new_node 
    return head_ref 

# Function to find the product and sum of 
# nodes which are divisible by k 
# of the given linked list 
def productAndSum(head, k): 

    # Pointer to traverse the list 
    ptr = head 

    product = 1 # Variable to store product 
    add = 0 # Variable to store sum 

    # Traverse the list and 
    # calculate the product 
    # and sum 
    while (ptr != None): 
        if (ptr.data % k == 0): 
            product = product * ptr.data 
            add = add + ptr.data 

        ptr = ptr.next

    # Print the product and sum 
    print("Product =", product) 
    print("Sum =", add) 

# Driver Code 
if __name__=='__main__':  

    head = None

    # create linked list 70.6.8.4.10 
    head = push(head, 70) 
    head = push(head, 6) 
    head = push(head, 8) 
    head = push(head, 4) 
    head = push(head, 10) 

    k = 10

    productAndSum(head, k) 

# This code is contributed by Srathore 

```

## C＃

```

// C# implementation to find the product  
// and sum of nodes which are divisible by k  
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

// Function to find the product and sum of  
// nodes which are divisible by k  
// of the given linked list  
static void productAndSum( Node head, int k)  
{  
    // Pointer to traverse the list  
    Node ptr = head;  

    int product = 1; // Variable to store product  
    int sum = 0; // Variable to store sum  

    // Traverse the list and  
    // calculate the product  
    // and sum  
    while (ptr != null) 
    {  
        if (ptr.data % k == 0) 
        {  
            product *= ptr.data;  
            sum += ptr.data;  
        }  

        ptr = ptr.next;  
    }  

    // Print the product and sum  
    Console.WriteLine( "Product = " + product );  
    Console.WriteLine( "Sum = " + sum);  
}  

// Driver Code  
public static void Main(String []args) 
{  
    Node head = null;  

    // create linked list 70.6.8.4.10  
    head = push(head, 70);  
    head = push(head, 6);  
    head = push(head, 8);  
    head = push(head, 4);  
    head = push(head, 10);  

    int k = 10;  

    productAndSum(head, k);  

} 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
Product = 700
Sum = 80

```

**时间复杂度：** O（N），其中N是链​​表中节点的数量。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。