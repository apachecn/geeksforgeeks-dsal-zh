# 在给定索引处打印链接列表的节点

给定一个按升序排序的单链表![l1](img/ef22f4f5e9e8d0d5bc762c4bd091359b.png "Rendered by QuickLaTeX.com")和另一个未排序的单链表![l2](img/cdb2756782724bb4ebc46f082a9e7ce9.png "Rendered by QuickLaTeX.com")。 任务是根据数据在第一链接列表的节点中指出的位置来打印第二链接列表的元素。 例如，如果第一个链表是 **1- > 2- > 5** ，则必须打印 1 <sup>st</sup> ，2 <sup>nd</sup> 和 第二个链表的第 5 <sup>个元素。</sup>

**范例**：

```
Input: l1 = 1->2->5
       l2 = 1->8->7->6->2->9->10
Output : 1->8->2
Elements in l1 are 1, 2 and 5\. 
Therefore, print 1st, 2nd and 5th elements of l2,
Which are 1, 8 and 2.

Input: l1 = 2->5 
       l2 = 7->5->3->2->8
Output: 5->8 

```

用两个指针使用两个嵌套循环遍历两个链表。 外循环分别指向第一个列表的元素，内循环分别指向第二个列表的元素。 在外循环的第一次迭代中，指向第一个链表头的指针指向其根节点。 我们遍历第二个链接列表，直到到达第一个链接列表中节点数据所指出的位置。 到达所需位置后，打印第二个列表的数据并再次重复此过程，直到到达第一个链接列表的末尾。

下面是上述方法的实现：

## C++

```cpp

// C++ program to print second linked list 
// according to data in the first linked list 
#include <iostream> 
using namespace std; 

// Linked List Node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to insert a node at the beginning */
void push(struct Node** head_ref, int new_data) 
{ 
    Node* new_node = new Node; 

    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Function to print the second list according 
// to the positions referred by the 1st list 
void printSecondList(Node* l1, Node* l2) 
{ 
    struct Node* temp = l1; 
    struct Node* temp1 = l2; 

    // While first linked list is not null. 
    while (temp != NULL) { 
        int i = 1; 

        // While second linked list is not equal 
        // to the data in the node of the 
        // first linked list. 
        while (i < temp->data) { 
            // Keep incrementing second list 
            temp1 = temp1->next; 
            i++; 
        } 

        // Print the node at position in second list 
        // pointed by current element of first list 
        cout << temp1->data << " "; 

        // Increment first linked list 
        temp = temp->next; 

        // Set temp1 to the start of the 
        // second linked list 
        temp1 = l2; 
    } 
} 

// Driver Code 
int main() 
{ 
    struct Node *l1 = NULL, *l2 = NULL; 

    // Creating 1st list 
    // 2 -> 5 
    push(&l1, 5); 
    push(&l1, 2); 

    // Creating 2nd list 
    // 4 -> 5 -> 6 -> 7 -> 8 
    push(&l2, 8); 
    push(&l2, 7); 
    push(&l2, 6); 
    push(&l2, 5); 
    push(&l2, 4); 

    printSecondList(l1, l2); 

    return 0; 
} 

```

## Java

