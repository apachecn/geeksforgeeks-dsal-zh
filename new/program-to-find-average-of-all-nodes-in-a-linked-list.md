# 程序，用于查找链接列表

中所有节点的平均值

给定一个单链表。 任务是找到给定[单链表](https://www.geeksforgeeks.org/data-structures/linked-list/)的所有节点的平均值。

**范例**：

```
Input: 7->6->8->4->1
Output: 26
Average of nodes:
(7 + 6 + 8 + 4 + 1 ) / 5 = 5.2

Input: 1->7->3->9->11->5
Output: 6

```

**迭代解决方案：**

1.  用链接列表的开头初始化一个指针ptr，并将sum变量初始化为0。
2.  使用循环开始遍历链表，直到遍历所有节点。
3.  将当前节点的值添加到总和，即总和+ = ptr-> data。
4.  增加指向链接列表下一个节点的指针，即ptr = ptr-> next。
5.  将总和除以节点总数，然后返回平均值。

下面是上述方法的实现：

## C ++

```

// C++ implementation to find the average of 
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

// Function to iteratively find the avg of 
// nodes of the given linked list 
float avgOfNodes(struct Node* head) 
{ 
    // if head = NULL 
    if (!head) 
        return -1; 

    int count = 0; // Initialize count 
    int sum = 0; 
    float avg = 0.0; 

    struct Node* current = head; // Initialize current 
    while (current != NULL) { 
        count++; 
        sum += current->data; 
        current = current->next; 
    } 

    // calculate average 
    avg = (double)sum / count; 

    return avg; 
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

    cout << "Average of nodes = " << avgOfNodes(head); 

    return 0; 
} 

```

## 爪哇

```

// Java implementation to find the average of 
// nodes of the Linked List 
class GFG 
{  

/* A Linked list node */
static class Node  
{ 
    int data; 
    Node next; 
}; 

// function to insert a node at the 
// beginning of the linked list 
static Node push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list to the new node */
    new_node.next = (head_ref); 

    /* move the head to point to the new node */
    (head_ref) = new_node; 
    return head_ref; 
} 

// Function to iteratively find the avg of 
// nodes of the given linked list 
static double avgOfNodes(Node head) 
{ 
    // if head = null 
    if (head == null) 
        return -1; 

    int count = 0; // Initialize count 
    int sum = 0; 
    double avg = 0.0; 

    Node current = head; // Initialize current 
    while (current != null) 
    { 
        count++; 
        sum += current.data; 
        current = current.next; 
    } 

    // calculate average 
    avg = (double)sum / count; 

    return avg; 
} 

// Driver Code 
public static void main(String args[]) 
{ 
    Node head = null; 

    // create linked list 7.6.8.4.1 
    head=push(head, 7); 
    head=push(head, 6); 
    head=push(head, 8); 
    head=push(head, 4); 
    head=push(head, 1); 

    System.out.println("Average of nodes = " + avgOfNodes(head)); 
} 
} 
// This code is contributed by Arnab Kundu 

```

## Python3

```

# Python3 implementation to find the average of  
# nodes of the Linked List  
class newNode:  

    # Constructor to create a new node  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# function to insert a node at the  
# beginning of the linked list  
def push(node,data): 

    ''' allocate node '''
    if (node == None):  
        return (newNode(data))  

    else: 
        node.next = push(node.next, data)  
        return node  

# Function to iteratively find the avg of  
# nodes of the given linked list  
def avgOfNodes(head): 

    # if head = NULL  
    if (head == None): 
        return -1

    count = 0 # Initialize count  
    sum = 0
    avg = 0.0

    while (head != None): 
        count += 1
        sum += head.data  
        head = head.next

    # calculate average  
    avg = sum / count  
    return avg  

# Driver Code  

# create linked list 7.6.8.4.1  
head = newNode(7)  
push(head, 6)  
push(head, 8)  
push(head, 4)  
push(head, 1)  
print("Average of nodes = ",avgOfNodes(head)) 

# This code is contributed by 
# Shubham Singh(SHUBHAMSINGH10)  

```

## C＃

```

// C# implementation to find the average  
// of nodes of the Linked List  
using System; 

class GFG  
{  

/* A Linked list node */
public class Node  
{  
    public int data;  
    public Node next;  
};  

// function to insert a node at the  
// beginning of the linked list  
static Node push(Node head_ref,  
                 int new_data)  
{  
    /* allocate node */
    Node new_node = new Node();  

    /* put in the data */
    new_node.data = new_data;  

    /* link the old list to the new node */
    new_node.next = (head_ref);  

    /* move the head to point to the new node */
    (head_ref) = new_node;  
    return head_ref;  
}  

// Function to iteratively find the avg of  
// nodes of the given linked list  
static double avgOfNodes(Node head)  
{  
    // if head = null  
    if (head == null)  
        return -1;  

    int count = 0; // Initialize count  
    int sum = 0;  
    double avg = 0.0;  

    Node current = head; // Initialize current  
    while (current != null)  
    {  
        count++;  
        sum += current.data;  
        current = current.next;  
    }  

    // calculate average  
    avg = (double)sum / count;  

    return avg;  
}  

// Driver Code  
public static void Main(String []args)  
{  
    Node head = null;  

    // create linked list 7.6.8.4.1  
    head=push(head, 7);  
    head=push(head, 6);  
    head=push(head, 8);  
    head=push(head, 4);  
    head=push(head, 1);  

    Console.WriteLine("Average of nodes = " +  
                           avgOfNodes(head));  
}  
}  

// This code is contributed by Rajput-Ji 

```

**Output:**

```
Average of nodes = 5.2

```

**时间复杂度：** O（n）
其中n等于节点数。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。