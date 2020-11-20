# 将单链表转换为数组

> 原文：[https://www.geeksforgeeks.org/convert-a-singly-linked-list-to-an-array/](https://www.geeksforgeeks.org/convert-a-singly-linked-list-to-an-array/)

给定一个单链表，任务是将其转换为数组。

**示例**：

> **输入**：列表= 1-> 2-> 3-> 4-> 5->空
> **输出**：1 2 3 4 5
> 
> **输入**：列表= 10-> 20-> 30-> 40-> 50->空
> **输出**：10 20 30 40 50

**方法**：在此文章的[中讨论了一种从给定数组创建链表的方法。 在这里，将讨论一种将给定的链表转换为数组的方法。](https://www.geeksforgeeks.org/create-linked-list-from-a-given-array/)

*   找到给定链表的长度，例如 **len** 。

*   创建一个大小为 **len** 的数组。

*   遍历给定的链表，并将元素一次存储在数组中。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <iostream> 
using namespace std; 

// Singly Linked List structure 
struct node { 
    int data; 
    node* next; 
}; 

// Function to add a new node 
// to the Linked List 
node* add(int data) 
{ 
    node* newnode = new node; 
    newnode->data = data; 
    newnode->next = NULL; 
    return newnode; 
} 

// Function to print the array contents 
void printArr(int a[], int n) 
{ 
    for (int i = 0; i < n; i++) 
        cout << a[i] << " "; 
} 

// Function to return the length 
// of the Linked List 
int findlength(node* head) 
{ 
    node* curr = head; 
    int cnt = 0; 
    while (curr != NULL) { 
        cnt++; 
        curr = curr->next; 
    } 
    return cnt; 
} 

// Function to convert the 
// Linked List to an array 
void convertArr(node* head) 
{ 

    // Find the length of the 
    // given linked list 
    int len = findlength(head); 

    // Create an array of the 
    // required length 
    int arr[len]; 

    int index = 0; 
    node* curr = head; 

    // Traverse the Linked List and add the 
    // elements to the array one by one 
    while (curr != NULL) { 
        arr[index++] = curr->data; 
        curr = curr->next; 
    } 

    // Print the created array 
    printArr(arr, len); 
} 

// Driver code 
int main() 
{ 
    node* head = NULL; 
    head = add(1); 
    head->next = add(2); 
    head->next->next = add(3); 
    head->next->next->next = add(4); 
    head->next->next->next->next = add(5); 

    convertArr(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
class GFG 
{ 

// Singly Linked List structure 
static class node 
{ 
    int data; 
    node next; 
} 

// Function to add a new node 
// to the Linked List 
static node add(int data) 
{ 
    node newnode = new node(); 
    newnode.data = data; 
    newnode.next = null; 
    return newnode; 
} 

// Function to print the array contents 
static void printArr(int a[], int n) 
{ 
    for (int i = 0; i < n; i++) 
        System.out.print(a[i]+" "); 
} 

// Function to return the length 
// of the Linked List 
static int findlength(node head) 
{ 
    node curr = head; 
    int cnt = 0; 
    while (curr != null) 
    { 
        cnt++; 
        curr = curr.next; 
    } 
    return cnt; 
} 

// Function to convert the 
// Linked List to an array 
static void convertArr(node head) 
{ 

    // Find the length of the 
    // given linked list 
    int len = findlength(head); 

    // Create an array of the 
    // required length 
    int []arr = new int[len]; 

    int index = 0; 
    node curr = head; 

    // Traverse the Linked List and add the 
    // elements to the array one by one 
    while (curr != null)  
    { 
        arr[index++] = curr.data; 
        curr = curr.next; 
    } 

    // Print the created array 
    printArr(arr, len); 
} 

// Driver code  
public static void main(String []args) 
{ 
    node head = new node(); 
    head = add(1); 
    head.next = add(2); 
    head.next.next = add(3); 
    head.next.next.next = add(4); 
    head.next.next.next.next = add(5); 

    convertArr(head); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python3

```py

# Pytho3 implementation of the approach 

# Structure of a Node  
class node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to add a new node 
# to the Linked List 
def add(data): 

    newnode = node(0) 
    newnode.data = data 
    newnode.next = None
    return newnode 

# Function to print the array contents 
def printArr(a, n): 

    i = 0
    while(i < n): 
        print (a[i], end = " ") 
        i = i + 1

# Function to return the length 
# of the Linked List 
def findlength( head): 

    curr = head 
    cnt = 0
    while (curr != None): 

        cnt = cnt + 1
        curr = curr.next

    return cnt 

# Function to convert the 
# Linked List to an array 
def convertArr(head): 

    # Find the length of the 
    # given linked list 
    len1 = findlength(head) 

    # Create an array of the 
    # required length 
    arr = [] 

    index = 0
    curr = head 

    # Traverse the Linked List and add the 
    # elements to the array one by one 
    while (curr != None):  
        arr.append( curr.data) 
        curr = curr.next

    # Print the created array 
    printArr(arr, len1) 

# Driver code  
head = node(0) 
head = add(1) 
head.next = add(2) 
head.next.next = add(3) 
head.next.next.next = add(4) 
head.next.next.next.next = add(5) 
convertArr(head) 

# This code is contributed by Arnab kundu 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG 
{ 

// Singly Linked List structure 
public class node 
{ 
    public int data; 
    public node next; 
} 

// Function to add a new node 
// to the Linked List 
static node add(int data) 
{ 
    node newnode = new node(); 
    newnode.data = data; 
    newnode.next = null; 
    return newnode; 
} 

// Function to print the array contents 
static void printArr(int []a, int n) 
{ 
    for (int i = 0; i < n; i++) 
        Console.Write(a[i] + " "); 
} 

// Function to return the length 
// of the Linked List 
static int findlength(node head) 
{ 
    node curr = head; 
    int cnt = 0; 
    while (curr != null) 
    { 
        cnt++; 
        curr = curr.next; 
    } 
    return cnt; 
} 

// Function to convert the 
// Linked List to an array 
static void convertArr(node head) 
{ 

    // Find the length of the 
    // given linked list 
    int len = findlength(head); 

    // Create an array of the 
    // required length 
    int []arr = new int[len]; 

    int index = 0; 
    node curr = head; 

    // Traverse the Linked List and add the 
    // elements to the array one by one 
    while (curr != null)  
    { 
        arr[index++] = curr.data; 
        curr = curr.next; 
    } 

    // Print the created array 
    printArr(arr, len); 
} 

// Driver code  
public static void Main(String []args) 
{ 
    node head = new node(); 
    head = add(1); 
    head.next = add(2); 
    head.next.next = add(3); 
    head.next.next.next = add(4); 
    head.next.next.next.next = add(5); 

    convertArr(head); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
1 2 3 4 5

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。