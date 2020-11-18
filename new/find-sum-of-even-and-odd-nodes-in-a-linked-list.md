# 在链表

> 原文：[https://www.geeksforgeeks.org/find-sum-of-even-and-odd-nodes-in-a-linked-list/](https://www.geeksforgeeks.org/find-sum-of-even-and-odd-nodes-in-a-linked-list/)

中查找偶数和奇数节点的总和

给定一个链表，任务是在其中分别查找偶数和奇数节点的总和。

**示例**：

> **输入**：1-> 2-> 3-> 4-> 5-> 6-> 7
> **输出**：
> 偶数和= 12
> 奇数和= 16
> 
> **输入**：5-> 7-> 8-> 10-> 15
> **输出**：
> 偶数= 18
> 赔率总和= 27

**方法**：遍历整个链表以及每个节点：

1.  如果元素是偶数，那么我们将该元素添加到保存偶数元素之和的变量中。

2.  如果元素是奇数，那么我们将该元素添加到保存奇数元素之和的变量中。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <iostream> 
using namespace std; 

// Represents node of the linked list 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to insert a node at the 
// end of the linked list 
void insert(Node** root, int item) 
{ 
    Node *ptr = *root, *temp = new Node; 
    temp->data = item; 
    temp->next = NULL; 

    if (*root == NULL) 
        *root = temp; 
    else { 
        while (ptr->next != NULL) 
            ptr = ptr->next; 
        ptr->next = temp; 
    } 
} 

// Function to print the sum of even 
// and odd nodes of the linked lists 
void evenOdd(Node* root) 
{ 
    int odd = 0, even = 0; 
    Node* ptr = root; 
    while (ptr != NULL) { 

        // If current node's data is even 
        if (ptr->data % 2 == 0) 
            even += ptr->data; 

        // If current node's data is odd 
        else
            odd += ptr->data; 

        // ptr now points to the next node 
        ptr = ptr->next; 
    } 

    cout << "Even Sum = " << even << endl; 
    cout << "Odd Sum = " << odd << endl; 
} 

// Driver code 
int main() 
{ 
    Node* root = NULL; 
    insert(&root, 1); 
    insert(&root, 2); 
    insert(&root, 3); 
    insert(&root, 4); 
    insert(&root, 5); 
    insert(&root, 6); 
    insert(&root, 7); 

    evenOdd(root); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach  
class GfG  
{ 

// Represents node of the linked list  
static class Node  
{  
    int data;  
    Node next;  
} 
static Node root; 

// Function to insert a node at the  
// end of the linked list  
static void insert(int item)  
{  
    Node ptr = root, temp = new Node();  
    temp.data = item;  
    temp.next = null;  

    if (root == null)  
        root = temp;  
    else 
    {  
        while (ptr.next != null)  
            ptr = ptr.next;  
        ptr.next = temp;  
    }  
}  

// Function to print the sum of even  
// and odd nodes of the linked lists  
static void evenOdd(Node root)  
{  
    int odd = 0, even = 0;  
    Node ptr = root;  
    while (ptr != null)  
    {  

        // If current node's data is even  
        if (ptr.data % 2 == 0)  
            even += ptr.data;  

        // If current node's data is odd  
        else
            odd += ptr.data;  

        // ptr now points to the next node  
        ptr = ptr.next;  
    }  

    System.out.println("Even Sum = " + even);  
    System.out.println("Odd Sum = " + odd);  
}  

// Driver code  
public static void main(String[] args)  
{  
    // Node* root = NULL;  
    insert( 1);  
    insert( 2);  
    insert( 3);  
    insert( 4);  
    insert(5);  
    insert(6);  
    insert( 7);  

    evenOdd(root);  
} 
}  

// This code is contributed by Prerna Saini 

```

## Python3

```py

# Python3 implementation of the approach 
import math 

# Represents node of the linked list 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to insert a node at the 
# end of the linked list 
def insert(root, item): 
    ptr = root 
    temp = Node(item) 
    temp.data = item 
    temp.next = None

    if (root == None): 
        root = temp 
    else: 
        while (ptr.next != None): 
            ptr = ptr.next
        ptr.next = temp 

    return root 

# Function to print the sum of even 
# and odd nodes of the linked lists 
def evenOdd(root): 
    odd = 0
    even = 0
    ptr = root 
    while (ptr != None): 

        # If current node's data is even 
        if (ptr.data % 2 == 0): 
            even = even + ptr.data 

        # If current node's data is odd 
        else: 
            odd = odd + ptr.data 

        # ptr now points to the next node 
        ptr = ptr.next

    print( "Even Sum = ", even) 
    print( "Odd Sum = ", odd) 

# Driver code 
if __name__=='__main__':  
    root = None
    root = insert(root, 1) 
    root = insert(root, 2) 
    root = insert(root, 3) 
    root = insert(root, 4) 
    root = insert(root, 5) 
    root = insert(root, 6) 
    root = insert(root, 7) 

    evenOdd(root) 

# This code is contributed by AbhiThakur 

```

## C#

```cs

// C# implementation of the approach  
using System; 

class GfG  
{  

// Represents node of the linked list  
public class Node  
{  
    public int data;  
    public Node next;  
}  
static Node root;  

// Function to insert a node at the  
// end of the linked list  
static void insert(int item)  
{  
    Node ptr = root, temp = new Node();  
    temp.data = item;  
    temp.next = null;  

    if (root == null)  
        root = temp;  
    else
    {  
        while (ptr.next != null)  
            ptr = ptr.next;  
        ptr.next = temp;  
    }  
}  

// Function to print the sum of even  
// and odd nodes of the linked lists  
static void evenOdd(Node root)  
{  
    int odd = 0, even = 0;  
    Node ptr = root;  
    while (ptr != null)  
    {  

        // If current node's data is even  
        if (ptr.data % 2 == 0)  
            even += ptr.data;  

        // If current node's data is odd  
        else
            odd += ptr.data;  

        // ptr now points to the next node  
        ptr = ptr.next;  
    }  

    Console.WriteLine("Even Sum = " + even);  
    Console.WriteLine("Odd Sum = " + odd);  
}  

// Driver code  
public static void Main(String []args)  
{  
    // Node* root = NULL;  
    insert( 1);  
    insert( 2);  
    insert( 3);  
    insert( 4);  
    insert(5);  
    insert(6);  
    insert( 7);  

    evenOdd(root);  
}  
}  

// This code is contributed by Arnab Kundu  

```

**Output:**

```
Even Sum = 12
Odd Sum = 16

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。