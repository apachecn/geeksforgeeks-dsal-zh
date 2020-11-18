# 在链接列表

中查找峰元素

给定一个整数链接列表。 任务是在其中找到一个峰值元素。 如果列表中的一个元素不小于其相邻元素，则称该元素为**峰**。 对于拐角元素，我们只需要考虑一个邻居。 例如：

*   如果输入列表为{5-> 10-> 20-> 15}，则 20 是唯一的峰元素。
*   对于输入列表{10-> 20-> 15-> 2-> 23-> 90-> 67}，有两个峰元素：20 和 90。请注意，需要返回任何一个峰元素。

以下一些极端情况可以更好地解决这个问题：

1.  如果输入列表严格按升序排序，则最后一个元素始终是峰值元素。 例如，50 是{10-> 20-> 30-> 40-> 50}中的峰值元素。
2.  如果输入列表按严格降序排序，则第一个元素始终是峰值元素。 100 是{100-> 80-> 60-> 50-> 20}中的峰值元素。
3.  如果输入列表的所有元素都相同，则每个元素都是峰值元素。

**范例**：

```
Input : List =  {1 -> 6 -> 8 -> 4 -> 12}
Output : 8

Input : List = {10 -> 20 -> 15 -> 2 -> 23 -> 90 -> 67}
Output : 90

```

想法是遍历链表，并检查当前元素是否为峰元素。 如果是，则返回当前元素，否则在列表中向前移动。

如果当前元素大于其上一个和下一个元素，则它将是一个峰值元素。

下面的程序说明了上述方法：

## C++

```cpp

// C++ implementation to find the peak 
// element in the Linked List 
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
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Function to find the peak element 
int findPeak(struct Node* head) 
{ 
    // Return -1 to indicate that 
    // peak does not exist 
    if (head == NULL) 
        return -1; 

    // If there is only one node 
    if (head->next == NULL) 
        return head->data; 

    // Traverse till last node (starting from 
    // second node) 
    int prev = head->data; 
    Node *curr; 
    for (curr = head->next; curr->next != NULL; 
         curr = curr->next) { 

        // check if current node is greater 
        // than both neighbours 
        if (curr->data > curr->next->data 
            && curr->data > prev) 
            return curr->data; 

        prev = curr->data; 
    } 

    // We reach here when curr is last node 
    if (curr->data > prev) 
        return curr->data; 

    // Peak does not exists 
    else
        return -1; 
} 

// Driver program 
int main() 
{ 
    struct Node* head = NULL; 

    // create linked list 1->6->8->4->12 
    push(&head, 12); 
    push(&head, 4); 
    push(&head, 8); 
    push(&head, 6); 
    push(&head, 1); 

    cout << "Peak element is: "
         << findPeak(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation to find the peak  
// element in the Linked List  
class GFG 
{ 

// A Linked list node / 
static class Node  
{  
    int data;  
    Node next;  
};  

// function to insert a node at the  
// beginning of the linked list  
static Node push( Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node;  
    return head_ref; 
}  

// Function to find the peak element  
static int findPeak( Node head)  
{  
    // Return -1 to indicate that  
    // peak does not exist  
    if (head == null)  
        return -1;  

    // If there is only one node  
    if (head.next == null)  
        return head.data;  

    // Traverse till last node (starting from  
    // second node)  
    int prev = head.data;  
    Node curr;  
    for (curr = head.next; curr.next != null;  
        curr = curr.next) 
    {  

        // check if current node is greater  
        // than both neighbours  
        if (curr.data > curr.next.data  
            && curr.data > prev)  
            return curr.data;  

        prev = curr.data;  
    }  

    // We reach here when curr is last node  
    if (curr.data > prev)  
        return curr.data;  

    // Peak does not exists  
    else
        return -1;  
}  

// Driver program  
public static void main(String args[]) 
{  
    Node head = null;  

    // create linked list 1.6.8.4.12  
    head=push(head, 12);  
    head=push(head, 4);  
    head=push(head, 8);  
    head=push(head, 6);  
    head=push(head, 1);  

    System.out.print("Peak element is: "
        + findPeak(head));  
}  
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation to find the peak  
# element in the Linked List  

# Link list node  
class Node : 
    def __init__(self): 
        self.data = 0
        self.next = None

# function to insert a node at the  
# beginning of the linked list  
def push( head_ref, new_data) : 

    new_node = Node()  
    new_node.data = new_data  
    new_node.next = (head_ref)  
    (head_ref) = new_node  
    return head_ref 

# Function to find the peak element  
def findPeak( head):  

    # Return -1 to indicate that  
    # peak does not exist  
    if (head == None) : 
        return -1

    # If there is only one node  
    if (head.next == None) : 
        return head.data  

    # Traverse till last node (starting from  
    # second node)  
    prev = head.data  
    curr = head.next
    while( curr.next != None ): 

        # check if current node is greater  
        # than both neighbours  
        if (curr.data > curr.next.data and curr.data > prev) : 
            return curr.data  

        prev = curr.data  
        curr = curr.next

    # We reach here when curr is last node  
    if (curr.data > prev) : 
        return curr.data  

    # Peak does not exists  
    else: 
        return -1

# Driver program  

head = None

# create linked list 1.6.8.4.12  
head = push(head, 12)  
head = push(head, 4)  
head = push(head, 8)  
head = push(head, 6)  
head = push(head, 1)  

print("Peak element is: ", findPeak(head))  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to find the peak  
// element in the Linked List 
using System; 

class GFG  
{  

// A Linked list node /  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// function to insert a node at the  
// beginning of the linked list  
static Node push(Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node;  
    return head_ref;  
}  

// Function to find the peak element  
static int findPeak(Node head)  
{  
    // Return -1 to indicate that  
    // peak does not exist  
    if (head == null)  
        return -1;  

    // If there is only one node  
    if (head.next == null)  
        return head.data;  

    // Traverse till last node  
    // (starting from second node)  
    int prev = head.data;  
    Node curr;  
    for (curr = head.next; curr.next != null;  
         curr = curr.next)  
    {  

        // check if current node is greater  
        // than both neighbours  
        if (curr.data > curr.next.data  
            && curr.data > prev)  
            return curr.data;  

        prev = curr.data;  
    }  

    // We reach here when curr is last node  
    if (curr.data > prev)  
        return curr.data;  

    // Peak does not exists  
    else
        return -1;  
}  

// Driver Code 
public static void Main(String[] args)  
{  
    Node head = null;  

    // create linked list 1.6.8.4.12  
    head = push(head, 12);  
    head = push(head, 4);  
    head = push(head, 8);  
    head = push(head, 6);  
    head = push(head, 1);  

    Console.Write("Peak element is: " +  
                   findPeak(head));  
}  
}  

// This code is contributed by Rajput-Ji 

```

**Output:**

```
Peak element is: 8

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。