# 检查链接列表是否成对排序

给定一个链表。 任务是检查链接列表是否成对排序。

如果每个连续的数字对都按排序（非降序）顺序，则认为链表是成对排序的。 如果节点数为奇数，则忽略最后一个节点，并且结果基于剩余的偶数个节点。

**示例**：

```
Input: List =  10 -> 15 -> 9 -> 9 -> 1 -> 5
Output: YES

Input: List = 10 -> 15 -> 8 -> 9 -> 10 -> 5
Output: NO

```

**方法**：的想法是从左到右遍历链表。 成对比较节点，如果任何一对违反属性，则返回 false。 如果没有一对违反属性，则返回 True。

下面是上述方法的实现：

## C++

```cpp

// C++ program to check if linked list is 
// pairwise sorted 
#include <iostream> 

using namespace std; 

// A linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to check if linked list is 
// pairwise sorted 
bool isPairWiseSorted(struct Node* head) 
{ 
    bool flag = true; 

    struct Node* temp = head; 

    // Traverse further only if there 
    // are at-least two nodes left 
    while (temp != NULL && temp->next != NULL) { 
        if (temp->data > temp->next->data) { 
            flag = false; 
            break; 
        } 

        temp = temp->next->next; 
    } 

    return flag; 
} 

// Function to add a node at the 
// beginning of Linked List 
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

// Driver program to test above function 
int main() 
{ 
    struct Node* start = NULL; 

    /* The constructed linked list is:  
    10->15->9->9->1->5 */
    push(&start, 5); 
    push(&start, 1); 
    push(&start, 9); 
    push(&start, 9); 
    push(&start, 15); 
    push(&start, 10); 

    if (isPairWiseSorted(start)) 
        cout << "YES"; 
    else
        cout << "NO"; 

    return 0; 
} 

```

## Java

```java

// Java program to check if linked list is  
// pairwise sorted  
class GFG 
{  

// A linked list node  
static class Node 
{  
    int data;  
    Node next;  
};  
static Node start; 

// Function to check if linked list is  
// pairwise sorted  
static boolean isPairWiseSorted(Node head)  
{  
    boolean flag = true;  

    Node temp = head;  

    // Traverse further only if there  
    // are at-least two nodes left  
    while (temp != null && temp.next != null)  
    {  
        if (temp.data > temp.next.data)  
        {  
            flag = false;  
            break;  
        }  

        temp = temp.next.next;  
    }  
    return flag;  
}  

// Function to add a node at the  
// beginning of Linked List  
static void push(Node head_ref, int new_data)  
{  

    /* allocate node */
    Node new_node = new Node();  

    /* put in the data */
    new_node.data = new_data;  

    /* link the old list off the new node */
    new_node.next = head_ref;  

    /* move the head to point to the new node */
    head_ref = new_node;  
        start = head_ref; 
}  

// Driver Code 
public static void main(String[] args)  
{ 
    start = null;  

    /* The constructed linked list is:  
    10.15.9.9.1.5 */
    push(start, 5);  
    push(start, 1);  
    push(start, 9);  
    push(start, 9);  
    push(start, 15);  
    push(start, 10);  

    if (isPairWiseSorted(start))  
        System.out.println("YES"); 
    else
        System.out.println("NO"); 
    } 
} 

// This code is contributed by PrinciRaj1992  

```

## Python

```py

# Python program to check if linked list is  
# pairwise sorted  

# Linked List node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

start = None

# Function to check if linked list is  
# pairwise sorted  
def isPairWiseSorted(head) : 

    flag = True

    temp = head  

    # Traverse further only if there  
    # are at-least two nodes left  
    while (temp != None and temp.next != None) : 

        if (temp.data > temp.next.data) : 
            flag = False
            break

        temp = temp.next.next

    return flag  

# Function to add a node at the  
# beginning of Linked List  
def push(head_ref, new_data) : 

    global start 
    # allocate node  
    new_node = Node(0)  

    # put in the data  
    new_node.data = new_data  

    # link the old list off the new node  
    new_node.next = head_ref  

    # move the head to point to the new node  
    head_ref = new_node  
    start = head_ref 

# Driver Code 
start = None

# The constructed linked list is:  
# 10.15.9.9.1.5  
push(start, 5)  
push(start, 1)  
push(start, 9)  
push(start, 9)  
push(start, 15)  
push(start, 10)  

if (isPairWiseSorted(start)) : 
    print("YES") 
else: 
    print("NO") 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to check if linked list is  
// pairwise sorted  
using System; 
class GFG 
{  

// A linked list node  
public class Node 
{  
    public int data;  
    public Node next;  
};  
static Node start; 

// Function to check if linked list is  
// pairwise sorted  
static Boolean isPairWiseSorted(Node head)  
{  
    Boolean flag = true;  

    Node temp = head;  

    // Traverse further only if there  
    // are at-least two nodes left  
    while (temp != null && temp.next != null)  
    {  
        if (temp.data > temp.next.data)  
        {  
            flag = false;  
            break;  
        }  

        temp = temp.next.next;  
    }  
    return flag;  
}  

// Function to add a node at the  
// beginning of Linked List  
static void push(Node head_ref, int new_data)  
{  

    /* allocate node */
    Node new_node = new Node();  

    /* put in the data */
    new_node.data = new_data;  

    /* link the old list off the new node */
    new_node.next = head_ref;  

    /* move the head to point to the new node */
    head_ref = new_node;  
    start = head_ref; 
}  

// Driver Code 
public static void Main(String[] args)  
{ 
    start = null;  

    /* The constructed linked list is:  
    10.15.9.9.1.5 */
    push(start, 5);  
    push(start, 1);  
    push(start, 9);  
    push(start, 9);  
    push(start, 15);  
    push(start, 10);  

    if (isPairWiseSorted(start))  
        Console.WriteLine("YES"); 
    else
        Console.WriteLine("NO"); 
    } 
} 

// This code is contributed by Rajput-Jiv 

```

**Output:**

```
YES

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。