```java

// Java program to print second linked list  
// according to data in the first linked list  
class GFG 
{ 

// Linked List Node  
static class Node 
{  
    int data;  
    Node next;  
};  

/* Function to insert a node at the beginning */
static Node push( Node head_ref, int new_data)  
{  
    Node new_node = new Node();  

    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node; 
    return head_ref;  
}  

// Function to print the second list according  
// to the positions referred by the 1st list  
static void printSecondList(Node l1, Node l2)  
{  
    Node temp = l1;  
    Node temp1 = l2;  

    // While first linked list is not null.  
    while (temp != null) 
    {  
        int i = 1;  

        // While second linked list is not equal  
        // to the data in the node of the  
        // first linked list.  
        while (i < temp.data)  
        {  
            // Keep incrementing second list  
            temp1 = temp1.next;  
            i++;  
        }  

        // Print the node at position in second list  
        // pointed by current element of first list  
        System.out.print( temp1.data + " ");  

        // Increment first linked list  
        temp = temp.next;  

        // Set temp1 to the start of the  
        // second linked list  
        temp1 = l2;  
    }  
}  

// Driver Code  
public static void main(String args[])  
{  
    Node l1 = null, l2 = null;  

    // Creating 1st list  
    // 2 . 5  
    l1 = push(l1, 5);  
    l1 = push(l1, 2);  

    // Creating 2nd list  
    // 4 . 5 . 6 . 7 . 8  
    l2 = push(l2, 8);  
    l2 = push(l2, 7);  
    l2 = push(l2, 6);  
    l2 = push(l2, 5);  
    l2 = push(l2, 4);  

    printSecondList(l1, l2);  
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to prsecond linked list 
# according to data in the first linked list 

# Linked List Node 
class new_Node:  

    # Constructor to initialize the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None

''' Function to insert a node at the beginning '''
def push(head_ref, new_data): 
    new_node = new_Node(new_data) 
    new_node.next = head_ref 
    head_ref = new_node 
    return head_ref 

# Function to prthe second list according 
# to the positions referred by the 1st list 
def printSecondList(l1,l2): 

    temp = l1 
    temp1 = l2 

    # While first linked list is not None. 
    while (temp != None): 
        i = 1

        # While second linked list is not equal 
        # to the data in the node of the 
        # first linked list. 
        while (i < temp.data): 
            # Keep incrementing second list 
            temp1 = temp1.next
            i += 1

        # Prthe node at position in second list 
        # pointed by current element of first list 
        print(temp1.data,end=" ") 

        # Increment first linked list 
        temp = temp.next

        # Set temp1 to the start of the 
        # second linked list 
        temp1 = l2 

# Driver Code 
l1 = None
l2 = None

# Creating 1st list 
# 2 . 5 
l1 = push(l1, 5) 
l1 = push(l1, 2) 

# Creating 2nd list 
# 4 . 5 . 6 . 7 . 8 
l2 = push(l2, 8) 
l2 = push(l2, 7) 
l2 = push(l2, 6) 
l2 = push(l2, 5) 
l2 = push(l2, 4) 

printSecondList(l1, l2) 

# This code is contributed by shubhamsingh10 

```

## C#

```cs

// C# program to print second linked list  
// according to data in the first linked list  
using System; 

class GFG  
{  

// Linked List Node  
public class Node  
{  
    public int data;  
    public Node next;  
};  

/* Function to insert a node at the beginning */
static Node push( Node head_ref, int new_data)  
{  
    Node new_node = new Node();  

    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node;  
    return head_ref;  
}  

// Function to print the second list according  
// to the positions referred by the 1st list  
static void printSecondList(Node l1, Node l2)  
{  
    Node temp = l1;  
    Node temp1 = l2;  

    // While first linked list is not null.  
    while (temp != null)  
    {  
        int i = 1;  

        // While second linked list is not equal  
        // to the data in the node of the  
        // first linked list.  
        while (i < temp.data)  
        {  
            // Keep incrementing second list  
            temp1 = temp1.next;  
            i++;  
        }  

        // Print the node at position in second list  
        // pointed by current element of first list  
        Console.Write( temp1.data + " ");  

        // Increment first linked list  
        temp = temp.next;  

        // Set temp1 to the start of the  
        // second linked list  
        temp1 = l2;  
    }  
}  

// Driver Code  
public static void Main()  
{  
    Node l1 = null, l2 = null;  

    // Creating 1st list  
    // 2 . 5  
    l1 = push(l1, 5);  
    l1 = push(l1, 2);  

    // Creating 2nd list  
    // 4 . 5 . 6 . 7 . 8  
    l2 = push(l2, 8);  
    l2 = push(l2, 7);  
    l2 = push(l2, 6);  
    l2 = push(l2, 5);  
    l2 = push(l2, 4);  

    printSecondList(l1, l2);  
}  
}  

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
5 8

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。