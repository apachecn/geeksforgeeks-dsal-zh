# 单链接列表

的节点总和

给定一个单链表。 任务是找到给定链表的节点总数。

![](img/d97a233bf3c89e80c46e6a3193e851d6.png)

任务是做 A + B + C +D。

**Examples:**

```
Input: 7->6->8->4->1
Output: 26
Sum of nodes:
7 + 6 + 8 + 4 + 1 = 26

Input: 1->7->3->9->11->5
Output: 36

```

**递归解决方案：**

*   通过传递 head 和变量来存储总和来调用函数。

    *   然后通过传递当前节点的下一个和求和变量来递归调用该函数。

        *   将当前节点的值加到总和上。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find the sum of 
// nodes of the Linked List 
#include <bits/stdc++.h> 
using namespace std; 

/* A Linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// function to insert a node at the 
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

// function to recursively find the sum of 
// nodes of the given linked list 
void sumOfNodes(struct Node* head, int* sum) 
{ 
    // if head = NULL 
    if (!head) 
        return; 

    // recursively traverse the remaining nodes 
    sumOfNodes(head->next, sum); 

    // accumulate sum 
    *sum = *sum + head->data; 
} 

// utility function to find the sum of  nodes 
int sumOfNodesUtil(struct Node* head) 
{ 

    int sum = 0; 

    // find the sum of  nodes 
    sumOfNodes(head, &sum); 

    // required sum 
    return sum; 
} 

// Driver program to test above 
int main() 
{ 
    struct Node* head = NULL; 

    // create linked list 7->6->8->4->1 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 8); 
    push(&head, 4); 
    push(&head, 1); 

    cout << "Sum of nodes = "
         << sumOfNodesUtil(head); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find the sum of  
// nodes of the Linked List  
class GFG  
{ 

static int sum=0; 

// A Linked list node / 
static class Node 
{  
    int data;  
    Node next;  
}  

// function to insert a node at the  
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

// function to recursively find the sum of  
// nodes of the given linked list  
static void sumOfNodes( Node head)  
{  
    // if head = null  
    if (head == null)  
        return;  

    // recursively traverse the remaining nodes  
    sumOfNodes(head.next);  

    // accumulate sum  
    sum = sum + head.data;  
}  

// utility function to find the sum of nodes  
static int sumOfNodesUtil( Node head)  
{  

    sum = 0;  

    // find the sum of nodes  
    sumOfNodes(head);  

    // required sum  
    return sum;  
}  

// Driver program to test above  
public static void main(String args[]) 
{  
    Node head = null;  

    // create linked list 7.6.8.4.1  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 8);  
    head = push(head, 4);  
    head = push(head, 1);  

    System.out.println( "Sum of nodes = "
        + sumOfNodesUtil(head));  
}  
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation to find the sum of  
# nodes of the Linked List  
import math 

# class for a Sum 
class Sum: 
    tsum = None

# A Linked list node  
class Node: 
    def __init__(self,data): 
        self.data = data 
        self.next = None

# function to insert a node at the  
# beginning of the linked list  
def push(head, data): 
    if not head: 
        return Node(data) 

    # put in the data  
    # and allocate node  
    new_node = Node(data) 

    # link the old list to the new node  
    new_node.next = head 

    # move the head to point 
    # to the new node  
    head = new_node 
    return head 

# function to recursively find   
# the sum of nodes of the given 
# linked list  
def sumOfNode(head, S): 

    # if head = NULL 
    if not head: 
        return

    # recursively traverse the  
    # remaining nodes 
    sumOfNode(head.next, S) 

    # accumulate sum 
    S.tsum += head.data  

# utility function to find  
# the sum of nodes 
def sumOfNodesUtil(head): 
    S = Sum() 
    S.tsum = 0

    # find the sum of nodes 
    sumOfNode(head, S) 

    # required sum 
    return S.tsum 

# Driver Code 
if __name__=='__main__': 
    head = None

    # create linked list 7->6->8->4->1  
    head = push(head, 7) 
    head = push(head, 6) 
    head = push(head, 8) 
    head = push(head, 4) 
    head = push(head, 1) 
    print("Sum of Nodes = {}" .  
           format(sumOfNodesUtil(head))) 

# This code is contributed  
# by Vikash Kumar 37 

```

## C#

```cs

// C# implementation to find the sum of  
// nodes of the Linked List  
using System; 

class GFG  
{  
    public static int sum = 0;  

    // A Linked list node /  
    public class Node  
    {  
        public int data;  
        public Node next;  
    }  

    // function to insert a node at the  
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

    // function to recursively find the sum of  
    // nodes of the given linked list  
    static void sumOfNodes(Node head)  
    {  
        // if head = null  
        if (head == null)  
            return;  

        // recursively traverse the remaining nodes  
        sumOfNodes(head.next);  

        // accumulate sum  
        sum = sum + head.data;  
    }  

    // utility function to find the sum of nodes  
    static int sumOfNodesUtil(Node head)  
    {  
        sum = 0;  

        // find the sum of nodes  
        sumOfNodes(head);  

        // required sum  
        return sum;  
    }  

    // Driver program to test above  
    public static void Main(String[] args)  
    {  
        Node head = null;  

        // create linked list 7.6.8.4.1  
        head = push(head, 7);  
        head = push(head, 6);  
        head = push(head, 8);  
        head = push(head, 4);  
        head = push(head, 1);  

        Console.WriteLine("Sum of nodes = " + 
                           sumOfNodesUtil(head));  
    }  
}  

// This code is contributed by Rajput-Ji 

```

**Output:**

```
Sum of nodes = 26

```

**时间复杂度：**`O(n)`，N 是链表中节点的数量。

**辅助空间：**`O(n)`，仅当在递归调用期间考虑堆栈大小时。

**迭代解决方案：**

1.  用链接列表的开头初始化一个指针 ***ptr*** ，并将 ***和*** 变量设为 0。

2.  使用循环开始遍历链表，直到遍历所有节点。

    *   将当前节点的值添加到总和，即 ***sum + = ptr->数据*** 。

    *   递增指向链表的下一个节点的指针，即 ***ptr = ptr-> next*** 。

3.  返回 ***和*** 。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find the sum of 
// nodes of the Linked List 
#include <bits/stdc++.h> 
using namespace std; 

/* A Linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// function to insert a node at the 
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

// function to find the sum of 
// nodes of the given linked list 
int sumOfNodes(struct Node* head) 
{ 
    struct Node* ptr = head; 
    int sum = 0; 
    while (ptr != NULL) { 

        sum += ptr->data; 
        ptr = ptr->next; 
    } 

    return sum; 
} 

// Driver program to test above 
int main() 
{ 
    struct Node* head = NULL; 

    // create linked list 7->6->8->4->1 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 8); 
    push(&head, 4); 
    push(&head, 1); 

    cout << "Sum of nodes = "
         << sumOfNodes(head); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find the sum of 
// nodes of the Linked List 

class GFG  
{ 

static Node head;  

/* A Linked list node */
static class Node 
{ 
    int data; 
    Node next; 
}; 

