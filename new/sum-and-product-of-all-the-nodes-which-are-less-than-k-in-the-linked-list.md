# 链表中所有小于`K`的节点的总和与乘积

> 原文：[https://www.geeksforgeeks.org/sum-and-product-of-all-the-nodes-which-are-less-than-k-in-the-linked-list/](https://www.geeksforgeeks.org/sum-and-product-of-all-the-nodes-which-are-less-than-k-in-the-linked-list/)

给定一个链表和一个键`K`。任务是计算小于键`K`的所有节点的总和和乘积。

**示例**：

> **输入**：`12 -> 15 -> 9 -> 11 -> 5 -> 6, K = 9`
>
> **输出**：`sum = 11, product = 30`
> 
> **输入**：`13 -> 4 -> 16 -> 9 -> 22 -> 45 -> 5 -> 16 -> 6, K = 10`
>
> **输出**：`sum = 24, product = 1080`

**方法**：从头开始遍历，检查当前节点的值是否小于`K`。如果是，则将该节点加到总和上并乘以该节点乘积，然后在列表中向前移动。

下面是上述方法的实现：

## C++

```cpp

// C++ program to sum and product all the 
// nodes from the list that are lesser 
// than the specified value K 
#include <bits/stdc++.h> 
using namespace std; 

// structure of a node 
struct Node { 
    int data; 
    Node* next; 
}; 

// function to get a new node 
Node* getNode(int data) 
{ 
    Node* newNode = new Node; 
    newNode->data = data; 
    newNode->next = NULL; 
    return newNode; 


// function to sum all the nodes from the list 
// that are lesser than the specified value K 
int sumLesserNodes(Node** head_ref, int K) 
{ 
    Node* temp = *head_ref; 

    int sum = 0; 
    while (temp != NULL) { 
        if (temp->data < K) 
            sum += temp->data; 
        temp = temp->next; 
    } 

    return sum; 
} 

// function to product all the nodes from the list 
// that are lesser than the specified value K 
int productLesserNodes(Node** head_ref, int K) 
{ 
    Node* temp = *head_ref; 

    int product = 1; 
    while (temp != NULL) { 
        if (temp->data < K) 
            product *= temp->data; 
        temp = temp->next; 
    } 

    return product; 
} 

// Driver code 
int main() 
{ 
    // Create list: 12->15->9->11->5->6 
    Node* head = getNode(12); 
    head->next = getNode(15); 
    head->next->next = getNode(9); 
    head->next->next->next = getNode(11); 
    head->next->next->next->next = getNode(5); 
    head->next->next->next->next->next = getNode(6); 

    int K = 9; 
    cout << "Sum = " << sumLesserNodes(&head, K) << endl; 
    cout << "Product = " << productLesserNodes(&head, K) << endl; 

    return 0; 
} 

```

## Java

```java

// Java program to sum and product all the 
// nodes from the list that are lesser 
// than the specified value K 
class GFG  
{ 

// structure of a node 
static class Node  
{ 
    int data; 
    Node next; 
}; 

// function to get a new node 
static Node getNode(int data) 
{ 
    Node newNode = new Node(); 
    newNode.data = data; 
    newNode.next = null; 
    return newNode; 
} 

// function to sum all the nodes from the list 
// that are lesser than the specified value K 
static int sumLesserNodes(Node head_ref, int K) 
{ 
    Node temp = head_ref; 

    int sum = 0; 
    while (temp != null)  
    { 
        if (temp.data < K) 
            sum += temp.data; 
        temp = temp.next; 
    } 

    return sum; 
} 

// function to product all the nodes from the list 
// that are lesser than the specified value K 
static int productLesserNodes(Node head_ref, int K) 
{ 
    Node temp = head_ref; 

    int product = 1; 
    while (temp != null)  
    { 
        if (temp.data < K) 
            product *= temp.data; 
        temp = temp.next; 
    } 

    return product; 
} 

// Driver code 
public static void main(String[] args)  
{ 

    // Create list: 12->15->9->11->5->6 
    Node head = getNode(12); 
    head.next = getNode(15); 
    head.next.next = getNode(9); 
    head.next.next.next = getNode(11); 
    head.next.next.next.next = getNode(5); 
    head.next.next.next.next.next = getNode(6); 

    int K = 9; 
    System.out.println("Sum = " + sumLesserNodes(head, K)); 
    System.out.println("Product = " + productLesserNodes(head, K)); 
} 
} 

// This code has been contributed by 29AjayKumar 

```

## Python3

```py

# Python3 program to sum and product all the 
# nodes from the list that are lesser 
# than the specified value K 

# Node of the single linked list  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.next = None

# function to get a new node 
def getNode(data): 

    newNode = Node(0) 
    newNode.data = data 
    newNode.next = None
    return newNode 

# function to sum all the nodes from the list 
# that are lesser than the specified value K 
def sumLesserNodes(head_ref, K): 

    temp = head_ref 

    sum = 0
    while (temp != None) : 
        if (temp.data < K): 
            sum += temp.data 
        temp = temp.next

    return sum

# function to product all the nodes from the list 
# that are lesser than the specified value K 
def productLesserNodes(head_ref,K): 

    temp = head_ref 

    product = 1
    while (temp != None) : 
        if (temp.data < K): 
            product *= temp.data 
        temp = temp.next

    return product 

# Driver Code 
if __name__ == "__main__":  

    # Create list: 12.15.9.11.5.6 
    head = getNode(12) 
    head.next = getNode(15) 
    head.next.next = getNode(9) 
    head.next.next.next = getNode(11) 
    head.next.next.next.next = getNode(5) 
    head.next.next.next.next.next = getNode(6) 

    K = 9
    print("Sum =", sumLesserNodes(head, K)) 
    print("Product =", productLesserNodes(head, K)) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to sum and product all the 
// nodes from the list that are lesser 
// than the specified value K 
using System; 

class GFG  
{ 

// structure of a node 
public class Node  
{ 
    public int data; 
    public Node next; 
}; 

// function to get a new node 
static Node getNode(int data) 
{ 
    Node newNode = new Node(); 
    newNode.data = data; 
    newNode.next = null; 
    return newNode; 
} 

// function to sum all the nodes from the list 
// that are lesser than the specified value K 
static int sumLesserNodes(Node head_ref, int K) 
{ 
    Node temp = head_ref; 

    int sum = 0; 
    while (temp != null)  
    { 
        if (temp.data < K) 
            sum += temp.data; 
        temp = temp.next; 
    } 

    return sum; 
} 

// function to product all the nodes from the list 
// that are lesser than the specified value K 
static int productLesserNodes(Node head_ref, int K) 
{ 
    Node temp = head_ref; 

    int product = 1; 
    while (temp != null)  
    { 
        if (temp.data < K) 
            product *= temp.data; 
        temp = temp.next; 
    } 

    return product; 
} 

// Driver code 
public static void Main(String[] args)  
{ 

    // Create list: 12->15->9->11->5->6 
    Node head = getNode(12); 
    head.next = getNode(15); 
    head.next.next = getNode(9); 
    head.next.next.next = getNode(11); 
    head.next.next.next.next = getNode(5); 
    head.next.next.next.next.next = getNode(6); 

    int K = 9; 
    Console.WriteLine("Sum = " + sumLesserNodes(head, K)); 
    Console.WriteLine("Product = " + productLesserNodes(head, K)); 
} 
} 

// This code contributed by Rajput-Ji 

```

**输出**：

```
Sum = 11
Product = 30

```

**时间复杂度**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。