# 从给定数组

> 原文：[https://www.geeksforgeeks.org/create-linked-list-from-a-given-array/](https://www.geeksforgeeks.org/create-linked-list-from-a-given-array/)

创建链表

给定大小为`N`的数组`arr[]`。 任务是从给定数组创建链表。

**示例**：

```
Input : arr[]={1, 2, 3, 4, 5}
Output : 1->2->3->4->5

Input :arr[]={10, 11, 12, 13, 14}
Output : 10->11->12->13->14

```

**简单方法**：对于数组`arr[]`的每个元素，我们在链表中创建一个节点，并将其插入到末尾。

## C++

```cpp

#include <iostream> 
using namespace std; 

// Representation of a node 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to insert node 
void insert(Node** root, int item) 
{ 
    Node* temp = new Node; 
    Node* ptr; 
    temp->data = item; 
    temp->next = NULL; 

    if (*root == NULL) 
        *root = temp; 
    else { 
        ptr = *root; 
        while (ptr->next != NULL) 
            ptr = ptr->next; 
        ptr->next = temp; 
    } 
} 

void display(Node* root) 
{ 
    while (root != NULL) { 
        cout << root->data << " "; 
        root = root->next; 
    } 
} 

Node *arrayToList(int arr[], int n) 
{ 
    Node *root = NULL; 
    for (int i = 0; i < n; i++) 
        insert(&root, arr[i]); 
   return root; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 1, 2, 3, 4, 5 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    Node* root = arrayToList(arr, n); 
    display(root); 
    return 0; 
}

```

## Java

```java

// Java implementation of the approach 
import java.util.*; 
class GFG 
{  

// Representation of a node 
static class Node  
{ 
    int data; 
    Node next; 
}; 

// Function to insert node 
static Node insert(Node root, int item) 
{ 
    Node temp = new Node(); 
    Node ptr; 
    temp.data = item; 
    temp.next = null; 

    if (root == null) 
        root = temp; 
    else 
    { 
        ptr = root; 
        while (ptr.next != null) 
            ptr = ptr.next; 
        ptr.next = temp; 
    } 
    return root; 
} 

static void display(Node root) 
{ 
    while (root != null)  
    { 
        System.out.print( root.data + " "); 
        root = root.next; 
    } 
} 

static Node arrayToList(int arr[], int n) 
{ 
    Node root = null; 
    for (int i = 0; i < n; i++) 
        root = insert(root, arr[i]); 
    return root; 
} 

// Driver code 
public static void main(String args[]) 
{ 
    int arr[] = { 1, 2, 3, 4, 5 }; 
    int n = arr.length; 
    Node root = arrayToList(arr, n); 
    display(root); 
} 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation of the approach  
import math 

# Representation of a node 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to insert node 
def insert(root, item): 
    temp = Node(item) 

    if (root == None): 
        root = temp 
    else : 
        ptr = root 
        while (ptr.next != None): 
            ptr = ptr.next
        ptr.next = temp 

    return root 

def display(root): 
    while (root != None) : 
        print(root.data, end = " ") 
        root = root.next

def arrayToList(arr, n): 
    root = None
    for i in range(0, n, 1): 
        root = insert(root, arr[i]) 

    return root 

# Driver code 
if __name__=='__main__':  
    arr = [1, 2, 3, 4, 5] 
    n = len(arr) 
    root = arrayToList(arr, n) 
    display(root) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# implementation of the above approach  
using System;  

class GFG 
{  

// Representation of a node 
public class Node  
{ 
    public int data; 
    public Node next; 
}; 

// Function to insert node 
static Node insert(Node root, int item) 
{ 
    Node temp = new Node(); 
    Node ptr; 
    temp.data = item; 
    temp.next = null; 

    if (root == null) 
        root = temp; 
    else
    { 
        ptr = root; 
        while (ptr.next != null) 
            ptr = ptr.next; 
        ptr.next = temp; 
    } 
    return root; 
} 

static void display(Node root) 
{ 
    while (root != null)  
    { 
        Console.Write(root.data + " "); 
        root = root.next; 
    } 
} 

static Node arrayToList(int []arr, int n) 
{ 
    Node root = null; 
    for (int i = 0; i < n; i++) 
        root = insert(root, arr[i]); 
    return root; 
} 

// Driver code 
public static void Main(String []args) 
{ 
    int []arr = { 1, 2, 3, 4, 5 }; 
    int n = arr.Length; 
    Node root = arrayToList(arr, n); 
    display(root); 
} 
} 

// This code is contributed by PrinciRaj1992  

```

**输出**：

```
1 2 3 4 5

```

时间复杂度：`O(n * n)`

**高效方法**：我们从结尾遍历数组，并将每个元素插入列表的开头。

## C++

```cpp

#include <iostream> 
using namespace std; 

// Representation of a node 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to insert node 
void insert(Node** root, int item) 
{ 
    Node* temp = new Node; 
    temp->data = item; 
    temp->next = *root; 
    *root = temp; 
} 

void display(Node* root) 
{ 
    while (root != NULL) { 
        cout << root->data << " "; 
        root = root->next; 
    } 
} 

Node *arrayToList(int arr[], int n) 
{ 
    Node *root = NULL; 
    for (int i = n-1; i >= 0 ; i--) 
        insert(&root, arr[i]); 
    return root; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 1, 2, 3, 4, 5 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    Node* root = arrayToList(arr, n); 
    display(root); 
    return 0; 
}

```

## Java

```java

// Java program to print level order traversal 
// in spiral form using one queue and one stack. 
import java.util.*; 
class GFG  
{  

// Representation of a node 
static class Node  
{ 
    int data; 
    Node next; 
}; 
static Node root;  

// Function to insert node 
static Node insert(Node root, int item) 
{ 
    Node temp = new Node(); 
    temp.data = item; 
    temp.next = root; 
    root = temp; 
    return root; 
} 

static void display(Node root) 
{ 
    while (root != null)  
    { 
        System.out.print(root.data + " "); 
        root = root.next; 
    } 
} 

static Node arrayToList(int arr[], int n) 
{ 
    root = null; 
    for (int i = n - 1; i >= 0 ; i--) 
        root = insert(root, arr[i]); 
    return root; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int arr[] = { 1, 2, 3, 4, 5 }; 
    int n = arr.length; 
    Node root = arrayToList(arr, n); 
    display(root); 
} 
} 

// This code is contributed by Princi Singh 

```

## Python3

```py

# Python3 program to prlevel order traversal  
# in spiral form using one queue and one stack.  

# Representation of a Node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = next

# Function to insert Node  
def insert(root, item):  
    temp = Node(0)  
    temp.data = item  
    temp.next = root  
    root = temp 
    return root  

def display(root):  
    while (root != None):  
        print(root.data, end=" ")  
        root = root.next 

def arrayToList(arr, n):  
    root = None 
    for i in range(n - 1, -1, -1):  
        root = insert(root, arr[i]) 
    return root  

# Driver code  
if __name__ == '__main__':  
    arr = [1, 2, 3, 4, 5];  
    n = len(arr)  
    root = arrayToList(arr, n);  
    display(root)  

# This code is contributed by 29AjayKumar  

```

## C#

```cs

// C# program to print level order traversal 
// in spiral form using one queue and one stack. 
using System; 

class GFG  
{  

// Representation of a node 
public class Node  
{ 
    public int data; 
    public Node next; 
}; 
static Node root;  

// Function to insert node 
static Node insert(Node root, int item) 
{ 
    Node temp = new Node(); 
    temp.data = item; 
    temp.next = root; 
    root = temp; 
    return root; 
} 

static void display(Node root) 
{ 
    while (root != null)  
    { 
        Console.Write(root.data + " "); 
        root = root.next; 
    } 
} 

static Node arrayToList(int []arr, int n) 
{ 
    root = null; 
    for (int i = n - 1; i >= 0 ; i--) 
        root = insert(root, arr[i]); 
    return root; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    int []arr = { 1, 2, 3, 4, 5 }; 
    int n = arr.Length; 
    Node root = arrayToList(arr, n); 
    display(root); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
1 2 3 4 5

```

**时间复杂度**：`O(n)`

替代有效解决方案是维护尾指针，从左到右遍历数组元素，在尾插入并在插入后更新尾。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。