// function to insert a node at the 
// beginning of the linked list 
// Inserting node at the beginning 
static Node push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list to the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    return head=head_ref; 
} 

// function to find the sum of 
// nodes of the given linked list 
static int sumOfNodes( Node head) 
{ 
    Node ptr = head; 
    int sum = 0; 
    while (ptr != null)  
    { 

        sum += ptr.data; 
        ptr = ptr.next; 
    } 

    return sum; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    // create linked list 7.6.8.4.1 
    push(head, 7); 
    push(head, 6); 
    push(head, 8); 
    push(head, 4); 
    push(head, 1); 

    System.out.println("Sum of nodes = "
        + sumOfNodes(head)); 
} 
} 

/* This code is contributed by PrinciRaj1992 */

```

## Python3

```py

# Python3 implementation to find the  
# sum of nodes of the Linked List 
import math  

# A Linked list node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# function to insert a node at the 
# beginning of the linked list 
def push(head_ref, new_data): 

    # allocate node  
    new_node = Node(new_data) 

    # put in the data  
    new_node.data = new_data 

    # link the old list to the new node  
    new_node.next = head_ref 

    # move the head to po to the new node  
    head_ref = new_node 
    return head_ref 

# function to find the sum of 
# nodes of the given linked list 
def sumOfNodes(head): 
    ptr = head 
    sum = 0
    while (ptr != None): 

        sum = sum + ptr.data 
        ptr = ptr.next

    return sum

# Driver Code 
if __name__=='__main__': 
    head = None

    # create linked list 7.6.8.4.1 
    head = push(head, 7) 
    head = push(head, 6) 
    head = push(head, 8) 
    head = push(head, 4) 
    head = push(head, 1) 

    print("Sum of nodes =",  
           sumOfNodes(head)) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# implementation to find the sum of  
// nodes of the Linked List  
using System; 

class GFG  
{  

static Node head;  

/* A Linked list node */
public class Node  
{  
    public int data;  
    public Node next;  
};  

// function to insert a node at the  
// beginning of the linked list  
// Inserting node at the beginning  
static Node push(Node head_ref, int new_data)  
{  
    /* allocate node */
    Node new_node = new Node();  

    /* put in the data */
    new_node.data = new_data;  

    /* link the old list to the new node */
    new_node.next = head_ref;  

    /* move the head to point to the new node */
    head_ref = new_node;  
    return head=head_ref;  
}  

// function to find the sum of  
// nodes of the given linked list  
static int sumOfNodes( Node head)  
{  
    Node ptr = head;  
    int sum = 0;  
    while (ptr != null)  
    {  

        sum += ptr.data;  
        ptr = ptr.next;  
    }  

    return sum;  
}  

// Driver code  
public static void Main(String[] args)  
{  
    // create linked list 7.6.8.4.1  
    push(head, 7);  
    push(head, 6);  
    push(head, 8);  
    push(head, 4);  
    push(head, 1);  

    Console.WriteLine("Sum of nodes = "
        + sumOfNodes(head));  
}  
}  

// This code is contributed by 29AjayKumar 

```

**Output:**

```
Sum of nodes = 26

```

**时间复杂度：**`O(n)`，N 是链表中节点的数量。

**辅助空间：**`O(1)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。