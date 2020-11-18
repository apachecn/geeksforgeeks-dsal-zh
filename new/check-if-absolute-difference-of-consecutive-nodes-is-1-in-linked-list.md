# 检查链接列表

中连续节点的绝对差是否为1

给定一个单链表。 任务是检查链接列表中连续节点之间的绝对差是否为1。

**示例：**

> **输入：**列表= 2- > 3- > 4- > 5- > 4- > 3- > 2- > 1- > NULL
> **输出：**是
> **说明：**列表中相邻节点之间的差为1。因此，给定的列表是一个跳线序列。
> 
> **输入：**列表= 2- > 3- > 4- > 5- > 3- > 4- >空
> **输出：[** 否

**简单方法**：

1.  用一个临时指针遍历列表。
2.  将标志变量初始化为true，指示连续节点的绝对差为1。
3.  开始遍历列表。
4.  检查连续节点的绝对差是否为1。
5.  如果是，则继续遍历，否则将标志变量更新为零并停止进一步遍历。
    返回标志。

下面是上述方法的实现：

## C++

```cpp

// C++ program to check if absolute difference 
// of consecutive nodes is 1 in Linked List 

#include <bits/stdc++.h> 
using namespace std; 

// A linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Utility function to create a new Node 
Node* newNode(int data) 
{ 
    Node* temp = new Node; 
    temp->data = data; 
    temp->next = NULL; 

    return temp; 
} 

// Function to check if absolute difference 
// of consecutive nodes is 1 in Linked List 
bool isConsecutiveNodes(Node* head) 
{ 
    // Create a temporary pointer 
    // to traverse the list 
    Node* temp = head; 

    // Initialize a flag variable 
    int f = 1; 

    // Traverse through all the nodes 
    // in the list 
    while (temp) { 

        if (!temp->next) 
            break; 

        // count the number of jumper sequence 
        if (abs((temp->data) - (temp->next->data)) != 1) { 
            f = 0; 
            break; 
        } 

        temp = temp->next; 
    } 

    // return flag 
    return f; 
} 

// Driver code 
int main() 
{ 
    // creating the linked list 
    Node* head = newNode(2); 
    head->next = newNode(3); 
    head->next->next = newNode(4); 
    head->next->next->next = newNode(5); 
    head->next->next->next->next = newNode(4); 
    head->next->next->next->next->next = newNode(3); 
    head->next->next->next->next->next->next = newNode(2); 
    head->next->next->next->next->next->next->next = newNode(1); 

    if (isConsecutiveNodes(head)) 
        cout << "YES"; 
    else
        cout << "NO"; 

    return 0; 
} 

```

## Java

```java

// Java program to check if absolute difference 
// of consecutive nodes is 1 in Linked List 
class GFG  
{ 

// A linked list node 
static class Node  
{ 
    int data; 
    Node next; 
}; 

// Utility function to create a new Node 
static Node newNode(int data) 
{ 
    Node temp = new Node(); 
    temp.data = data; 
    temp.next = null; 

    return temp; 
} 

// Function to check if absolute difference 
// of consecutive nodes is 1 in Linked List 
static int isConsecutiveNodes(Node head) 
{ 
    // Create a temporary pointer 
    // to traverse the list 
    Node temp = head; 

    // Initialize a flag variable 
    int f = 1; 

    // Traverse through all the nodes 
    // in the list 
    while (temp != null)  
    { 

        if (temp.next == null) 
            break; 

        // count the number of jumper sequence 
        if (Math.abs((temp.data) - (temp.next.data)) != 1) 
        { 
            f = 0; 
            break; 
        } 

        temp = temp.next; 
    } 

    // return flag 
    return f; 
} 

// Driver code 
public static void main(String[] args)  
{ 
        // creating the linked list 
    Node head = newNode(2); 
    head.next = newNode(3); 
    head.next.next = newNode(4); 
    head.next.next.next = newNode(5); 
    head.next.next.next.next = newNode(4); 
    head.next.next.next.next.next = newNode(3); 
    head.next.next.next.next.next.next = newNode(2); 
    head.next.next.next.next.next.next.next = newNode(1); 

    if (isConsecutiveNodes(head) == 1) 
        System.out.println("YES"); 
    else
        System.out.println("NO"); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

## Python3

```py

# Python3 program to check if absolute difference 
# of consecutive nodes is 1 in Linked List 
import math 

# A linked list node 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Utility function to create a new Node 
def newNode(data): 
    temp = Node(data) 
    temp.data = data 
    temp.next = None
    return temp 

# Function to check if absolute difference 
# of consecutive nodes is 1 in Linked List 
def isConsecutiveNodes(head): 

    # Create a temporary pointer 
    # to traverse the list 
    temp = head 

    # Initialize a flag variable 
    f = 1

    # Traverse through all the nodes 
    # in the list 
    while (temp): 

        if (temp.next == None): 
            break

        # count the number of jumper sequence 
        if (abs((temp.data) -
                (temp.next.data)) != 1) : 
            f = 0
            break

        temp = temp.next

    # return flag 
    return f 

# Driver code 
if __name__=='__main__':  

    # creating the linked list 
    head = newNode(2) 
    head.next = newNode(3) 
    head.next.next = newNode(4) 
    head.next.next.next = newNode(5) 
    head.next.next.next.next = newNode(4) 
    head.next.next.next.next.next = newNode(3) 
    head.next.next.next.next.next.next = newNode(2) 
    head.next.next.next.next.next.next.next = newNode(1) 

    if (isConsecutiveNodes(head)): 
        print("YES") 
    else: 
        print("NO") 

# This code is contributed by Srathore 

```

## C#

```cs

// C# program to check if absolute difference 
// of consecutive nodes is 1 in Linked List 
using System; 

public class GFG  
{ 

// A linked list node 
public class Node  
{ 
    public int data; 
    public Node next; 
}; 

// Utility function to create a new Node 
static Node newNode(int data) 
{ 
    Node temp = new Node(); 
    temp.data = data; 
    temp.next = null; 

    return temp; 
} 

// Function to check if absolute difference 
// of consecutive nodes is 1 in Linked List 
static int isConsecutiveNodes(Node head) 
{ 
    // Create a temporary pointer 
    // to traverse the list 
    Node temp = head; 

    // Initialize a flag variable 
    int f = 1; 

    // Traverse through all the nodes 
    // in the list 
    while (temp != null)  
    { 

        if (temp.next == null) 
            break; 

        // count the number of jumper sequence 
        if (Math.Abs((temp.data) - (temp.next.data)) != 1) 
        { 
            f = 0; 
            break; 
        } 

        temp = temp.next; 
    } 

    // return flag 
    return f; 
} 

// Driver code 
public static void Main(String[] args)  
{ 
        // creating the linked list 
    Node head = newNode(2); 
    head.next = newNode(3); 
    head.next.next = newNode(4); 
    head.next.next.next = newNode(5); 
    head.next.next.next.next = newNode(4); 
    head.next.next.next.next.next = newNode(3); 
    head.next.next.next.next.next.next = newNode(2); 
    head.next.next.next.next.next.next.next = newNode(1); 

    if (isConsecutiveNodes(head) == 1) 
        Console.WriteLine("YES"); 
    else
        Console.WriteLine("NO"); 
    } 
} 

// This code contributed by Rajput-Ji 

```

**Output:**

```
YES

```



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。